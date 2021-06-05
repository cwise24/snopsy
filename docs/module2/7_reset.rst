Reset 
~~~~~~~


Reset
^^^^^^

Reset is a simple way to "rollback" to a previous commit. We will create a local repository and practice this.

.. code ::
   
   mkdir  resetlab
   cd resetlab
   git init
   vim example
   This is line one 
   :wq 
   git add 
   git commit 
   git log --oneline

.. figure:: imgs/gitlog.png
   :scale: 60%
   :align: center
.. centered:: Fig 1

Now let's edit the file **example** and add another line

.. code ::
   
   vim example

Add this line:
   This is line two

   And now let's save ``:wq`` our file with the new changes, then add to staging and commit
.. code ::

   :wq 
   git add example 
   git commit -m "two"
   git log --oneline

.. figure:: imgs/gitlog2.png
   :scale: 60%
   :align: center
.. centered:: Fig 2

Now let's edit the file again and add another line

.. code ::
   
   vim example

Add this line:
   This is line three

And now let's save ``:wq`` our file with the new changes, then add to staging and commit
.. code ::

   :wq 
   git add example 
   git commit -m "three"
   git log --oneline 

.. figure:: imgs/gitlog3.png
   :scale: 60%
   :align: center
.. centered:: Fig 3

Now let's rollback to our second commit. Using **Fig 4** as a reference we will issue the command ``git reset --hard <hash>`` with the hash of our second commit

.. figure:: imgs/gitreset1.png
   :scale: 60%
   :align: center
.. centered:: Fig 4

Now the git HEAD has been moved to our second commit and we have completed a *rollback* of our file. 

.. figure:: imgs/gitlog_reset.png
   :scale: 60%
   :align: center
.. centered:: Fig 5

Running the command ``cat example`` we can now see the third line has been removed

Revert 
^^^^^