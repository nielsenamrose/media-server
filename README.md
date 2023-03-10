# media-server

### Setup static IP

```
connmanctl services
sudo connmanctl config ethernet_88c2556c4fee_cable --ipv4 manual 192.168.1.10 255.255.255.0 192.168.1.1 --nameservers 8.8.8.8 8.8.4.4
```

### Setup ddclient to update dynamic DNS

```
sudo apt-get install ddclient
```
see [tutorial](https://serdima.wordpress.com/2018/04/23/tutorial-updating-dynamic-dns-with-ddclient/)

```
protocol=dyndns2
use=web, web=checkip.dyndns.com, web-skip='IP Address'
server=api.dynu.com
login=nielsen74
password='<password>'
giessinglund.freeddns.org
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
Edit /etc/samba/smb.conf add
```
[Media]
path = /media/usb
writable = yes
guest ok = yes

[Private]
path = /media/usb
writable = yes
guest ok = no
write list = root, debian
```

```
$ sudo smbpasswd -a debian
```

### Mount other smb share

```
sudo apt-get install cifs-utils
cd /mnt
sudo mkdir Public
sudo mount -t cifs //192.168.1.100/Public /mnt/Public
```

