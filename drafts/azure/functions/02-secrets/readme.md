---
title: Azure Functions - Reading users from microsoft graph
series: Azure Functions - Getting started
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

# Creating secrets

```powershell
dotnet user-secrets init 
```

This step will create a folder on **%APPDATA%\Microsoft\UserSecrets** and this folder name will be added on your .csproj file in a UserSecretsId tag.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
    <AzureFunctionsVersion>v4</AzureFunctionsVersion>
    <UserSecretsId>12345678-1234-1234-1234-1234567890ab</UserSecretsId>
  </PropertyGroup>
  
  ...

</Project>
```

Then you can add new values to your secret

```powershell
dotnet user-secrets set tenantId "MY_TENANT_ID"
dotnet user-secrets set clientId "MY_CLIENT_ID"
dotnet user-secrets set clientSecret "MY_CLIENT_SECRET"
```

**MY_TENANT_ID** => It's a GUID value like '12345678-1234-1234-1234-1234567890ab'. You can get this value on your tenant's overview page. https://aad.portal.azure.com/
**MY_CLIENT_ID** => It's a GUID value like '12345678-1234-1234-1234-1234567890ab'. You can get this value on your app registration's overview page. https://portal.azure.com/
**MY_CLIENT_SECRET** => It's like an ecrypted password Q~nfpjRObkLeRjQsyD. You can get this value once when you create a new client secret on your app registration's page. https://portal.azure.com/

Then your values will be kept in a **secrets.json** file

```json
{
  "tenantId": "12345678-1234-1234-1234-1234567890ab",
  "clientId": "12345678-1234-1234-1234-1234567890ab",
  "clientSecret": "Q~nfhpjRgObkjLeRmjQTsryD"
}
```

## Sources
- [Build Azure Functions with Microsoft Graph](https://docs.microsoft.com/en-us/graph/tutorials/azure-functions)
- [App Secrets](https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets)
- [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/overview)

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.