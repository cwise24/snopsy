BGP LAB 1
=========

Now that the basics are taken care of, let's peer the rest of the routers.

Peering
+++++++

Time to start peering the reamining routers, start to distribute routes and test reachability.

Since R1-1 and R2-1 are peered and in the same Autonomous System (AS), we will only need to peer the remaining router R3-1 to R1-1. This too will be an iBGP
peer. Rembering that iBGP needs full mesh or route reflector, in this lab we will use route reflector. 

.. NOTE:: 
   iBGP does not share routes it learns from other iBGP peers. This is a route loop prevention mechanism and why we need full mesh or route reflector.

