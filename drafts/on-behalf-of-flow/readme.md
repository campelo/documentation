---
title: 
published: false
description: 
tags: ''
cover_image: ../../assets/cover.png
canonical_url: null
id: 
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

# On-Behalf-Of Flow

## OBO Client

```bash
# Install the Angular CLI
npm install -g @angular/cli

# Generate a new Angular app
ng new obo-client --routing=true --style=scss

# Change to the app directory
cd obo-client

# Install the Angular Material component library
npm install @angular/material @angular/cdk

# Install MSAL Browser and MSAL Angular in your application
npm install @azure/msal-browser @azure/msal-angular

# To add a home page
ng generate component home

# To add a profile page
ng generate component profile
```

## App registration

- Sign in [Azure portal](https://portal.azure.com/)
- Go to Azure Active Directory
- App registrations > New registration
- Enter a name for your application.
- Choose a supported account types.
- On Redirect URI, select type as SPA and value http://localhost:4200/

app.module.ts 
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { NgModule } from '@angular/core';
import { HTTP_INTERCEPTORS, HttpClientModule } from "@angular/common/http";

import { MatButtonModule } from '@angular/material/button';
import { MatToolbarModule } from '@angular/material/toolbar';
import { MatListModule } from '@angular/material/list';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { ProfileComponent } from './profile/profile.component';

import { MsalModule, MsalRedirectComponent, MsalGuard, MsalInterceptor } from '@azure/msal-angular';
import { PublicClientApplication, InteractionType } from '@azure/msal-browser';

const isIE = window.navigator.userAgent.indexOf('MSIE ') > -1 || window.navigator.userAgent.indexOf('Trident/') > -1;

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    ProfileComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    AppRoutingModule,
    MatButtonModule,
    MatToolbarModule,
    MatListModule,
    HttpClientModule,
    MsalModule.forRoot(new PublicClientApplication({
      auth: {
        // Application (client) ID from the app registration
        clientId: '',
        // {CLOUD-INSTANCE}/{TENANT-INFO} The Azure cloud instance and the app's sign-in audience (tenant ID, common, organizations, or consumers).
        //
        // {CLOUD-INSTANCE} This is the instance of the Azure cloud. For the main or global Azure cloud, enter https://login.microsoftonline.com. For national clouds (for example, China), see National clouds.
        //
        // {TENANT-INFO} Set to one of the following options: 
        // If your application supports accounts in this organizational directory, replace this value with the directory (tenant) ID or tenant name (for example, contoso.microsoft.com). 
        // If your application supports accounts in any organizational directory, replace this value with organizations. 
        // If your application supports accounts in any organizational directory and personal Microsoft accounts, replace this value with common. 
        // To restrict support to personal Microsoft accounts only, replace this value with consumers.
        authority: 'https://login.microsoftonline.com/',
        // This is your redirect URI
        redirectUri: 'http://localhost:4200'
      },
      cache: {
        cacheLocation: 'localStorage',
        // Set to true for Internet Explorer 11
        storeAuthStateInCookie: isIE
      }
    }), {
      // MSAL Guard Configuration
      interactionType: InteractionType.Redirect, 
      authRequest: {
        scopes: ['user.read']
      }
    }, {
      // MSAL Interceptor Configuration
      interactionType: InteractionType.Redirect,
      // Examples:
      //
      // ["user.read"] for Microsoft Graph
      // ["<Application ID URL>/scope"] for custom web APIs (that is, api://<Application ID>/access_as_user)
      protectedResourceMap: new Map([ 
          ['https://graph.microsoft.com/v1.0/me', ['user.read']]
      ])
    })
  ],
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: MsalInterceptor,
      multi: true
    },
    MsalGuard
  ],
  bootstrap: [
    AppComponent,
    MsalRedirectComponent
  ]
})
export class AppModule { }
```

app-routing.module.ts 
```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { MsalGuard } from '@azure/msal-angular';
import { BrowserUtils } from '@azure/msal-browser';
import { HomeComponent } from './home/home.component';
import { ProfileComponent } from './profile/profile.component';

const routes: Routes = [
  {
    path: 'profile',
    component: ProfileComponent,
    canActivate: [MsalGuard]
  },
  {
    path: '',
    component: HomeComponent
  }
];

const isIframe = window !== window.parent && !window.opener;

@NgModule({
  imports: [RouterModule.forRoot(routes, {
    // Don't perform initial navigation in iframes or popups
    // Set to enabledBlocking to use Angular Universal
   initialNavigation: !BrowserUtils.isInIframe() && !BrowserUtils.isInPopup() ? 'enabledNonBlocking' : 'disabled' 
  })],
  exports: [RouterModule]
})
export class AppRoutingModule { }

```

app.component.html
```html
<mat-toolbar color="primary">
  <a class="title" href="/">{{ title }}</a>

  <div class="toolbar-spacer"></div>

  <a mat-button [routerLink]="['profile']">Profile</a>

  <button mat-raised-button *ngIf="!loginDisplay" (click)="login()">Login</button>
  <button mat-raised-button *ngIf="loginDisplay" (click)="logout()">Logout</button>

