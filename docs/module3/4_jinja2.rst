Jinja2
======




Delimiters

  *  ``{%....%}`` are for statements
  *  ``{{....}}`` are expressions used to print to template output
  *  ``{#....#}`` are for comments which are not included in the template output
  *  ``#....##`` are used as line statements

Let's create a new playbook named **jinja.yml** and use the code below. One additional Jinja function we'll use is **joiner**. *Joiner* allows the passing of list items
and all but the last item will get the delimiter added to it. In our example that's the `,` .

.. code-block:: yaml
   :caption: jinja.yml 

   ---
   - hosts: all
     gather_facts: False
     connection: local 

     vars:
       var1: itema,itemb,itemc,itemd

     tasks:

     - name: Set Fact from vars (build a list)
       ansible.builtin.set_fact:
         jinja: "{{ var1.split(',') }}"

     - name: Echo jinja List 
       ansible.builtin.debug:
         var: jinja 

     - name: Echo jinja loop 
       ansible.builtin.debug:
         msg: "{% set comma=joiner(',') %} {% for item in jinja %} {{comma()}} {{ item }} {% endfor %}"

To run this example:

.. code-block:: bash

   ansible-playbook -i "localhost," jinja.yml 

An example of a F5 deployment using a j2 (Jinja) template

.. code-block:: yaml 
   :caption: Example Ansible task
   :linenos:

   - name: Push Declaration
     uri:
       url: "https://{{ hostvar[groups['adc'][0]]['ansible_host']/mgmt/shared/appsvcs/declare"
       method: POST
       body: "{{ lookup('template', 'exampleFile.j2', split_lines=False) }}"
       body_format: json
       headers:
         Content-type: application/json
         X-F5-Auth-Token: "{{ Auth.tok.json.token.token }}"
       status_code: 200
       timeout: 300
       validate_certs: no
     delegate_to: localhost



This example (thanks to Forrest Crenshaw @F5 on `Linklight <https://ansible.github.io/workshops/exercises/ansible_f5/>`_ Exercise 3) is used to loop through all our pool members from inventory and add them to the Virtual Server

::

    "members": [
            {
                "servicePort": {{ item.svc_port }},
                "serverAddresses": [
                {% set comma = joiner(",") %}
                {% for mem in item.pool_members %}
                  {{comma()}} "{{ hostvars[mem]['ansible_host'] }}"
                {% endfor %}
                ]

You can run Jinja2 functions on an online parser `here <http://jinja.quantprogramming.com/>`_ .

In this example you can use the online parser to run your tempate code and supply the associated YAML values.

.. code-block:: json
   :caption: Jinja Template

    {
      "allowed-ip": [
        {% set comma = joiner(",") %}
        {% for acl in acls %}{{ comma() }}
          {
            "name": "{{ acl.acl_name }}",
            "config": {
                "ipv4": {
                    "address": "{{ acl.acl_ip }}",
                    "prefix-length": "{{ acl.acl_prefixLength }}",
                    "port": {{ acl.acl_port }}
                }
            }
          }{% endfor %}
      ]
    }

.. code-block:: yaml
   :caption: Values(YAML)

   acls:
     - acl_name: test
       acl_ip: 10.1.10.11
       acl_prefixLength: 24
       acl_port: 22
     - acl_name: test
       acl_ip: 10.1.10.12
       acl_prefixLength: 24
       acl_port: 22
