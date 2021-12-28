# Developement

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

## OIDC Flows 
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
  - Starts the same as Authorization code flow but also involves 
  - Obtain a token for the end user on the back end for calling out to downstream services or APIs on behalf of the user.
  - 
- Implicit (deprecated)
  - ***Today, you should use Authorization Code with Proof Key for Code Exchange (PKCE) , pronounced/aka pixie, instead of Implicit flows*** Source: [IETF | Internet Engineering Task Force](https://www.ietf.org/) have released two new guidance documents around the OIDC and OAuth 2 standards [OAuth 2.0 Security Best Current Practice](https://noyes.me/oauth2-sbcp) and [OAuth 2.0 For Browser-Based Apps](https://noyes.me/obba)
  - STS returns the token explicitly on the url.

- Authorization Code + PKCE
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

# Git

## Stash
git stash save "description"
git fetch --prune
git checkout -b newLocalBranchName
git merge origin/remoteBranchName
git push origin localBranchName:newRemoteBranchName

# CSS
## measures 
px, cm, %, em, in, vh...

# Node

## Install specific version
npm install @angular/material@13.0.0
npm install @angular/material@13.0.*
npm install @angular/material@13.*

caret ^
^4.3.0
will load the latest 4.x.x release, but will not load 5.x.x

tilde ~
~4.3.0
will load the latest 4.3.x release, but will not load 4.4.x

