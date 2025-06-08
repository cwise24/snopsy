BGP LAB 1
=========

Now that the basics are taken care of, let's peer the rest of the routers.


Terminal
++++++++

Basic terminal commands 

We won't go into detail on these commands, but here are the basic commands you will need to know.

enable

show [command]

configure terminal (config t)

do [command]



Peering
+++++++

Time to start peering the reamining routers, start to distribute routes and test reachability.

Since R1-1 and R2-1 are peered and in the same Autonomous System (AS), we will only need to peer the remaining router R3-1 to R1-1. This too will be an iBGP
peer. Rembering that iBGP needs full mesh or route reflector, in this lab we will use route reflector. 

.. NOTE:: 
   iBGP does not share routes it learns from other iBGP peers. This is a route loop prevention mechanism and why we need full mesh or route reflector.

Let's beging with R3-1 and R1-1 by accessing their web console. On your tab in the command prompt, issue the command

.. code-block:: bash
   :caption: Web Console
   
   frr# config t
   frr(config)#
   
In either router you can issue the command ``do show run`` to see the running configuration. 

.. list-table:: 
   :widths: 30 30
   :header-rows: 1

   * - R1-1
     - R3-1

   * - .. code-block::  

          Current configuration:
          !
          frr version 8.2.2
          frr defaults datacenter
          hostname frr
          service integrated-vtysh-config
          !
          interface eth0
           description link to R3-1
           ip address 10.1.13.0/31
          exit 
          interface eth1
           description link to R2-1
           ip address 10.1.12.0/31
          exit 
          interface lo
           description local loopback
           ip address 1.1.1.1/32
          exit
          !
          router bgp 1
           bgp router-id 1.1.1.1
           bgp cluster-id 1.1.1.1
           neighbor pgroup peer-group
           neighbor 10.1.12.1 remote-as 1
           !
           address-family ipv4 unicast
            neighbor 10.1.12.1 route-reflector-client 
           exit address-family
          exit
          !
          end
     - .. code-block::  

          Current configuration:
          !
          frr version 8.2.2
          frr defaults datacenter
          hostname frr
          service integrated-vtysh-config
          !
          interface eth0
           description link to R3-1
           ip address 10.1.13.0/31
          exit 
          interface eth1
           description link to R2-1
           ip address 10.1.12.0/31
          exit 
          interface lo
           description local loopback
           ip address 1.1.1.1/32
          exit