Jinja Playbook
==============


| Using *'set_fact'* to build a new variable *'interface'* and using Jinja filters for only the interfaces
| { Lines 13-14 }


.. code-block:: yaml
   :linenos:
   :emphasize-lines: 13,14


     ---
     - hosts: [switches]
       gather_facts: false
      
       tasks:

       - name: Gather vlan info
         ios_command:
           commands: show vlan
         register: vland


       - set_fact:
           interface: "{{ vland.stdout_lines[0][2].split(\"\") | select('match', '^(Fa|Gi)') | list }}"


       - debug:
           var: interface

Now that we have captured only index 2 of our inner list, we can further split the string up by whitespaces and only keeping those strings starting with *Fa* or *Gi* and storing those items into our new list *interface*
