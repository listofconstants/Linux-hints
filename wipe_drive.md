### Use dd to wipe drive while showing progress
```
lsblk  # identify device
dd if=/dev/urandom of=/dev/sdX bs=4k status=progress
```
