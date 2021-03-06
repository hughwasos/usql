
# U-SQL

### Can I read/write files using code that is running within a U-SQL User-defined Operator (UDO)?

No. This is disallowed.

### Q: Can I get a single value back from a rowset?

You may be trying to do something like ehat is shown below - and expect MaxDate to be a single scalar value

    @MaxSize = SELECT MAX(Size) AS MaxSize FROM input;

U-SQL does not support retrieving a single scalar value from a rowset. You can only retrieve another rowset.

Thus, @MaxSize is not a value of type long, but instead is a rowset with a single row and a single column of type long called MaxSize.

### Q: How can I do something like Excel's AVERAGEIF( )?

Use C# expression syntax, for example if the column you want (called foo) is of type int then use

    @rows = SELECT AVG(foo > 0 ? (int?)foo : (int?)null) AS AvgFoo 

### Q: How can a create an "empty" rowset - a rowset with zero rows?

   // Pending an Answer from the U-SQL team 

### Q: Can my U-SQL script make a network call to some other machine?

No. This is explicitly disallowed and unsupported. 


### Q: How can I test if a stream exists in a U-SQL script?

There is no way to do this from within a U-SQL Script.

### Q: How can I do a correlated subquery like in SQL?

U-SQL  doesn't have correlated subqueries.

Most scenarios for correlated subquery can be expressed via a JOIN. Use that technique instead.


### Q: How can I Assign Unique IDs to rows?

Use Windowing Functions.

    @rs1 = SELECT *, ROW_NUMBER() OVER ( ) AS UID 
         FROM @rs0;  

### Q: Can I have a different schema for each row in a a U-SQL rowset?

No. A U-SQL RowSet must contains rows and each rwo must have the same schema: same column names, with the same types, in the same order


# U-SQL Catalog

### Q: Is there an API to read or write a U-SQL table locally?

If you are looking for an API like "CreateTable(name)"... no.

The only supported way of creating a table is to run a U-SQL script in ADL Tools for Visual Studio.


