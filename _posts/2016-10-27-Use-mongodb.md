---
layout: post
title:  "Mongodb-basics"
date:   2016-10-27
excerpt: "Install Mongodb and more"
project: true
tag:
- mongo
- database
- blog
- nosql
- install
- shell
- bash
---

{% include toc.html %}
    
![Logo]({{ site.url }}/{{ site.picture }}){: .selfie}
    
<center>This doc will try to show detailed installation of mongodb and more </center>
    
## Install MongoDB

1.**Determine which MongoDB build you need.**

There are three builds of MongoDB for Windows:

MongoDB for Windows Server 2008 R2 edition (i.e. 2008R2) runs only on Windows Server 2008 R2, Windows 7 64-bit, and newer versions of Windows. This build takes advantage of recent enhancements to the Windows Platform and cannot operate on older versions of Windows.

MongoDB for Windows 64-bit runs on any 64-bit version of Windows newer than Windows XP, including Windows Server 2008 R2 and Windows 7 64-bit.

MongoDB for Windows 32-bit runs on any 32-bit version of Windows newer than Windows XP. 32-bit versions of MongoDB are only intended for older systems and for use in testing and development systems. 32-bit versions of MongoDB only support databases smaller than 2GB.

To find which version of Windows you are running, enter the following command in the Command Prompt:
{% highlight text %}
wmic os get osarchitecture {% endhighlight %}  
2.**Download MongoDB for Windows.**

Download the latest production release of MongoDB from the MongoDB downloads page. Ensure you download the correct version of MongoDB for your Windows system. The 64-bit versions of MongoDB does not work with 32-bit Windows.
3.**Install the downloaded file.**

In Windows Explorer, locate the downloaded MongoDB msi file, which typically is located in the default Downloads folder. Double-click the msi file. A set of screens will appear to guide you through the installation process.
4.**Move the MongoDB folder to another location (optional).**

To move the MongoDB folder, you must issue the move command as an Administrator. For example, to move the folder to C:\mongodb:

Select Start Menu > All Programs > Accessories.

Right-click Command Prompt and select Run as Administrator from the popup menu.

Issue the following commands:
{% highlight text %}
cd \
move C:\mongodb-win32-* C:\mongodb
{% endhighlight %}
MongoDB is self-contained and does not have any other system dependencies. You can run MongoDB from any folder you choose. You may install MongoDB in any folder (e.g. {% highlight text %}
D:\test\mongodb)
{% endhighlight %}
## Run MongoDB

**Warning:**

Do not make mongod.exe visible on public networks without running in “Secure Mode” with the auth setting. MongoDB is designed to be run in trusted environments, and the database does not enable “Secure Mode” by default.

1.**Set up the MongoDB environment.**

MongoDB requires a data directory to store all data. MongoDB’s default data directory path is \data\db. Create this folder using the following commands from a Command Prompt:
{% highlight text %}
md \data\db 
{% endhighlight %}
You can specify an alternate path for data files using the --dbpath option to mongod.exe, for example:

{% highlight text %}
C:\mongodb\bin\mongod.exe --dbpath d:\test\mongodb\data
{% endhighlight %}
If your path includes spaces, enclose the entire path in double quotes, for example:
{% highlight text %}
C:\mongodb\bin\mongod.exe --dbpath "d:\test\mongo db data"
{% endhighlight %}
2.**Start MongoDB.**

To start MongoDB, run mongod.exe. For example, from the Command Prompt:
{% highlight text %} 
C:\Program Files\MongoDB\bin\mongod.exe
{% endhighlight %}
This starts the main MongoDB database process. The waiting for connections message in the console output indicates that the mongod.exe process is running successfully.

Depending on the security level of your system, Windows may pop up a Security Alert dialog box about blocking “some features” of C:\Program Files\MongoDB\bin\mongod.exe from communicating on networks. All users should select Private Networks, such as my home or work network and click Allow access. For additional information on security and MongoDB, please see the Security Documentation.
3.**Connect to MongoDB.**

To connect to MongoDB through the mongo.exe shell, open another Command Prompt. When connecting, specify the data directory if necessary. This step provides several example connection commands.

If your MongoDB installation uses the default data directory, connect without specifying the data directory:

{% highlight text %}C:\mongodb\bin\mongo.exe
If you installation uses a different data directory, specify the directory when connecting, as in this example:

