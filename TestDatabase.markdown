# Test Database
The test database is an MDF file that contains the same schema as the main FSW database,
but none of the data.  The purpose of the database is to provide the un-mockable
[ObjectContext](https://msdn.microsoft.com/en-us/library/system.data.objects.objectcontext%28v=vs.110%29.aspx) a fake data source so that developers can write tests that
are as close to [unit tests](UnitTesting) as possible.

The test database should never be committed to the repository beyond what is already
available.  Instead, the database must be prepared before running any unit tests.

## Database File
The database file is part of the [FswGit](FSW/FswGit) repository.  The file can
be found in the following path:

`$/UnitTest/Database/Main.mdf`

The file can also be obtained [directly from the repository](FSW/FswGit/UnitTest/Database).

## Rules for the Database File
### Rule No. 1 of the Database Files
Do not commit changes to the database files.

### Rule No. 2 of the Database Files.
Do **NOT** commit changes to the database files.

## Connection Strings
All connection strings to the FSW database should be replaced to point to the database
file in the [**UnitTest**](TFS/FswGit/UnitTest) project.  You can use the following lines as templates:

```xml
<add name="FoodServiceWarehouseConnection" connectionString="Data Source=(LocalDB)\v11.0;AttachDbFileName=C:\FSWGIT\FSWGIT\UNITTEST\DATABASE\MAIN.MDF;Integrated Security=True;Pooling=False;MultipleActiveResultSets=False;Connect Timeout=30" providerName="System.Data.SqlClient" />
<add name="FoodServiceWarehouseConnectionString" connectionString="Data Source=(LocalDB)\v11.0;AttachDbFileName=C:\FSWGIT\FSWGIT\UNITTEST\DATABASE\MAIN.MDF;Integrated Security=True;Pooling=False;MultipleActiveResultSets=False;Connect Timeout=30" providerName="System.Data.SqlClient" />
<add name="FswEntities" connectionString="metadata=res://FswDataModel/FswDataModel.Main.FswDataModel.csdl|res://FswDataModel/FswDataModel.Main.FswDataModel.ssdl|res://FswDataModel/FswDataModel.Main.FswDataModel.msl;provider=System.Data.SqlClient;provider connection string=&quot;Data Source=(LocalDB)\v11.0;AttachDbFileName=C:\FSWGIT\FSWGIT\UNITTEST\DATABASE\MAIN.MDF;Integrated Security=True;Pooling=False;MultipleActiveResultSets=False;Connect Timeout=30&quot;" providerName="System.Data.EntityClient" />
```
_Make sure to change the **AttachDbFileName** setting to your appropriate path_

## Using the Database
### Adding to Visual Studio
1. Open the _Server Explorer_ window.
  * If you cannot find the _Server Explorer_ window, click on _VIEW > Server Explorer_.
2. Click the _Connect to Database_ icon.
3. In the _Add Conection_ window, click the _Change..._ button next to the _Data
Source_ field.
4. In the _Change Data Source_ window, select _Microsoft SQL Server Database File_
and click the _OK_ button.
5. In the _Add Connection_ window, click the _Browse..._ button.
6. In the _Select SQL Server Database File_ window, browse to the unit test database,
select it, and click the _OK_ button.
  * The database can be located in the _UnitTest/Database_ folder in the _FswGit_
  repository.
7. You can see the database as a _SQL Server Object_ by right-clicking on the _Main.mdf_
database connection in the _Server Explorer_ window and clicking the _Browse in
SQL Server Object Explorer_ option.

### Updating the Schema
1. Open the _SQL Server Object Explorer_ window.
  * If you cannot find the _SQL Server Object Explorer_ window, click on _VIEW >
  SQL Server Object Explorer_.
2. Expand the _(LocalDB)\v11.0_ server and _Databases_ folder until you see the
_Main.MDF_ file database.
3. Right-click on the _Main.MDF_ file database and click on _Schema Compare_.
4. In the _Schema Compare_ window, click on the _Switch source and target_ button
to make sure that the _Main.MDF_ database is on the right / target side.
5. In the _Source_ drop-down, select the _Select Source..._ option.
6. In the _Select Source Schema_ window, select the _Project_ option and _FswDB_
from the drop-down, then click the _OK_ button.
7. In the _Schema Compare_ window, click the _Compare_ button and wait for the
comparison.
8. Once the comparison is available, click the _Update_ button and confirm.
9. Drop the database constraints.

### Dropping Database Constraints
In order to simulate a closer unit testing strategy, we must be able to add data
and objects to the database without adding any prerequisites.  For example, we should
be allowed to create a **Project** without first having to create a **Contact**
or **Account**.
1. In the _Solution Explorer_ window, navigate to _UnitTest/Database_ and open
_RemoveConstraints.sql_.
2. In the Query window, click _Open Connection_.
  * If _Open Connection_ is not an option, click _Change Connection_.
3. In the _Connect to Server_ window, in the _Server name_ text box, type in the
name of the server and click _Connect_.
  * The server is usually _(LocalDB)\v11.0_.  You may not see it in the local database
  list.
4. In the _Available Databases_ drop-down list, select the _Main.MDF_ database.
5. Click the _Execute_ button or press _Ctrl + Shift + E_.
  * Do not press _F5_ or Visual Studio will enter Debug mode on any open solution.

### Writing Unit Tests with Data
Once the database has been added to the IDE and updated to the appropriate schema,
the database is ready to use.  Make sure that all appropriate connection strings
in the _App.config_ for the _UnitTest_ project are set up appropriately.  Then,
simply create an instance to a new **FswUnitOfWork**, add any necessary data, save
the database, and run your tests.

```csharp
[Fact]
public void Some_method_with_contact_with_no_projects_returns_false()
{
  var uow = new FswUnitOfWork();
  var newContactId = uow.Contacts.Max(c => c.ContactID) + 1;
  var contact = Contact.CreateContact(newContactId, 1, DateTime.Now, 1, 1, true);

  uow.Contacts.Add(contact);
  uow.SaveChanges();

  var svc = new ContactService();
  bool actual = svc.Some_method(newContactId);

  Assert.IsFalse(actual);
}
```
### Resetting the Test Database
After running your tests, chances are that trying to re-run them will cause conflicts
with the data created by your previous run.  In order to get the database file ready
to re-run tests, you may have to reset the database files.  This is a multi-step
process.
1. Exit _Visual Studio_ to unlock the database files.
  * It's also possible to disconnect the database, but then you will have to go
  through the connection process again.
2. Check-out the _Database_ folder in the _UnitTest_ project.
  * `git checkout -- UnitTest/Database`
3. Follow the steps in **[Updating the Schema](#updating-the-schema)** and
 **[Dropping Database Constraints](#dropping-database-constraints)**.
