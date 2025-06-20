Introduction
============

This lab is meant to make you familiar with BGP and some of its basic concepts. We'll be covering:

* FRR

* BGP

  * iBGP

  * eBGP

* BGP Peering

* BGP Attributes

This lab will be run on `FRR`_. FRR is capable of running all major routing modules and commands are very similar to Cisco/Arista.

What is Border Gateway Protocol (BGP)?
+++++++++++++++++++++++++++++++++++++++

Border Gateway Protocol (BGP) is the routing protocol that makes the internet work. Think of it as the postal service of the internet, 
responsible for finding the most efficient routes for data to travel from its source to its destination.

How it Works: Routing Between Networks

The internet is not a single, monolithic network. Instead, it's a collection of thousands of smaller, independent networks called Autonomous Systems (AS). 
These can be large internet service providers (ISPs), universities, or large corporations. Each AS manages its own internal routing.

BGP comes into play when data needs to travel between these different Autonomous Systems. It's the protocol that enables these distinct networks 
to exchange routing information, essentially telling each other which IP addresses they control and what paths are available to reach them.

BGP is a "path vector" protocol. This means that when a network advertises a route to another network, it includes the 
entire path of Autonomous Systems that the route traverses. This path information is crucial for preventing routing loops and for making informed 
routing decisions.

We will reference two key types of BGP through this lab:

- External BGP (*eBGP*)[**20**]: This is the primary function of BGP, used for communication and routing between different Autonomous Systems.

- Internal BGP (*iBGP*)[**200**]: This is used within a single Autonomous System to ensure that all routers within that network have a consistent view of the external routes learned via eBGP. iBGP comes with some caveats, and we will cover them in the lab.

What are those numbers in brackets?

Those numbers represent the default `administrative distance`_ for each type of BGP. Each routing protocol has a default administrative distance, the lower the 
number the more trusted the route is. Lets say we have the same route from two protocols, like OSPF and BGP, since OSPF has an administrative distance of 110
and BGP has an administrative distance of 20, the BGP route will be preferred.

.. _administrative distance: https://en.wikipedia.org/wiki/Administrative_distance


Features of each BGP type:
++++++++++++++++++++++++++

.. list-table:: **BGP Features**
   :widths: 20 35 35
   :header-rows: 1
   :align: left

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


Once you begin to configure BGP, you will see the following states process on your router. These states will progress based on the BGP messages exchanged between the routers.

.. list-table:: BGP States 
   :widths: 20 20
   :header-rows: 1

   * - State
     - Description
   * - Idle
     - Router is waiting for a start event (i.e. new neighbor or reset of established session)
   * - Connect
     - The BGP peer is in the process of connecting to the remote peer.
   * - Active
     - The BGP peer is in the process of establishing a connection to the remote peer. If success it will transition to OpenSent.
   * - OpenSent
     - The BGP peer has sent an Open message to the remote peer.
   * - OpenConfirm
     - The BGP peer has received an Open message from the remote peer.
   * - Established
     - The BGP peer is fully established and exchanging routes. 

Once your BGP session is established, you will see the following BGP messages exchanged between the routers.

BGP messages:

- **Open** - contains AS number, BGP version, and BGP options(hold timers) and BGP Router ID.

- **Update** - Route are updated or withdrawn in this message. Includes AS-Path and Next-Hop.

- **Keepalive** - as the name implies, it's a keepalive message to make certain the neighbor is still alive.

- **Notification** - sent when a BGP error is detected such as hold timer expiration or invalid message. BGP session is terminated. BGP table is cleared of entries from neighbor.

Attributes image

Now that BGP peering is established, we need to understand how BGP selects the best path, and what attributes are used to determine the best path.

.. list-table:: BGP Path Selection
   :widths: 20 35 35
   :header-rows: 1
  
   * - Priority
     - Attribute 
     - Preference
   * - 1
     - Weight
     - Highest Value 
   * - 2
     - Local Preference
     - Highest Value 
   * - 3
     - Originate
     - Local
   * - 4
     - AS Path
     - Shortest Path
   * - 5
     - Origin
     - Lowest Value(i<e<?)
   * - 6
     - Multi Exit Discriminator (MED)
     - Lowest Value
   * - 7
     - eBGP Path over iBGP Path
     - Prefer eBGP
   * - 8
     - IGP Cost
     - Lowest IGP Metric
   * - 9
     - Oldest Path
     - Recieved First
   * - 10
     - Router ID
     - Lowest Value
   * - 11
     - Neighbor IP address
     - Lowest Neighbor IP 

.. Note::
  
   Of the path selection attributes, AS-Path, Origin, and Next-Hop are considered **Well Known Mandatory** attributes. Without these attributes, the BGP will send a notification message.

.. _FRR: https://frrouting.org/