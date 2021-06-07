Git
~~~~

Git -

created by Linus Torvalds in 2005 for development of the Linux kernel [#f1]_

::  

    man git 

    GIT(1)                                    Git Manual                                GIT(1)
    
      NAME
        git -  the stupid content tracker

"is a distributed version-control system for tracking changes in source code during software development. 
It is designed for coordinating work among programmers, but it can be used to track changes in any set of files. 
Its goals include speed, data integrity, and support for distributed, non-linear workflows."  [#f1]_

What does this mean to a NetOps person.  We aren't building applications, but we are enabling them.  As a NetOps person we can use Git to track network infrastructure configurations and catch unwanted drift.
We can define how Vlans, routes or any simple task gets built.  By building our Ansible playbook in Git, we can version control it, even allow others to contribute (in a feature branch) in which we decide to allow the new additions or reject them.  It even allows 
users to file issues they've experienced and enable a means to fix those.

| **TL;DR** 
| A nice way to manage chaos across distributed teams

So here are the basics

Local 
* Local working directory/repository on your machine

Remote 
* The remote repository in this case Gitlab 

.. figure:: imgs/gitflow.png
   :scale: 50%
   :align: center

git add
 * Marks edited files for staging
 * Additional edits will not be staged without git add

git commit
 * Commit staged changes to local repository
 * The ‘-m’ provides important message about the change

git push
 * Push committed files to remote repository (i.e. Gitlab)

git pull
 * Pull files from Remote repository
 * Example - Project owner makes changes to files, in order to have the lastest copy you ‘pull’ from the Remote repo to update you local files

.. rubric::  Footnotes

.. [#f1] https://en.wikipedia.org/wiki/Git