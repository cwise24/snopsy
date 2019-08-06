Ansible
=======

Debug
---------

This module and setting the verbose level::

    -v
    -vv
    -vvv
    -vvvv

will truly become your best allies as you build playbooks.  You can use debug to print registered variables to screen or even print messages.  Below I'll cover using the ``msg:`` function and 
in a very Pythonic way, concatenating stings into our messages with ``+`` and quotes.

External Vars
------------------

Let's create a new playbook called ``ext.yml`` and use the contents below

``vim ext.yml``

.. code-block:: yaml
   :caption: Playbook
   :linenos:

   ---
   - hosts: all
     connection: local

     tasks:

     - debug:
         msg: "{{ \"This is var1: \" + var1 + \" 'and also' \" + \"This is var2: \" + var2 }}"

::

    ansible-playbook -i "localhost," ext.yml -e "var1= 'is var one' var2='is var two'"
    
.. figure:: imgs/ext_play.png
   :scale: 50%
   :align: center
   
.. centered:: Fig
Limit
-------

Tags
-------

Loops
---------

Conditionals
-----------------
Meta
--------