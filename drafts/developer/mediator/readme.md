---
title: Mediator
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

# Mediator

## Creating the project
Create a new Web API project

## Install nuget dependencies
```powershell
Install-Package MediatR
Install-Package MediatR.Extensions.Microsoft.DependencyInjection
```

## Add mediator services
```csharp
Services.AddMediatR(typeof(Program))
```

## Add a new controller
For this sample we're creating a ProductController.

Inside this class you have to add IMediator, ISender or IPublisher readonly field by dependency injection.
```csharp
private readonly IMediator _mediator;
```

Create also a new Product class with some properties like Id and Name, for example.

Create a new repository class ProductRepository to simulate or storage. Add to this class an initial list of products. And then add some basic async methods Create, GetAll.

Create three new folders called Commands, Queries, Notifications and Handlers.

Commands - Manage data (Create, Update, Delete)
Queries - Retrieve data (Get)
Handlers - Handle a command or query.
Notifications - Send notifications.
Behaviors - Behavior of 

## Query

Create a GetProductQuery record that implements IRequest<IEnumerable<Product>>. (Queries folder)
Create a GetProductHandler class that implements IRequestHandler<GetProductQuery, IEnumerable<Product>>. (Handlers folder)

Create a GetProductByIdQuery record that implements IRequest<Product>. (Queries folder)
Create a GetProductByIdHandler class that implements IRequestHandler<GetProductByIdQuery, Product>. (Handlers folder)

## Command

Create an AddProductCommnad(Product product) record that implements IRequest<Product>. (Commands folder)
Create an AddProductHandler that implements IRequestHandler<AddProductCommand, Product> or IRequestHandler<AddProductCommand, Unit> *Unit* is used instead of void. (Handlers folder)

## Notification

Create a new method on the repository EventOccured that has two parameters product and event (string)
Create a new record ProductAddedNotification(Product product) that implements INotification. (Notifications folder)
Create a new EmailHandler that implements INotificationHandler<ProductAddedNotification>. (Handlers folder)
Create a new CacheInvalidationHandler that implements INotificationHandler<ProductAddedNotification>. (Handlers folder)

## Behavior

Create a new LoggingBehavior<TRequest, TResponse> class that implements IPipelineBehavior<TRequest, TResponse> where TRequest inherits from IRequest<TResponse> (Behaviors folder). In this implementation, we can add a logger before calling the next action. Get the response ```var response = await next();```. Then log something after the response. Finally, return the response.

Add new middleware service AddSingleton(typeof(IPipelineBehavior<,>), typeof(LoggingBehavior<,>))

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.