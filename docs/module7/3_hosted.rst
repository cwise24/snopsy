Hosted
======

Once you've started the UDF course. Navigate to the **gns** system box and select the *ACCESS* dropdown and click on *WEB SHELL*

.. image:: imgs/webshell.png 
   :align: center
   :scale: 30%

Once open, issue the commands

.. code-block:: bash
   :caption: gns3 

   su -l ubuntu 
   gns3server

.. image:: imgs/gns3server.png
   :align: center
   :scale: 30%

Once the GNS3 server is up and running, we'll now use the web UI to access the BGP lab. Open the *FIREFOX* option from the *ACCESS* dropdown

.. image:: imgs/firefox.png
   :align: center
   :scale: 30%
   
From the new Firefox tab, open the BGP_Lab bookmark.

.. image:: imgs/bgpbookmark.png
   :align: center
   :scale: 30%

You should now see the lab topology like below.

.. image:: imgs/bgplabui.png
   :align: center
   :scale: 30%

The nameing conventions for the routers are **R** for router, the number router and the ASN the router is in. So R1-1 is Router 1 in the autonomous system 1.

Hover your mouse over **R1-1** and right click to show the router options, we will be starting the router.

.. image:: imgs/start.png
   :align: center
   :scale: 30%

Once the router is started you should now see in the legend to the far right it's greem status.

.. image:: imgs/running.png
   :align: center
   :scale: 30%

Now you'll need to start each router, we are doing it this way to keep resoure utilization down. If we started all the routers at once it would overwhelm the VM we have.
Please allow each router to start before starting the next one.

Once all the routers are started, you should see them all in the legend to the far right with green status. Now you can open the GNS3 web console for each router.

.. image:: imgs/webconsole.png
   :align: center
   :scale: 30%
   
You may need to verify the routers are all in the proper *starting configuration*. Those configurations are provided in the self hosted section.

An easy way to copy configurations if missing will be to connect to the via terminal option and then use telnet to access the router consoles.

.. image:: imgs/terminal_ssh_telnet.png
   :align: center
   :scale: 30%

You can now connect to each router via its unique port to copy/paste configuration. 

.. image:: imgs/ssh_telnet_config.png
   :align: center
   :scale: 30%

.. list-table:: Router Telnet Port
   :widths: 20 20 20
   :align: center
   :header-rows: 1
  
   * - Router
     - IP
     - Port
   * - R1-1
     - 10.1.1.4
     - 5001
   * - R2-1
     - 10.1.1.4
     - 5003
   * - R3-1
     - 10.1.1.4
     - 5005
   * - R1-4
     - 10.1.1.4
     - 5009
   * - R1-5
     - 10.1.1.4
     - 5007
   * - R1-6
     - 10.1.1.4
     - 5013
   * - R1-7
     - 10.1.1.4
     - 5011

.. note::
   To exit use ``Cntrl + ]`` followed by ``quit`` to exit telnet.