</mat-toolbar>
<div class="container">
  <!--This is to avoid reload during acquireTokenSilent() because of hidden iframe -->
  <router-outlet *ngIf="!isIframe"></router-outlet>
</div>
```

app.component.ts
```typescript
import { Component, OnInit, OnDestroy, Inject } from '@angular/core';
import { MsalService, MsalBroadcastService, MSAL_GUARD_CONFIG, MsalGuardConfiguration } from '@azure/msal-angular';
import { InteractionStatus, RedirectRequest } from '@azure/msal-browser';
import { Subject } from 'rxjs';
import { filter, takeUntil } from 'rxjs/operators';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit, OnDestroy {
  title = 'msal-angular-tutorial';
  isIframe = false;
  loginDisplay = false;
  private readonly _destroying$ = new Subject<void>();

  constructor(@Inject(MSAL_GUARD_CONFIG) private msalGuardConfig: MsalGuardConfiguration, private broadcastService: MsalBroadcastService, private authService: MsalService) { }

  ngOnInit() {
    this.isIframe = window !== window.parent && !window.opener;

    this.broadcastService.inProgress$
    .pipe(
      filter((status: InteractionStatus) => status === InteractionStatus.None),
      takeUntil(this._destroying$)
    )
    .subscribe(() => {
      this.setLoginDisplay();
    })
  }

  login() {
    if (this.msalGuardConfig.authRequest){
      this.authService.loginRedirect({...this.msalGuardConfig.authRequest} as RedirectRequest);
    } else {
      this.authService.loginRedirect();
    }
  }

  // using redirects
  logout() { 
    this.authService.logoutRedirect({
      postLogoutRedirectUri: 'http://localhost:4200'
    });
  }

  // using pop-ups
  logoutPopup() {
    this.authService.logoutPopup({
      mainWindowRedirectUri: "/"
    });
  }

  setLoginDisplay() {
    this.loginDisplay = this.authService.instance.getAllAccounts().length > 0;
  }

  ngOnDestroy(): void {
    this._destroying$.next(undefined);
    this._destroying$.complete();
  }
}
```

index.html
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>OboClient</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
  <app-redirect></app-redirect>
</body>
</html>

```

home.component.ts
```typescript
import { Component, OnInit } from '@angular/core';
import { MsalBroadcastService, MsalService } from '@azure/msal-angular';
import { EventMessage, EventType, InteractionStatus } from '@azure/msal-browser';
import { filter } from 'rxjs/operators';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.scss']
})
export class HomeComponent implements OnInit {
  loginDisplay = false;

  constructor(private authService: MsalService, private msalBroadcastService: MsalBroadcastService) { }

  ngOnInit(): void {
    this.msalBroadcastService.msalSubject$
      .pipe(
        filter((msg: EventMessage) => msg.eventType === EventType.LOGIN_SUCCESS),
      )
      .subscribe((result: EventMessage) => {
        console.log(result);
      });

    this.msalBroadcastService.inProgress$
      .pipe(
        filter((status: InteractionStatus) => status === InteractionStatus.None)
      )
      .subscribe(() => {
        this.setLoginDisplay();
      })
  }

  setLoginDisplay() {
    this.loginDisplay = this.authService.instance.getAllAccounts().length > 0;
  }
}
```

home.component.html
```html
<div *ngIf="!loginDisplay">
  <p>Please sign-in to see your profile information.</p>
</div>

<div *ngIf="loginDisplay">
  <p>Login successful!</p>
  <p>Request your profile information by clicking Profile above.</p>
</div>
```

profile.component.ts
```typescript
import { Component, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';

const GRAPH_ENDPOINT = 'https://graph.microsoft.com/v1.0/me';

type ProfileType = {
  givenName?: string,
  surname?: string,
  userPrincipalName?: string,
  id?: string
};

@Component({
  selector: 'app-profile',
  templateUrl: './profile.component.html',
  styleUrls: ['./profile.component.scss']
})
export class ProfileComponent implements OnInit {
  profile!: ProfileType;

  constructor(
    private http: HttpClient
  ) { }

  ngOnInit() {
    this.getProfile();
  }

  getProfile() {
    this.http.get(GRAPH_ENDPOINT)
      .subscribe(profile => {
        this.profile = profile;
      });
  }
}
```

profile.component.html
```html
<div>
  <p><strong>First Name: </strong> {{profile?.givenName}}</p>
  <p><strong>Last Name: </strong> {{profile?.surname}}</p>
  <p><strong>Email: </strong> {{profile?.userPrincipalName}}</p>
  <p><strong>Id: </strong> {{profile?.id}}</p>
</div>
```

```bash
npm install
npm start
```

## Sources

[Code](https://github.com/campelo/OnBehalfOfFlow)
[Sign in Angular](https://learn.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-angular-auth-code)
[App registration](https://learn.microsoft.com/en-us/azure/active-directory/develop/scenario-spa-app-registration)

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.