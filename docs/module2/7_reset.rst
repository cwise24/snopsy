Rolling Back
~~~~~~~~~~~

How do we rollback to a previous commit? Well there are a couple of options. Let's cover them.

Revert 
^^^^^

Git Revert allows the undoing of a previous commit, but it also keeps all the commit history by only adding to the commit history.  

.. note:: This is the preferred method to use.

Let's create a file named **example** then make the following edits and commits

.. code ::
   
   mkdir  resetlab
   cd resetlab
   git init
   vim example

.. code ::

   vim example

``This is line one``

.. code ::

   :wq
   git add example 
   git commit -m "one"

.. code ::
   
   vim example

Add this line to the example file:

``This is line two``

   And now let's save our file with the new changes, then add to staging and commit

.. code ::

   :wq 
   git add example 
   git commit -m "two"
   git log --oneline

.. code ::
   
   vim example

``This is line three``

And now let's save our file with the new changes, then add to staging and commit

.. code ::

   :wq 
   git add example 
   git commit -m "three"
   git log --oneline 

Next you will need to push this file to our repository with our 3 commits

.. code:: bash 

   git push -u git@gitlab.com:<username>/resetlab.git main
   

We will now select the commit we wish to remove, in this example it's commit three.

.. image:: imgs/gitrevert1.png
   :scale: 60%
   :align: center
.. centered:: Fig 1

Once you hit enter, you will be prompted for a revert message. Once you've added the revert message and saved ``:wq`` let's review the git log 

.. code ::

  git log --oneline


Here we can see that instead of dropping off the thrid commit using ``reset``, with ``revert`` it actually adds an extra commit and keeps previous commits. This is why revert is the preferred 
rollback method.

.. image:: imgs/gitlog_revert.png
   :align: center
.. centered:: Fig 7

Now you can push your reverted file

.. code ::

   git push

.. note:: Please use the :ref:`Cleanup` section below if you want to do the Reset lab

Reset
^^^^^

Reset is a simple way to "rollback" to a previous commit. The down side of reset, it will remove all the commit history back to the restoral point.
We will create a local repository and practice this.

.. code ::
   
   mkdir  resetlab
   cd resetlab
   git init
   vim example

Add this line to the newly created file

``This is line one`` 

.. code ::

   :wq 
   git add 
   git commit 
   git log --oneline

.. image:: imgs/gitlog.png
   :align: center
.. centered:: Fig 1

Now let's edit the file **example** and add another line

.. code ::
   
   vim example

Add this line to the example file:

``This is line two``

   And now let's save our file with the new changes, then add to staging and commit

.. code ::

   :wq 
   git add example 
   git commit -m "two"
   git log --oneline

.. image:: imgs/gitlog2.png
   :align: center
.. centered:: Fig 2

Now let's edit the file again and add another line

.. code ::
   
   vim example

``This is line three``

And now let's save our file with the new changes, then add to staging and commit
.. code ::

   :wq 
   git add example 
   git commit -m "three"
   git log --oneline 

.. image:: imgs/gitlog3.png
   :align: center
.. centered:: Fig 3

Now let's rollback to our second commit. Using **Fig 4** as a reference we will issue the command ``git reset --hard <hash>`` with the hash of our second commit

.. image:: imgs/gitreset1.png
   :align: center
.. centered:: Fig 4

Now the git HEAD has been moved to our second commit and we have completed a *rollback* of our file. As you can see though, all commits prior are now removed.

.. image:: imgs/gitlog_reset.png
   :align: center
.. centered:: Fig 5

Running the command ``cat example`` we can now see the third line has been removed.

In order to push this change to our remote, you must enable **Allow Force Push** as Gitlab will set this branch as protected, but again this is not a best practice method.

.. code:: bash
   
   :caption: Force
   
   git push -f 

Cleanup
^^^^^^

If you want to remove a remote repository to do the reset section here are the steps

.. code ::
    
    rm -fr .git 
    rm -fr example 

And delete the repository from Gitlab

Go to Settings and then General

.. figure:: imgs/deletegitrepo1.png
   :scale: 50%
   :align: center
.. centered:: Fig 8

Scroll to bottom and find Advanced and click Expand

.. figure:: imgs/deletegitrepo2.png
   :scale: 50%
   :align: center
.. centered:: Fig 9

Now click Delete project

.. figure:: imgs/deletegitrepo3.png
   :scale: 50%
   :align: center
.. centered:: Fig 10