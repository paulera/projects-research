# Xubuntu Live USB stick

## Lessons learned

* Increase lifetime
  * Add `noatime` to the mount options of `/` mount point in the file `/etc/fstab`
  * Disable swap: `sudo swapoff --all`
  * Highly used directories such as `/var/tmp/` and possibly `/var/log` can be relocated to RAM in `/etc/fstab` like this: `tmpfs /var/tmp tmpfs nodev,nosuid,size=50M 0 0`

## Making a persistent live USB

{% embed url="https://www.reddit.com/r/xubuntu/comments/8w6zhw/persistent\_usb\_bootable\_version\_of\_xubuntu/" %}

## Increase lifetime

{% embed url="https://askubuntu.com/questions/1058318/how-to-maximize-the-life-of-a-pendrive-which-has-a-full-installation-of-ubuntu-m" %}



