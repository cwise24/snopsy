Pull
~~~~
We've worked on our branches, keeping careful not to let things get out of sync.  But what happens with they do? This is where ``pull`` shorthand for ``fetch + merge`` come into play.
With ``git pull`` we can update our repository (local or on Gitlab) with new commits from the remote repository.

Since we now have a local and remote repository, let's see how pull can help us. If you go to your UI of Gitlab and alter a file, it will not show locally.  To ensure you are in sync with 
the remote repository we must pull
::

    git pull origin main 
