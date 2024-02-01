# post-installation-configuration

Part 1 (Create Virtual Machine in Azure)
Create a Resource Group
Create a Windows 10 Virtual Machine (VM) with 2-4 Virtual CPUs
When creating the VM, allow it to create a new Virtual Network (Vnet)

Part 2 (Installation)
Note: I wouldn't really consider this a “simple list” because the steps are just installing a bunch of prerequisite software, but you can use it as a guide to work through the lab. No need to try to memorize everything.


Create an Azure Virtual Machine Windows 10, 4 vCPUs
Name: Vm-osticket
Username: labuser (for example/whatever you chose)
Password: osTicketPassword1! (for example/whatever you chose)



Open this: Installation Files
We will use these files to install osTicket and some of the dependencies. I’m using this offline version to make sure everyone is using the same version of all the files :)

Install / Enable IIS in Windows WITH
CGI and Common HTTP Features
World Wide Web Services -> Application Development Features ->
[X] CGI
[X] Common HTTP Features
AND IIS Management Console
Internet Information Services -> Web Management Tools -> IIS Management Console
	[X] IIS Management Console
 ![Screenshot 2024-02-01 183919](https://github.com/lestersanchez1120/post-installation-configuration/assets/158239931/034db588-39dd-41e3-a62f-ea6a6276493f)



From the Installation Files, download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

From the Installation Files, download and install the Rewrite Module (rewrite_amd64_en-US.msi)

Create the directory C:\PHP

From the Installation Files, download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the contents into C:\PHP
!! ATTENTION !!
If this appears, choose to “Keep” the file:

![image](https://github.com/lestersanchez1120/post-installation-configuration/assets/158239931/165c1078-6afa-4f99-9074-0414abf75e16)

![image](https://github.com/lestersanchez1120/post-installation-configuration/assets/158239931/9c2e29ed-5723-4c6b-8224-2646b46b046a)





If you are still having trouble downloading PHP 7.3.8, please try downloading and installing Google Chrome and doing it from within there. 

From the Installation Files, download and install VC_redist.x86.exe.

From the Installation Files, download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
Typical Setup ->
Launch Configuration Wizard (after install) ->
Standard Configuration ->
Password1

Open IIS as an Admin

Register PHP from within IIS

Reload IIS (Open IIS, Stop and Start the server)

Install osTicket v1.15.8
Download osTicket from the Installation Files Folder
Extract and copy “upload” folder to c:\inetpub\wwwroot
Within c:\inetpub\wwwroot, Rename “upload” to “osTicket”

Reload IIS (Open IIS, Stop and Start the server)

Go to sites -> Default -> osTicket
On the right, click “Browse *:80”

Note that some extensions are not enabled
Go back to IIS, sites -> Default -> osTicket
Double-click PHP Manager
Click “Enable or disable an extension”
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opcache.dll
Refresh the osTicket site in your browse, observe the changes

Rename: ost-config.php
From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Assign Permissions: ost-config.php
Disable inheritance -> Remove All
New Permissions -> Everyone -> All

Continue Setting up osTicket in the browser (click Continue)
Name Helpdesk
Default email (receives email from customers)

From the Installation Files, download and install HeidiSQL.
Open Heidi SQL
Create a new session, root/Password1
Connect to the session
Create a database called “osTicket”

Continue Setting up osticket in the browser
MySQL Database: osTicket
MySQL Username: root
MySQL Password: Password1
Click “Install Now!”

Congratulations, hopefully it is installed with no errors!
Browse to your help desk login page: http://localhost/osTicket/scp/login.php

End Users osTicket URL:
http://localhost/osTicket/ 

Clean up
Delete: C:\inetpub\wwwroot\osTicket\setup
Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Notes:
Browse to your help desk login page: http://localhost/osTicket/scp/login.php  
End Users osTicket URL: http://localhost/osTicket/ 

Part 3 (Post Installation Setup)
Configure Roles
Admin Panel -> Agents -> Roles
Supreme Admin
Configure Departments
Admin Panel -> Agents -> Departments
System Administrators
Configure Teams
Admin Panel -> Agents -> Teams
Level I Support
Level II Support
Allow anyone to create tickets
Admin Panel -> Settings -> User Settings
Registration Required: Require registration and login to create tickets 
Configure Agents (workers)
Admin Panel -> Agents -> Add New
Jane
John
Configure Users (customers)
Agent Panel -> Users -> Add New
Karen
Ken
Configure SLA
Admin Panel -> Manage -> SLA
Sev-A (1 hour, 24/7)
Sev-B (4 hours, 24/7)
Sev-C (8 hours, business hours)
Configure Help Topics
Admin Panel -> Manage -> Help Topics
Business Critical Outage
Personal Computer Issues
Equipment Request
Password Reset
