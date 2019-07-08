Merge
~~~~~~


Let's now view our *Master* branch on Gitlab, notice our new file README.md is not there

.. figure:: imgs/masterb.png
   :scale: 60%
   :align: center
.. centered:: Fig 2

We can validate what branch we are on, you should see the asterisk on the *dev* branch
::

    git branch

    *dev
      master

Now using the *checkout* command, switch back to the *master* branch
::

    git checkout master

.. figure:: imgs/checkout_m.png
   :scale: 60%
   :align: center
.. centered:: Fig 3

Now we call the branch we want to merge into our current working branch.  We will merge dev into master.
::

    git merge dev

.. figure:: imgs/merge_d.png
   :scale: 60%
   :align: center
.. centered:: Fig 4

Remember, this is only a merge locally, you must still push these changed to the remote repository at Gitlab
::

    git push

.. Figure:: imgs/push_m.png
   :scale: 60%
   :align: center 
.. centered:: Fig 5

Flipping back over to our Gitlab site

.. figure:: imgs/master_gitlab.png
   :scale: 60%
   :align: center
.. centered:: Fig 6

From here we can click on History to view commits that have been made

.. figure:: imgs/master_gitlab_box.png
   :scale: 60%
   :align: center
.. centered:: Fig 7