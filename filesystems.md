# filesystems

## overlay

podman uses `overlay` storage driver by default

`overlay` is a kernel feature that takes two folders and stack them on top of each other, creating a single merged view.

- lowerdir - read-only layer that contains the base image and all the layers above it
- upperdir - read-write layer that contains the changes made to the container
- workdir - a directory used by the overlay driver to manage the merging of the lower and upper layers

this could be seen in the debug logs when building a container with podman:

```bash
DEBU[0000] overlay: 
mount_data=
lowerdir=/home/devops/.local/share/containers/storage/overlay/l/VHC4YUPPUYRX2Z4KLWU42S7QRN:/home/devops/.local/share/containers/storage/overlay/l/4MXXTOXPZTKTGKMLIPEHDFE4OP:/home/devops/.local/share/containers/storage/overlay/l/T5LY75QEXMWCPWSDIOGAUSPXTJ:/home/devops/.local/share/containers/storage/overlay/l/YJLRREF2KZ3CVBTXCKR3SSSCOG,
upperdir=/home/devops/.local/share/containers/storage/overlay/f6211f6778563620c7ab7ba5dab22b19642ecc65cfa4364ae835a3c25a011a56/diff,
workdir=/home/devops/.local/share/containers/storage/overlay/f6211f6778563620c7ab7ba5dab22b19642ecc65cfa4364ae835a3c25a011a56/work,userxattr,volatile
```

To mount an `overlay` filesystem, the Linux kernel strictly requires the user to be root