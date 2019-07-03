Installation
=======

MacOS
~~~~~~~
Install `homebrew <https://howtogeek.com/211541/homebrew-for-os-x-easily-installs-desktop-apps-and-terminal-utilities/>`_

 - brew install python3
 - pip3 install ansible

Linux
~~~~~~
Install python3-pip (apt/yum)

- pip3 install ansible

Windows
~~~~~~~~

| Just move to linux already, Windows is
| Follow the Docker CE link below

Docker
~~~~~~~~

| Install Docker CE `link <https://docs.docker.com/install/>`_
| Run the Ansible container:

::


    docker pull cwise24/ansiblelab:latest
    docker run -p 2222:22 --name ansiblec -dit ansiblelab


To run the Ansible container's shell:

::

    docker exec -it ansiblec /bin/sh


This will open a shell to the container as the user 'ansible'

Suggested list of packages to install:

 - Ansible
 - Yamllint
 - Jmespath
 - Netmiko
 - git

.. note:: If you are using the container, the above packages have been installed
