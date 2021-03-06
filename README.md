[![Build Status](https://travis-ci.org/carlosjdelgado/MySql.LightServer.svg?branch=master)](https://travis-ci.org/carlosjdelgado/MySql.LightServer)
[![Build status](https://ci.appveyor.com/api/projects/status/9vbaofala03rch1m/branch/master?svg=true)](https://ci.appveyor.com/project/carlosjdelgado/mysql-lightserver/branch/master)
# MySql.LightServer 
A Light MySql Server for tests.

## Use
You can download and use this via [NuGet](https://www.nuget.org/packages/MySql.LightServer/)

## Platforms supported
MySql.LightServer are supported in these frameworks:
* Net Framework 4.5.2
* Net Framework 4.6
* Net Framework 4.6.1
* Net Framework 4.6.2
* Net Standard 1.6 (NET Core)

You can run MySql on a Linux (NET Core) or a Windows machine, OSX is not supported, maybe in the future...

## How it works
Mysql.LightServer is simply running a minimal instance of MySql for tests. Server is created at run time and cleared at finish.

Mysql.LightServer makes it possible to create and run unit tests on a real MySql server without spending time on server setup.

## Examples
### Create server, table and data.

```c#
        //Get an instance
        MySqlLightServer dbServer = new MySqlLightServer();
        
        //Start the server
        dbServer.StartServer();
        
        //Create a database and use it
        MySqlHelper.ExecuteNonQuery(dbServer.GetConnectionString(), "CREATE DATABASE testserver; USE testserver;");
        
        //Insert data
        MySqlHelper.ExecuteNonQuery(dbServer.GetConnectionString(), "INSERT INTO testTable (`id`, `value`) VALUES (2, 'test value')"); 
        
        //Shut down server
        dbServer.ShutDown();
```
## API
### Constructor
You can specify a port and/or a folder where put the server, default port is 3306 and default server folder is the machine temporal folder.
```c#
        // Constructor by default (port 3306, temporal folder)
        MySqlLightServer dbServer = new MySqlLightServer();
        
        // Constructor with folder specified
        MySqlLightServer dbServer = new MySqlLightServer(rootPath: @"C:\MySqlLightServer");
        
        //Port specified
        MySqlLightServer dbServer = new MySqlLightServer(5000);
        MySqlLightServer dbServer = new MySqlLightServer(port: 5000); 
        
        //Port and folder specified
        MySqlLightServer dbServer = new MySqlLightServer(5000, @"C:\MySqlLightServer");
        MySqlLightServer dbServer = new MySqlLightServer(port: 5000, rootPath: @"C:\MySqlLightServer"); 
        
```
### Properties
* **MySqlServer.ServerPort**: Gets the port of the server (read only).

* **MySqlServer.ConnectionString**: Gets the connectionString of the server.

* **MySqlServer.IsRunning**: Gets if server is running.

### Methods
* **MySqlServer.StartServer()**: Starts the server.

* **MySqlServer.ShutDown()**: Shuts down the server and remove all files related to it.

