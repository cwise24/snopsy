Docker
======

This `link <https://www.codementor.io/djangostars/tutorial-what-is-docker-and-how-to-use-it-with-python-wowos9qte>`_ is a very good high level cover of most basic Docker commands you will use.

One thing not covered, and is a bit more advanced, is creating your own Docker network versus using the ``docker0`` bridge assigned IP address. I will cover the steps to build a custom
Docker network and assign that network and an IP address to a container.

First you have to create the network and give it an alias name::

    docker network create --subnet=172.10.1.0/24 mynet

To run a new container within this new network::

    docker run  --net mynet --ip 172.10.1.3 -p 81:80 -h web1.local.com --name web1 --restart unless-stopped -dit nginx

Where ``-h`` sets the hostname and ``--name`` sets an alias name for the container