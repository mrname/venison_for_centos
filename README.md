About
============================
This script is designed to automate the deployment of WordPress on a fresh (ve) server installation using an Nginx stack. It is an adaption of the Venison deploy script written by TJ Stein:

https://github.com/tjstein/venison

His script has been modified to operate on CentOS, and adds some extra features as well. 


Overview
============================
This script requires CentOS 6. It installs and configures the required OS packages and the MySQL/Nginx/PHP-FPM/Postfix deployment stack for WordPress. All packages are installed through yum for future upgrade ease, except for Nginx. The build of Nginx utilized requires third-party modules (discussed below). As a result, it needs to be compiled. 

NOTE: The script disables SSH root login, sets up a sudo user, and optionally changes the SSH port for server security. When you run the setup script, you will be prompted for these values. It is HIGHLY RECOMMENDED that you change your SSH port to something unique, although fail2ban is active upon deployment. 


Usage
============================
1. Download the script files from the GitHub repo as a tar file. 
2. Upload the tar file to /root. 
3. Login to the server as root and untar the file: 
	- tar -xzvf venison.tar.gz
4. Enter setup directory:
	- cd venison
5. sh setup.sh
6. Let it run
7. Enjoy the goodness, and tune as necessary!


Notes
============================
DO NOT LOG OUT of your root session. Once the script has completed, the root user can no longer SSH into the server. You need to use the login for the `sudo_user` you setup in the script variables. So, start a new SSH session and try to login using the account of the `sudo_user`. Once you have confirmed you can login successfully, you can close the root session.

This adaptation of Venison includes the following new features:

- Google Pagespeed Module For Nginx
      https://developers.google.com/speed/pagespeed/ngx
- Cache Purge Module For Nginx
      https://github.com/perusio/nginx-cache-purge
- Headers More Module For Nginx
      http://wiki.nginx.org/HttpHeadersMoreModule
- Fail2Ban - AutoBanning Software To Prevent Brute Force Attacks
      http://www.fail2ban.org/wiki/index.php/Main_Page

All Nginx modules are active on the inital WordPress deployment, and fail2Ban is immediately active, blocking the SSH port only. The WordPress install comes with the Nginx Helper plugin, which automatically purges the Nginx cache when content is updated. Although the plugin is active, it needs to have cache purging turned on, and settings configured. PageSpeed is using default settings. Depending on your website, you might need to change these. Consult the PageSpeed documentation for more info.


License
============================
Copyright (c) 2013 by Justin Crown

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
