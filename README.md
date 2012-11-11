jSSH
====


Description
-----------
jSSH is a command line auto login SSH tool that uses a sqlite backend to 
store connection information written in Python. jSSH database entries 
are completely managed using its built in command line features.

Installing
----------

To install jssh on your system, simply run the INSTALL script. If run as a standard user, it will be installed only for your user.
If run as root, it will be installed system wide.

jssh no longer installs plink for you. If you choose to install plink manually it will be used automatically by jssh.
If you do not have plink, jssh will aid you in setting up ssh keys for auto-login when you add a server to the database. (jssh --add-server)

Once installed, each system user has his/her own database of connection 
information located in ~/.jssh/

Using jSSH
-----------

Usage: jssh [options] [hostname/nickname]


**Adding a server to the database:**

>jssh -a root@this.that.com password

>jssh --add-server root@this.that.com password

This will add this.that.com to the database using the username 'root' 
and the password 'password'. jSSH will also parse the information you 
have given it to give the database entry a nickname. In most cases, it 
will default the the first section of the provided hostname. The 
nickname assigned from the above example would be 'this'. This will be 
useful when connecting. 


**Removing a server from the database:**

>jssh -r this.that.com
 
>jssh --remove-server this.that.com

The above example will remove this.that.com and its stored connection 
information from the database. Currently, you may only specify which 
server to remove by giving the complete hostname as the argument. 

**Searching the database:**
>jssh -s nickname/hostname

>jssh --search nickname/hostname

The above example will return the connection information that has been 
stored in the database for the given nickname or hostname provided as an 
argument.


**Using a non-default SSH port**

You may is -p or --port at any time to specify a custom port. This 
argument is one of the first check and will apply to any other 
operation. 


>jssh -add-server root@this.that.com password --port 2222

The above example will add this.that.com to the database using username 
'root' and password 'password' and will also connect on port 2222.

**Connecting to a server in the database:**
To connect to a server stored in the database, simply give either the 
servers hostname or the servers nickname as an argument to jSSH. 

For example, 

>jssh this.that.com

>jssh this


**List all servers in the jssh database**

The following will output a list of hostnames stored in the JSSH database.

> jssh -l

> jssh --list-servers

You may also use this in combination with the verbose flag to have all server information outputed. The following will print the hostname, username, password, port, and nickname of each server in the database.

> jssh -lv

> jssh --list-servers --verbose

**Connecting to a server that is not stored in the database:**

I have included an argument that will allow you to treat jSSH somewhat 
as a normal SSH client. -m or --manual will allow you to provide the 
connection info as arguments without anything being stored in the 
database. 

>jssh -m root@this.that.com password

>jssh --manual root@this.that.com password


