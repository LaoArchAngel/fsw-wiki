## Client/Consumer Requirements
We want our API's to be as easy to use as possible.  This means as little setup as necessary; hopefully nothing more than specifying which environment the API has been deployed to.  If possible run-time environment discovery would be even better (using an environment variable or shared config entry?).

Usage:
* Use NuGet to find and reference the API assembly
* Reference the API namespace as a using statement
* Use a static factory method on the service factory to create the needed service interface
* Call the service methods on the service as necessary

Example:
```csharp
using Disribution.Core.Api

public class MyConsumer {
    public static async Task<DistributableProduct> DoWork(String sku) {
        // use factory to get an instance of the ServiceInterface
        IDistributableProductService productSvc = ServiceFactory.GetIDistributableProductService(env);

        // call async methods on the service in a non-blocking way using await
        DistributableProduct product = await productSvc.FindBySkuAsync(sku);

        // ToString() is overridden so it will return a "pretty" representation including all public fields
        Console.Log(product.ToString()); 

        // return the retrieved product
        return product
    }
}
```

## Project File Naming Requirements
Assemblies should be properly named as follows:
* WinForm       - <projectname >_Winform
* Console       - <projectname >_Console
* Win service   - <projectname >_Service
* Class Library - <projectname >_Library
* Web Site      - <projectname >_Site
* Web Service   - <projectname >_WS
* Http Handler  - <projectname >_Handler

…where <projectName> is the base level namespace of all the contained classes.  For example:
* Distribution.Core.API_Library.csproj     (contains Distribution.Core.API classes and, possibly private implementation)
* Distribution.Core_Library.csproj         (contains all Distribution.Core classes except those contained in more specific projects/assemblies)

