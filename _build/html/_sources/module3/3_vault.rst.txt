Vault
=====

We will use ansible vault to encrypt all of our sensitive information AND to make sure our playbooks stay automated. I'm not saying this is the only way but this is how I 
keep my playbooks automated without having to enter any credentials.

From the ``.ansible.cfg`` in Module 1, we'll now uncomment the ``vault_password_file`` directive

.. code-block:: text
   :emphasize-lines: 6

    vim .ansible.cfg

    [defaults]
    Host_key_checking = False
    Log_path = ~/ansible_lab
    vault_password_file = .vault.key