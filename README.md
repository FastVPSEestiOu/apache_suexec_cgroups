apache_suexec_cgroups
=====================

Author: Pavel Odintsov, pavel.odintsov [at] gmail.com

Patch for adding cgroups support to Apache suexec (you can add cgi/mod_fcgid/mod_fastcgi processes into separate cgroups)

# Build suexec module on Debian Lenny

```bash
#!/bin/bash

# build tools
apt-get install -y dpkg-dev devscripts build-essential fakeroot

# get dependency
apt-get build-dep apache2-suexec

# get sources
cd /usr/src

# old method, is buggy: http://phpsuxx.blogspot.com/2010/12/source-apache2-debian.html
#apt-get source apache2-suexec
wget http://ftp.de.debian.org/debian/pool/main/a/apache2/apache2_2.2.9-10+lenny12.dsc
wget http://ftp.de.debian.org/debian/pool/main/a/apache2/apache2_2.2.9.orig.tar.gz
wget http://ftp.de.debian.org/debian/pool/main/a/apache2/apache2_2.2.9-10+lenny12.diff.gz
dpkg-source -x apache2_2.2.9-10+lenny12.dsc
cd apache2-2.2.9

# get patch
wget http://...../suexec.patch

# patch
patch -p1 < suexec.patch

# rebuild
debuild -us -uc # -us unsigned source, -uc unsigned changes

cd ..
```
