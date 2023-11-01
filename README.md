# Polypheny Control
Polypheny Control allows to easily setup and monitor Polypheny-DB. It takes care of pulling the required repositories and executing the builds.

Polypheny Control has been designed as a tool for automating the evaluation and benchmarking of Polypheny-DB. Its integrated REST interface allows to easily integrate it into complex benchmarking scenarios.


## Getting Started
This section describes how to set up Polypheny Control to build and run Polypheny-DB.


### Requirements
To build and start Polypheny-DB using Polypheny Control you need to have a Java JDK of version 11 or higher installed on your system.
Thanks to [JGit](https://eclipse.dev/jgit/), Polypheny Control contains a pure Java implementation of Git. Therefore, it is no longer required to have Git installed on the system.


### Setup
Download the latest [polypheny-control.jar](https://github.com/polypheny/Polypheny-Control/releases/latest) from the release section. 

On systems with a desktop environment, Polypheny Control can be started by double-clicking the JAR file. Polypheny Control then adds itself to the system tray.

Alternatively, you can also execute the JAR file with the argument `tray`:
```
java -jar polypheny-control.jar tray
```

#### Headless

Polypheny Control can be started in headless mode by specifying the parameter `control`:

```
java -jar polypheny-control.jar control
```

The browser-based user interface can now be accessed on port 8070. This port can be changed using the parameter `-p`:

```
java -jar polypheny-control.jar control -p 8070
```

We strongly recommend not to use any port between 8080 and 8089 as these are the default ports of services offered by Polypheny-DB.


### First Steps

After starting Polypheny Control, open the dashboard in your browser of choice by navigating to `localhost:8070`. If Polypheny Control is running in tray mode, the dashboard can also be opened by clicking on the icon in the system tray and selecting `dashboard`.

In order to start Polypheny-DB, we first need to trigger a build. This can be done by clicking on the :arrows_counterclockwise: button. When the build has completed, run Polypheny-DB by clicking on :arrow_forward:.

You can now open the Polypheny-UI by opening `localhost:8080` in your browser. 

### Authentication

Polypheny Control now allows you to use authentication to allow only verified users to use it. Authentication is available both in the command line and in the browser.
CLI authentication can be enabled/disabled using the `pcrtl.auth.cli` config option. It is disabled by default.
Authentication for `localhost` can be enabled/disabled using the `pcrtl.auth.local` config option. It is also disabled by default.
Authentication itself for be fully enabled/disabled using the `pcrtl.auth.enable` config option. It is enabled by default.

#### The passwd file

Polypheny Control stores user information in a file name **passwd**. This file is NOT protected. You can protect the file against modification by setting the immutable flag using `chattr` on Linux / MacOS and `attrib` on Windows.
But, remember to reset the flag when modifying the file using polypheny control.

#### Admin User

Polypheny Control requires a **admin** user to create and manage other users. So, before you can create any other user you will need to create a **admin** user using the following command:

```
java -jar polypheny-control.jar adduser
```

This will prompt you to enter a name and password. Enter "admin" as the name and a strong password for the user.
All of the user management actions need to be authorized using the admin password.

An example run of the user management features:

```
# Creating the admin user (The password is mandatory but won't be visible when you type it out)
> java -jar polypheny-control.jar adduser
Name: admin
Password: 
Confirm Password: 

# Creating a user
> java -jar polypheny-control.jar adduser
Name: Loki
Password: 
Confirm Password: 
Enter 'admin' password (Try 1/3):

# Modifying a user's password
> java -jar polypheny-control.jar moduser
Name: Loki
Password: 
Confirm Password: 
Enter 'admin' password (Try 1/3):

# Remove a user
> java -jar polypheny-control.jar remuser
Name: Loki
Enter 'admin' password (Try 1/3):

```


## Roadmap
See the [open issues](https://github.com/polypheny/Polypheny-DB/labels/A-control) for a list of proposed features (and known issues).


## Contributing
We highly welcome your contributions to _Polypheny Control_. If you would like to contribute, please fork the repository and submit your changes as a pull request. Please consult our [Admin Repository](https://github.com/polypheny/Admin) and our [Website](https://polypheny.org) for guidelines and additional information.

Please note that we have a [code of conduct](https://github.com/polypheny/Admin/blob/master/CODE_OF_CONDUCT.md). Please follow it in all your interactions with the project. 


## Credits
_Polypheny Control_ builds upon the great work of several other open source projects:

#### Frontend
* [ansi_up.js](https://github.com/drudru/ansi_up): Converting text with ANSI terminal codes into colorful HTML.
* [Font Awesome](https://fontawesome.com/): A set of web-related icons.
* [jQuery](https://jquery.com/): The library that makes Javascript usable.
* [jquery.serializeJSON](https://github.com/marioizquierdo/jquery.serializeJSON): Serialize an HTML Form to a JavaScript Object.
* [Tooltipster](https://calebjacob.github.io/tooltipster/): jQuery plugin for modern tooltips.

All these libraries are imported using [WebJars](https://www.webjars.org/).


#### Backend
* [Airline](https://rvesse.github.io/airline/): Annotation-driven Java library for building command line interfaces.
* [Apache Commons](http://commons.apache.org/): A bunch of useful Java utility classes.
* [GSON](https://github.com/google/gson): Convert Java Objects into their JSON representation and vice versa.
* [Guava](https://github.com/google/guava): Set of special collection types.
* [Javalin](https://javalin.io/): A simple and lightweight java web framework.
* [Java-WebSocket](http://tootallnate.github.io/Java-WebSocket/): WebSocket server and client implementation for Java.
* [JGit](https://www.eclipse.org/jgit/): Pure Java implementation of the Git version control system.
* [JSON.simple](https://code.google.com/archive/p/json-simple/): A simple Java toolkit for JSON.
* [Log4j](https://logging.apache.org/log4j/2.x/): Fast and flexible logging framework for Java.
* [Project Lombok](https://projectlombok.org/): A library providing compiler annotations for tedious tasks.
* [SLF4J](http://www.slf4j.org/): Provides a logging API by means of a facade pattern.
* [Typesafe Config](https://lightbend.github.io/config/): A configuration library using HOCON files.
* [Unirest](http://kong.github.io/unirest-java/): A lightweight HTTP client library.
* [WinP](http://winp.kohsuke.org/): Windows process management library.

These projects are used "as is" and are integrated as libraries.


## License
The Apache 2.0 License
