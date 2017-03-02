# Auto install Syncwerk Server CE* and PRO**

These installers offer a quick and easy way to set up a production ready Syncwerk Server using MariaDB, Memcached and NGINX as a reverse proxy in under 5 minutes.

\* Community Edition
** Professional Edition

## What's it for?
Install the [Syncwerk Server](http://syncwerk.com/en/home/) in a standard and more secure manner then our current out of the box setup scripts offer. Instead of SQLite we're using MariaDB and NGINX instead of Gunicorn.


## Why?
There are too many ways to misconfigure a manual Syncwerk server installation. We've noticed that many people don't realize that the default installation is very unsafe. In other cases people get stuck during the manual installation procedure or forget a step like changing `FILE_SERVER_ROOT` or use IP addresses instead of resolvable DNS names.

The scripts are derived from our [reference installation for Syncwerk Server Professional](https://wiki.syncwerk.com/tutorials/debian_8_jessie_64bit). They help us to standardize the installation procedure and identifying setup errors more easily.

## Supported OS

Just select the corresponding installer for your OS. All scripts are meant to run with the bare minimum OS setup. We strongly suggest not installing Syncwerk server besides desktop environment or hosting panels like Plesk, ISPConfig, etc. Professional installations which don't follow our setup suggestions, don't qualify for official support. Keep this in mind.

Minimal installations only!

#### [Community Edition](https://github.com/syncwerk/syncwerk-server-installer/tree/master/community-edition)
1. Debian Wheezy & Jessie
2. Ubuntu Trusty
3. Ubuntu Trusty (Pi / ARM)
4. Uberspace (Centos 6.x only)
5. CentOS 7

#### [Professional Edition](https://github.com/syncwerk/syncwerk-server-installer/tree/master/professional-edition)
1. Debian Wheezy & Jessie
2. Ubuntu Trusty
3. CentOS 7

## Caution
Never run these scripts on a production server. They are more or less a one trick pony and could seriously damage production systems. Run it only once and
delete it afterwards. If something goes wrong, restart with a fresh machine.

As a precaution I have added a few simple checks to abort installation if any of these fails:

1. Check if you're running this script as root. If not, abort.
2. Check if the user "syncwerk" exists. If yes, abort.
3. Check if the directory "/opt/syncwerk" exists. If yes, abort.


## Feature overview
1. HTTPS-Proxy
2. Redirect all HTTP to HTTPS
2. Seahub with FastCGI
3. [Syncwerk WebDAV (aka. SeafDAV)](http://manual.syncwerk.com/extension/webdav.html) with FastCGI
4. MariaDB
5. Memcached
6. Syncwerk auto start
7. Postfix
8. Firewall
9. Fail2ban
10. Autoupdate OS


## Installation
### Syncwerk Server CE
Except for the Uberspace installer **all installers need to run as root**. Running them with sudo will not work! Login as root or switch to root with sudo
su before installing with these installers. Make sure your OS package repository (e.g. /etc/apt/sources.list) is set correct before proceeding.

For **Debian Wheezy and Jessie (32bit and 64bit)**:


    apt-get install lsb-release -y
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/syncwerk_v5_debian
    bash syncwerk_v5_debian


For **Ubuntu Trusty (64bit)**:

    sudo su
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/community-edition/syncwerk-ce_ubuntu-trusty-amd64
    bash syncwerk-ce_ubuntu-trusty-amd64


BETA: For **Ubuntu Trusty (Pi/ARM)**:

    sudo su
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/community-edition/syncwerk-ce_ubuntu-trusty-arm
    bash syncwerk-ce_ubuntu-trusty-arm


For **Uberspace** run the following lines:

    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/community-edition/syncwerk-ce_uberspace
    bash syncwerk-ce_uberspace

For **CentOS 7 (64bit)**

    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/syncwerk_v5_centos
    bash syncwerk_v5_centos


### Syncwerk Server PRO
You will have to download the Syncwerk Professional Server package prior to the installation and save it to /usr/src/syncwerk/. Make sure the variable `SYNCWERK_VERSION` is set to the downloaded version before proceeding with the installation.

* [English: Syncwerk Professional (existing registration required)](https://download.syncwerk.com/)
* [Deutsch: Syncwerk Professional (bestehendes Konto erforderlich)](https://download.syncwerk.com/)

For **Debian Wheezy and Jessie (64bit only)** run the following lines as root

    apt-get install lsb-release -y
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/syncwerk_debian
    bash syncwerk_debian


For **CentOS 7 (64bit)**

    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/syncwerk_v5_centos
    bash syncwerk_v5_centos


## FAQs

***Where do I find the full installation log?***
At `/root/[installer_name]_installation.log`

***What's the unprivileged Syncwerk users name***
syncwerk

***How can I change the domain name of the Syncwerk server?***
Run the `syncwerk-server-change-address` script on the shell

***How can I login as the unprivileged Syncwerk user?***
Run `su - syncwerk -s /bin/bash` with root privileges on the shell

***How do I update Syncwerk?***
You will have to handle Syncwerk updates/upgrades manually after the initial installation.

To login as the Syncwerk users run `su - syncwerk -s /bin/bash` and then proceed with the update procedure as usual.

***What do I have to do after the installer has finished?***
1. Delete installer script. You wont need it anymore and might even seriously damage your system if you run it again.
2. Follow the suggested steps at the end of the installation to finalize your Syncwerk server installation.

## Troubleshooting
If your installation did not finish successfully, check `/root/[installer_name]_installation.log` for errors.

Alpha: Convert syncwerk.db (SQLite DB) to MySQL - **Use with extreme caution only**

This is only needed if your syncwerk-db was mistakenly created as SQLite database by one of the older installers. Only installations till end of May 2015 should be affected. To find out if you are affected, just run `find / -type f -name syncwerk.db -print`. If it finds the file we suggest converting your installation. You can use this script, but be cautios. **It is not very well tested and could seriously brake things.** Make a backup before running syncwerk-db-fixer... If you want to fix the problem manually, consult http://manual.syncwerk.com/deploy/migrate_from_sqlite_to_mysql.html for general instructions.

    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/misc/syncwerk-db-fixer
    bash syncwerk-db-fixer

## License
Copyright 2015, Alexander Jackson <alexander.jackson@syncwerk.com>

This program is free software: you can redistribute it and/or modify
it under the terms of the [GNU Affero General Public License](http://www.gnu.org/licenses/agpl-3.0.html) as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

## Where can I submit bugs or add suggestions?
Create an issue on Github or just reply in the [corresponding forum thread](https://forum.syncwerk.com/t/howto-syncwerk-server-community-edition-on-debian-jessie-amd64/1464).
