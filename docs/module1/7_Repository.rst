Repository
===========


Create directories to serve as our local repository

.. code-block:: bash
   :caption: make directory and files
   :linenos:
   :emphasize-lines: 1,2,3


   mkdir ansible_lab
   touch error.yml      { create blank file named error.yml }
   touch noerror.yml
   touch inventory
   touch ios.yml

.. note:: Highlighted lines show files already created in the container


If this was successful then let's add the blank inventory to the repository.  From our project directory ``ansible_lab`` let's initialize this project
::

    git config --global init.defaultBranch main
    git init

Let's configure our git config

::

  
  git config --global user.email "your@email.com"
  git config --global user.name "username"
  git config --list

.. note:: Git config options set the email and username and is used when making commits, you can also see what url you are using

Let's start pushing code from our local repository up to GitLab. You and add individual files or all files. This marks all files ``.`` in the working directory to be added to staging

.. code-block:: bash 
   :caption: Add all Files

    git add .

.. code-block:: bash 
   :caption: Add individual Files

    git add <filename1> <filename2>

Now we can move the staged files to commit.  We use the switch ``-m`` for the commit message and will see this in Gitlab.

::

    git commit -m "initial push"

.. warning:: Make sure you use the switch ``-m`` and add a message
    
Now let's set the remote repository (Gitlab) and sync our local files to the remote main

::

    git push -u git@gitlab.com:<username>/ansible_lab.git main

You can also see what branches you have within your repository:

::

    git branch
    * main 

This shows the branch *'main'* that we just made and that we are in that branch denoted by the ``*``

We can now edit files locally and push them to our remote repository by

::

   git push

.. centered:: **IF moving to Module2, GitOps, click** `here`_ 

.. _here: https://snopsy.readthedocs.io/en/latest/module2/module2.html