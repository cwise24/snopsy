Lab 1
======

In this lab you will create a Dockerfile which will be used to create a static container.

Create 

- Project folder called lab1 ( mkdir ~/lab1)
- Create files:
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