# Auto install Syncwerk Server CE* and PRO**

These installers offer a quick and easy way to set up a production ready Syncwerk Server using MariaDB, Memcached and NGINX as a reverse proxy in under 5 minutes.

\* Community Edition
** Professional Edition

## What's it for?
Install the [Syncwerk Server](http://www.syncwerk.com) in a standard and more secure manner then our current out of the box setup scripts offer. Instead of SQLite we're using MariaDB and NGINX instead of Gunicorn.


## Supported OS

### Debian Wheezy, Jessie & Stretch

Just select the corresponding installer for your OS. All scripts are meant to run with the bare minimum OS setup. We strongly suggest not installing Syncwerk server beside desktop environments or hosting panels like Plesk, ISPConfig, etc. 
Professional installations which don't follow our setup suggestions, don't qualify for official support. Please keep this in mind.

Minimal installations only!

## Caution
Never run these scripts on a production server. They are more or less a one trick pony and could seriously damage production systems. Run it only once and delete it afterwards. If something goes wrong, restart with a fresh machine.

As a precaution I have added a few simple checks to abort installation if any of these fails:

1. Check if you're running this script as root. If not, abort.
2. Check if the user "syncwerk" exists. If yes, abort.
3. Check if the directory "/opt/syncwerk" exists. If yes, abort.


## Feature overview
1. HTTPS-Proxy
2. Redirect all HTTP to HTTPS
2. FastCGI enabled
3. WebDAV enabled
4. MariaDB
5. Memcached
6. Auto start services
7. Postfix Mailserver
8. UFW-Firewall
9. Fail2ban
10. Autoupdate OS


## Installation
### Syncwerk Server CE
**All installers need to be executed as root**. Running them with sudo will not work! Login as root or switch to root with `sudo
su` before installing with these installers. Make sure your OS package repository (e.g. /etc/apt/sources.list) is configured correctly before proceeding.

For **Debian Wheezy, Jessie or Stretch (64bit)**:

    apt-get git lsb-release ca-certificates net-tools -y
    cd /root
    wget https://raw.githubusercontent.com/syncwerk/syncwerk-server-installer/master/syncwerk_v5_debian
    bash syncwerk_v5_debian


### Syncwerk Server PRO
You will have to download the Syncwerk Professional Server package prior to the installation and save it to /usr/src/syncwerk/.

* [English: Syncwerk Professional (existing registration required)](https://download.syncwerk.com/)
* [Deutsch: Syncwerk Professional (bestehendes Konto erforderlich)](https://download.syncwerk.com/)

**FYI:** To download Syncwerk Professional you need an account on our [download portal](https://download.syncwerk.com/). Only pre-existing customers of Syncwerk GmbH (former Seafile GmbH) will receive access to these restricted sources. Contact us at support@syncwerk.com if you have lost your login details.


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
