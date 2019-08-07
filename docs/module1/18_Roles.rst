Roles
======

Definition:
"Roles are a robust feature of Ansible that facilitate reuse and further promote modularization of configuration, but Ansible roles are often overlooked in lieu of straightforward playbooks for the task at hand. The good news is that Ansible roles are simple to get set up and allow for complexity when necessary" [#]_

With roles we can define how things get built, what actions need to be taken after (i.e. restart web-server after config file is updated) and make all of this modular to be consumed by others.


Let's use Ansible Galaxy to build our file structure for our role ``ansible_role``

::

    ansible-galaxy init ansible_role

.. figure:: imgs/galaxy_init.png
   :scale: 60%
   :align: center
.. centered:: Fig 8

Ansible Galaxy has now made our directory ``ansible_role`` and the complete folder structure as shown below

.. figure:: imgs/galaxy_tree.png
   :scale: 60%
   :align: center
.. centered:: Fig 9

Folder breakdown
^^^^^^^^^^^^^^

Tasks
 * main.yml - this is file will contain our plays; this serves as the same ``tasks`` section of our playbook

Vars
 * main.yml - Variables you may wish to include in the role

Handlers
 * main.yml - Here is where we'll define actions to take. Example, your task changes a config file for Apache and you must now restart the Apache service.  Your task would 
 notify a handler to perform that action for you 

.. code-block:: yaml
   :linenos:
   :caption: Task/main.yml

   notify: restart-apache
   become: yes

.. code-block:: yaml
   :linenos:
   :caption: Handler/main.yml

   - name: restart-apache 
     systemd:
       name: httpd
       state: restarted
       enabled: yes
     become: yes


Meta
  * main.yml - Add dependencies here for Ansible-Galaxy roles you want to include

.. rubric:: Footnote

.. [#] https://linuxacademy.com/blog/red-hat/ansible-roles-explained/
