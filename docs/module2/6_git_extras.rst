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

.. code-block:: yaml
   :linenos:
   :caption: .pre-commit-config.yaml

   ---
   - repo: https://github.com/ansible/ansible-lint.git
     rev:
     hooks:
        - id: ansible-lint  

Other pre-canned hooks can be found `here <https://github.com/pre-commit/pre-commit-hooks>`_

`Installation <https://pre-commit.com>`_

Self Signed Certificate
------------------------------

In my local lab, I have Gitlab running on a container using a self signed certificate which causes my issues for just local testing.  Within my project folder I change the
``http.sslVerify`` directive to false

.. code-block:: bash
   :caption: Turn ssl validate off

   git config --global http.sslVerify false

Tags
-------
