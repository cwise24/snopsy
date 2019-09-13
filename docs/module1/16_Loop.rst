Loop
=====

Now let's make use of our new variable

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 23

   ---
   - hosts: [ios]
     gather_facts: false

     tasks:

     - name: Gather vlan info
       ios_command:
         commands: show vlan
       register: vland

     - set_fact:
          interface: "{{ vland.stdout_lines[0][3].split(\" \") | select('match', '^(Fa|Gi)') | list  }}"

     - name: Show interfaces debug
       debug:
         var: interfaces 

     - name: Get interface config
       tags: shorun
       ios_command:
          commands: show running-config view full | section interface *{{ item }}
       with_items: "{{ interfaces }}"
       register: shorunint

     - name: show interface variable
       tags: showrun
       debug:
         var: shorunint    


We can now loop through all the interfaces in our list *interface* using the Ansible *with_items* module and collect each interfaces configuration.

For an even better experience, check out the `Network Engine command parser <https://galaxy.ansible.com/ansible-network/network-engine>`_