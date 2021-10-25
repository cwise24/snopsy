Basics
=====

User details

Who am I?

.. code-block:: bash
   who 
   whoami 
   groups 


Directory details 

.. code-block:: bash 
   pwd 
   ls 
   ls -la 

Working with files

.. code-block:: bash 
   touch 
   mkdir
   rm
   rm -fr 
   cp
   mv
   scp

Permissions

.. code-block:: bash
   chmod
   chown 

Working with bash history and filters

.. code-block:: bash 
   history
   history | grep <keyword>
   less 
   more

You can simply invoke any previous command used shown to you by ``history`` by simply stating ``!<command number>``

``cntrl+r`` is of great help as well to reverse search 

   Is that process running?

   .. code-block:: bash 
      ps -aux | grep <process name>