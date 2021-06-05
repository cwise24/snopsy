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

.. figure:: imgs/gitlog2.png
   :scale: 60%
   :align: center
.. centered:: Fig 2

.. figure:: imgs/gitlog3.png
   :scale: 60%
   :align: center
.. centered:: Fig 3

.. figure:: imgs/gitreset1.png
   :scale: 60%
   :align: center
.. centered:: Fig 4

.. figure:: imgs/gitlog_reset.png
   :scale: 60%
   :align: center
.. centered:: Fig 5

Revert 
^^^^^