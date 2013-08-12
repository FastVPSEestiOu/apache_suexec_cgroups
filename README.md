apache_suexec_cgroups
=====================

Author: Pavel Odintsov, pavel.odintsov [at] gmail.com

Patch for adding cgroups support to Apache suexec (you can add cgi/mod_fcgid/mod_fastcgi processes into separate cgroups)

# Build suexec module on Debian Squeeze 

```bash
# build tools
apt-get install -y dpkg-dev devscripts build-essential fakeroot

# get dependency
apt-get build-dep apache2-suexec

# get sources
cd /usr/src

apt-get source apache2-suexec
dpkg-source -x apache2_2.2.16-6+squeeze11.dsc
cd apache2-2.2.16

# get patch
wget https://raw.github.com/FastVPSEestiOu/apache_suexec_cgroups/master/suexec.patch

# patch
patch -p1 < suexec.patch

# rebuild
debuild -us -uc # -us unsigned source, -uc unsigned changes

cd ..
dpkg -i apache2-suexec_2.2.16-6+squeeze11_amd64.deb
```

After that, you need create cgroups (memory, cpu, blkio) in this path (sorry, it hardcoded):
```bash
/mnt/cgroup/%username%/tasks
```

Viva la cgroups! 
