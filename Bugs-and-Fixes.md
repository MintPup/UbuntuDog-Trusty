All fixes for previous iso version moved [here.](https://github.com/DebianDog/MintPup-Trusty/blob/a84b068604c441721cfcf059119035d875cdc30f/Bugs-and-Fixes.md)

[Click here first for important changes in the new iso.](https://github.com/DebianDog/MintPup-Trusty/blob/d690419d3d86aa8ce58ce8d13ddada190c68a467/Bugs-and-Fixes.md)

[Experimental save on exit in directory for casper-boot.](https://github.com/DebianDog/MintPup-Trusty/blob/master/Extra-options.md)


**Fixes for MintPup-jwm-icewm-hybrid-07.05.2016.iso:**

**1.** Some Firefox functions as "Open link in new tab" do not work. The latest Firefox version in the repository is special Mint build. I guess it will be fixed in time. Till then if you use Firefox downgrade it to the official Ubuntu version:
```
sudo apt-get -t trusty install firefox
``` 

**2.** Change /etc/apt/sources.list.d/official-package-repositories.list to:

```
deb http://archive.ubuntu.com/ubuntu trusty main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu trusty-updates main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://archive.canonical.com/ubuntu/ trusty partner

deb http://packages.linuxmint.com rebecca main upstream import  #id:linuxmint_main
deb http://extra.linuxmint.com rebecca main #id:linuxmint_extra

```

Now you can upgrade the system if you like:

```
apt-get update
```

```
apt-get upgrade
```

**3.** Some scripts changes:
https://github.com/DebianDog/MintPup-Trusty/tree/master/scripts

All fixes above included in [mintpup-trusty-mp1_0.0.1_i386.deb](https://github.com/DebianDog/MintPup-Trusty/releases/download/v.1.0/mintpup-trusty-mp1_0.0.1_i386.deb)

I don't see any reason to update the iso image yet. It is useful the way it is. Just install the above maintain pack deb. What it does you can read inside the postinst scripts:

```
#!/bin/sh

mv -f -t /etc/apt/sources.list.d /opt/temp/official-package-repositories.list
mv -f -t /usr/local/bin /opt/temp/apt2sfs-cli-fullinst
mv -f -t /opt/bin /opt/temp/ffmpeg2sfs
mv -f -t /opt/bin /opt/temp/sfs-get-mint
rmdir /opt/temp

if [ -x "`which update-menus 2>/dev/null`" ]; then
	update-menus
fi

```

Probably any new fixes will be provided the same way.

**4.** Upgrading newer xserver-xorg-video-intel package will fail to startx if you run MintPup on very pld machine with intel GPU like this one:

```
lspci | grep VGA
00:01.0 VGA compatible controller: Intel Corporation 82810 DC-100 (CGC) Chipset Graphics Controller (rev 03)
```
The fix is to install [xserver-xorg-video-intel_2.99.910-0ubuntu1.7_i386.deb](https://github.com/DebianDog/MintPup-Trusty/releases/download/v.1.0/xserver-xorg-video-intel_2.99.910-0ubuntu1.7_i386.deb) to restore the included in the iso driver.
