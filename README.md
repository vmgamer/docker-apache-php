# Docker Apache PHP

## To Build manual way
``` bash
git clone https://github.com/vmgamer/docker-apache-php.git
cd docker-apache-php
sudo docker build -t="eugeneware/docker-apache-php" .
CONTAINER=$(docker run -d -p 8082:80 -p 33060:3306 -v ~/domainesia.com/www:/var/www/html --name domainesia.com eugeneware/docker-apache-php)
sudo docker ps

cd ..
rm -rf docker-apache-php
```

### To Run

Use [docker volumes](http://docs.docker.io/use/working_with_volumes/) to expose
your web content to the apache web server.

``` bash
# run docker apache php
$ CONTAINER=$(docker run -d -p 8082:80 -p 33060:3306 -v /your/path/to/serve:/var/www/html eugeneware/docker-apache-php)

# get the http port
# $ docker port $CONTAINER 80
# 0.0.0.0:49206
```

### To access the database
``` bash
# get the mysql port
# $ docker port $CONTAINER 3306
# 0.0.0.0:49205

# get [dockerhost] IP reading 'inet addr' value
$ ifconfig docker0 | grep 'inet addr'
          inet addr:172.17.42.1  Bcast:0.0.0.0  Mask:255.255.0.0

$ mysql -h172.17.42.1 -uroot -P 33060
```
