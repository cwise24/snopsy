Introduction
============

This lab is meant to make you familiar with BGP and some of its basic concepts. We'll be covering:

* FRR

* BGP

  * iBGP

  * eBGP

* Peering

* Attributes

This lab will be run on `FRR`_. FRR is capable of running all major routing modules and commands are very similar to Cisco/Arista.

What is Border Gateway Protocol (BGP)?

Border Gateway Protocol (BGP) is the routing protocol that makes the internet work. Think of it as the postal service of the internet, 
responsible for finding the most efficient routes for data to travel from its source to its destination.

  How it Works: Routing Between Networks
The internet is not a single, monolithic network. Instead, it's a collection of thousands of smaller, independent networks called Autonomous Systems (AS). 
These can be large internet service providers (ISPs), universities, or large corporations. Each AS manages its own internal routing.

BGP comes into play when data needs to travel between these different Autonomous Systems. It's the protocol that enables these distinct networks 
to exchange routing information, essentially telling each other which IP addresses they control and what paths are available to reach them.


Key Concepts Made Simple
Path Vector Protocol: BGP is a "path vector" protocol. This means that when a network advertises a route to another network, it includes the 
entire path of Autonomous Systems that the route traverses. This path information is crucial for preventing routing loops and for making informed 
routing decisions.


Policy-Based Routing: Unlike many internal routing protocols that simply look for the shortest path, BGP allows network administrators to implement 
routing policies. These policies can consider various factors beyond just the number of network hops, such as cost, network congestion, and 
business relationships between providers. This flexibility is essential for the commercial and political realities of the internet.


We will reference two key types of BGP through this lab:

External BGP (eBGP)[20]: This is the primary function of BGP, used for communication and routing between different Autonomous Systems.
Internal BGP (iBGP)[200]: This is used within a single Autonomous System to ensure that all routers within that network have a consistent view of 
the external routes learned via eBGP. iBGP comes with some caveats, and we will cover them in the lab.


BGP messages
- Open
- Update
- Keepalive
- Notification

Attributes image

.. _FRR: https://frrouting.org/


.. list-table:: Title
   :widths: 25 25 50
   :header-rows: 1

   * - Feature
     - eBGP (External BGP)
     - iBGP (Internal BGP)
   * - Purpose
     - Communication between different Autonomous Systems.
     - Communication within a single Autonomous System.
   * - Peer Connection
     - Peers are in different AS numbers.
     - Peers are in the same AS number.
   * - Administrative Distance
     - The default administrative distance for eBGP is 20.
     - The default administrative distance for iBGP is 200.
   * - Next-Hop Behavior
     - The next-hop address is updated to the IP address of the advertising router.
     - The next-hop address is not changed by default.
   * - Loop Prevention
     - Uses the AS_PATH attribute. A router will not accept a route if it sees its own AS number in the path.
     - Uses a split-horizon rule. A route learned from an iBGP peer cannot be advertised to another iBGP peer.
   * - Topology
     - Typically a direct connection between peers.
     - Requires a full mesh of connections between all iBGP routers or the use of route reflectors or `confederation`_.

.. _confederation: https://www.rfc-editor.org/rfc/rfc1966
     
     