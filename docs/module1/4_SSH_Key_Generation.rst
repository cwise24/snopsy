SSH Key Generation
===================


Create Public and Private key pair::


From a terminal screen you can generate a ssh key of type (-t) rsa and length (-b) 2048.

.. code-block:: bash
   :caption: Create SSH Key
   
   ssh-keygen -t rsa -b 2048

::

    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/ansible/.ssh/id_rsa): ``.ssh/ansible_key``
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 


.. figure:: imgs/ssh_key_gen.png
   :scale: 40%
   :align: center

   Fig 1


The above command would produce two files:

 - ansible_key
 - ansible_key.pub

Let's validate our files exist
   .. figure:: imgs/validate_key.png
      :scale: 40%
      :align: center

      Fig 2
