Lab 2
=====

Create Directories 
+++++++++++++++++++

.. code-block:: bash 
   :caption: Create Directories

   mkdir -p lab2/html 
   mkdir -p lab2/conf

We will now copy our *index.html* and *web.conf* files from Lab1 to this project. ``cp`` is the Linux copy command and works as such:
``cp source destination``. Using the trailing ``.`` in our destination lets Linux know we want to use the same name as the source.

.. code-block:: bash 
   :caption: Copy Files 

   cp lab1/index.html lab2/html/.
   cp lab1/web.conf lab2/conf/.



Attach Volume to Container
+++++++++++++++++++++++++++


.. code-block:: bash
   :caption: Attach Volume 

   docker run -p 81:80 -v ~/lab2/conf:/etc/nginx/conf.d/web.conf -v ~/lab2/html:/usr/share/nginx/html --name docweb -dit nginx 

Validate the site is working

.. code-block:: bash 

   docker ps -a 

Navigate to 

http://localhost:81 


Now, lets go to your *index.html* file in *lab2/html/index.html* and alter some text like highlighted below.

.. code-block:: html 
   :caption: Alter text
   :emphasize-lines: 6

   <html>
   <head>
   <title> TEST SITE</title>
   </head>
   <body>
   Lab 2 
   <p>Demo site for training.</p>
   </body>
   </html>

Once your change is made, you should be able to reload your page by either Cntrl r or CMD r and observe your code update.