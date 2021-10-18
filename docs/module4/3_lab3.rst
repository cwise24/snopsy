Lab 3
======

Advanced Dockerfile
+++++++++++++++++++

What if we need to expose additional ports that aren't part of the base image? And we need different server *listeners* for that
port?

Create directory *lab3* and we'll copy over the files *lab2/conf/web.conf* and *lab2/html/index.html* plus create two new files 

.. code-block:: bash 
   :caption: Lab 3 Files

   mkdir lab3
   cd lab3  
   cp /lab2/html/index.html .
   cp /lab2/conf/web.conf .
   touch app.html 
   touch Dockerfile 

.. code-block:: bash 
   :caption: Dockerfile 

   FROM nginx
   RUN rm -f /etc/nginx/conf.d/default.conf 

   COPY web.conf /etc/nginx/conf.d/web.conf
   COPY index.html /usr/share/nginx/html/index.html 
   COPY app.html /usr/share/nginx/html/app.html 

   EXPOSE 8333/tcp 

Now we'll need to modify the *web.conf* file for our new content 

.. code-block:: bash 
   :caption: Modify web.conf 

   server {
     listen 80;
     server_name docweb.lab.lan;

     root /usr/share/nginx/html;
     index index.html;

     location / {

     }
   }

   server {
     listen 833;
     server_name docweb.lab.lan;

     root /usr/share/nginx/html;
     index app.html 
    
     location / {

     }
   }

Now to create the *app.html* webpage 

.. code-block:: html 
   :caption: app.html 

   <html>
   <head>
   <title>app site</title>
   </head>
   <body>
   application page 
   <p>app.html is not a normal index page.</p>
   </body>
   </html>

Almost there, we still need to complete a couple of steps. Our old volume container is still around and even if it's not 
running, it's *using* the **docweb** name and we don't want that.

.. code-block:: bash 
   :caption: Remove docweb 

   docker rm -f docweb 

Time to create our new image 

.. code-block:: bash 
   :caption: docnew Image 

   docker build -t docnew .

Once the image is ready, it's time to run our new container 

.. code-block:: bash 
   :caption: Docker Run 

   docker run -p 81:80 -p 82:8333 --name docweb -dit docnew 

Navigate to 
* http://localhost:81 
* http://localhost:82
