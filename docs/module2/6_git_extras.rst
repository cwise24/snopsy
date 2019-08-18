Git Extras
=========

Pre-Commit
-----------------
 
I had spent (aka wasted) time on using Jenkins to run linting tools on my code after a push triggered my pipeline.  As I was spending time trying to ``groovy`` a simple for loop I stumbled across
an article that made total sense, Why do this?? Why have your CI tool import a project to find problems, solve them **before** commit. I agree, so below we'll cover the setup of pre-commit

 After you have initialzed your local repo, within the ``.git`` folder you will see  ``.git/hooks`` and if we look there we will see the list of examples.

 Here is a link to the pre-commit site, but I will cover how I did it locally.

 .. code-block:: bash
    :caption: Install pre-commit
     
     pip3 install pre-commit

From your project folder you can now run 
``pre-commit install``
This will install the git hooks scripts needed

.. figure:: imgs/pre-commit.png
   :scale: 50%
   :align: center
   
   Fig 17
   

Next you'll have to add the ``.pre-commit-config.yaml`` file to your repository

.. code-block:: yaml
   :linenos:
   :caption: .pre-commit-config.yaml

   ---
   - repo: https://github.com/ansible/ansible-lint.git
     rev: v0.9
     hooks:
        - id: ansible-lint  

Other pre-canned hooks can be found `here <https://pre-commit.com/hooks.html>`_

Pre-commit site for `installation <https://pre-commit.com>`_  instructions

Self Signed Certificate
------------------------------

In my local lab, I have Gitlab running on a container using a self signed certificate which causes my issues for just local testing.  Within my project folder I change the
``http.sslVerify`` directive to false

.. code-block:: bash
   :caption: Turn ssl validate off

   git config --global http.sslVerify false

Tags
-------

Used to mark specific points in a repository's history.

.. code-block:: bash 
   :caption: git tag  

   git tag -a "v1.2" -m "version 1.2"

.. code-block:: bash
   :caption: list git tags

   git tag -l 