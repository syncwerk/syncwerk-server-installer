# Auto install Seafile Server CE* and PRO**

These installers offer a quick and easy way to set up a production ready Seafile Server using MariaDB, Memcached and NGINX as a reverse proxy in under 5 minutes.

\* Community Edition
** Professional Edition

## What's it for?

Install the [Seafile Server](http://seafile.com/en/home/) in a standard and more secure manner then our current out of the box setup scripts offer.


## Supported OS

Just select the corresponding installer for your OS. All scripts are meant to run with the bare minimum OS setup. We strongly suggest not installing Seafile server besides desktop environment or hosting panels like Plesk, ISPConfig, etc. Professional installations which don't follow our setup suggestions, don't qualify for official support. Keep this in mind.

### Minimal installations only!

#### [Community Edition](https://github.com/haiwen/seafile-server-installer/tree/master/community-edition)
1. Debian Wheezy & Jessie
2. Ubuntu Trusty
3. CentOS 7

#### [Professional Edition](https://github.com/haiwen/seafile-server-installer/tree/master/professional-edition)
1. Debian Wheezy & Jessie
2. Ubuntu Trusty
3. CentOS 7

## Caution
Never run these scripts on a production server. They are more or less a one trick pony and could seriously damage production systems. Run it only once and
delete it afterwards. If something goes wrong, restart with a fresh machine.

As a precaution I have added a few simple checks to abort installation if any of these fails:

1. Check if you're running this script as root. If not, abort.
2. Check if the user "seafile" exists. If yes, abort.
3. Check if the directory "/opt/seafile" exists. If yes, abort.


## Feature overview
1. HTTPS-Proxy
2. Redirect all HTTP to HTTPS
2. Seahub with FastCGI
3. [Seafile WebDAV (aka. SeafDAV)](http://manual.seafile.com/extension/webdav.html) with FastCGI
4. MariaDB
5. Memcached
6. Seafile auto start
7. Postfix
8. Firewall
9. Fail2ban
10. Autoupdate OS


## Installation
### Seafile Server CE
Except for the Uberspace installer **all installers need to run as root**. Running them with sudo will not work! Login as root or switch to root with sudo
su before installing with these installers. Make sure your OS package repository (e.g. /etc/apt/sources.list) is set correct before proceeding.

For **Debian Wheezy and Jessie (32bit and 64bit)**:


    apt-get install lsb-release -y
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/haiwen/seafile-server-installer/master/seafile_v5_debian
    bash seafile_v5_debian


For **Ubuntu Trusty (64bit)**:

    sudo su
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/haiwen/seafile-server-installer/master/community-edition/seafile-ce_ubuntu-trusty-amd64
    bash seafile-ce_ubuntu-trusty-amd64


For **CentOS 7 (64bit)**

    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/SeafileDE/seafile-server-installer/master/seafile_v5_centos
    bash seafile_v5_centos


### Seafile Server PRO
You will have to download the Seafile Professional Server package prior to the installation and save it to /usr/src/seafile/. Make sure the variable `SEAFILE_VERSION` is set to the downloaded version before proceeding with the installation.


For **Debian Wheezy and Jessie (64bit only)** run the following lines as root

    apt-get install lsb-release -y
    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/haiwen/seafile-server-installer/master/seafile_debian
    bash seafile_debian


For **CentOS 7 (64bit)**

    cd /root
    wget --no-check-certificate https://raw.githubusercontent.com/haiwen/seafile-server-installer/master/seafile_v5_centos
    bash seafile_v5_centos


## FAQs

***Where do I find the full installation log?***
At `/root/[installer_name]_installation.log`

***What's the unprivileged Seafile users name***
seafile

***How can I change the domain name of the Seafile server?***
Run the `seafile-server-change-address` script on the shell

***How can I login as the unprivileged Seafile user?***
Run `su - seafile -s /bin/bash` with root privileges on the shell

***How do I update Seafile?***
You will have to handle Seafile updates/upgrades manually after the initial installation. Consult http://manual.seafile.com/deploy/upgrade.html on how to upgrade Seafile.

To login as the Seafile users run `su - seafile -s /bin/bash` and then proceed with the update procedure as usual.

BTW: Ideas on how to automate upgrades are very welcome!

***What do I have to do after the installer has finished?***
1. Delete installer script. You wont need it anymore and might even seriously damage your system if you run it again.
2. Follow the suggested steps at the end of the installation to finalize your Seafile server installation.

## Troubleshooting
If your installation did not finish successfully, check `/root/[installer_name]_installation.log` for errors.


## License

Copyright (c) 2016, Seafile Ltd.

Copyright 2015, Alexander Jackson <alexander.jackson@seafile.de>

This program is free software: you can redistribute it and/or modify
it under the terms of the [GNU Affero General Public License](http://www.gnu.org/licenses/agpl-3.0.html) as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.
