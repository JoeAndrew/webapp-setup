Extended web-server configurator for Gentoo with webapp-config
==============================================================

## webapp-setup

Setup extension for webapp-config in Gentoo

### Gentoo install

```bash
eselect repository add joe-overlay git https://github.com/JoeAndrew/joe-overlay
```

or clone joe-overlay from https://github.com/JoeAndrew/joe-overlay and add it as custom overlay

```bash
$ echo "app-admin/webapp-setup **" >> /etc/portage/package.accept_keywords/joe-overlay
$ emerge webapp-setup
```

### Manual Installation on non Gentoo System

$ git clone https://github.com/JoeAndrew/webapp-setup.git

$ cd webapp-setup

For Apache create a file wiht this:

```bash
cat << EOF >> install
#!/bin/sh

mkdir -p /etc/apache2/sites-{available,enabled}
cp a2* /usr/sbin
chmod +x /usr/sbin/a2*
echo "Include /etc/apache2/sites-enabled/" >>/etc/apache2/httpd.conf
EOF
```
for Nginx this:

```bash
cat << EOF >> install
#!/bin/sh

mkdir -p /etc/nginx/sites-{available,enabled}
cp n2* /usr/sbin
chmod +x /usr/sbin/n2*
echo "Include /etc/nginx/sites-enabled/" >>/etc/nginx/nginx.conf
EOF
```
or both
```bash
$ sudo sh install
```

Done

## Usage

### webapp-setup has syntax from webapp-config

```bash
webapp-setup -I nextcloud 22.2.3 -h nextcloud.home
```

this command passes the parameters to webapp-config then creates the web server alias, enables the virtual host, creates the local hosts file entry, and restarts the web server with the new data.

```bash
webapp-setup -C nextcloud 22.2.3 -h nextcloud.home
```

this removes the created entries and webapp-config deletes the virtual server. The vhost.conf file is not deleted.

### a(n)2en(dis)site is Debian style web-server configurator for Gentoo

For the scripts to work, you first need to create your virtual host in the /etc/apache2/sites-available folder.
The a2ensite script is run with only 1 argument: the name of the virtual-host file. It then links the file to the sites-enabled folder, checks for any syntax errors and restarts your apache.

The a2dissite script disables the virtualhost by removing the link in the sites-enabled folder and restarts apache.

#### to be continued...
#### to do list

nginx support

lightdm support
