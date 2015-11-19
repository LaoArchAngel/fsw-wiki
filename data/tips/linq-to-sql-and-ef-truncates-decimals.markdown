LINQ to SQL (and apparently LINQ to Entities (EF)) truncate values when the target DB data type (e.g. decimal(18,2)) has less precision than a .NET value (e.g. decimal type with 5 decimal places). The value is truncated when generating the SQL (e.g. in response to ```SubmitChanges()``` call) before sending the SQL to the database.  This truncation is different than perhaps the expected behavior of rounding.

#### Sources

http://stackoverflow.com/questions/8593447/sql-server-rounding-issue-on-insert/8605642#8605642

http://stackoverflow.com/questions/570342/linq-to-sql-decimal-datatype-truncated-instead-of-rounded

http://stackoverflow.com/questions/2339806/decimal-places-not-rounding-correctly-is-this-a-linq-to-sql-bug