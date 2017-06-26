# This Dockerfile is inspired by https://github.com/hiroakis/docker-sensu-server
FROM centos:latest

MAINTAINER Baptiste Gaillard <baptiste.gaillard@gomoob.com>

ENV RABBIT_MQ_VERSION 3.1.4
ENV SENSU_VERSION 0.29.0-11
ENV UCHIWA_VERSION 0.25.2-1

# Basic packages
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-9.noarch.rpm \
  && yum -y install passwd sudo git wget openssl openssh openssh-server openssh-clients

# Redis
RUN yum install -y redis

# RabbitMQ
RUN yum install epel-release
RUN wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm
RUN rpm -Uvh erlang-solutions-1.0-1.noarch.rpm
RUN yum install -y erlang-20.0
RUN yum install -y socat
RUN rpm --import https://www.rabbitmq.com/rabbitmq-signing-key-public.asc
RUN rpm -Uvh https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.10/rabbitmq-server-3.6.10-1.el7.noarch.rpm

ADD ./etc/rabbitmq/rabbitmq.config /etc/rabbitmq/
RUN rabbitmq-plugins enable rabbitmq_management

# Sensu server
ADD ./etc/yum.repos.d/sensu.repo /etc/yum.repos.d/
RUN rpm -Uvh https://sensu.global.ssl.fastly.net/yum/7/x86_64/sensu-$SENSU_VERSION.el7.x86_64.rpm
ADD ./etc/sensu/config.json /etc/sensu/

# uchiwa
RUN rpm -Uvh http://dl.bintray.com/palourde/uchiwa/uchiwa-$UCHIWA_VERSION.x86_64.rpm
ADD ./etc/sensu/uchiwa.json /etc/sensu/

# Sensu plugins
RUN yum install -y gcc libstdc++ gcc-c++ ruby ruby-devel rubygems
RUN gem install sensu-plugins-mailer

# supervisord
# see https://gist.github.com/didip/802561
RUN wget http://peak.telecommunity.com/dist/ez_setup.py;python ez_setup.py \
  && easy_install supervisor
ADD ./etc/supervisord.conf /etc/supervisord.conf
RUN mkdir /var/log/supervisord

EXPOSE 3000 4567 5671 15672

CMD ["/usr/bin/supervisord"]
