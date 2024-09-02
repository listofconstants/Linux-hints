### Make bootable Linux installer in Mac OS
*not tested*

List connected storage devices:
```
diskutil list
```

Identify and format the USB drive:
```
diskutil eraseDisk FAT32 LINUX_INSTALL /dev/diskX
```

Mount the ISO via a roundabout method if the Mac will not mount it:
```
# ref: https://superuser.com/questions/1395815/macos-mojave-iso-images-and-no-mountable-file-systems-error
# the '-nomount' option avoids the 'mount failed' error
hdiutil attach -nomount <ubuntu-XXX>.iso

# verify disk is a block device (indicated by 'b' at line start)
ls -l /dev/diskY

# create mount point
mkdir -p /tmp/ubuntu-installer

# mount the disk
mount -t cd9660 /dev/diskY /tmp/ubuntu-installer
ls -l /tmp/ubuntu-installer
```

Copy files from the mounted directory to the USB drive:
```
cp -r /tmp/ubuntu-installer/* /Volumes/LINUX_INSTALL
```

Unmount and detach the ISO:
```
# this will fail if the disk is being used
umount /dev/diskY
hdiutil detach /dev/diskY
rm -r /tmp/ubuntu-installer
```
