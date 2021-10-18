Lab 1
======

Create Directory and Files
+++++++++++++++++++++++++++

In this lab you will create a Dockerfile which will be used to create a static container.

Create 

- Project folder called lab1
.. code-block:: bash

   mkdir ~/lab1
   
- Create the following files inside the *lab1* directory
   * index.html
   * web.conf 
   * Dockerfile

What did I just do?

*index.html* 

- This is the default webserver page that gets served up first

*web.conf*

- This has our server block configurations for our Nginx webserver 

*Dockerfile*

- Holds instructions for Docker to build our customer docker image and adds it to our local docker repository 

.. code-block:: html
   :caption: index.html 

   <html>
   <head>
   <title> TEST SITE</title>
   </head>
   <body>
   First Page 
   <p>Demo site for training.</p>
   </body>
   </html>

.. code-block:: bash 
   :caption: web.conf 

   server {
     listen 80;
     server_name docweb.lab.lan;

     root /usr/share/nginx/html;
     index index.html;

     location / {

     }

     location /doc_status {
       stub_status on;
       allow 172.17.0.1;
       deny all;
     }
   }

.. code-block:: bash
   :caption: Dockerfile

   FROM nginx

   RUN rm -f /etc/nginx/conf.d/default.conf 

   COPY web.conf /etc/nginx/conf.d/web.conf
   COPY index.html /usr/share/nginx/html/index.html 

How the Dockerfile works:

| *FROM the publicly available Nginx container, usually Docker Hub (use this as our base image)*
| **FROM nginx**

| *RUN the Linux command to remove the default.conf file we will install our own web.conf file*
| **RUN rm -f /etc/nginx/conf.d/default.conf** 

| *COPY in the new files to the container during creation*
| **COPY web.conf /etc/nginx/conf.d/web.conf**
| **COPY index.html /usr/share/nginx/html/index.html**

Build and Run the Container
+++++++++++++++++++++++++++

From the *lab1* directory


.. code:: bash 
   :caption: Build image

   docker build -t docimg .

.. code:: bash
   :caption: Run Container

   docker run -p 81:80 --name docweb -h docweb.lab.local -dit docimg 

Let's validate the new container is running. docker ps -a will show all docker processes both running and excited. Take note 
of the column hearders. On **note** Container ID, Image, Status, Ports and Names.

.. code:: bash

   docker ps -a 

For additional container inspection run the command ``ifconfig``, this command is much like the windows ipconfig and will show
all the interfaces on your machine, we want to see the *docker0* interface and ip address. Typically this lives in the 
172.17.0.0 neighborhood. Mac and Windows do **NOT** expose the docker bridge.

.. code:: bash 
   :caption: Docker inspect

   docker inspect docweb 

This command will show up all the details of our newly constructed container. You should find it's ip address within the docker0
cidr.

.. code:: bash 
   :caption: Container Shell 

   docker exec -it docweb nginx -t
   docker exec -it docweb nginx -s reload 
   docker exec -it docweb /bin/bash

Using your browser, navigate to 

* http://localhost:81 
* http://localhost:81/doc_status 


Now let's view the logs from your container 

.. code:: bash 
   :caption: Docker Logs 

   docker logs docweb 


Remove Container
++++++++++++++++

We will *force* remove the container, this will stop and delete it in one command. 

.. code:: bash
   
   docker rm -f docweb 

Now we want to find and delete our now *old* customer docker image. Let's get its container id: 

.. code:: bash 
   :caption: Image ID 

   docker images | grep docimg 

Copy the contianer id from the above step and paste it in place of the words *container_id* below

.. code:: bash 
   :caption: Delete Image 

   docker rmi container_id

