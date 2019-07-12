Pull
~~~~
We've worked on our branches, keeping careful not to let things get out of sync.  But what happens with they do? This is where ``pull`` shorthand for ``fetch + merge`` come into play.
With ``git pull`` we can update our local repository with new commits from the remote repository.

Let's say you have a remote repository, 

::

    git remote -v
    
    git pull git@gitlab.com:<user>/<repo>.git
    git remote add origin git@gitlab.com:<user>/<repo>.git
    git remote -v
      origin	git@gitlab.com:<user>/<repo>t.git (fetch)
      origin	git@gitlab.com:<user>/<repo>.git (push)

    git push origin master
