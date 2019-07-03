Repository
=======


Create directories to server as our local repository

 * mkdir ansible_roles
 * mkdir ansible_lab
 * cd ansible_lab       { change directory to ansible_lab }
 * touch error.yml      { create blank file named error.yml }
 * touch noerror.yml
 * touch inventory
 * touch ios.yml
 * git init             { initialize git }


Time to test our ssh key with Gitlab:

::

    ssh -T git@gitlab.com

If this was successful then let's add the blank inventory to the repository

Let's configure our git config

::

  
  git config --global user.email "your@email.com"
  
  git config --global user.name "username"


This marks all files '.' in the working directory to be added to stagging

::

    git add .

Now we can move the stagged files to commit.  We use the *'-m'* for the commit message and will see this in Gitlab.

::

    git commit -m "initial push"

.. warning:: Make sure you use the switch -m and add a message
    
Now let's set the remote repository (Gitlab) and sync our local files to the remote master

::

    git push --set-upstream git@gitlab.com:<username>/ansible_lab.git master

You can also see what branches you have within your repository:

::

    git branch
    * master

This shows the branch *'master'* that we just made and that we are in that branch denoted by the '*'

We can now edit files locally and push them to our remote repository by

::

   git push
