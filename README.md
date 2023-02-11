# media-server

### Setup static IP

```
connmanctl services
sudo connmanctl config ethernet_88c2556c4fee_cable --ipv4 manual 192.168.1.10 255.255.255.0 192.168.1.1 --nameservers 8.8.8.8 8.8.4.4
```

### Mount USB harddisk

Add NTFS support (Not sure this was required)
```
sudo apt-get install ntfs-3g
```

Create mount point (Not sure this was required)
```
cd /media
sudo mkdir usb
sudo chmod ugo=+wrxst usb
```

Edit /etc/fstab
```
/dev/sda1 /media/usb ntfs rw,user,exec,auto,nofail 0 0
```

### Install SAMBA

```
sudo apt-get update
sudo apt-get install samba
```