C:\mongodb\bin\mongod.exe --dbpath d:\test\mongodb\data{% 
If your path includes spaces, enclose the entire path in double quotes. For example:

C:\mongodb\bin\mongod.exe --dbpath "d:\test\mongo db data"
If you want to develop applications using .NET, see the documentation of C# and MongoDB for more information. {% endhighlight %}
4.**Begin using MongoDB.**

To begin using MongoDB, see Getting Started with MongoDB. Also consider the Production Notes document before deploying MongoDB in a production environment.

Later, to stop MongoDB, press Control+C in the terminal where the mongod instance is running.
## Configure a Windows Service for MongoDB

Note:

There is a known issue for MongoDB 2.6.0, SERVER-13515, which prevents the use of the instructions in this section. For MongoDB 2.6.0, use Manually Create a Windows Service for MongoDB to create a Windows Service for MongoDB instead.

1**Configure directories and files.**

Create a configuration file and a directory path for MongoDB log output (logpath):

Create a specific directory for MongoDB log files:
{% highlight text %}
md "C:\Program Files\MongoDB\log"
In the Command Prompt, create a configuration file for the logpath option for MongoDB:
echo logpath=C:\Program Files\MongoDB\log\mongo.log > "C:\Program Files\MongoDB\mongod.cfg"
{% endhighlight %}
2**Run the MongoDB service.**

Run all of the following commands in Command Prompt with “Administrative Privileges:”

Install the MongoDB service. For --install to succeed, you must specify the logpath run-time option.

"C:\Program Files\MongoDB\bin\mongod.exe" --config "C:\Program Files\MongoDB\mongod.cfg" --install
Modify the path to the mongod.cfg file as needed.

To use an alternate dbpath, specify the path in the configuration file (e.g. C:\Program Files\MongoDB\mongod.cfg) or on the command line with the --dbpath option.

If the dbpath directory does not exist, mongod.exe will not start. The default value for dbpath is \data\db.

If needed, you can install services for multiple instances of mongod.exe or mongos.exe. Install each service with a unique  --serviceName and --serviceDisplayName. Use multiple instances only when sufficient system resources exist and your system design requires it.
3**Stop or remove the MongoDB service as needed.**

To stop the MongoDB service use the following command:

net stop MongoDB
To remove the MongoDB service use the following command:
"C:\Program Files\MongoDB\bin\mongod.exe" --remove
## Manually Create a Windows Service for MongoDB

The following procedure assumes you have installed MongoDB using the MSI installer, with the default path C:\Program Files\MongoDB 2.6 Standard.

If you have installed in an alternative directory, you will need to adjust the paths as appropriate.

**Open an Administrator command prompt.**

**Windows 7 / Vista / Server 2008 (and R2)**

Press Win + R, then type cmd, then press Ctrl + Shift + Enter.

Windows 8

Press Win + X, then press A.

Execute the remaining steps from the Administrator command prompt.
2.**Create directories.**

Create directories for your database and log files:
{% highlight text %}mkdir c:\data\db
mkdir c:\data\log {% endhighlight %}
Create a configuration file.

3.**Create a configuration file. This file can include any of the configuration options for mongod, but must include a valid setting for logpath:

The following creates a configuration file, specifying both the logpath and the dbpath settings in the configuration file:
echo logpath=c:\data\log\mongod.log> "C:\Program Files\MongoDB 2.6 Standard\mongod.cfg"
echo dbpath=c:\data\db>> "C:\Program Files\MongoDB 2.6 Standard\mongod.cfg"
4.**Create the MongoDB service.**

Create the MongoDB service.

sc.exe create MongoDB binPath= "\"C:\Program Files\MongoDB 2.6 Standard\bin\mongod.exe\" --service --config=\"C:\Program
Files\MongoDB 2.6 Standard\mongod.cfg\"" DisplayName= "MongoDB 2.6 Standard" start= "auto"

sc.exe requires a space between “=” and the configuration values (eg “binPath=”), and a “” to escape double quotes.

## If successfully created, the following log message will display:
**[SC] CreateService SUCCESS
Start the MongoDB service.
net start MongoDB
Stop or remove the MongoDB service as needed.

To stop the MongoDB service, use the following command:

net stop MongoDB
To remove the MongoDB service, first stop the service and then run the following command:
sc.exe delete MongoDB **
basic useless doc