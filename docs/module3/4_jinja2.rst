Jinja2
======




Delimiters

  *  ``{%....%}`` are for statements
  *  ``{{....}}`` are expressions used to print to template output
  *  ``{#....#}`` are for comments which are not included in the template output
  *  ``#....##`` are used as line statements

Let's create a new playbook named **jinja.yml** and use the code below.

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
       set_fact:
         jinja: "{{ var1.split(',') }}"

     - name: Echo jinja List 
       debug:
         var: jinja 

     - name: Echo jinja loop 
       debug:
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
