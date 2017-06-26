# Supported tags and respective `Dockerfile` links

- [`1.0.3` (*1.0.0/Dockerfile*)](https://github.com/gomoob/docker-sensu-server/blob/master/1.0.0/Dockerfile)

# What is docker-sensu-server ?

[docker-sensu-server](https://github.com/gomoob/docker-sensu-server "docker-sensu-server") is an all-in-one Sensu 
server. It contains a preconfigured Sensu server, Sensu API, a RabbitMQ broker and the Uchiwa web console inside only 
one Docker container.

# How to use this image.

```console
$ docker run --name sensu-server -d -p 3000:3000 -p 4567:4567 -p 5671:5671 -p 15672:15672 gomoob/php-websocket-server:1.1.0
```

*WARNING* : Please note that under Windows the server will be accessible at `http://192.168.99.100` in 
this case.


## About Gomoob

At [Gomoob](https://www.gomoob.com) we build high quality software with awesome Open Source frameworks everyday. Would 
you like to start your next project with us? That's great! Give us a call or send us an email and we will get back to 
you as soon as possible !

You can contact us by email at [contact@gomoob.com](mailto:contact@gomoob.com) or by phone number 
[(+33) 6 85 12 81 26](tel:+33685128126) or [(+33) 6 28 35 04 49](tel:+33685128126).

Visit also http://gomoob.github.io to discover more Open Source softwares we develop.
