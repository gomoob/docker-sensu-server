# Supported tags and respective `Dockerfile` links

- [`0.29.0-11` (*1.0.0/Dockerfile*)](https://github.com/gomoob/docker-sensu-server/blob/master/1.0.0/Dockerfile)

# What is docker-sensu-server ?

[docker-sensu-server](https://github.com/gomoob/docker-sensu-server "docker-sensu-server") is an all-in-one Sensu
server. It contains a preconfigured Sensu server, Sensu API, a RabbitMQ broker and the Uchiwa web console inside only
one Docker container.

# How to use this image.

## With command line

```console
$ docker run --name sensu-server -d -p 3000:3000 -p 4567:4567 -p 5671:5671 -p 15672:15672 gomoob/php-websocket-server:1.1.0
```

*WARNING* : Please note that under Windows the server will be accessible at `http://192.168.99.100` in 
this case.

## With Docker compose


## Using custom configuration

The container has default configuration files which are stored inside the `/etc/sensu` and `/etc/rabbimq` directories
inside the container.

You can overwrite those configuration files by creating 2 folders on you host and mapping them using Docker volumes. We 
advise you to create a hierarchy of files and folders by using one of the zip files we provide for each version of the 
container.

```
/home/john.doe/etc
  |
  |- rabbitmq
  \- sensu
```

Then simply update the files you want and start the container using Docker volume mappings on each of the 2 folders.

```
$ docker run --name sensu-server -d \
    -v /home/john.doe/etc/sensu:/etc/sensu \
    -v /home/john.doe/etc/rabbitmq:/etc/rabbitmq \
    -p 3000:3000 -p 4567:4567 -p 5671:5671 -p 15672:15672 gomoob/php-websocket-server:1.1.0
```

# Production settings

The configuration files we provide are in most cases well configured to start quickly. But if need to deploy a Sensu 
server and lot of clients we found that custom settings could be necessary to support the load.

This chapter details the most important settings to configure for production environments with several hundreds Sensu 
clients.

## RabbitMQ

For RabbitMQ event if your configuration is not perfect the least you can do is to confire Memory and Disk Alarms
correctly to be alerted when a problem is encountered. 

This is very important because if your RabbitMQ server stops to work and one of your Sensu client crashes then you'll 
not be alerted of this crash.

The documentation about RabbitMQ alarms is available at the following address https://www.rabbitmq.com/alarms.html.

# About Gomoob

At [Gomoob](https://www.gomoob.com) we build high quality software with awesome Open Source frameworks everyday. Would 
you like to start your next project with us? That's great! Give us a call or send us an email and we will get back to 
you as soon as possible !

You can contact us by email at [contact@gomoob.com](mailto:contact@gomoob.com) or by phone number 
[(+33) 6 85 12 81 26](tel:+33685128126) or [(+33) 6 28 35 04 49](tel:+33685128126).

Visit also http://gomoob.github.io to discover more Open Source softwares we develop.
