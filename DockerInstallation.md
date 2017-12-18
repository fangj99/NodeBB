
# Docker Installation of Nodebb

### Create docker container from image with ubuntu 16.04, I am using Image :

```
alexcomu/docker-nginx-ssh-mysql-php7:latest

User Name: Topix
Password: Topix
```

### Then we can create the container with ports exposed as following
```
sudo docker run -p 7000:22 -p 80:80 -p 443:443 -p 4567:4567 -p 27017:27017 --name nodebb  -h nodebb  -d alexcomu/docker-nginx-ssh-mysql-php7:latest 

ssh -p7000 topix@localhost
```
### Shutdown mysql and php

```
sudo service stop mysql
sudo service php7.0-fpm stop
```

### Install Node.js and check version (node >= v6.9.5 npm >=3.10.10)

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs

node -v
npm -v
```

# Install MongoDB, the following steps are different from the nodebb's official document and much simple
```
sudo apt-get update
sudo apt-get install mongodb
```
### Configure MongoDB
```
$ mongo
> use admin
> db.createUser( { user: "<Enter a username>", pwd: "<Enter a secure password>", roles: [ { role: "readWriteAnyDatabase", db: "admin" }, { role: "userAdminAnyDatabase", db: "admin" } ] } )
> use nodebb
> db.createUser( { user: "nodebb", pwd: "<Enter a secure password>", roles: [ { role: "readWrite", db: "nodebb" }, { role: "clusterMonitor", db: "admin" } ] } )
> quit()

```
### Enable Security of MongoDB (not working with official, will update later)
```
```
### Test MongoDB
```
$ sudo service mongod restart
$ mongo -u your_username -p your_password --authenticationDatabase=admin
```

### Install NodeBB
```
sudo apt-get install -y git build-essential
git clone -b v1.6.x https://github.com/NodeBB/NodeBB.git $HOME/nodebb
cd nodebb
 ./nodebb setup
 ./nodebb start
```


















