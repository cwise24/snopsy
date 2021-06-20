Playbook
=========

Connect to Lab WiFi
~~~~~~~~~~~~~~~~~~

.. code-block:: text
   :caption: WiFi
      
    SSID:                F5UserGrp_5
    Password:            f5usergrp123!

.. note:: Lab WiFi is only for running plays against the switches, there is **no** internet connectivity


Running a play
~~~~~~~~~~~~~~~

.. code-block:: text
   :caption: inventory file 

   [ios]
   S1 ansible_host=192.168.2.11
   S3 ansible_host=192.168.2.12

   [ios:vars]
   ansible_connection=network_cli
   ansible_network_os=ios
   ansible_ssh_pass="P@55w0rd!"
   ansible_user=f5usergrp

   [junos]
   S2 ansible_host=192.168.2.21

   [junos:vars]
   ansible_connection=network_cli
   ansible_network_os=junos
   ansible_ssh_pass="P@55w0rd!"
   ansible_user=f5usergrp

.. sidebar::  Play Details
 
    This play will log into the group [ios] and get the vlan info from each S1 and S3. The information will be stored in the variable *'vland'*.

.. code-block:: yaml
   :caption: ios.yml

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

This play will log into the group [ios] and get the vlan info from each S1 and S3. The information will be stored in the variable *'vland'*.

.. code-block:: bash
   :caption: Run the play  

   ansible-playbook -i inventory ios.yml


Now that the play has executed, let's look at the logs generated.

.. code-block:: bash
   :caption: Ansible logs

   cat ansible.log

If time permits, you can re-run this play but ``limit`` the play to a single host even though we are using the group name

.. code-block:: bash
   :caption: Limit 

   ansible-playbook -i inventory ios.yml --limit "S1"