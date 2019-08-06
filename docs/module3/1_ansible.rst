Ansible
=======

Debug
---------

External Vars
------------------

Let's create a new playbook called ``ext.yml`` and use the contents below

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