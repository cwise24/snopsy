Loop
=====

Now let's make use of our new variable

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 17, 18

   ---
   - hosts: [switches]
     gather_facts: false

     tasks:

     - name: Gather vlan info
       ios_command:
         commands: show vlan
       register: vland

     - set_fact:
          interface: "{{ vland.stdout_lines[0][2].split(\"\") | select('match', '^(Fa|Gi) | list  }}"

     - name: Get interface config
       ios_command:
          commands: show running-config interface {{ item }}
       with_items: "{{ interface }}"
       register: shorunint

We can now loop through all the interfaces in our list *interface* using the Ansible *with_items* module and collect each interfaces configuration.
