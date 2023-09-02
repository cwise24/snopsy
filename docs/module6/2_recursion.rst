Recursion
==========

Say you'd want to search a returned json response for certain values, however sometimes the key values are named differently. All the work we've done so far means you'd
need to write custom filters parse the content twice. What if you could "flatten" out the json data. Let's do this with Recursive Decent **..**.

We'll use a real world example for this lab. Using the NIST National Vulnerability Database (NVD) I have pulled down the json output for *CVE-2022-34305*. The file is large
but can be viewed from the `repository`_

.. _repository: https://raw.githubusercontent.com/cwise24/snopsy/wise_jsonfile/cvss.json

.. code-block:: json
   :caption: json file

   {
        "cars":
   }


Let's first display the file with only recursion 

.. code-block:: bash 

    cat file.json | jq ..

You should see something like 

.. code-block:: json 
   :caption: output 
   
   "blah": "", 