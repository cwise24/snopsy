Recursion
==========

Say you'd want to search a returned json response for certain values, however sometimes the key values are named differently. All the work we've done so far means you'd
need to write custom filters parse the content twice. What if you could "flatten" out the json data. Let's do this with Recursive Decent **..**.

We'll use a real world example for this lab. Using the NIST National Vulnerability Database (NVD) I have pulled down the json output for *CVE-2022-34305*. The file is large
but can be viewed from the `repository`_

.. _repository: https://raw.githubusercontent.com/cwise24/snopsy/wise_jsonfile/cvss.json


The task is, we need to sort the scores of the CVE, **HOWEVER** if you viewed the file we have two scoring metrics
- cvssMetricsV2
- cvssMetricsV31 

We'll want both base scores along with what is the corresponding metric version.

Let's first display the file with only recursion 

.. code-block:: bash 

    curl https://raw.githubusercontent.com/cwise24/snopsy/wise_jsonfile/cvss.json | jq ..

You should now see the json output has been *flattened* by one level.

.. code-block:: json

   {
     "resultsPerPage": 1,
     "startIndex": 0, 
     "totalResults": 1, 
     "format": "NVD_CVE", 
     "version": "2.0", 
     "Vulnerabilities": [
     ....
     ]

.. code-block:: json 

   1
   0 
   1 
   "NVD_CVE" 
   "2.0" 
   [
   ....
   ]