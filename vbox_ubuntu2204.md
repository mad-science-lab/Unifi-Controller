# Virtual Ubuntu 22.04

Create new VM
* Install distro ubuntu-22.04.1-desktop-amd64.iso
* Attended install
* Minimal install
* Download updates

## Install Virtualbox guest media
1. Open terminal navigate to the "CD" directory 

Run install
```
sudo bash ./VBoxLinuxAdditions.run
```
Reboot the system and then update and upgrade
```
sudo apt update && sudo apt upgrade
```

## <b>OPTIONAL:</b> Install SSH
```
sudo install openssh-server
```
