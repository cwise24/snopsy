Configurations
===============

We will associate our newly generated key to be used for Gitlab connections.  Doing it this way, we can separate ssh keys between many sites.

.. code-block:: bash
   :caption: VIM editor

   vim .ssh/config

.. code-block:: bash
   :caption: ssh config file

    Host gitlab.com
      HostName gitlab.com
      IdentityFile ~/.ssh/ansible_key


To exit vim:

::

   press  <esc>

   type   :wq

Now let's get a copy of your public ssh key

::

    cat .ssh/ansible_key.pub 

Copy the output, it should start like below:

::

    ssh-rsa

Now go to `Gitlab <https://gitlab.com/users/sign_in>`_ and create an account, once that is created we will upload your public ssh key to Gitlab (ansible_lab.pub).

 * Click on your icon (top right, then Settings)
 * On the left hand side you should see SSH Keys
 * Paster your public key
    
.. warning:: Make certain you are ``NOT`` about to put your private keys in the cloud

Now we can configure the Ansible config file, but first let's move to our Project Directory

.. code-block:: bash
   :caption: Change Directory

   cd ansible_lab

Fist let's add our Ansible Config file with a few directives:

*Ansible has host key checking enabled by default.*

*If a host is reinstalled and has a different key in ‘known_hosts’, this will result in an error message until corrected. If a host is not initially in ‘known_hosts’ this will result in prompting for confirmation of the key, which results in an interactive experience if using Ansible, from say, cron. You might not want this.*

*If you understand the implications and wish to disable this behavior, 
you can do so by editing* *ansible.cfg* [#]_

.. code-block:: bash
   :caption: VIM editor

   vim ansible.cfg

.. code-block:: bash 
   :linenos:
   :caption: ansible.cfg

    [defaults]
    host_key_checking = False
    inventory = inventory
    log_path = ansible.log
    #vault_password_file = .vault.key

.. note:: Pro-Tip configure an **ansible.cfg** per project



.. rubric:: Footnotes
.. [#] https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html#host-key-checking