## Project Scaffolding Generation
A Service Library scaffolding generator has been create to simplify the process of creating new service libraries or new Service Models and their associated Service Interfaces as well as Service Implementation, Repository, and Test classes.  This also includes changes necessary to include the new source files in the .csproj files as well as creation of new methods on the service factory.  It is presently a work in progress, but will be completed in the coming weeks (1-2 weeks to completion).  For more information about scaffolding generation, or to contribute to the code generator source code, please see the [generator git repo](http://gitlab.fsw.com/architecture/generator-service-lib/tree/master) 

## System API Requirements
Subsystem API's can exist in their own assembly separate from the Domain Code/Business Logic but will most often be combined with a private default implementation, hidden from consumers.  A `System API` must consist of one or more `Service Model`s, one or more `Service Interface`s, and a `Service Factory`; clearly indicated as a public, consumable API by their presence in a namespace ending with `API`. 

### Service Models (Portable Types)
Service Models are expected to be Portable types and, therefore, must be Serializable.  Typically the SerializableAttribute can be used to instruct the framework to use the default serialization process. If you need more control, your Service Models can implement the ISerializable interface and implement your own code to serialize the object in the GetObjectData method (and updating the SerializationInfo object that is passed in to it).

```csharp
[Serializable]
public class DistributableProduct {
    .
    .
    .
}
```
-

Additionally, for convenience, Service Models should implement `ICloneable.Clone()`, which is a deep copy.  A specific `Clone()` implementation maybe provided in the future to ensure implementation consistency.

```csharp
[Serializable]
public class DistributableProduct: ICloneable {
    object ICloneable.Clone()
    {
        //call the strongly typed version
        return this.Clone();
    }

    public DistributableProduct Clone()
    {
        return (DistributableProduct) CloneHelper.CloneBySerializing(this);
    }
}
```
-

Service Models must override ToString(), GetHashCode(),  and Equals() – Specific guidance (regarding exactly how these methods should be implemented) will be provided in order to ensure a standard approach.
```csharp
    public override String ToString() {...}

    public override Int32 GetHashCode() {...}

    public override Boolean Equals(Object o) {...}
```
-

Service Models should not represent tree structures and should not contain circular associations.  Composite Service Models should be kept small, if used at all, and should always be completely hydrated -- partially hydrated service models should be considered INVALID.
All dates should be stored as a DateTimeOffsetTime object.  This ensures that time zone is not lost and allows the ToUniveralTime() method to always calculate DateTime correctly.  Dates and times should always be serialized to RFC1123 format.

```csharp
// Tue, 17 Apr 2012 16:46:48 GMT - Used for HTTP headers
String rfc1123 = myDate.ToString("r");
```
-

Service Models should avoid inheritance under most circumstances.  Inheritance causes serializability issues which is one of the most important features of Service Models (portable types).  Marker interfaces are generally OK, and only serializable generic types should be used within Service Models due to serializability(portability) issues.

### Service Interfaces
The public behavioral contract for any system should be specified using Service Interfaces.  Service Interfaces specify what behaviors the API provides and should, under most circumstances, take and return `Service Models`.  All service models should return Task or Task<T> to ensure future proofing for async behavior since Task can ultimately behave synchronously as well as asynchronously.  As much as possible require Service Models instead of Id's as parameters to service functions.  In fact, it is preferable to create a new Service Model having only an Id property and bind to that in the service contract instead of accepting a raw Id parameter.  This guidance is, of course, not applicable to `FindByIdAsnc()` methods.  Decisions made in this area are use case specific, however, the architecture team should be consulted before exceptions are made.
```csharp

// an actual sellable product (from another pillar API)
public class SellableProduct {
    public Guid Id { get; set; }
    .
    .
    .
}

// specifically created for use by IOrderService.AddLineItem() (part of current API)
public class ProductReference {
    public Guid Id { get; set; }
}

// ordering service interface
public interface IOrderService {
    // preferred
    Task AddLineItemAsync(Order order, SellableProduct product);

    // acceptable
    Task AddLineItemAsync(Order order, ProductReference productRef);

    // discouraged
    Task AddLineItemAsync(Order order, Guid sellableProductId);

    // a standard async find by Id method
    Task<Order> FindByIdAsync(Guid id);
    .
    .
    .
}
```

### Service Factories
Service Interfaces must be instantiated using a public Service Factory.  The point of the service factory is to control the creation of Services without leaking implementation details.  The minimal implementation of a Service Factory should be as follows:

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Distribution.Core.Impl;

namespace Distribution.Core.Api
{
    public static class ServiceFactory
    {
        public static IDistributableProductService IDistributableProductService() {
            return new Business.DistributableProductService();
        }
         public static IInventoryService IInventoryService() {
            return new Business.InventoryService();
        }
   }
}  
```

## Service Implementation Requirements
Concrete service classes that implement service interfaces should be instantiated by a service factory.  Service implementation classes should be package visible and **NEVER Public**.  All service methods must validate the parameter input to ensure data consistency and detect (escape) injection attacks.

```csharp
class DistributableProductService: IDistributableProductService {
   public async Task Create(DistributableProduct) {...}
   public async Task<DistributableProduct> FindById(Guid id) {...}
   public async Task<DistributableProduct> FindBySku(String sku) {...}
   public async Task<IList<DistributableProduct>> FindByCost(double cost) {...}
   public async Task Update(DistributableProduct) {...}
   public async Task Delete(DistributableProduct) {...}
}
``` 

## Data Access Framework Requirements
Data access code must use either [Dapper Framework](https://github.com/StackExchange/dapper-dot-net) or [Entity Framework](https://github.com/aspnet/EntityFramework/wiki) for data persistence.  Data tiers should use a Repository Facade encapsulating the data access framework within the Repository implementation and use async persistence methods when they exist.  While the Repository can create a *Persistable Model* (Data Model), using the *Service Model* is preferred whenever possible to avoid excess object-to-object mapping/serialization.  If the data to be persisted is not exactly the same as the fields exposed by the *Service Model*, a *Persistable Model* will be required.  More detail to come.

## Exception Handling Requirements
If we follow [this guidance](https://itworksonmymachine.wordpress.com/2008/05/06/exception-handling-dos-and-donts/) we will be in great shape.  However, since the reference exception handling article does not explicitly address them, additional points of guidance have been provided below:
* **Don't** catch an exception if you do not know how to handle it -- just let the exception bubble up.  The application should support a `catch-all` exception handler so we should never be afraid of allow exceptions to bubble out of our code.
* **Don't** log and exception if it is not being handled.  That is to say,  If your code catches all exceptions for the sole purpose of logging the exception, **resist the temptation**!  Instead, let the exception bubble to the `catch-all` error handler.
* **Do** log handled exceptions if they are truly exceptional or provide useful information about what happened and how the exception is being handled by the application.  If a handled exception occurs often be sure to lower the log-level at which it is being logged (debug?).

## Logging Requirements
A good baseline regarding log levels and how to use them can be found [at the joy of coding](http://www.thejoyofcode.com/Logging_Levels_and_how_to_use_them.aspx).  This is a good base set of guidance, the bulk of which has been included below:

* Debug - This is the most verbose logging level (maximum volume setting). I usually consider Debug to be out-of-bounds for a production system and used it only for development and testing. I prefer to aim to get my logging levels just right so I have just enough information and endeavor to log this at the Information level or above.
* Information - The Information level is typically used to output information that is useful to the running and management of your system. Information would also be the level used to log Entry and Exit points in key areas of your application. However, you may choose to add more entry and exit points at Debug level for more granularity during development and testing.
* Warning - Often used for handled 'exceptions' or other important log events. For example, if your application requires a configuration setting but has a default in case the setting is missing, then the Warning level should be used to log the missing configuration setting.
* Error - Used to log all unhandled exceptions. This is typically logged inside a catch block at the boundary of your application.
* Fatal - Fatal is reserved for special exceptions/conditions where it is imperative that you can quickly pick out these events. I normally wouldn't expect Fatal to be used early in an application's development. It's usually only with experience I can identify situations worthy of the FATAL moniker experience do specific events become worth of promotion to Fatal. After all, an error's an error.

## Instrumentation Requirements
We should use LogCentral to capture application metrics and request-level instrumentation.  LogCentral supports MS MVC web applications as well as MS Web API applications.  The implementation details vary depending which web technology is used.  Specific details regarding LogCentral can be found [here](http://gitlab.fsw.com/LogCentral/logcentral.net) TODO: Find the correct link!
