Configurations
=======

For Mac you'll want to associate this new key for use (automatically), otherwise you will have to use the `-i` switch every time. 

::

    vi .ssh/config
    IdentityFile ~/.ssh/ansible_key


To exit vim:

::

    esc

    :wq

Now we can configure the Ansible config file:

::

    vi .ansible.cfg

    [defaults]
    Host_key_checking = False
    Log_path = ~/ansible_lab
    #vault_password_file = .vault.key

Now let's get a copy of your public ssh key

::

    cat .ssh/ansible_lab.pub 

Copy the output, it should start like below:

::

    ssh-rsa ASADSADGSSNTY+/z7j84it5gmfogi


Now go to `Gitlab <https://gitlab.com/users/sign_in>`_ and create an account, once that is created upload your public ssh key to Gitlab (ansible_lab.pub)  Click on your icon (top right, then Settings).  On the left hand side you should see SSH Keys

.. warning:: Make certain you are not about to put your private keys in the cloud
