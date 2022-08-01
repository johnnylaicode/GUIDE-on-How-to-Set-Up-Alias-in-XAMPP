# TECH-NOTE-How-to-Set-Up-Alias-in-XAMPP
This technical note describes how to set up alias in XAMPP. 

XAMPP is a popular open-source PHP development environment, containing Apache, MariaDB, PHP, and Perl ([website](https://www.apachefriends.org/)).

## What is Alias
Alias enables you to store web application resources (e.g., files and images) in different locations other than the DocumentRoot. Using alias, you can move your resources around the server or to a completely different server(s), while keeping the application's friendly URLs the same. Alias allows the server to take a URL received from the client and translate it into a different one which is the actual resource location. This entire process is transparent to the client. The client, when receiving the requested resource, is unaware of any redirection that took place at the server. 

## Setup Instructions
Note: The following instructions are based on using a Windows machine.

### Step 1: Create the Alias Directory
It is required to create a folder named `alias` in XAMPP at the following location:
`C:\xampp\apache\conf\alias`

### Step 2: Create the Alias Configuration File
In the `C:\xampp\apache\conf\alias` folder, create a configuration file to define the aliases.
For example, let's assume that
- the web application's friendly URL path is: `/photos/`
- the actual resource location path is: `C:/image-store/public/photos/`

You can create a configuration file named `photos.conf` to contain the alias definition. Depending on the version of XAMPP, the configuration file content can be different, as described below.

#### Configuration File for Old Version of XAMPP
For an old version of XAMPP, such as version 5.6, the `photos.conf` file content would be:
```
Alias /photos/ "C:/image-store/public/photos/"
<Directory "C:/image-store/public/photos/">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride all
    Order allow,deny
    Allow from all
</Directory>
```
#### Configuration File for New Version of XAMPP
For a new version of XAMPP, such as version 8.0, the `photos.conf` file content would be:
```
Alias /photos/ "C:/image-store/public/photos/"
<Directory "C:/image-store/public/photos/">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride all
    Require all granted
</Directory>
```

With the above alias configuration, if the client's request URL is `https://www.<website name>/photos/pic123.jpg`, the server automatically translates it to `C:/image-store/public/photos/pic123.jpg` and retrieves the requested resource of `pic123.jpg`.

### Step 3: Update the "httpd.conf" File
The next step in the process is to update the `httpd.conf` file in XAMPP.

Open the file: `C:\xampp\apache\conf\httpd.conf`

Add the following line to the end of file: `Include "conf/alias/*"`

Then save the file.

### Step 4: Restart XAMPP
Lastly, restart the XAMPP to activate the alias capability.

----------
[Web Link](https://johnnylaicode.github.io/TECH-NOTE-How-to-Set-Up-Alias-in-XAMPP)

[GitHub Link](https://github.com/johnnylaicode/TECH-NOTE-How-to-Set-Up-Alias-in-XAMPP)