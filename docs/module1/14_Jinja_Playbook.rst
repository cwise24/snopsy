Jinja Playbook
===============

What is Jinja2?

*"Jinja2 is a modern day templating language for Python developers. It was made after Django’s template. 
It is used to create HTML, XML or other markup formats that are returned to the user via an HTTP request."*[#]_

| Using ``set_fact`` to build a new variable ``interface`` and using Jinja filters for only the interfaces
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
           interface: "{{ vland.stdout_lines[0][2].split(\" \") | select('match', '^(Fa|Gi)') | list }}"


       - debug:
           var: interface

Now that we have captured only index 2 of our inner list, we can further split the string up by white spaces and only keeping those strings starting with *Fa* or *Gi* and storing those items into our new list *interface*


.. rubric:: Footnotes
.. [#] https://codeburst.io/jinja-2-explained-in-5-minutes-88548486834e