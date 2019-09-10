Installation
=============

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

| Just move to Linux already! Windows can be a more complex installation
| Follow the Docker CE link below to use the containerized version of this class. 

Or you can use `Docker Toolbox <https://docs.docker.com/toolbox/toolbox_install_windows/>`_

WSL
^^^^^

However, for those more adventurous Windows Subsystem for Linux (**WSL**) can work nicely (Thank you Jason)

Ensure that the registry key ``HKLM\CurrentControlSet\Control\Session Manager\Environment _PSLockdownPolicy`` is set to ``0``. If it is not your installation of Docker CE will not be able to start due to Powershell code execution lockdown. 

Install Windows Subsystem for Linux(WSL) `here <https://docs.microsoft.com/en-us/windows/wsl/install-win10>`_ .
Follow this `guide <https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly>`_ to allow you to use WSL Ubuntu as your terminal for Docker.


In your newly configured WSL shell run the following commands: 
 * apt install python3-pip
 * pip3 install ansible

OS packages
^^^^^^^^^^

Suggested list of packages to install:

- Ansible
- Ansible-Lint
- Yamllint
- Jmespath
- Netmiko
- Git


Docker
~~~~~~~~

| Install Docker CE `link <https://docs.docker.com/install/>`_
| Run the Ansible container:

::


    docker pull cwise24/ansiblelab:latest
    docker run --name ansiblec -dit cwise24/ansiblelab


To run the Ansible container's shell:

::

    docker exec -it ansiblec /bin/bash


This will open a shell to the container as the user 'ansible'


.. note:: If you are using the container, the above packages have been installed
