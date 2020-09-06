Commands
=========


Other switches that can be added:

* -b for *become*
* -K *ask for password*
* -e *pass extra variables in*

  * pass a variable -e "var=one"
  * pass a file of variables -e "@file.yml"

Extra runs with verbose (for troubleshooting):

::

  ansible-playbook -i inventory ios.yml -v
  ansible-playbook -i inventory ios.yml -vv
  ansible-playbook -i inventory ios.yml -vvv
  ansible-playbook -i inventory ios.yml -vvvv
