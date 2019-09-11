Playbook
=========

.. code-block:: text
   :caption: inventory file 

   [ios]
   S1 ansible_host=192.168.2.11
   S3 ansible_host=192.168.2.12

   [ios:vars]
   ansible_connection=network_cli
   ansible_network_os=ios
   ansible_ssh_pass="YourSecretHere"
   ansible_user=f5usergrp

   [junos]
   S2 ansible_host=192.168.2.21

   [junos:vars]
   ansible_connection=network_cli
   ansible_network_os=junos
   ansible_ssh_pass="YourSecretHere"
   ansible_user=f5usergrp

.. sidebar::  Play Details
 
    This play will log into the group [switches] and get the vlan info from each mdf1 and mdf2. The information will be stored in the variable *'vland'*.

.. code-block:: yaml
   :linenos:
   :caption: playbook1.yml

   ---
   - hosts: [ios]
     gather_facts: no

     tasks:

     - name: Play to run
       ios_command:
          commands: show vlan
       register: vland

     - debug:
         var: vland

This play will log into the group [switches] and get the vlan info from each mdf1 and mdf2. The information will be stored in the variable *'vland'*.
