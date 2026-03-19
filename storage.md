# storage

## make bootable USB with debian image

Why? Because Windows 11 is a piece of shit and I want to install proper (debian) OS on my laptop.

Download the latest Debian image from the official website: https://www.debian.org/distrib/
```
wget https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/debian-13.4.0-amd64-DVD-1.iso -P /debian 
```

Use `dd` tool to write the image to the USB drive. Make sure to replace `/dev/sdb` with the correct device name for your USB drive (check it using `lsblk` command):

```
dd if=/debian/debian-13.4.0-amd64-DVD-1.iso of=/dev/sdb bs=4M status=progress conv=fsync
```


## connect usb drive to the Pi and list files on it

Physically connect the USB drive to the Raspberry Pi.

See block name of the USB drive using `lsblk` command:

```bash
lsblk
```

Mount the USB drive to a directory (e.g., /mnt/usb):

```bash
sudo mount /dev/sdb1 /mnt/usb
```

List files on the USB drive:
```bash
ls /mnt/usb
```