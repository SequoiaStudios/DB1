# DB1: A Sublime Text Database Client

DB1 allows you to execute queries against multiple database types (currently PostgreSQL and MySQL) from inside Sublime without installing any dependencies (a local database installation is not required). 

If you'd like to read the full documentation for DB1, you can see it [here](https://sequoiastudios.io/db1/documentation)

As an introduction to DB1 (after [installing](#installation)), we'd highly suggest the [Quick Start](#quick-start) guide.

## INDEX
* [Installation](#installation)
* [Quick Start](#quick-start)
* [Reporting Issues and Feature Requests](#feedback)
* [Changelog](#changelog)
    - [V1.0.1](#v101)
    - [V1.0.2](#v102)

## <a href="#installation" name="installation">Installation</a>

If [Package Control](https://packagecontrol.io) is already installed: 

1. Open the Sublime Text command palette (```"Tools" > "Command Palette"```) 
2. Enter ```Package Control: Install Package```
3. Enter ```DB1```

Congratulations! DB1 will now be installed. If you are not greeted with the DB1 installation message from Package Control, please restart Sublime Text. 

If [Package Control](https://packagecontrol.io) is not already installed, please follow [the instructions for installation](https://packagecontrol.io/installation), and then follow the above instructions. 


## <a href="#quick-start" name="quick-start">Quick Start</a>
The first step to getting started is making sure that DB1 is [installed](#installation). 

Once that's finished, the first big command is ```db1_connect```. ```db1_connect``` initiates a connection for a single view in Sublime Text. This means that there's a one-to-one relationships of connections to views. Each connection is then tied to the database it's connected to, such that in view #1 you can execute queries on database 'A', and in View #2 you can execute queries on database 'B'. 

When using the ```db1_connect``` you'll need to know the username, host, port (if it's not the default) and password of the database you're connecting to.

To help streamline workflow, if there is not a connection on a view when one of the ```db1_execute``` commands is run, the connection process will be initiated before the query is then run (this allows for a more streamlined workflow). 

To connect to a database, you'll need a username, password and host(which can be localhost) for the database. In addition to this, in cases like PostgreSQL authentication (where authentication is [trust](https://www.postgresql.org/docs/9.0/static/auth-methods.html) based) a password is not required. 

Once you're connected, DB1 will prompt you with a list of databases to choose from. The database you select is the one you can now execute queries against. 

Now that we're ready to run some queries, DB1 supports a couple different workflows. 


1. The Results Window Workflow 

The Results Window workflow allows for you to have a continuously open window to display query results. This contrasts the disposability of the Quick Query window, where results are lost when the window is closed.

![Results Window](https://i.imgur.com/gMS8rH4.png)

As you can see above, we are free to execute queries in the left view, while the results are displayed in the Results Window on the right. 

**A quick note:** By default, when executing queries to the Results Window, after the query execution, the focus is changed to the Results Window. This can be annoying to some as you then have to reselect the query view on the left to write new queries. However, you can change functionality of it using the ```"focus_results_window_on_execution"``` setting to leave the focus on the execution view.

In addition to the above setting, by default the contents of Results Window is deleted with every query, but that setting can be changed to either ```"results_window_append_style": "prepend"``` or ```"results_window_append_style": "append"``` the prepend or append the results.

This workflow tends to work really well if you'd like to be able to interact with results, as you can do things like search for text in the Results Window. 

2. The Quick Query view. 
The Quick Query view outputs the results of a query to a disposable (you can't save it, and when it's gone, you can't recover the contents) output view at the bottom of a sublime window. 

![Quick Query view](https://i.imgur.com/37qXYFW.png)

Much like the Results Window, many aspects of the Quick Query view are fully customizable. 

For more information about the DB1 Settings and commands please see the [full documentation](https://sequoiastudios.io/db1/documentation)


## <a href="#feedback" name="feedback">Reporting Issues and Feature Requests</a>
Please report all issues and feedback to the [DB1 Issue and Request Tracker](https://github.com/SequoiaStudios/DB1/issues). All issues will be posted and followed there. In the event that Github is unavailable or extremely inconvenient, please email [support@sequoiastudios.io](mailto:support@sequoiastudios.io)

In addition to issues and feature requests, the documentation file used here is also hosted in that repository so as to track changes.

## <a href="#changelog" name="changelog">Changelog</a>

### <a href="#v101" name="v101">V1.0.1</a>

##### Improvements:
  * None.

##### Bug Fixes:
  * Removed Ubuntu dependency on Libpython that caused DB1 to not load on 64-but ubuntu.

### <a href="#v102" name="v102">V1.0.2</a>

##### Improvements:
  * You can now specify ports using user@host:port syntax.
  * Postgresql 8.1 and early have increased performance.
  * You can now customize all aspects of a connection in the "stored_connections" setting.

##### Bug Fixes:
  * Fixed a bug causing issues with older versions of postgresql.
  * Fixed a bug that caused DB1 to sometimes ignore ports that were manually changed.

