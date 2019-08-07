Ansible
=======

Debug
---------

This module and setting the verbose level::

    -v
    -vv
    -vvv
    -vvvv  { connection level }

will truly become your best allies as you build playbooks.  You can use debug to print registered variables to screen or even print messages.  Below I'll cover using the ``msg:`` function and 
in a very Pythonic way, concatenating stings into our messages with ``+`` and quotes.

External Vars
------------------

Let's create a new playbook called ``ext.yml`` and use the contents below

``vim ext.yml``

.. code-block:: yaml
   :caption: ext.yml
   :linenos:

   ---
   - hosts: all
     connection: local

     tasks:

     - debug:
         msg: "{{ \"This is var1: \" + var1 + \" 'and also' \" + \"This is var2: \" + var2 }}"

Now we'll run this play against the localhost.  A couple of items to watch when running playbooks against the localhost
* The ``hosts:`` line should have the value of all
* ``connection`` should have the value of local, you can leave this out of the YAML file but you will need to include ``-c local`` in the ansible-playbook command

::

    ansible-playbook -i "localhost," ext.yml -e "var1= 'is var one' var2='is var two'"

Example of connection directive missing from YAML file

::

    ansible-playbook -i "localhost," -c local ext.yml -e "var1='is var one' var2='is var two'"
    
.. figure:: imgs/ext_play.png
   :scale: 50%
   :align: center
   
.. centered:: Fig 1
Limit
-------
One way to reduce all awesome power of automation (to kill everything) is to limit what hosts your playbooks run on.  This can be accomplished with ``limit`` or ``tags``.

Below we run a play on only ``host1`` @ line 1 but @ line 2 we run the playbook against all hosts *except* ``host1``

.. code-block:: text
   :linenos:
   :caption: Limit

    ansible-playbook -i inventory someplay.yml --limit "host1"
    ansible-playbook -i inventory someplay.yml --limit "all:!host1"

Tags
^^^^^

Adding tags to individual plays can greatly help when you only want to test or skip specific plays. 

.. code-block:: yaml
   :linenos:
   :caption: Tags

   ---
   - hosts: all
     connection: local

     tasks:

     - name: Ansible Date Example
       debug:
            var=ansible_date_time.date
       tags:
         - tag1

     - name: Ansible Date Example
       debug:
            var=ansible_date_time.epoch
       tags:
        - tag2


Only show date ``ansible-playbook -i inventory someplay.yml --tags "tag1"``

Only show epoch ``ansible-playbook -i inventory someplay.yml --skip-tags "tag1"``

.. figure:: imgs/date_tag.png
   :scale: 50%
   :align: center

.. centered:: Fig 2

Loops
---------

Conditionals
-----------------

There are too many to cover and that's why we have the internet.  `Ansible Docs <https://docs.ansible.com/ansible/latest/user_guide/playbooks_error_handling.html>`_

My most used:
 * ignore_errors
 * until/retries/delay
 * status_code
 * when
 * fail_when

This play will download the checksum file from F5 if it does not exist within the specified directory (the ``path`` directive)

.. code-block:: yaml 
   :linenos:
   :caption: File Exists Check

   - name: Check if DO rpm exist
     stat:
       path: "{{ roles_d }}/f5_do_install/files/{{ doRPM }}"
     register: do_stat

   - name: Download DO RPM sha256 checksum
     get_url:
       url: https://github.com/F5Networks/f5-declarative-onboarding/raw/master/dist/{{ doSha }}
       dest: "{{ roles_d }}/f5_do_install/files/{{ doSha }}"
     when: do_stat.stat.exists == False

Pause
--------------

Give a process time before running the next inline task

.. code-block:: yaml
   :linenos:
   :caption: Pause

   - pause:
        seconds: 10

When an action fails, prompt user to accept and continue rather than stop/fail.  I use the below when my docker network already exists

.. code-block:: yaml
   :linenos:
   :caption: Pause & Prompt

   - pause:
       prompt: "{{ dnet.results[0].stderr_lines[0] }}.  Press Enter to continue "
     when: dnet.results[0].rc  != 0

Meta
--------

In one of my playbooks I use dynamic inventory to populate my inventory file, meaning I must refresh (inventory files are loaded at runtime)

.. code-block:: yaml
   :linenos:
   :caption: refresh inventory

   - meta: refresh_inventory

Network Automation
---------------------------
No reason for me to repeat, `Ansible Docs <https://docs.ansible.com/ansible/latest/network/getting_started/network_differences.html>`_