Jinja2
======




Delimiters

  *  {%....%} are for statements
  *  {{....}} are expressions used to print to template output
  *  {#....#} are for comments which are not included in the template output
  *  #....## are used as line statements

Within a j2 template

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