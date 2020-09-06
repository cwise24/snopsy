Jinja2
======




Delimiters

  *  {%....%} are for statements
  *  {{....}} are expressions used to print to template output
  *  {#....#} are for comments which are not included in the template output
  *  #....## are used as line statements

Let's create a new playbook named **jinja.yml** and use the code below.

.. code-block:: yaml
   :caption: jinja.yml 
   :linenos:

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


Within a j2 template

.. code-block:: yaml 
   :caption: Example Ansible task
   :linenos:

   - name: Push Declaration
     uri:
       url: "https://{{ hostvar[groups['adc'][0]]['ansible_host']/mgmt/shared/appsvcs/declare"
       method: POST
       body: "{{ lookup('template', 'exampleFile.j2', split_lines=False) }}"



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

.. code-block:: yaml
   :caption: File contents to variable
   
    app_cert: "{{ lookup('file', '/home/user/roles/role_certs/files/as3.lab.local.crt') }}"