# libguestfs-ubuntu20
* ubuntu20 image for libguestfs
* also freebsd 12.1

Uses
<pre>
[ubuntu20]
uri=http://mirror.trouble-free.net/libguestfs/index.asc
gpgkey=file:///etc/xdg/virt-builder/repos.d/ubuntu20.gpg
</pre>

copy ubuntu20.gpg and ubuntu-20.conf to /etc/xdg/virt-builder/repos.d/


* build your image
<pre>
virt-builder ubuntu-20.04 --root-password password:CHOOSEYOURPASS --update --hostname ubuntu-20.is.cc --format qcow2 -o ubuntu-20.qcow2
[   2.2] Downloading: http://mirror.trouble-free.net/libguestfs/ubuntu-20-04.img.xz
##################################################################################################################################################################### 100.0%
[  25.0] Planning how to build this image
[  25.0] Uncompressing
[  48.8] Converting raw to qcow2
[ 136.9] Opening the new disk
[ 184.5] Setting a random seed
virt-builder: warning: random seed could not be set for this type of guest
[ 184.5] Updating packages
[ 241.0] Setting the hostname: ubuntu-20.is.cc
[ 243.6] Setting passwords
[ 245.0] Finishing off
                   Output file: ubuntu-20.qcow2
                   Output size: 6.0G
                 Output format: qcow2
            Total usable space: 5.8G
                    Free space: 4.0G (68%)
</pre>


* As always
IMPORTANT WARNING:
It seems to be impossible to create an Ubuntu >= 14.04 image using
preseed without creating a user account.  Therefore this image
contains a user account 'builder'.  I have disabled it, so that
people who don't read release notes don't get caught out, but you
might still wish to delete it completely.
 
This image does not contain SSH host keys.  To regenerate them use:
 
 --firstboot-command "dpkg-reconfigure openssh-server"

* The command used to generate
<pre>
'virt-install' \
    '--transient' \
    '--name=tmp-msgb0g0m' \
    '--ram=2048' \
    '--cpu=host' \
    '--vcpus=4' \
    '--os-variant=ubuntu17.04' \
    '--initrd-inject=/tmp/65iqip61.tmp/preseed.cfg' \
    '--extra-args=auto console=tty0 console=ttyS0,115200 rd_NO_PLYMOUTH' \
    '--disk=/tmp/tmp-msgb0g0m.img,size=6,format=raw' \
    '--location=http://archive.ubuntu.com/ubuntu/dists/focal/main/installer-amd64' \
    '--serial=pty' \
    '--nographics'
</pre>
