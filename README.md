# Raspberry-Pi-Dev-Config
Configuration for a Raspberry Pi with Samba etc for development.
This is mainly to be able to edit files using visual studio code or some other IDE. While visual studio code has the SSH extension, it is resource heavy and takes up a ton of memory on the PI. This is a much lighter weight solution. You will have to have a terminal open to execute code, but thats easy enough to do. Just put a small putty terminal below visual studio code as if it were the built in terminal.

## Install Samba
1. `sudo apt update` (optional to do a `sudo apt upgrade`) 
2. `sudo apt install samba samba-common-bin`

### Configure shared folder
1. `sudo touch /opt`
2. `sudo chown <user>.<user> /opt`

### Edit Samba Config
1. `sudo vi /etc/samba/smb.conf`
2. Add the following to the end of the file
```
[devshare]
  path = /opt
  writable = yes
  browsable = yes
  public = no
  guest ok = no
  valid users = @<user>
```
### Setup Access to Share
1. `sudo smbpasswd -a <user>`

### Restart Samba on the Pi
1. `sudo systemctl restart smbd`

## Access the share
On your computer you should be able to get to the Pi by going to `\\<ipaddress>/devshare`

