Fetch and Pull
~~~~~~~~~~~

Since we now have a local and remote repository, let's see how fetch and pull can help us. If you go to 
your UI of Gitlab and alter a file (or create a new one), it will not show locally. 
To ensure you are in sync with the remote repository we must *get* those new commits into our local repository.

.. image:: imgs/gitlab_newfile.png
   :scale: 60%
   :align: center
.. centered:: Fig 9

Fetch 
^^^^^

What if you only wanted to see changes made to an upstream, but not have them merged in?  This is where **fetch** comes into play.  This action can really come into
play when we discuss *Forking* a repository. 

We need to check if we have our Gitlab Repository set as the *origin*

::

  git remote -v 

If this comes back with nothing,and most likely will, you will want to add your clone link as the origin. The reason this will need to be done, we created the repository locally on your machine.

::

  git remote add origin git@gitlab.com:username/ansible_lab.git      # use your Gitlab username
  git remote -v                                                      # Check origin is set
  git fetch origin                                                   # Fetch origin updates
  git log origin/main ^main                                          # Show commit differences 

We only see the differences, the new files are not merged into our local project.

Pull 
^^^^

``Pull`` shorthand for ``fetch + merge``  makes keeping our local repository in sync easy. 


::

    git pull origin main 
