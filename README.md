# seafile-server-community_debian-jessie-amd64


### What's it for?
Installing the Seafile Server Community Edition on a Debian Jessie (64bit) in a more secure way then the shipped setup scripts allow.


### Which components are used?
1. Newest Seafile Server Community Edition
2. NGINX (Forced SSL + [SeafDAV](http://manual.seafile.com/extension/webdav.html))
3. MariaDB
4. Memcached


### Operating system
It's meant to run on a [Debian Jessie minimal installation](https://www.youtube.com/watch?v=BCwz9oSSt8g). No desktop environment or other weird stuff like hosting panels (Plesk, ISPConfig, etc.)...


### Mind the gap
Never run the script on a production server. It's more or less a one trick pony and can seriously damage productions systems. So run it only one time and delete it afterwards. As a precaution I have added a few simple checks to abort installation if the unprivileged Seafile user or Seafile installation directory pre-exist.


### How do I update Seafile?

You will have to handle Seafile updates/upgrades manually after the initial installation. Consult http://manual.seafile.com/deploy/upgrade.html on how to upgrade Seafile. 


### How do I run it?
<pre>
cd /tmp
wget --no-check-certificate https://raw.githubusercontent.com/alexanderjackson/seafile-server-community_debian-jessie-amd64/master/seafile-server-community_debian-jessie-amd64
time bash seafile-server-community_debian-jessie-amd64
</pre>


### What does the installer do?
1. Update and upgrade Debian
2. Install NGINX from http://nginx.org/packages/mainline/debian/
3. Create Seafile init script and add it to system start-up
4. Create unprivilieged system user "Seafile" with home directory "/opt/seafile"
5. Download and extract latest Seafile server sources from https://download.seafile.com.de/seafile-server_latest_x86-64.tar.gz
6. Create "seafile" database user and actual Seafile databases (DB-Credentials in ~/.my.cnf)
7. Create various Seafile files
8. Enable SeafDAV, Memcached and MariaDB
9. Setup Seafile to listen to IP (hostname -i) instead of DNS (Switch this to DNS before live deployment)
10. Create Seafile admin with individual password
11. Display setup infos and what to do next.


### What do I have to do after the installer has finished?

1. Delete installer script. You wont need it anymore and might even seriously damage your system if ran again.
2. Follow the suggested steps at the end of the installation to finalize your Seafile server installation. As a bare minimum you most definitely will want to change the listening IP to a valid DNS name. Run "seafile-server-change-address" as root to change the DNS name...


### Where can I submit bugs or add suggestions?
Contact me at alexander.jackson@seafile.com.de or create an [Issue](https://github.com/alexanderjackson/seafile-server-community_debian-jessie-amd64/issues/new) on Github.
