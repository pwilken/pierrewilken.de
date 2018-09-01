---
layout: post
title: Database to code with a Firebird database
lang: en
ref: dbtocodefirebird
date: 2018-04-21 11:45:00 +0300
description: Database to code with a Firebird database
img: scaffold.jpg
tags: [Firebird, Database to code, scaffolding, entityframework core, ASP.Net Core]
---

# Database to Code with a Firebird Database
Generate Models, Controller and Views in a "ASP.Net Core Web Application" using a existing Firebird Database

## Step 1: Create a ASP.Net Core Web Application

## Step 2: Add the following nuget-packages
- EntityFrameworkCore.FirebirdSql
- Microsoft.AspNetCore.All
- Microsoft.NETCore.App
- Microsoft.VisualStudio.Web.CodeGeneration.Design

## Step 3: Build and Save the connection string to your DB 
Using example values.

String for dbfilename.fdb 
```sh
"User=sysdba;Password=masterkey;Database=/firebird/data/dbfilename.fdb;DataSource=127.0.0.1;
Port=3050;Dialect=3;Charset=NONE;Role=;Connection lifetime=15;Pooling=true;MinPoolSize=0;
MaxPoolSize=50;PacketSize=8192;ServerType=0;"
```

## Step 4: Use Scaffold to reverse the DB-Models
Use the following command, for example in the Package Manager Console
```sh
Scaffold-DbContext "User=sysdba;Password=masterkey;Database=/firebird/data/dbfilename.fdb;
DataSource=127.0.0.1;Port=3050;Dialect=3;Charset=NONE;Role=;Connection lifetime=15;
Pooling=true;MinPoolSize=0;MaxPoolSize=50;PacketSize=8192;ServerType=0;"
EntityFrameworkCore.FirebirdSQL -o Models
```

## Step 5: Generate Controller and View
Right-Click on your project -> Add -> New Scaffolded Item...
-> MVC Controller with views, using Entity Framework

![Foo](http://pierrewilken.de/assets/img/dbtocode_fb.png)

The data context class is generated for all Models of the database.

## Step 6: Small Modification
Add in Startup.cs -> ConfigureServices(IServiceCollection services)
 ```sh           
services.AddDbContext<_firebird_data_dbfilename_fdbContext>(
   options => options.UseFirebird(
   Database.GetConnectionString()
 ));
```

Add this constructor in _firebird_data_dbfilename_fdbContext
 ```sh    
public _firebird_data_dbfilename_fdbContext(DbContextOptions<_firebird_data_dbfilename_fdbContext> options) 
                                            base(options)
{            
}
```

## Step 7: View the result
Just start without debugging and put the Controller name without "Controller" at the end of the url.
http://localhost:51710/AddContacts

