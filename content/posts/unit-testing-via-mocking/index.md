---
title: "Is Unit Testing via Mocking Enough?"
date: 2022-10-22T16:38:13-07:00
draft: false
---

At the onset, I will admit that I am not a fan of mocking, in the conventional sense, for testing. The conventional 
mocking is using mocking libraries like Mockito or Moq for mocking objects and interfaces. I have used them 
extensively, and still use them sometimes, but for me they have never served the _raison d'être_ of testing itself, 
namely, to catch breaking changes in the code. They may superficially serve testing the _initial_ behaviour of the 
code, but have never served me well for code maintenance. In fact, at one point, I loathed writing unit tests via 
mocking frameworks because I was forced to change my design in order to make my code "testable".

#### Design modifications
For example, I was forced to, only for writing tests, make changes like following only because of the test framework:
* Make `private` objects either package-private (Java) or `internal` (C#)
* Remove `static` objects or methods
* Remove `final` (Java)/`sealed` (C#) from classes

In such scenario, you either change your design to suit the whims of the mocking framework, or change the framework 
to something like PowerMockito - which comes with its own can of worms. Neither of these are acceptable scenarios, 
why change the design to make the code more "testable"? Why unnecessarily expose `private` methods or unseal the 
classes? Won't these changes compromise security or design only because our code is more _testable_? The tests 
should test the design, the design should not change because of tests. For this reason, I came to detest the 
so-called unit testing and mocking frameworks.

Consider another example, suppose you are writing a program (in C#) for connecting to a SQL-Server DB and running a 
query. The program may look like:

```csharp
var sql = @"RESTORE DATABASE test-db FROM DISK=N'C:\test.bak'";
using var conn = new SqlConnection("connection-string");
using var cmd = new SqlCommand(sql, conn);
conn.open();
int output = cmd.ExecuteNonQuery();
```

And, if you were writing unit tests with mocking, then you will likely mock the connection to the DB server with 
something like:

```csharp
mockCmd.Setup(x => x.ExecuteNonQuery()).Return(0);
```

The tests will run successfully, you will check in the code, only to realise that your code is not running as expected!
The SQL Server will complain about `-` in `test-db`, in order to correct it, you need to enclose the name of DB in `
[` and `]`, like `[test-db]`. What purpose, then, has this test served?

We have assumed that the code is written correctly, and we proceeded to mock the DB connection. That is exactly 
opposite of what a test is supposed to do! And this is another reason of my dislike for such _unit_ tests. 

#### No way to benchmark performance
Suppose you have mocked out your call to DB, and you make thousands of queries. Since the mock gives you 
instantaneous results, you will not be able to find out the cost of your operations

Extending the example of database mocks, what are the memory considerations of running a complex query? Even though 
you have tested the query on DB, and it is working as desired, what will happen when you execute that query from the 
code? Complex DB queries can have significant memory overhead. This is because the drivers try to parse and optimise 
the query as much as possible before sending it over the network, this is to minimise the load on DB server.  



### What, then, are unit tests? What should be mocked?
Mocking the data is one good example of mocking. If an application is designed for an ETL (Extraction, 
Transformation, and Loading) pipeline, then a test database containing all possible sorts of input for this 
application will ensure not-only the testing of database connection, but also the business logic itself. No need to 
change internal design, like making `private` methods `public` in order to make the code _testable_. Such mocking 
will not only help with initial coding but also be far more effective in identifying future code modification/addition 
may break existing implementation.

Another example of a valid mock is to mock the responses of a REST-API being developed by another team, which do not 
involve external network hops. If the teams have agreed on the Request-Response data, then it makes little sense for 
the team consuming the response to wait for the deployment of the dependent API. This way the development can be 
done in parallel even though one team depends on another. 

Another scenario, in which mocks may be implemented is when calling external resource involves cost in terms of time 
and/or money. For example, making a call to some external vendor (say Wolfram Alpha)  where they charge for each API 
call, we don't want to exhaust our quota just because we are running unit tests. Or, in a scenario where getting a 
response takes a long time; in such case, the unit tests will take too long to finish. This is with a caveat though, 
that these unit tests are acceptable in the maintenance phase, not development phase of the application. While 
developing the application, it is assumed that the application has been thoroughly tested against actual resource 
calls. 

#### A rule of thumb
As a general rule of thumb, we should be mocking at the lowest possible level of abstraction. Concretely, if we want 
to check if the application is working with data (databases, datasets) then it is best to mock the data itself, 
rather than mock db connection. If it involves triggering another API and working with the response, then it is 
acceptable to mock the responses. The idea is to take the mocks as far away from the implementation as possible (and 
eliminate altogether, if practical). 

### Is such mocking possible as part of regular development? What about the server costs ?
The above suggestions may seem like prohibitively expensive, particularly the one which requires setting up a DB, 
inserting it with mocked data, just for the purpose of testing. But in the world of CI/CD (continuous 
integration/continuous deployment) where containerisation has become a standard, it is a one-time effort to write 
scripts for starting a container with DB or other services for running the tests.

In fact, writing scripts for containers takes less time than writing the mocks, the benefits, however, are 
exponentially high. 

