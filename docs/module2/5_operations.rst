Operations
~~~~~~~~~~
Clone
^^^^^
Cloning creates a local repository (on your computer) from your repository say on Gitlab or Github. You cannot contribut back to the source repository (if it is not yours)  unless you are added 
as an collaborator.  For this module, we will only clone a forked repository so we may have a local working copy.


Fork
^^^^
When you fork a repository, you make a copy of the source repository and are able to freely make changes without affecting the source repository. There will be a connection between the source
repository and yours so you may contribute back.  You may also pull updates from the source repository into your fork.


::

    git remote -v


Origin
---------
Your own repository (i.e. git@gitlab.com:your_username/your_reposity.git )
To set an origin (and origin is just a name space, could easy be just your name)
``git remote add origin git@gitlab.com:<username>/<repo>.git``

Upstream
-------------
The source repository you're forked from (i.e. git@gitlab.com:someonelse_username/their_reposity.git  )
