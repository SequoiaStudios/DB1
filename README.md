DB1 Documentation
===============
Welcome to the DB1 Documentation.

As an introduction to DB1 (after [installing](#installation)), we'd highly suggest the [Quick Start](#quick-start) guide.

## INDEX
* [Installation](#installation)
* [Quick Start](#quick-start)
* [Reporting Issues and Feature Requests](#feedback)
* [Changelog](#changelog)
    - [V1.0.1](#v101)
    - [V1.0.2](#v102)
    - [V1.1.0](#v110)
* [Commands](#commands)
    - [Connect To Database](#connect)
    - [Change Database](#use-database)
    - [Remove Stored Connection](#remove-connection)
    - [Execute Sql](#execute-sql)
    - [Execute Quick Sql](#execute-quick-sql)
    - [Execute Template](#execute-template)
    - [Commit Changes](#commit-changes)
    - [Rollback Changes](#rollback-changes)
    - [Toggle Autocommit](#toggle-autocommit)
    - [Set Isolation Level](#set-isolation-level)
    - [Set Deferrable (PostgreSQL Only)](#set-deferrable)
    - [Set Readonly (PostgreSQL Only)](#set-readonly)
    - [Open Results Window](#open-results-window)
    - [Open Documentation](#open-documentation)
    - [Report Issue](#report-issue-command)
* [Connection Issues](#connection-issues)
* [Settings](#settings)
    - [Stored Connections](#stored-connections)
    - [Set Syntax on Execute](#set-syntax-on-execute)
    - [Results Table Format](#results-table-format)
    - [Show DB1 Header](#show-db1-header)
    - [Show Query](#show-query)
    - [Query Table Format](#query-table-format)
    - [Show Query Number](#show-query-number)
    - [Show Query Execution Time](#show-query-execution-time)
    - [Show Execution Datetime](#show-execution-datetime)
    - [Datetime Format](#datetime-format)
    - [Show Autocommit Status](#show-autocommit-status)
    - [Show Isolation Level](#show-isolation-level)
    - [Show Deferrable Status (PostgreSQL only)](#show-deferrable-status)
    - [Show Readonly Status (PostgreSQL only)](#show-readonly-status)    
    - [Align Numbers](#align-numbers)
    - [Align Strings](#align-strings)
    - [Erase Results Window](#erase-results-window)
    - [Focus Results Window on Execution](#focus-results-window-on-execution)
    - [Results Window Append Style](#results-window-append-style)
    - [Results Window Location OSX](#results-window-location-osx)
    - [Results Window Location Windows](#results-window-location-windows)
    - [Results Window Location Linux](#results-window-location-linux) 
* [Key Bindings](#key-bindings)
* [License Information](#license-information)
    - [Entering Your License](#enter-license)
    - [Recovering a Lost License](#recover-license)
    - [Alternative Payment](#alternative-payment)
    - [Bulk Discounts](#bulk-discounts)
    - [Refunds](#refunds)
    - [Educational Discounts](#education-discount)
    - [Tax](#tax)
    - [Other](#other)
* [Open Source Libraries Used](#open-source)
    - [pymysql](#pymysql)
    - [psycopg2](#psycopg2)
    - [sqlparse](#sqlparse)
    - [tabulate](#tabulate)
    - [fuzzyfilenav](#fuzzyfilenav)

## <a href="#installation" name="installation">Installation</a>

If [Package Control](https://packagecontrol.io) is already installed: 

1. Open the Sublime Text command palette (```"Tools" > "Command Palette"```) 
2. Enter ```Package Control: Install Package```
3. Enter ```DB1```

Congratulations! DB1 will now be installed. If you are not greeted with the DB1 installation message from Package Control, please restart Sublime Text. 

If [Package Control](https://packagecontrol.io) is not already installed, please follow [the instructions for installation](https://packagecontrol.io/installation), and then follow the above instructions. 


## <a href="#quick-start" name="quick-start">Quick Start</a>
The first step to getting started is making sure that DB1 is [installed](#installation). Once that's done, it might help to check out some of the [commands](#commands) available to DB1.  

Once that's finished, the first big command is ```DB1: Connect to a Database```. ```DB1: Connect to a Database``` initiates a connection for a single view in Sublime Text. This means that there's a one-to-one relationship of connections to views. Each connection is then tied to the database it's connected to, such that in view #1 you can execute queries on database 'A', and in View #2 you can execute queries on database 'B'. 

When using the ```DB1: Connect to a Database``` you'll need to know the database type, username, host, port (if it's not the default) and password of the database you're connecting to. In cases like PostgreSQL authentication (where authentication is [trust](https://www.postgresql.org/docs/9.0/static/auth-methods.html) based) a password is not required. 

To help streamline workflow, if there is not a connection active in the view, then running one of the ```DB1: Execute ... SQL``` will initiate the connection process before the query is then run. 

Once you're connected, DB1 will prompt you with a list of databases to choose from. The database you select is the one you can now execute queries against. You can then change databases using the ```DB1: Change Database``` command. 

Now that we're ready to run some queries, DB1 supports a couple different workflows. 

1. The Results Window Workflow 

Using the command ```DB1: Execute SQL``` will open the Results Window. The Results Window allows for you to have a continuously open window to display query results. This contrasts the disposability of the Quick Query window, where results are lost when the window is closed.

![Results Window](https://i.imgur.com/gMS8rH4.png)

As you can see above, we are free to execute queries in the left view, while the results are displayed in the Results Window on the right. 

**A quick note:** By default, when executing queries to the Results Window, after the query execution, the focus is changed to the Results Window. This can be annoying to some as you then have to reselect the query view on the left to write new queries. However, you can change [this setting](#focus-results-window-on-execution) to leave the focus on the execution view.

In addition to the above setting, by default the contents of Results Window is deleted with every query, but [that can be changed](#erase-results-window) to either ```"prepend"``` or ```"append"``` the results.

This workflow tends to work really well if you'd like to be able to interact with results, as you can do things like search for text in the Results Window. 

2. The Quick Query view. 

Using the command ```DB1: Execute Quick SQL``` will open the Quick Query view. The Quick Query view allows you to output the results of a query to a disposable (you can't save it, and when it's gone, you can't recover the contents) output view at the bottom of the window. 

![Quick Query view](https://i.imgur.com/37qXYFW.png)

This view is easy to use if you're just executing a quick SQL query and the query results don't have any sort of permanence.


Finally, regardless of the view that you choose, most aspects of the results are customizable. In the PostgreSQL query below, all possible options for query display are enabled. 

<pre><code>DB1: Connected to alexggordon@10.0.1.195 using database alexggordon 

Query 1: Executed in 0.0143s. Executed at 2015-10-16 15:10:59.
Autocommit is off. Isolation Level Database Default. Deferrable Database Default. Readonly off. 
------------------
select * from pet;
------------------
+--------+---------+-------+
| name   | owner   |   age |
|--------+---------+-------|
| Libby  | Alex    |    16 |
+--------+---------+-------+
</code></pre>

To associate the connected settings, see the items below for the associated settings. 

<br>

* [Show DB1 Header](#show-db1-header)

```DB1: Connected to alexggordon@10.0.1.195 using database alexggordon``` 

<br>

* [Show Query Number](#show-query-number)

```Query 1:```

<br>

* [Show Query Execution Time](#show-query-execution-time)

```Executed in 0.0143s.```

<br>

* [Show Execution Datetime](#show-execution-datetime)

```Executed at 2015-10-16 15:10:59.```

<br>

* [Show Autocommit Status](#show-autocommit-status)

```Autocommit is off.```

<br>

* [Show Isolation Level (PostgreSQL only)](#show-isolation-level)

```Isolation Level Database Default.```

<br>

* [Show Deferrable Status (PostgreSQL only)](#show-deferrable-status)

```Deferrable Database Default.```

<br>

* [Show Readonly Status (PostgreSQL only)](#show-readonly-status)

```Readonly off.```

<br>

* [Show Query](#show-query)

* [Query Table Format](#query-table-format)

<pre><code>------------------
select * from pet;
------------------
</code></pre>

<br>

* [Results Table Format](#results-table-format)

* [Align Numbers](#align-numbers)

* [Align Strings](#align-strings)

<pre><code>+--------+---------+-------+
| name   | owner   |   age |
|--------+---------+-------|
| Libby  | Alex    |    16 |
+--------+---------+-------+
</code></pre>


After fully customizing you're results, you should be good to go!



## <a href="#feedback" name="feedback">Reporting Issues and Feature Requests</a>
Please report all issues and feedback to the [DB1 Issue and Request Tracker](https://github.com/SequoiaStudios/DB1/issues). All issues will be posted and followed there. In the event that Github is unavailable or extremely inconvenient, please email [support@sequoiastudios.io](mailto:support@sequoiastudios.io)

In addition to issues and feature requests, the documentation file used here is also hosted in that repository so as to track changes.

## <a href="#changelog" name="changelog">Changelog</a>

### <a href="#v101" name="v101">V1.0.1</a>

##### Improvements:
  * None.

##### Bug Fixes:
  * Removed Ubuntu dependency on Libpython that caused DB1 to not load on x64_86 Linux.


### <a href="#v102" name="v102">V1.0.2</a>

##### Improvements:
  * You can now specify ports using user@host:port syntax.
  * Postgresql 8.1 and early have increased performance.
  * You can now customize all aspects of a connection in the "stored_connections" setting.

##### Bug Fixes:
  * Fixed a bug causing issues with older versions of postgresql.
  * Fixed a bug that caused DB1 to sometimes ignore ports that were manually changed.


### <a href="#v110" name="v110">V1.1.0</a>

##### Feature Additions:
  * You can now connect to MariaDB and local SQLite databases through DB1.

##### Improvements:
  * Improved settings management and error correcting.

##### Bug Fixes:
  * Fixed 'null' port storage for some databases using the default port.
  * Fixed result window being reopened if the results window was in a separate window pane.
  * Fixed some connection timeout issues. 

## <a href="#commands" name="commands">Commands</a>
As a note, all commands make heavy use of the Sublime Text status bar located at the bottom of the screen. After a command is executed, the status bar is almost always updated with the result, and in the case of longer running commands (connecting, and query execution) a loading indicator will show. 


### <a href="#connect" name="connect">Connect To Database</a>
Command: ```db1_connect```

This initiates a connection to a database. Required information is:

* Database Type
* db_username@host:port (:port is optional. If none is specified, then the default port will be used.)
* password

If your database uses a custom port, you can also enter the port during the connection. You can do this when prompted for the address (```user@host:port```) and by appending the port onto the end of connection string after a ```:``` marker. The full connection string, with the optional port, should look similar to ```alex@hostname:1111```. 

After a connection is initiated, you will be prompted for the database you would like to use. You can select any database you'd like to, (you can always [change later](#use-database)).

If there is an issue connecting, the error will be displayed at the bottom of your view. 

For issues connecting, please see the [connection issues](#connection-issues) section. 

### <a href="#remove-connection" name="remove-connection">Remove Stored Connection</a>
Command ```db1_remove_connection```

This command removes a [stored connection](#stored-connections) permanently. 


### <a href="#use-database" name="use-database">Change Database</a>
Command ```db1_use_database``` 

This command allows a user to change the database. The user will be prompted with a list of databases available to change to, from which they can select the database they're prefer. If there is no active connection in the view, one will be created upon execution of the command. 


### <a href="#execute-sql" name="execute-sql">Execute Sql</a>
Command ```db1_execute_sql```

This command executes sql and exports the results to the Results Window. The Results Window is simply a file to which query results are written. You can customize the location (and other aspects of the Results Window) of the file in your [Settings](#settings).  

By default, the Results Window will look like this upon query execution:

![Results Window](https://i.imgur.com/AIkWzpV.png)

The sql that this command executes can be passed to it through a couple of ways. 

* If there is **no selection** in the active view, then this command will parse and execute **the entire** view as sql. 
* If there **a single selection** in the view, then this command will just execute that text. 
* If there are **multiple selections** in the view, this command will parse the multiple selections for queries, and execute those queries.

The [default setting](#erase-results-window) is to **erase** the results window on every query execution. In addition to this, by default [the focus will be moved](#focus-results-window-on-execution) to the Results Window after every query execution.


### <a href="#execute-quick-sql" name="execute-quick-sql">Execute Quick Sql</a>
Command ```db1_execute_quick_sql```

This command executes sql and exports the results to the Quick Query view (Sublime Text output window). This view is a disposable window located at the bottom of the screen.

![Quick Query view](https://i.imgur.com/nSVXKVV.png)



### <a href="#execute-template" name="execute-template">Execute Template</a>
Command ```db1_execute_template```

The ```db1_execute_template``` command is special in that it allows the user to execute any predefined sql, with any number of variables (0 - &infin;). This command follows the format:

<pre><code>    {
        "keys": ["command+shift+1"],
        "command": "db1_execute_template",
        "args": {
            "mysql_pattern": "select * from %s;",
            "postgresql_pattern": "select * from %s;",
            "maria_pattern": "select * from %s;",
            "sqlite_pattern": "select * from %s;",
            "output_type": "quickpanel"
        }
    }
</code></pre>

In the case of this command, there is one variable, represented by the ```%s```.  If the text **```pet```** was highlighted in a Sublime Text view (the Quick Query view doesn't count), and the keyboard shortcut ```command+shift+1``` was run, then the sql statement 

```select * from pet;``` 

would be run. 

It's important to note that variables **are not required** for this command nor are multiple ```"_pattern"``` options required. To execute SQL against just a MySQL database, then just the ```"mysql_pattern"``` is required, like the following simpler version of the template. 

<pre><code>    {
        "keys": ["command+shift+1"],
        "command": "db1_execute_template",
        "args": {
            "mysql_pattern": "select * from pet limit 100;",
            "output_type": "window"
        }
    }
</code></pre>

The above command can be executed by the keyboard shortcut regardless of what text is highlighted, or the view you are currently in and will appear in the Results Window. 

The final option in the shortcut is to choose the location of the output for this command. The two possibilities are:

* **```"output_type": window```** Export the results of the query to the Results Window (pictured [here](#execute-quick-sql))
* **```"output_type": quickpanel```** Export the results to the disposable quickpanel (pictured [here](#execute-quick-sql))

### <a href="#commit-changes" name="commit-changes">Commit Changes</a>
Command ```db1_commit_changes```

Connections to the database will default to either have autocommit on, or autocommit off. If autocommit is off, then any changes made to the database will not be permanent until they are committed. This command will commit those changes and make them permanent. 

### <a href="#rollback-changes" name="rollback-changes">Rollback Changes</a>
Command ```db1_rollback_changes```

Connections to the database will default to either have enable autocommit , or disable autocommit. If autocommit is off, then any changes made to the database will not be permanent until they are committed. This command will rollback any changes made to the database. 

### <a href="#toggle-autocommit" name="toggle-autocommit">Toggle Autocommit</a>
Command ```db1_toggle_autocommit```

This command will either disable autocommit or enable it. When the command is run, if you have previously toggled autocommit, the menu will show you the currently set value. 

### <a href="#set-isolation-level" name="set-isolation-level">Set Isolation Level</a>
Command ```db1_set_isolation_level```

This command will allow you to change the isolation level of your current PostgreSQL or SQLite connection

##### PostgreSQL: 

The values are:

* Read uncommitted  
* Read committed
* Repeatable read
* Serializable

To read more about PostgreSQL isolation levels, please check out the [PostgreSQL documentation.](https://www.postgresql.org/docs/9.1/static/transaction-iso.html)

##### SQLite:

The values are:

* None
* DEFERRED
* IMMEDIATE
* EXCLUSIVE

For SQLite, autocommit is tied into isolation level. When the isolation level is set to None, then autocommit is turned on, however, all other isolation levels disable autocommit for SQLite.


### <a href="#set-deferrable" name="set-deferrable">Set Deferrable (PostgreSQL Only)</a>
Command ```db1_set_deferrable```

This command will either disable the deferrable status of the PostgreSQL connection. When the command is run, if you have previously toggled the deferrable status, the menu will show you the currently set value. 

This defaults to the database default for the connection

### <a href="#set-readonly" name="set-readonly">Set Readonly (PostgreSQL Only)</a>
Command ```db1_set_readonly```

This command will either disable the readonly status of the PostgreSQL connection. When the command is run, if you have previously toggled the readonly status, the menu will show you the currently set value.

If the connection is set to readonly then changes cannot be made to the database. This defaults to the database default for the connection.


### <a href="#open-results-window" name="open-results-window">Open Results Window</a>
Command ```db1_open_results_window```

This command opens the Results Window. The Results Windows stores the output of the queries executed by the [```db1_execute_sql```](#execute-sql) command. If there is no active connection in the view, one will be created upon execution of the command. 


### <a href="#open-documentation" name="open-documentation">Open Documentation Command</a>
Command ```db1_open_documentation```

The command opens the [DB1 documentation](/db1/documentation).

### <a href="#report-issue-command" name="report-issue-command">Report Issue Command</a>
Command ```db1_report_issue```

The command opens the [DB1 Issue and Feature Tracker](https://github.com/SequoiaStudios/DB1/issues).

## <a href="#connection-issues" name="connection-issues">Connection Issues</a>

One of the more common connection issues is connections timing out. By default the connection timeout for a new connection is 5 seconds. You can change the amount of time a connection takes to timeout in the settings (see the [stored connections](#stored-connections) setting for examples). 


## <a href="#settings" name="settings">Settings</a>
To edit your personal DB1 settings, please navigate to:

``` "Preferences" > "Package Settings" > "DB1" > "Settings - User"```

If you would like to see the default options, please see the file at:

``` "Preferences" > "Package Settings" > "DB1" > "Settings - Default"```

**REMEMBER,** the default settings are routinely reset. While saving your user settings there may temporarily work, please save them in the user settings mentioned above.

### <a href="#stored-connections" name="stored-connections">Stored Connections</a>

    "stored_connections":
    {
        "user@1.1.1.1":
        {
            "database_type": "MySQL",
            "password": "hunter2",
            "port": 3306,
            // settings below are optional. The setting they will default to is shown. 
            // 'DEFAULT' refers to the database default for the setting. 
            "autocommit": false,
            // connection timeout in seconds
            "connection_timeout": 5,
        },
        "user@localhost":
        {
            "database_type": "PostgreSQL",
            "password": "",
            "port": 5432,
            // settings below are optional. The setting they will default to is shown. 
            // 'DEFAULT' refers to the database default for the setting. 
            "autocommit": false,
            "connection_timeout": 5,
            // optional, postgresql only settings
            "isolation_level": 'DEFAULT', // can be 0, 1, 2, or 3. 
            "readonly": false,
            "deferrable": 'DEFAULT'
        }
    }

Stored Connections are where all stored user database connections go. They are automatically stored through the [db1_connect](#connect) command. If you have a custom port to use, you can update the connection manually, using following the syntax:

    "stored_connections":
    {
        "database_type": "MySQL",
        "password": "password",
        "port": 3306
    }


Or when using the [db1_connect](#connect) command, you can append the port onto the end of the connection string, like:

    user@host:port
    


In general all field are required, in the case of password-less PostgreSQL authentication, please leave the password field as an empty string (```password: ""```). 

If you use SSH tunneling to connect to your database, please use the local port of the SSH tunnel in the settings.


### <a href="#set-syntax-on-execute" name="set-syntax-on-execute">Set Syntax on Execute</a>
Default Setting:

    "set_syntax_on_execute": True


When set to true, if a view does not have a syntax file assigned to it when executing SQL, then DB1 will set the syntax of the view to the relevant sql file (either PostgreSQL or MySQL).

### <a href="#results-table-format" name="results-table-format">Results Table Format</a>
Default Setting:

    "results_table_format": "psql"


The Results Table Format defines the appearance of the box around the **just** the query results. This applies to both the Results Window and Quick Query view. 

Available Options when executing the query ```select * from pet;```

* **"grid"**

<pre><code>+--------+---------+-------+
| name   | owner   |   age |
+========+=========+=======+
| Libby  | alex    |    16 |
+--------+---------+-------+
</code></pre>


*  **"fancy_grid"**

<pre><code>╒════════╤═════════╤═══════╕
│ name   │ owner   │   age │
╞════════╪═════════╪═══════╡
│ Libby  │ alex    │    16 │
╘════════╧═════════╧═══════╛   
</code></pre>


*  **"psql"** (default)
    
<pre><code>+--------+---------+-------+
| name   | owner   |   age |
|--------+---------+-------|
| Libby  | alex    |    16 |
+--------+---------+-------+
</code></pre>


* **"pipe"**

<pre><code>| name   | owner   |   age |
|:-------|:--------|------:|
| Libby  | alex    |    16 |
</code></pre>


* **"orgtbl"**

<pre><code>| name   | owner   |   age |
|--------+---------+-------|
| Libby  | alex    |    16 |
</code></pre>


* **"simple"**

<pre><code>name    owner      age
------  -------  -----
Libby   alex        16
</code></pre>


* **"plain"**

<pre><code>name    owner      age
Libby   alex        16
</code></pre>


* **"html"**

<pre><code>&lt;table&gt;
&lt;tr&gt;&lt;th&gt;name  &lt;/th&gt;&lt;th&gt;owner  &lt;/th&gt;&lt;th style=&quot;text-align: right;&quot;&gt;  age&lt;/th&gt;&lt;/tr&gt;
&lt;tr&gt;&lt;td&gt;Libby &lt;/td&gt;&lt;td&gt;alex   &lt;/td&gt;&lt;td style=&quot;text-align: right;&quot;&gt;   16&lt;/td&gt;&lt;/tr&gt;
&lt;/table&gt;
</code></pre>


### <a href="#show-db1-header" name="show-db1-header">Show DB1 Header</a>
Default Setting

    "show_db1_header": true

At the top of the Results Window and Quick Query view, there is a header that looks like this:

    DB1: Connected to user@host using database adventure_land 

This setting defined whether or not that header shows. 


### <a href="#show-query" name="show-query">Show Query</a>
Default Setting:

    "show_query": true

By default, above the query results, the query currently being executed is shown. This setting defines whether or not the query is shown. 

### <a href="#query-table-format" name="query-table-format">Query Table Format</a>
Default Setting:

    "query_table_format": "simple"

This setting only applies if the [```"show_query"```](#show-query) setting is ```true```. It defines the appearance of the query displayed.


Available Options when executing the query ``` select * from pet;```

* **"grid"**

<pre><code>+--------------------+
| select * from pet; |
+--------------------+
</code></pre>


*  **"fancy_grid"**

<pre><code>╒════════════════════╕
│ select * from pet; │
╘════════════════════╛
</code></pre>


*  **"psql"**
    
<pre><code>+--------------------+
| select * from pet; |
+--------------------+
</code></pre>


* **"pipe"**

<pre><code>|:-------------------|
| select * from pet; |
</code></pre>


* **"orgtbl"**

<pre><code>| select * from pet; |
</code></pre>


* **"simple"** (default)

<pre><code>------------------
select * from pet;
------------------
</code></pre>


* **"plain"**

<pre><code>select * from pet;
</code></pre>


* **"html"**

<pre><code>&lt;table&gt;
&lt;tr&gt;&lt;td&gt;select * from pet;&lt;/td&gt;&lt;/tr&gt;
&lt;/table&gt;
</code></pre>


### <a href="#show-query-number" name="show-query-number">Show Query Number</a>
Default Setting:

    "show_query_number": true

By default, the number of the query being executed is show in front of each query. For example, when executing 2 queries, "Query 1" will show in front of the first query, and "Query 2" will show in front of the second query. This controls the display of that. 

### <a href="#show-query-execution-time" name="show-query-execution-time">Show Query Execution Time</a>
Default Setting:

    "show_query_execution_time": true

By default, this will show the amount of time it took to execute the query. The format will follow: 
 
    "Executed in 0.0016s."

### <a href="#show-execution-datetime" name="show-execution-datetime">Show Execution Datetime</a>
Default Setting:

    "show_execution_datetime": true

By default, this will show the date and time the query was executed at. The format will follow:

    "Executed at 2015-10-08 10:45:55." 

### <a href="#datetime-format" name="datetime-format">Datetime Format</a>
Default Setting:

    "datetime_format": "%Y-%m-%d %H:%M:%S"

This setting only applies if the [```"show_execution_datetime"```](#show-execution-datetime) setting is ```true```. It defines the format of the date and time.

We strongly recommend using [strftime.org](https://strftime.org/) to format this. 

If this is formatted incorrectly, nothing will be displayed. 


### <a href="#show-autocommit-status" name="show-autocommit-status">Show Autocommit Status</a>
Default Setting:

    "show_autocommit_status": true

By default, this will show the status for the connection. This defaults to the database default, for all database types.

If [Autocommit](#toggle-autocommit) is "off", then any changes must be [committed](#commit-changes) or [rolled back](#rollback-changes) before they have a permanent effect. 

If the connection is closed (Sublime Text is quit, or internet connection is lost), all changes will be rolled back. 

### <a href="#show-isolation-level" name="show-isolation-level">Show Isolation Level (PostgreSQL only)</a>
Default Setting:

    "show_isolation_level": false

Will not show by default. When set to ```true``` this will show the isolation level of the connection. 

##### PostgreSQL:
Show isolation level will show one of the following:

* ```Isolation Level Database Default.```
* ```Isolation Level Read Committed.```
* ```Isolation Level Repeatable Read.```
* ```Isolation Level Serializable.```
* ```Isolation Level Read Uncommitted.```

##### SQLite:
Show isolation level will show one of the following:

* ```Isolation Level None```
* ```Isolation Level Deferred```
* ```Isolation Level Immediate```
* ```Isolation Level Exclusive```


The isolation level for both database types can be changed through the [Set Isolation Level](#set-isolation-level) command. 

### <a href="#show-deferrable-status" name="show-deferrable-status">Show Deferrable Status (PostgreSQL only)</a>
Default Setting:

    "show_deferrable_status": false

Will not show by default. When set to ```true``` this will show the deferrable status of the connection. It will show one of the following:

* ```Deferrable Database Default.```
* ```Deferrable On.```
* ```Deferrable Off.```

The deferrable status can be changed through the [Set Deferrable](#set-deferrable) command. 

### <a href="#show-readonly-status" name="show-readonly-status">Show Deferrable Status (PostgreSQL only)</a>
Default Setting:

    "show_readonly_status": true

By default, this shows the readonly status of the connection. It will show one of the following:

* ```Readonly Database Default.```
* ```Readonly On.```
* ```Readonly Off.```

The deferrable status can be changed through the [Set Readonly](#set-readonly) command. 

### <a href="#align-numbers" name="align-numbers">Align Numbers</a>
Default Setting:

    "align_numbers": "decimal"

This setting controls how numbers (and the corresponding columns headers) are aligned in the results tables. The available options are:

* ```"right"```  right align all numbers
* ```"center"```  center align all numbers
* ```"left"```  left align all numbers
* ```"decimal"```  align all numbers along the decimal point (or where the decimal point would be for whole numbers)

### <a href="#align-strings" name="align-strings">Align Strings</a>
Default Setting:

    "align_strings": "left"

This setting controls how text (and the corresponding columns headers) are aligned in the results tables. The available options are:

* ```"right"```  right align all text
* ```"center"```  center align all text
* ```"left"```  left align all text
* ```false```  do not align  text


### <a href="#erase-results-window" name="erase-results-window">Erase Results Window</a>
Default Setting:

    "erase_results_window": true

By default, on every query execution the results window is erased. Changing this setting to ```false``` means that the results will either be prepended or appended to the Results Window depending on the [results window append style](#results-window-append-style).

### <a href="#focus-results-window-on-execution" name="focus-results-window-on-execution">Focus Results Window on Execution</a>
Default Setting:

    "focus_results_window_on_execution": true

By default, when executing queries, the Results Window will come into focus. However, when simply scrolling through the results, this "feature" can be annoying, so by setting this to ```false```, the focus will not be changed upon query execution. 

### <a href="#results-window-append-style" name="results-window-append-style">Results Window Append Style</a>
Default Setting:

    "results_window_append_style": "append"

This setting only applies if [```"erase_results_window"```](#erase-results-window) is set to ```false```. 
Depending on your workflow, some people prefer to append query results (put new results at the end of the Results Window) or prepend (put new results at the beginning of Results Window) the results. 

Available options: 

* ```"append"``` (default)
* ```"prepend"```

### <a href="#results-window-location-osx" name="results-window-location-osx">Results Window Location Osx</a>
Default Setting:

    "results_window_location_osx": "/tmp/results.txt"

We recommend care when changing this setting, as Sublime Text needs write access to this location. This is simply the location of the Results Window. every time a query is executed to the Results Window, the file is saved. 

### <a href="#results-window-location-windows" name="results-window-location-windows">Results Window Location Windows</a>
Default Setting:

    "results_window_location_windows": "C:\\WINDOWS\\TEMP\\results.txt"

**When changing this setting, please escape backslashes**

We recommend care when changing this setting, as Sublime Text needs write access to this location. This is simply the location of the Results Window. every time a query is executed to the Results Window, the file is saved. 

### <a href="#results-window-location-linux" name="results-window-location-linux">Results Window Location Linux</a>
Default Setting:

    "results_window_location_linux": "/tmp/results.txt"

We recommend care when changing this setting, as Sublime Text needs write access to this location. This is simply the location of the Results Window. every time a query is executed to the Results Window, the file is saved. 


## <a href="#key-bindings" name="key-bindings">Key Bindings</a>
Custom Sublime Text key bindings are defined in ``` "Preferences" > "Key Bindings - User" ``` setting. 

By default there are only two default DB1 commands. 

On OSX they are:

* **```{ "keys": ["command+shift+e"], "command": "db1_execute_sql" }```**
* **```{ "keys": ["command+shift+r"], "command": "db1_execute_quick_sql" }```**

and Linux and Windows:

* **```{ "keys": ["ctrl+shift+e"], "command": "db1_execute_sql" }```**
* **```{ "keys": ["ctrl+shift+r"], "command": "db1_execute_quick_sql" }```**

All other DB1 commands (listed below) can be set in the ```"Key Bindings - User"``` file mentioned above and must follow the format:

**```{ "keys": ["command+o"], "command": "open_file" }```**


**The only exception** to the above is the [```db1_execute_template```](#execute-template) command. This command is special in that it allows the user to execute any predefined sql, with any number of variables. This command follows the format:

<pre><code>    {
        "keys": ["command+shift+1"],
        "command": "db1_execute_template",
        "args": {
            "mysql_pattern": "select * from %s;",
            "postgresql_pattern": "select * from %s;",
            "maria_pattern": "select * from %s;",
            "sqlite_pattern": "select * from %s",
            "output_type": "window"
        }
    }
</code></pre>

In the case of this command, there is one variable, represented by the ```%s```.  If the text **```pet```** was highlighted in a Sublime Text view (the Quick Query view doesn't count), and the keyboard shortcut ```command+shift+1``` was run, then the sql statement 

```select * from pet;``` 

would be run in the current view. As usual, if there is no connection active in the view, you will be prompted to initiate one.

It's important to note that variables **are not required** for this command, and an **indefinite number of variables** can be used. For more information, see the [```db1_execute_template```](#execute-template) documentation.


**All DB1 Commands:**

* **```db1_connect```**
* **```db1_use_database```**
* **```db1_remove_connection```**
* **```db1_execute_sql```**
* **```db1_execute_quick_sql```**
* **```db1_execute_template```**
* **```db1_commit_changes```**
* **```db1_rollback_changes```**
* **```db1_toggle_autocommit```**
* **```db1_set_isolation_level```**
* **```db1_set_readonly```**
* **```db1_set_deferrable```**
* **```db1_open_results_window```**
* **```db1_open_documentation```**
* **```db1_report_issue```**


## <a href="#license-information" name="license-information">License Information</a>

### <a href="#enter-license" name="enter-license">Entering Your License</a>
To enter your license, first you need to [purchase one](/cart). If you've done that (yay), then the next step is to open the DB1 User Settings file at:

``` "Preferences" > "Package Settings" > "DB1" > "Settings - User"```

You then need the **three** pieces of information (```db1_license_name```, ```db1_license_email```, and ```db1_license_code```)  included in the license email you received.

After it's entered, your settings file should look similar to this:

<pre><code>{
    "db1_license_code": "DB1-A98U5-A98U5-A98U5-A98U5",
    "db1_license_email": "support@sequoiastudios.io",
    "db1_license_name": "Sequoia Studios"
}
</code></pre>

Then place those in the DB1 user settings file (remember, you can't modify the license email or name after purchasing). If you receive a message like:

![error](https://i.imgur.com/fUp9Oja.png)

Then you may have forgotten a comma, colon, or quotation mark after one of the elements.

If for some reason you've followed the above, and are still getting the unregistered message, [email](mailto:support@sequoiastudios.io) us with your purchasing information and we'll get it fixed ASAP. 


### <a href="#recover-license" name="recover-license">Recovering a Lost License</a>
To recover a lost license key please [email](mailto:support@sequoiastudios.io) us with the name, license email address and quantity of licenses purchased. We'll get your licenses to you as fast as the minions allow.


### <a href="#alternative-payment" name="alternative-payment">Alternative Payment</a>
As an alternative to payment for DB1, we would be more than happy to supply you with a license upon proof of a donation of $29.99 (USD) or more to [Will Bond](https://packagecontrol.io/say_thanks). This software wouldn't be possible without his work on [packagecontrol](https://packagecontrol.io), and his original idea and implementation of a Sublime Text database client.


### <a href="#bulk-discounts" name="bulk-discounts">Bulk Discounts</a>
If you, like us, enjoy saving money, send us an email at [support@sequoiastudios.io](mailto:support@sequoiastudios.io) with the quantity of licenses you'd like to purchase, and any other incentives you can throw in. We're up for a good negotiating session.


### <a href="#refunds" name="refunds">Refunds</a>
So DB1 sucks for you. Sorry about that. [Email](mailto:support@sequoiastudios.io) us and we'll refund you as soon as possible. Let us know if there's anything we can do to mitigate that though.

### <a href="#education-discount" name="education-discount">Educational Discount</a>
We'd love to be able to help out students, so if you are one, send us an email from your student account, with the projects or classes you'd like to use DB1 for, and we'll work something out!


### <a href="#tax" name="tax">Tax Information</a>
Why do we charge tax in Massachusetts? Because unfortunately since we're an LLC registered in Massachusetts, we have to charge tax on any goods we sell, including digital goods. If the tax annoys you, [shoot us an email](mailto:support@sequoiastudios.io) when you're in Massachusetts and we'll buy you a beer to make up for it.

For any EU customers that are subject to VAT tax, while it's regrettable that we do this at this point, we don't currently support charging or reporting VAT tax. Please follow your local laws regarding this. 


### <a href="#other" name="other">Other</a>
For all other inquiries please email [support@sequoiastudios.io](mailto:support@sequoiastudios.io) (you're probably seeing a pattern now). Be kind though, Brian works through a lot of email every day :\).


## <a href="#open-source" name="open-source">Open Source Libraries Used</a>
DB1 Uses several open source libraries in its code. These licenses are also distributed with DB1 and can be found in the root DB1 folder in a folder called licenses.

Please report any issues with the licenses to the [issues page](https://github.com/SequoiaStudios/DB1/issues) 

In no particular order: 
### <a href="https://github.com/PyMySQL/PyMySQL" name="pymysql">Pymysql</a>

Licensed under MIT License.

<pre><code>Copyright (c) 2010, 2013 PyMySQL contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
</code></pre>


### <a href="https://github.com/psycopg/psycopg2" name="psycopg2">Psycopg2</a>

Licensed under LGPL

<pre><code>psycopg2 and the LGPL
=====================

psycopg2 is free software: you can redistribute it and/or modify it
under the terms of the GNU Lesser General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

psycopg2 is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public
License for more details.

In addition, as a special exception, the copyright holders give
permission to link this program with the OpenSSL library (or with
modified versions of OpenSSL that use the same license as OpenSSL),
and distribute linked combinations including the two.

You must obey the GNU Lesser General Public License in all respects for
all of the code used other than OpenSSL. If you modify file(s) with this
exception, you may extend this exception to your version of the file(s),
but you are not obligated to do so. If you do not wish to do so, delete
this exception statement from your version. If you delete this exception
statement from all source files in the program, then also delete it here.

You should have received a copy of the GNU Lesser General Public License
along with psycopg2 (see the doc/ directory.)
If not, see <http://www.gnu.org/licenses/>.


Alternative licenses
====================

If you prefer you can use the Zope Database Adapter ZPsycopgDA (i.e.,
every file inside the ZPsycopgDA directory) user the ZPL license as
published on the Zope web site, http://www.zope.org/Resources/ZPL.

Also, the following BSD-like license applies (at your option) to the
files following the pattern psycopg/adapter*.{h,c} and
psycopg/microprotocol*.{h,c}:

 Permission is granted to anyone to use this software for any purpose,
 including commercial applications, and to alter it and redistribute it
 freely, subject to the following restrictions:

 1. The origin of this software must not be misrepresented; you must not
    claim that you wrote the original software. If you use this
    software in a product, an acknowledgment in the product documentation
    would be appreciated but is not required.

 2. Altered source versions must be plainly marked as such, and must not
    be misrepresented as being the original software.

 3. This notice may not be removed or altered from any source distribution.
</code></pre>

### <a href="https://github.com/andialbrecht/sqlparse" name="sqlparse">Sqlparse</a>

Licensed under BSD License.

<pre><code>Copyright (c) 2009, Andi Albrecht <albrecht.andi@gmail.com>
All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

    * Redistributions of source code must retain the above copyright notice,
      this list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above copyright notice,
      this list of conditions and the following disclaimer in the documentation
      and/or other materials provided with the distribution.
    * Neither the name of the authors nor the names of its contributors may be
      used to endorse or promote products derived from this software without
      specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

</code></pre>

### <a href="https://bitbucket.org/astanin/python-tabulate" name="tabulate">Tabulate</a>

Licensed under the MIT License.

<pre><code>Copyright (c) 2011-2015 Sergey Astanin

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
</code></pre>


### <a href="https://github.com/facelessuser/FuzzyFileNav" name="fuzzyfilenav">FuzzyFileNav</a>

Licensed under the MIT License.

<pre><code>License
Fuzzy File nav is released under the MIT license.

Copyright (c) 2012 - 2015 Isaac Muse isaacmuse@gmail.com

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

</code></pre>








