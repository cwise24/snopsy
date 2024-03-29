Pipeline
======

Pipelines allow for continuous integration, delivery and deployment. Anytime your repository is updated we *may* now run extensive testing to validate changes and produce 
reports (artifacts) proving new changes will work (or not work).

.. image:: imgs/pipeline1.png
   :scale: 60%
   :align: center
.. centered:: Fig 31

CI file
---------------

The ci file determines how the pipeline workflow will run. We can add variables, conditions and select custom container builds for our testing. Some different versions of this file are:

- Jenkinsfile {uses Groovy lang)
- .gitlab-ci.yml {uses YAML}
- azure-pipelines.yml {uses YAML }
- cloudbuild.yaml { uses YAML or JSON }


Building a simple pipeline

Here we will build a simple pipeline to run ansible-lint against our playbook to look for errors and return artifacts. Let's start off this lab with some pre-built ansible playbooks. From the command
line please verify you are in the */home/ansible* directory 

.. code-block:: bash 
   :caption: Working Directory

   pwd
   /home/ansible

.. image:: imgs/pwd.png
   :align: center
   :scale: 60%
.. centered:: Fig 32

Now let's clone the below repository:

``git clone https://gitlab.com/cwise24/snopsy.pipeline``


Once cloned, change directory `cd` into the new directory

::
   
  cd snopsy.pipeline

You must create the the **ci** file using the below code block. Notice the variable **SITE** has the value `site2`. After your pipeline runs we will change this to `site1`, add our 
rules and update the repository.

.. important::  Pay close attention to indentation, YAML is very picky!!

.. code-block:: yaml
   :caption: .gitlab-ci.yml
   :emphasize-lines: 2

   variables:
     SITE: "site2"

   stages:
      - lint 

   Linting:
     stage: lint 
     image: 
       name: cytopia/ansible-lint:latest 
       entrypoint: ["/bin/sh", "-c"]
     before_script:
       - python3 -m pip install --upgrade pip
       - python3 -m pip install ansible-lint[yamllint]
       - ansible-lint --version
     script:
       - echo "${SITE} Report" > site_Report.txt 
       - ansible-lint $SITE.yml >> site_Report.txt 2>&1
     artifacts:
       when: always
       paths:
         - site_Report.txt
       expire_in: 2 days 


It is time to push and create this repository with the new CI file to begin pipeline execution

::

  git add .gitlab-ci.yml 
  git commit -m "start pipeline"
  git push -u git@gitlab.com:<your_gitlab_username>/snopsy.pipeline.git 

Pipeline
-----------

.. role:: blue 

.. role:: green

The figure below shows our new pipeline completed. You can click on the commit hash (:green:`green box`) to view changes and in the :blue:`blue box` you will be able to 
download artifacts (if any) generated.


.. image:: imgs/pipeline2.png
   :scale: 60%
   :align: center

.. centered:: Fig 33

You can also click on Build -> Jobs and the Job number to view the logs from Gitlab Runner (Fig 4)

.. figure:: imgs/pipeline3.png
   :scale: 60%
   :align: center
.. centered:: Fig 34


.. figure:: imgs/pipeline4.png
   :scale: 60%
   :align: center
.. centered:: Fig 35

Let's change our variable SITE to ``site1`` and run the pipeline again


.. code-block:: yaml
   :linenos:
   :caption: .gitlab-ci.yml
   :emphasize-lines: 2,24-28

   variables:
     SITE: "site1"

   stages:
      - lint 

   Linting:
     stage: lint 
     image: 
       name: cytopia/ansible-lint:latest 
       entrypoint: ["/bin/sh", "-c"]
     before_script:
       - python3 -m pip install --upgrade pip
       - python3 -m pip install ansible-lint[yamllint]
       - ansible-lint --version
     script:
       - echo "${SITE} Report" > site_Report.txt
       - ansible-lint $SITE.yml >> site_Report.txt 2>&1
     artifacts:
       when: always
       paths:
         - site_Report.txt
       expire_in: 2 days
     rules:
       - changes:
          - site1.yml
          - site2.yml 
          - .gitlab-ci.yml  

.. important::  Notice the added lines starting at line 24, pipelines will only run if those files have changed

You could now update your README file (or any file, other than those 3)  and the pipeline would no longer execute.

It's now time to push with the updated CI file to begin pipeline execution. 

::

  git add .gitlab-ci.yml 
  git commit -m "site1 pipeline"
  git push

Once this pipeline completes we should see a failure. Navigating back to the Job that just executed we can browse to our report

.. figure:: imgs/pipeline5.png
   :scale: 60%
   :align: center
.. centered:: Fig 36

Now you can view the report:

.. figure:: imgs/pipeline6.png
   :scale: 60%
   :align: center
.. centered:: Fig 37

A helpful link to see all the keywords available in your ci file:

`Gitlab Keyword Link`_

.. _Gitlab Keyword Link: https://docs.gitlab.com/ee/ci/yaml/
