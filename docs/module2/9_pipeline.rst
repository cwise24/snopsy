Pipeline
~~~~~~~

Pipeline

what is a pipeline, uses etc

CI file

What is a ci file, links examples etc


Building a simple pipeline

Herre we will build a simple pipeline to run ansible-lint against our playbook to look for errors and return artifacts. Let's start off this lab with some pre-built ansible playbooks.

``git clone https://gitlab.com/cwise24/snopsy.pipeline``

.. code-block:: yaml
   :lineos:
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
git push -u git@gitlab.com:<gitlab_username>/snopsy_pipeline.git