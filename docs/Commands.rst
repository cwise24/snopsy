Commands
======

To run this playbook:

Make suer you are in the working directory for both your play and inventory

::

  cd ansible_lab

  ansible-playbook -i inventory ios.yml


Other switches that can be added:

 * -b for *become*
 * -K *ask for password*
 * -e *pass extra varialbes in*

Extra runs with verbose (for troubleshooting):

::

  ansible-playbook -i inventory ios.yml -v
  ansible-playbook -i inventory ios.yml -vv
  ansible-playbook -i inventory ios.yml -vvv
  ansible-playbook -i inventory ios.yml -vvvv
