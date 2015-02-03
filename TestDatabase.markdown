# Test Database
The test database is an MDF file that contains the same schema as the main FSW database,
but none of the data.  The purpose of the database is to provide the unmockable
[ObjectContext](https://msdn.microsoft.com/en-us/library/system.data.objects.objectcontext%28v=vs.110%29.aspx) a fake data source so that developers can write tests that
are as close to [unit tests](UnitTesting) as possible.

The test database should never be committed to the repository beyond what is already
available.  Instead, the database must be prepared before running any unit tests.

## Database File
The database file is part of the [FswGit](FSW/FswGit) repository.  The file can
be found in the following path:

`$/UnitTest/Database/Main.mdf`

The file can also be obtained [directly from the repository](FSW/FswGit/UnitTest/Database).

## Connection Strings
All connection strings to the FSW database should be replaced to point to the database
file in the repository.
