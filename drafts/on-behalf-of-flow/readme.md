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

## App registration

- Sign in [Azure portal](https://portal.azure.com/)
- Go to Azure Active Directory
- App registrations > New registration
- Enter a name for your application.
- Choose a supported account types.
- On Redirect URI
  - select type as SPA and value http://localhost:4200
- On Expose an API
  - Set APP ID URI to the default value api://{client-id}
  - Create a new scope
- On Certificates & secrets
  - Create a new client secret

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

# To add a middle-tier page
ng generate component middleTier

# To add a middle-tier service
ng generate service middleTier

# To add configuration application environments
ng generate environments
```

Configure application login using MSAL authentication.

Set authentication header in communications with middle-tier using MSAL interceptor configurations.

```bash
npm install
npm start
```

## OBO Middle-Tier

Create an Azure Function.

Configure CORS.

Configure settings to use scope, client and tenant informations.

Validate the user token.

Get a new token using On-Behalf-Of flow.

## Sources

[Code](https://github.com/campelo/OnBehalfOfFlow)
[Microsoft On-Behalf-Of flow](https://learn.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
[Sign in Angular](https://learn.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-angular-auth-code)
[App registration](https://learn.microsoft.com/en-us/azure/active-directory/develop/scenario-spa-app-registration)
[MSAL interceptor](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/docs/v2-docs/msal-interceptor.md)
[Angular config file](https://devblogs.microsoft.com/premier-developer/angular-how-to-editable-config-files)
[Implementing On-Behalf-Of flow](https://aakashbhardwaj619.github.io/2021/07/27/Azure-Function-CSharp-OBO.html)

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.