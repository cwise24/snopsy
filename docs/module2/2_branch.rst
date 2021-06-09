Branch 
~~~~~~~

Let's first take a definition straight from git [#]_ itself

.. centered:: "*Branching means you diverge from the main line of development and
                continue to do work without messing with that main line.*"

With *branches*, we can introduce (or reject) new changes into our production branch. 

A NetOps example of this would be to clone the repository housing the running router configs. A feature branch could be created to test and develop an improved BGP process. Once designed 
and tested, this new BGP process can be merged into the production branch. And since this is all in Git, we have the necessary documentation:

*  Who did this?
*  What problem did it solve (commit message)
*  When did this happen?
*  Who approved it?

We can also use compare the differences within Git, making very easy to review.

..  centered::  Commands we will use for Branch

::

    git branch                      { show the working branch }
    git checkout <branch name>      { command to switch our working branch }
    git checkout -b <new branch>    { creates a new branch }
    git checkout -d <branch name>   { deletes branch name }

From module 1 we created our main branch (default branch), let's verify that using:

.. code:: bash 

    git branch

.. important:: **DO NOT MAKE CHANGES IN THE MAIN BRANCH, HARD LESSON LEARNED HERE**

Now we will create a new branch *'dev'*, this is where we will make our changes and merge them back into the mainline *main* branch.

::

    git checkout -b dev 

This will create a branch locally, we'll now add a README.md to our *dev* branch.

.. sidebar::  VIM Cheat Sheet


    | i       { for insert }
    | esc   { to exit for saving }
    | :wq   { write & quit }

.. code:: bash 

    vim README.md

And now insert some text

::

    This is a readme file


Once that file is created and saved, let's set our up-stream dev branch and commit our file

.. code:: bash

    git add README.md
    git commit -m "new readme"
    git push --set-upstream git@gitlab.com:<username>/ansible_lab.git dev

Now we can verify our new file and branch are present from out Gitlab page

.. figure::  imgs/devb.png
   :scale: 60%
   :align: center

.. centered:: Fig 2
   
.. rubric:: Footnotes
..  [#] https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell