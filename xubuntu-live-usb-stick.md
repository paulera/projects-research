# Xubuntu Live USB stick

## Boot a live USB entirely on the RAM

You will need this to be able to use **mkusb** \(below\) to rebuild the USB as a persistent live one. Other option is to have 2 USB sticks, one for boot as Live USB, and another one to make as the persistent drive.

* During the live USB boot, highlight the option `Try without installing`press `E`, in the line that starts with `linux` add `toram` after `quiet splash`

![](.gitbook/assets/image%20%283%29.png)

## Make a persistent Live USB with **mkusb**

* This tool runs on linux, so you will need to create an ubuntu VM and use it to setup the USB stick
* Edit the file `/etc/apt/sources.list`
* Add the PPA:`deb http://ppa.launchpad.net/mkusb/ppa/ubuntu focal main # stable version, tested and reliable`
* Import the GPG key: `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 54B8C8AC`
* Install **mkusb**: `sudo apt-get update` then `sudo apt-get install mkusb`
* Run **mksub** and select the option `p: Plug (New, easy to use)`
* Follow instructions from **mkusb**.

## Increase lifetime of the USB stick

* Add `noatime` to the mount options of `/` mount point in the file `/etc/fstab`
  * This will make the OS to not compute the "Last Access" value of files when they are read
* Disable swap: `sudo swapoff --all`
* Highly used directories such as `/var/tmp/` and possibly `/var/log` can be relocated to RAM in `/etc/fstab` like this: `tmpfs /var/tmp tmpfs nodev,nosuid,size=50M 0 0`

```text
overlay / overlay rw,noatime 0 0
tmpfs /tmp tmpfs nosuid,nodev,noatime,size=250M 0 0
tmpfs /var/tmp tmpfs nosuid,nodev,noatime,size=100M 0 0
tmpfs /var/log tmpfs nosuid,nodev,noatime,size=250M 0 0
tmpfs /var/run tmpfs nosuid,nodev,noatime,size=50M 0 0
```

* Make firefox use RAM for cahe instead of disk:
  * browse `about:config`
  * browser.cache.disk.enable = false
  * browser.cache.memory.enable = true
  * browser.cache.memory.capacity = 204800
    * memory capacity is KB, so 204800 = 200MB

## Bookmarks

### Making a persistent live USB

{% embed url="https://www.reddit.com/r/xubuntu/comments/8w6zhw/persistent\_usb\_bootable\_version\_of\_xubuntu/" %}

### Increase lifetime

{% embed url="https://askubuntu.com/questions/1058318/how-to-maximize-the-life-of-a-pendrive-which-has-a-full-installation-of-ubuntu-m" %}

### Boot Linux fully into RAM, can remove disk or edit it after boot

{% embed url="https://askubuntu.com/questions/829917/can-i-boot-a-live-usb-fully-to-ram-allowing-me-to-remove-the-disk" %}

{% embed url="https://askubuntu.com/questions/1126145/can-i-convert-a-live-ubuntu-usb-to-one-with-persistent-memory" %}

### Installing mkusb

{% embed url="https://help.ubuntu.com/community/mkusb/install-to-debian" %}

### profile-sync-daemon: Store browser profile in RAM and flush from time to time to the disk

{% embed url="https://ostechnix.com/how-to-sync-browser-profile-into-tmpfs-ram-in-linux/" %}

```text
sudo apt-get install profile-sync-daemon

# first run:
psd
# First time running psd so please edit
# /home/sk/.config
/psd/psd.conf to your liking
# and run again.

vim /home/paulo/.config/psd/psd.conf

# EDIT THIS LINE
# [...]
# BROWSERS="chromium firefox"
# [...]

# Enable and start PSD service
systemctl --user enable psd
systemctl --user start psd

# Check whether it is running
systemctl --user status psd

# Check what PSD is doing
 psd p
 
 # change syn interval
 crontab -e
 # update the entry accordingly
 # */15 * * * *     /usr/bin/profile-sync-daemon sync &> /dev/null
 
 

```

### Disable overlayroot to be able to make permanent chages to the system

{% embed url="https://spin.atomicobject.com/2015/03/10/protecting-ubuntu-root-filesystem/" %}

override any overlayroot configuration by passing `overlayroot=disabled` to the kernel at boot.

### Reduce cache pressure

{% embed url="https://askubuntu.com/questions/643080/how-to-create-a-live-system-on-usb-drive-with-persistent-changes-on-disk-hdd" %}

In your `/etc/sysctl.conf` add:

```text
# Fabby: change the "swappiness" to 10 to prevent swapping as much as possible
# to not wear out the USB stick as the Ubuntu default is optimized for a server.
# 10 to balance with vfs_cache_pressure
vm.swappiness = 10

# Fabby: Lower vfs_cache_pressure to 75% 
# (once cached, probably not immediately needed any more)
#
# This percentage value controls the tendency of the kernel to reclaim
# the memory which is used for caching of directory and inode objects.
#
# At the default value of vfs_cache_pressure=100 the kernel will attempt to
# reclaim dentries and inodes at a "fair" rate with respect to pagecache and
# swapcache reclaim.  Decreasing vfs_cache_pressure causes the kernel to prefer
# to retain dentry and inode caches.
vm.vfs_cache_pressure = 75

# Fabby: Good to improve sequential reads (stop stuttering in movie play)
# Can also be implemented per disk using udev rules
vm.max-readahead=2048
vm.min-readahead=1024
```

### Add mount commands to rc.local because /etc/fstab keeps being rewritten on persistent live USB

{% embed url="https://askubuntu.com/questions/56719/what-file-resets-fstab-on-persistent-live-environments" %}

 Add your mount commands in **`/etc/rc.local`**

```text
...
mount -t ntfs-3g -L Inter /media/Inter -o uid=1000,gid=999,umask=002
exit
```

