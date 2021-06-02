Pull
~~~~
We've worked on our branches, keeping careful not to let things get out of sync.  But what happens with they do? This is where ``pull`` shorthand for ``fetch + merge`` comes into play.
With ``git pull`` we can update our local repository with new commits from the remote repository.

Since we now have a local and remote repository, let's see how pull can help us. If you go to your UI of Gitlab and alter a file (or create a new one), it will not show locally.  To ensure you are in sync with 
the remote repository we must pull

.. figure:: imgs/gitlab_newfile.png
   :scale: 60%
   :align: center
.. centered:: Fig 1


Now run:

::

    git pull origin main 
