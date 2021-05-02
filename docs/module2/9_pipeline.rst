Pipeline
======

Pipelines allow for continuous integration, delivery and deployment. Anytime your repository is updated we can now run extensive testing to validate changes and produce 
reports (artifacts) proving new changes will work (or not work).

The CI file
---------------

The ci file determines how the pipeline workflow will run. We can add variables, conditions and select custom container builds for our testing. Some different versions of this file are:

 - Jenkinsfile {uses Groovy lang)
 - .gitlab-ci.yml {uses YAML}


Building a simple pipeline

Here we will build a simple pipeline to run ansible-lint against our playbook to look for errors and return artifacts. Let's start off this lab with some pre-built ansible playbooks.

``git clone https://gitlab.com/cwise24/snopsy.pipeline``


Now, let's go into the new repository you just cloned

::
   cd snopsy.pipeline

Now you must create the the **ci** file using the below code block

.. code-block:: yaml
   :linenos:
   :caption: .gitlab-ci.yml 

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
      - python3 -m ansible-lint[yamllint]
      - ansible-lint --version
    script:
      - ansible-lint $SITE.yml | tee site_Report.txt
    artifacts:
      when: always
      paths:
        - site_Report.txt
      expire_in: 2 days 


Now it's time to push and create this repository with the new CI file to begin pipeline execution

::

  git add .gitlab-ci.yml 
  git commit -m "start pipeline"
  git push -u git@gitlab.com:<your_gitlab_username>/snopsy.pipeline.git 