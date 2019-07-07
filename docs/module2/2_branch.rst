Branch 
~~~~~~~

Let's first take a definition straight from [#]_ git itself

::

    "Branching means you diverge from the main line of development and continue to do work without messing with that main line."

What does this mean to a NetOps person.  We aren't building applications, but we are enabling them.  As a NetOps person we can use Git to track network infrastructure configurations and catch unwanted drift.
We can define how Vlans, routes or any simple task gets built.  By building our Ansible playbook in Git, we can version control it, even allow others to contribute (in a feature branch) in which we decide to allow the new additions or reject them.  It even allows 
users to file issues they've expericed and use to fix those.

..  centered::  Commands we will use for Branch

::

    git branch
    git checkout <branch name>
    git checkout -b <new branch>


..  [#] https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell