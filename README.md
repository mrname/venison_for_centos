About
============================
This script is designed to automate the deployment of WordPress on a fresh (ve) server installation using an Nginx stack. It is an adaption of the Venison deploy script written by TJ Stein:

https://github.com/tjstein/venison

His script has been modified to operate on CentOS, and adds some extra features as well. 


Overview
============================
This script requires CentOS 6. It installs and configures the required OS packages and the MySQL/Nginx/PHP-FPM/Postfix deployment stack for WordPress. All packages are installed through yum for future upgrade ease.

NOTE: The script disables SSH root login, sets up a sudo user, and optionally changes the SSH port for server security. At the top of the script, you can see the variables that should be set prior to running the script. All variables should have value, otherwise the script will not run.


Usage
============================
1. Download the script files from the GitHub repo as a tar file. 
2. Upload the tar file to /root. 
3. Login to the server as root and untar the file: 
	- tar -xzvf venison.tar.gz
4. Enter setup directory:
	- cd venison
5. Edit script variables for your configuration: 
	- vim setup.sh
	- Edit lines 4-12 to match your needs
	- save the changes
5. sh setup.sh
6. Let it run


Notes
============================
DO NOT LOG OUT of your root session. Once the script has completed, the root user can no longer SSH into the server. You need to use the login for the `sudo_user` you setup in the script variables. So, start a new SSH session and try to login using the account of the `sudo_user`. Once you have confirmed you can login successfully, you can close the root session.

This adaptation of Venison includes the following new features:

- Google Pagespeed Module For Nginx
- Cache Purge Module For Nginx
- Headers More Module For Nginx
- Fail2Ban

All Nginx modules are active on the inital WordPress deployment, and fail2Ban is immediately active, blocking the SSH port. The WordPress install comes with the Nginx Helper plugin, which automatically purges the Nginx cache when content is updated. Although the plugin is active, it needs to have cache purging turned on, and settings configured. 


License
============================
Copyright (c) 2013 by Justin Crown

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
