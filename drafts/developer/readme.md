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

## Start multiple projects in Visual Studio
- Select the project as startup projet
- Change from IIS Express to Console (project's name)
- Right-click on solution -> Set Startup Projects
- Select multiple and chose all of the projets to be started

## Security Considerations

### Authentication 
You can enter to the application

### Authorization
You can use a fonctionality of the app

### Transport Protection
HTTPS -> Security Sockets Layer SSL (outdated) -> Transport Layer Security (TLS)

### Cross Origin Resource Sharing (CORS)
Restrict the sites that can make requests to the server.

### Cross Site Request Forgery (CSRF)
While using cookies, your browser will keep the authorization information in your browser's cookies. Another site opened in a beside table could use that information to send requests to the first one.
OpenID and OAuth2 require your client-side code to explicitly put the tokens into authorization headers of any HTTP request to your APIs.

### Cross site Scripting (XSS)
 The site will take direct input from a user (string in a textbox) and then inject that directly into the DOM. An script block can be executed as soon as it's inserted into the DOM, or it can set
 up event handlers that execute later.
 Angular will sanitize or escape parts of values that contain something like a script block that can be executed.
 
## JSON Web Token (JWT)
- pronounced/aka "jot"

## OpenID Provider
- aka OAuth Authorization Server, aka Identity Provider, aka Security Token Service (STS)

## OpenID Connect (OIDC)
client (Angular App) -> calls for login -> Identity Provider
Identity Provider -> sends a token -> This user is authenticated to use your app
Host Website to rendering the website
Backend APIS to receive the app requests (with tokens) from clients


## OIDC Flows (used on client side)
- Authorization Code 
  - The user opens the client app 
  - Client app call the Identity Provider 
  - Identity Provider show login page to user 
  - Identity Provider validate Credentials
  - Identity Provider redirecto to client app
  - Client app calls token endpoint of Identity Provider
  - Identity Provider responds with tokens
  - Client app make calls to backend api with tokens

- Hybrid
  - *ResponseType* 'code id_token'
  - Starts the same as Authorization code flow but also involves 
  - Obtain a token for the end user on the back end for calling out to downstream services or APIs on behalf of the user.
  - 
- Implicit (deprecated)
  - ***Today, you should use Authorization Code with Proof Key for Code Exchange (PKCE) , pronounced/aka pixie, instead of Implicit flows*** Source: [IETF | Internet Engineering Task Force](https://www.ietf.org/) have released two new guidance documents around the OIDC and OAuth 2 standards [OAuth 2.0 Security Best Current Practice](https://noyes.me/oauth2-sbcp) and [OAuth 2.0 For Browser-Based Apps](https://noyes.me/obba)
  - *ResponseType* 'token'
  - STS returns the token explicitly on the url.

- Authorization Code + PKCE
  - *ResponseType* 'code'
  - The user opens the client app 
  - Client app generates a **code verifier** and using a crypto algorithm, client app generates its hash version also called **code challenge**
  - Client app call the authority URL from Identity Provider sending the code_challenge
  - STS will hold on the **code challenge**
  - Identity Provider show login page to user 
  - Identity Provider validate Credentials
  - Identity Provider redirecto to client app with **auth code**
  - Client app calls token endpoint of Identity Provider as an API call not a redirect passing **Auth Code + code verifier**
  - The STS will apply the same hashing algorithm to the code verifier and it will compare the result with the code challenge sent at the beggining of the process
  - Identity Provider returns a payload containing the ID + Access Tokens
  - Client app make calls to backend api with tokens

## Grant Types (used on server side)
- Authorization Code + PKCE

- Implicit (deprecated)

- Resource Owner Password Credential
  - Applications that have highly trusted relationship with the STS. (Desktop, mobile apps...)
  - Can use the operating system to authentitcation and obtain the access token instead of the client app managing flow itself.

- Client Credential
  - Service-to-service communication where there is no end user in the loop. Eg.: A back-end could be triggeered by a timer or incoming data from an event source and then needs to call another service to process that event.

## Access Token Contents
- client_id -> Client ID
- sub -> Subject ID. Id for the end user at the STS
- iss -> Issuer. Information about witch identity provider issued the access token.
- nbf -> Issue timestamp. When the token was issued.
- exp -> Expiration timestamp. When the token expires.
- aud -> Audience. That represents the API resources that the token allows access to.
- scope -> Scope claims. Access control identifiers that can represent more fine-grained permissions at the API resource.
- Additional claims.

For further details, look at [policy-based authorization](https://docs.microsoft.com/en-us/aspnet/core/security/authorization/policies). That document presents you how to make your API's methods more secure using policies.

## Identity providers 
[Certified protocol compliant](https://openid.net/certification/)
Google, Facebook, Twitter
Azure Active Directory (AAD)
Auth0, Okta, Ping Identity and others
IdentityServer4 - Open source

## Client libraries
angular-jwt
Microsoft Azure Active Directory Authentication Library (ADAL)
Microsoft Authentication Library (MSAL)
oidc-client

## OIDC in STS
- Create new "ASP.NET Core Empty" project. 
```
dotnet new web
```
- Add IdentityServer4 nuget package
- Add Services for IdentityServer4 on Startup class
- Update applicationUrl of launchSettings.json
- https://{server}:{port}/.well-known/openid-configuration

## OIDC in Service Provider
- Add IdentityServer4.AccessTokenValidation nuget package
- Configure Authentication in startup class
- UseAuthentication before UseAuthorization. If not you get into a weird redirect loop with identity provider
- Add **Authorize** attribute to controllers.
- Run the Service Provider and call api. Http Error 401 will show on the page.

## OIDC in Angular
- npm i oidc-client --save
- create auth.service.ts
- add User and UserManager fields
- add stsAuthority url, clientId and clientRoot to environment file
- add stsSettings to UserManager
- response_type -> 'code' for authorization code + PKCE and 'id_token token' for impliciit flow (deprecated)
- add login, isLoggedIn methods and loginChange subject to AuthService
- call authService from AppComponent
- add button and method login to AppComponent

## MSAL on Angular
authority: cloud instance + tenant 
https://login.microsoftonline.com/111-111-111-111
- cloud instance
        normally https://login.microsoftonline.com
- tenant ID
  - for tenant only => A **GUID** (Tenant ID = Directory ID)
  - any organization and personal accounts => **'common'**
  - any organization => **'organizations'**
  - Microsoft personal accounts => **'consumers'**
- protectedResourceMap
  - service urls that will require tokens
- custom scope
  - it will look like this "api://<Application ID>/access_as_user"
[Source](https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-angular-auth-code)
### Azure 
- Create a new tenant (optional)
- [Admin Portal](https://aad.portal.azure.com)
- Create a new App registration "MyApp-Frontend"
- For the SPA's Redirect URI add **http://localhost:4200**

## MSAL on Server
- Add AzureAd section to config file (appsettings.json)
- Install Microsoft.Identity.Web nuget package
- 
[Source](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-protected-web-api-app-configuration)

### Azure 
Create a new App registration "MyApp-Backend"
No redirect URI needed
- Under *Expose an API*
  - create new application ID URI
  - create new scope
  - add authorized clients (optional)
- Under *Overview* (Optional)
  - Click over the application's name link on *Managed application in local directory*
  - On the new page, click over *Properties*
  - Check *Assignment required* as **Yes**. This option requires that users and apps must first be assigned the application before being able to access it.
[Source](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-protected-web-api-app-registration)

## Azure 
Create a new tenant (optional)
[Admin Portal](https://aad.portal.azure.com)
Create a new App registration "MyApp-FrontEnd"
For the SPA's Redirect URI add **http://localhost:4200**

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.