About
============================
This script is designed to automate the deployment of WordPress on a fresh (ve) server installation using an Nginx stack. It is an adaption of the Venison deploy script written by TJ Stein:

https://github.com/tjstein/venison

His script has been modified to operate on CentOS, and adds some extra features as well. 

IMPORTANT!!!!
============================
This repo has not been updated, as it has been superceded by:

https://github.com/mrname/venison_plus_apache_for_centos

Why?
----------------------------
Adding Apache into the mix makes the build more robust, especially for applications that need .htaccess (yea, I know thats lame). I have done extensive testing with siege and this build is almost as fast as venison without apache. Since I do not have time to maintiain both repos, the one listed above is maintained, and this one is not. I strongly urge you to use 'Venison Plus Apache For Centos'.

It also adds some nice extra features like 'venisonctl' which allows you to add/remove domains and wordpress installations via cli, and uses the most up to date versions of nginx + pagespeed. Try it! If you are the stubbon type (Lu) then go ahead and just install this one. 


Overview
============================
This script requires CentOS 6. It installs and configures the required OS packages and the MySQL/Nginx/PHP-FPM/Postfix deployment stack for WordPress. You can choose between MySQL, Percona, and MariaDB. All packages are installed through yum for future upgrade ease, except for Nginx. The build of Nginx utilized requires third-party modules (discussed below). As a result, it needs to be compiled. 

NOTE: The script disables SSH root login, sets up a sudo user, and optionally changes the SSH port for server security. When you run the setup script, you will be prompted for these values. It is HIGHLY RECOMMENDED that you change your SSH port to something unique, although fail2ban is active upon deployment. 


Installation
============================

Installing with git:

1. git clone https://github.com/mrname/venison_for_centos.git
2. Enter setup directory:
        - cd venison_for_centos
3. sh setup.sh
4. Let it run
5. Enjoy the goodness, and tune as necessary!

Install Manually:

1. Login to the server via ssh, download the script files from the GitHub repo as a zip file, and unzip:
   wget https://github.com/mrname/venison_for_centos/archive/master.zip && unzip master.zip
2. Enter setup directory:
	- cd venison_for_centos
3. sh setup.sh
4. Let it run
5. Enjoy the goodness, and tune as necessary!


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

All Nginx modules are active on the inital WordPress deployment, and fail2Ban is immediately active, blocking the SSH port only. Fail2Ban has a preset jail for DDOS protection which can be activated in the 'jail.conf' file. The WordPress install comes with the Nginx Helper plugin, which automatically purges the Nginx cache when content is updated. Although the plugin is active, it needs to have cache purging turned on, and settings configured. PageSpeed is using default settings. Depending on your website, you might need to change these. This can be changed in the 'pagespeed.conf' file in the document root of your website, at the same level as the 'public' directory. Consult the PageSpeed documentation for more info.


License
============================
Copyright (c) 2013 by Justin Crown

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
