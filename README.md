# Unifi-Controller

This is for my personal use. I have put it here for safe keeping. if you use any of the information contained here; it is provided with absolutely no support, warranty, guarantee, etc..

DRAFT January 2023

## Key Notes
- Requirements 
	- libssl1.0.0
		- https://packages.ubuntu.com/bionic/amd64/libssl1.0.0/download
	- Mongo-db-org 3.4
	

## Pre-Work: Create a list file

Unifi Repository [^1]
```
echo 'deb {trusted=yes] https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/unifi-install.list
```
### MongoDB Repositories
Debian [^3]
```
echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.4 main" | sudo tee /etc/apt/sources.list.d/unifi-install.list 
```
Ubuntu 14.04 [^2]
```
echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/unifi-install.list
```
Ubuntu 16.04 [^2]
```
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/unifi-install.list 
```

#### Reload the package database
```
sudo apt-get update
```


## Install libssl1.0.0*
Download libssl1.0.0 
```
wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/libssl1.0.0_1.0.2n-1ubuntu5.10_amd64.deb
```
Install SSL 1.0  :(
```
sudo apt install ./libssl1.0.0_1.0.2n-1ubuntu5.10_amd64.deb
```
## Install Mongo DB
Add the GPG key [^2][^3] 
```
wget -qO - https://www.mongodb.org/static/pgp/server-3.4.asc | sudo apt-key add - </b>
```
If you get an error [^4]


Next install MongoDB. You added the repository in prework and SSL 1.0 is prerequisite.[^2][^3]
```
sudo apt-get install -y mongodb-org
```
Start Mongo
```
sudo service mongod start
```

## Install Unifi Controller

1. Install required packages before you begin with the following command: [^1]
```
sudo apt-get install ca-certificates apt-transport-https 
```
2. Use the following command to add a new source list: [^1]
```
echo 'deb https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt-unifi.list
```
3. Add the GPG Keys. To add the GPG Keys use one of the two methods described below (Method A is recommended). 
(Method A) Install the following trusted key into /etc/apt/trusted.gpg.d
```
sudo wget -O /etc/apt/trusted.gpg.d/unifi-repo.gpg https://dl.ui.com/unifi/unifi-repo.gpg 
```
(Method B) Using apt-key.
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50 
```

4. Install and upgrade the UniFi Network application.

```
sudo apt-mark hold openjdk-11-*
```
Install and upgrade the UniFi Network application with the following command:
```
sudo apt-get update && sudo apt-get install unifi -y
```

## Load Unifi Controller
```
http://localhost:8443
```



[^1]: https://help.ui.com/hc/en-us/articles/220066768-UniFi-Network-Updating-Third-Party-non-Console-UniFi-Network-Applications-Linux-Advanced-
[^2]: https://www.mongodb.com/docs/v3.4/tutorial/install-mongodb-on-ubuntu/
[^3]: https://www.mongodb.com/docs/v3.4/tutorial/install-mongodb-on-debian/
[^4]: https://itsfoss.com/solve-gpg-error-signatures-verified-ubuntu/
