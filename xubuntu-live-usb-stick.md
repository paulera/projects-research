# Xubuntu Live USB stick

## Lessons learned

* Increase lifetime
  * Add `noatime` to the mount options of `/` mount point in the file `/etc/fstab`
  * Disable swap: `sudo swapoff --all`
  * Highly used directories such as `/var/tmp/` and possibly `/var/log` can be relocated to RAM in `/etc/fstab` like this: `tmpfs /var/tmp tmpfs nodev,nosuid,size=50M 0 0`
* Boot a live USB entirely on the RAM:
  * You will need this to be able to use **mkusb** \(below\) to rebuild the USB as a persistent live one. Other option is to have 2 USB sticks, one for boot as Live USB, and another one to make as the persistent drive.
  * Boot to RAM: During the live USB boot, highlight the option `Try without installing`press `E`, in the line that starts with `linux` add `toram` after `quiet splash`
* Tool for making persistent USB **mkusb**
  * This tool runs on linux, so you will need to create an ubuntu VM and use it to setup the USB stick
  * Edit the file `/etc/apt/sources.list`
  * Add the PPA:`deb http://ppa.launchpad.net/mkusb/ppa/ubuntu focal main # stable version, tested and reliable`
  * Import the GPG key: `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 54B8C8AC`
  * Install **mkusb**: `sudo apt-get update` then `sudo apt-get install mkusb`
  * Run **mksub** and select the option `p: Plug (New, easy to use)`
  * Follow instructions from **mkusb**.
  * 

## Making a persistent live USB

{% embed url="https://www.reddit.com/r/xubuntu/comments/8w6zhw/persistent\_usb\_bootable\_version\_of\_xubuntu/" %}

## Increase lifetime

{% embed url="https://askubuntu.com/questions/1058318/how-to-maximize-the-life-of-a-pendrive-which-has-a-full-installation-of-ubuntu-m" %}

## Boot Linux fully into RAM, can remove disk or edit it after boot

{% embed url="https://askubuntu.com/questions/829917/can-i-boot-a-live-usb-fully-to-ram-allowing-me-to-remove-the-disk" %}

{% embed url="https://askubuntu.com/questions/1126145/can-i-convert-a-live-ubuntu-usb-to-one-with-persistent-memory" %}

![](.gitbook/assets/image%20%283%29.png)

## Installing mkusb

{% embed url="https://help.ubuntu.com/community/mkusb/install-to-debian" %}



