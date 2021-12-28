# Windows 11
win + r
tpm.msc
specific version

system information
secure boot state

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
 

## OpenID Connect
client (Angular App) -> calls for login -> Identity Provider
Identity Provider -> sends a token -> This user is authenticated to use your app
Host Website to rendering the website
Backend APIS to receive the app requests (with tokens) from clients

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

