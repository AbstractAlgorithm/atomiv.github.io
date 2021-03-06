---
title: Get Started
category: dotnet
authors: [ valentina-cupac, milan-vidakovic ]
---

## Template Installation

Note: If you're using Visual Studio, then: Run Visual Studio \(in the "Getting Started", select "Continue without code"\), use the Package Manager Console \(Tools &gt; NuGet Package Manager &gt; Package Manager Console\) to install the Atomiv Template \(in the future you can also uninstall and re-install newer versions\):

Run the following command:

```text
dotnet new -i Atomiv.Templates
```

## Create project

Create the directory for your new project \(MyWebShop\) and go inside that directory:

```text
mkdir MyWebShop
cd MyWebShop
```

Create a new solution \(MyWebShop.sln\) based on the template inside that directory:

```text
dotnet new atomiv
```

You should see output like:

```text
The template "Atomiv" was created successfully.
```

## Open project

Note: If you're using Visual Studio, then open the solution \(MyWebShop.sln\) and set MyWebShop.Web.RestApi as the StartUp project.

Build the solution:

```text
dotnet build .\MyWebShop.sln
```

You should see output like:

```text
Microsoft (R) Build Engine version 16.5.0+d4cbfca49 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.
...
Build succeeded.
...
```

## Database connections

You can check the database connections, in the following:

* Src\Web\MyWebShop.Web.RestApi
* Src\Tools\MyWebShop.Tools.Migrator
* Test\Web\MyWebShop.RestApi.IntegrationTest

Open up the appsettings files and check DefaultConnection.

## Run project

Run the project from the command line:

```text
dotnet run --project .\src\Web\MyWebShop.Web.RestApi
```

You will see output here, including the environment and the url:

```text
Hosting environment: Development
Content root path: C:\Users\Valentina.Cupac\source\repos\MyWebShop\src\Web\MyWebShop.Web.RestApi
Now listening on: http://localhost:5100
Now listening on: https://localhost:5101
Application started. Press Ctrl+C to shut down.
```

Type in https://localhost:5101 in your browser, you will see Swagger, then run the command POST /api/customers and verify that you get a success message.

At the end, type in Ctrl+C to shut down the API (or the stop button, if you're running this inside Visual Studio Package Manager Console).

Note: If you're using Visual Studio, then you can run the application in Debug mode. The application opens up automatically, e.g. [https://localhost:44315/](https://localhost:44315/api/values). You can stop debugging at the end.

## Run project (via Docker)

In Visual Studio, select to debug with "Docker" (instead of "IIS Express").

When you run it, this should open up the REST API. You should see Swagger.

Then run the command POST /api/customers and verify that you get a success message.

<!-- TODO: VC: Command line way currently not working for Docker, pending check -->

## Manual tests

You can manually run the REST API via Swagger. Go to [https://localhost:5101](https://localhost:5101) and you will see the Swagger page.

Click on POST /api/customers, then click on "Try it out", then click on "Execute". Check that you see the response code 201.

You can also run this test via Postman.

You can also execute API calls via swagger, e.g. [https://localhost:44315/swagger/index.html](https://localhost:44315/swagger/index.html) and verify that the response is successful. \(Note that the port on your computer may differ from the port here.\) Finally, at the end you can stop debugging.

## Automated tests

You can run tests via the command:

```text
dotnet test .\MyWebShop.sln
```

You should see output like:

```text
Microsoft (R) Test Execution Command Line Tool Version 16.5.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...

...

Test Run Successful.
```

Note: If you're using Visual Studio, then to run the automated tests, open up the Test Explorer \(Visual Studio main menu: Test &gt; Windows &gt; Test Explorer\) and rebuild the solution to discover all the tests. For Integration and System tests, you can set the database connection string \(opening up appsettings.Test.json inside the test projects and setting a value for DefaultConnection\). Click on “Run All” inside the Test Explorer \(all tests should pass\).

## Custom development - Overview

We recommend you familiarize yourself with the solution and then you can adapt it to your own needs. This current template uses the eCommerce sample, with Customers, Products and Orders. However, let's say you're making an application for dentists, you could have Dentists, Patients and Appointments, etc.

## Custom development - Migrations



```text
dotnet ef database update --project .\src\Tools\MyWebShop.Tools.Migrator
```

You should see outout like:

```text
Build started...
Build succeeded.
The environment is Development.
Applying migration ...
Applying migration ...
Done.
```

You can verify inside SQL Server Management Studio that the database has been created.



To add a new migration:

```text
PM> dotnet ef migrations add NameOfTheNewMigration --project .\src\Tools\MyWebShop.Tools.Migrator
```

To remove the last run migration:

```text
PM> dotnet ef migrations remove --project .\src\Tools\MyWebShop.Tools.Migrator
```

To update the database based on migrations:

```text
PM> dotnet ef database update --project .\src\Tools\MyWebShop.Tools.Migrator
```
