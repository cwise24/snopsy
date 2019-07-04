Adhoc
=======

Using Ansible, the host (localhost in this case) is defined and the '-m' switch for *module* (setup module in this example) will return facts about your machine.

::

    ansible localhost -m setup

This returns a large amout of data that would be extremely time consuming to sift through.
Let's filter it using the '-a' switch for *argument*

::

    ansible localhost -m setup -a "filter=ansible_distribution*"
