Vault
=====

We will use ansible vault to encrypt all of our sensitive information AND to make sure our playbooks stay automated. I'm not saying this is the only way but this is how I 
keep my playbooks automated without having to enter any credentials.

Let's create a new *master* ansible-vault key, this will be stored as a hiden file within your home directory

::

    vim .vault.key
    
    s3cr3T1

From the ``.ansible.cfg`` in Module 1, we'll now uncomment the ``vault_password_file`` directive

.. code-block:: text
   :emphasize-lines: 6

    vim .ansible.cfg

    [defaults]
    Host_key_checking = False
    Log_path = ~/ansible_lab
    vault_password_file = .vault.key

Now you may create new files by using ``ansible-vault create <filename>``, this will create the new file and open vim. This new file will use the passphrase from our previouly generated file
``.vault.key``

Another way to encrypt a new file is ``ansible-vault create <filename>`` or an existing file ``ansible-vault encrypt <filename>`` and you will be prompted for the new passphrase 

.. note:: If you configure the ``vault_password_file`` this will automatically be used as the passphrase