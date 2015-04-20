## Internationalization Requirements
Do we want to specify the use of resource managers and externalizing all resource strings that are otherwise exposed to the users?

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
The public behavioral contract for any system should be specified using Service Interfaces.  Service Interfaces specify what behaviors the API provides and should, under most circumstances, take and return `Service Models`.

### Service Factories
Service Interfaces must be instantiated using a public Service Factory. The minimal implementation of a Service Factory should be as follows:

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
Concrete service classes that implement service interfaces should be instantiated by a service factory.  Service implementation classes should be package visible **NOT Public**.  All service methods must validate the parameter input to ensure data consistency and detect (escape) injection attacks.

## Data Access Framework Requirements
Data access code must use either Dapper framework or Entity framework for data tier.  Data tier should use a Repository class for data persistence encapsulating the data access framework behind the repository class.  While the repository can create a *Persistable Model*, taking the *Service Model* is preferred whenever possible.  If the data being persisted is not exactly the same as the fields exposed by the *Service Model*, a *Persistable Model* will be required.

## Exception Handling Requirements
*** Need to outline minimum level of exception handling (reference framework components) ***

## Logging Requirements
*** Need to outline minimum level of logging (reference framework components) ***

## Instrumentation Requirements
*** Need to outline minimum level of instrumentation (reference framework components) ***
