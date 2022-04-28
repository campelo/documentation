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

# Dependency Injection

## Prerequisites

Before you can use dependency injection, you must install the following NuGet packages:

- [Microsoft.Azure.Functions.Extensions](https://www.nuget.org/packages/Microsoft.Azure.Functions.Extensions/)

- [Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/) package version 1.0.28 or later

- [Microsoft.Extensions.DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection/) (currently, only version 2.x or later supported)


## Creating Startup Class

You should create a startup class to configure all of your dependencies.

```C#
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.DependencyInjection;

[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]

namespace MyNamespace
{
    public class Startup : FunctionsStartup
    {
        public override void Configure(IFunctionsHostBuilder builder)
        {
            builder.Services.AddTransient<IMyTransientService, MyTransientService>();
            builder.Services.AddScoped<IMyScopedService, MyScopedService>();
            builder.Services.AddSingleton<IMySingletonService, MySingletonService>();
        }
    }
}
```

## Creating your Interfaces and Implementations

Now, you can create all new interfaces and their implementations.

**IMyTransientService.cs**

```C#
using System.Threading.Tasks;

namespace MyNamespace
{
  public interface IMyTransientService
    {
        Task DoSomething();
    }
}
```

**MyTransientService.cs**

```C#
using System.Net.Http.Headers;
using System.Threading.Tasks;
using Microsoft.Graph;
using Microsoft.Identity.Client;

namespace MyNamespace
{
  public class MyTransientService : IMyTransientService
  {
    public async Task DoSomething()
    {
      // your implementation here...
    }
  }
}
```

## Using your classes by DI

Then you can use your injected object as usual.

```C#
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using System.Threading.Tasks;

namespace MyNamespace
{
  public class FunctionForTest
  {
    private readonly IConfiguration _configuration;
    private readonly IMyTransientService _myTransientService;

    public FunctionForTest(IConfiguration configuration, IMyTransientService myTransientService)
    {
      _configuration = configuration;
      _myTransientService = myTransientService;
    }

    [FunctionName("FunctionForTest")]
    public async Task<IActionResult> Run(
        [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequest req,
        ILogger log)
    {
      log.LogInformation("C# HTTP trigger FunctionForTest processed a request.");

      string qParam = req.Query["qParam"];
      
      // your code here...

      await this._myTransientService.DoSomething();

      return new OkObjectResult("Action finished!");
    }
  }
}
```

## To read about
- **knownClientApplications** in manifest

## Sources
- [Dependency Injection in Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-dotnet-dependency-injection)
- [Build Azure Functions with Microsoft Graph](https://docs.microsoft.com/en-us/graph/tutorials/azure-functions)

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.