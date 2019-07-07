SSH Key Generation
===================


Create Public and Private key pair::


From a terminal screen you can generate a ssh key of type (-t) rsa and length (-b) 2048.

    `ssh-keygen -t rsa -b 2048`


   .. figure:: imgs/ssh_key_gen.png
      :align: center

      Fig 1

..


The above command would produce two files:

 - ansible_key
 - ansible_key.pub
