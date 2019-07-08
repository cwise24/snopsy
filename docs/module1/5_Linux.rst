Linux
======

.. centered::  Some useful Linux commands

Help - you will find help for any package in the 'man' pages or 'info' pages. Each switch will be described and some examples. 

::

   man <pachage name>
   info <package name>


vim or visual editor

::

  vim <filename> { opens or creates file for editing }
  i             { stands for insert and allows you enter text }
  esc           { escape key, exits editor mode }
  :wq           { write quit; saves and quits vi }
  :q            { quit vi }
  :q!           { quit and do not save }

Directories

::

  pwd            { shows current working directory }
  cd             { change directory }
  cd ..          { change directory up one level }
  cd -           { return to last directory }
  mkdir          { make directory }
  ls             { list contents of a directory; files and folders }
  ls -la         { list contents to include hidden files and permissions }

Files

::

  cat            { print contents of a file }
  touch          { creates a blank file; or updates the timestamp on the file } 
  rm             { remove file }

No in scope for this particular training, but build some aliases. These are located in different places depending on your OS and shell. For the BASH shell in Linux
::

    vim .bashrc

From here you can add an aliases
::

    alias ap='ansible-playbook'
| Now instead of typing 
| ``ansible-playbook -i inventory error.yml`` 
| you can just use the alias 
| ``ap -i inventory error.yml``