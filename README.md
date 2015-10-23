### Learning Docker http://docker.io/ by creating a RabbitMQ container.

http://docs.docker.io/en/latest/use/builder/#dockerfile-examples

http://www.rabbitmq.com/install-debian.html

### To build:

    sudo docker build ursuad/docker-rabbitmq.git

### To run:

    sudo docker pull ursuad/docker-rabbitmq
    sudo docker run -it --rm --name rabbit -p 5672:5672 -p 15672:15672 ursuad/docker-rabbitmq
    
### To persist your data:

Here we persistently save our data to the host machine's ``/tmp/rabbitmq/mnesia`` directory.

    mkdir -p /tmp/rabbitmq/mnesia
    chmod 777 /tmp/rabbitmq/mnesia
    sudo docker run -it --rm --name rabbit -h rabbithost -p 5672:5672 -p 15672:15672 -v /tmp/rabbitmq/mnesia:/var/lib/rabbitmq/mnesia ursuad/docker-rabbitmq

Since RabbitMQ uses the ``$HOSTNAME`` in its data path, we need to explicitly set it for the container.

    $ sudo docker run -it --rm --name rabbit -h rabbithost -p 5672:5672 -p 15672:15672 -v /tmp/rabbitmq/mnesia:/var/lib/rabbitmq/mnesia ursuad/docker-rabbitmq
    WARNING: Docker detected local DNS server on resolv.conf. Using default external servers: [8.8.8.8 8.8.4.4]
    
                  RabbitMQ 3.1.5. Copyright (C) 2007-2013 GoPivotal, Inc.
      ##  ##      Licensed under the MPL.  See http://www.rabbitmq.com/
      ##  ##
      ##########  Logs: /var/log/rabbitmq/rabbit@rabbithost.log
      ######  ##        /var/log/rabbitmq/rabbit@rabbithost-sasl.log
      ##########
                  Starting broker... completed with 6 plugins.

