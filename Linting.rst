Linting
=======

.. centered:: *"the process of running a program that will analyze code for potential errors"*

::

    yamllint <filename>.yml


In our example files:

.. literalinclude:: ../error.yml
   :linenos:
   :language: yaml

.. centered:: error.yml

.. literalinclude:: ../noerror.yml
   :linenos:
   :language: yaml

.. centered:: noerror.yml

::

   yamllint error.yml
   yamllint noerror.yml






.. figure:: ../imgs/lint.png
   :scale: 40%
   :align: center

   Fig 2

