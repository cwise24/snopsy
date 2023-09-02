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

Focusing in on the section we want to extract, we can see we still have a few layers to go:
 - cvssMetric*
 - cvssData
 - version, baseScore

.. code-block:: json 

   {
     "cvssMetricV31": [
       {
         "source": "nvd@nist.gov",
         "type": "Primary",
         "cvssData": {
           "version": "3.1",
           "vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N",
           "attackVector": "NETWORK",
           "attackComplexity": "LOW",
           "privilegesRequired": "NONE",
           "userInteraction": "REQUIRED",
           "scope": "CHANGED",
           "confidentialityImpact": "LOW",
           "integrityImpact": "LOW",
           "availabilityImpact": "NONE",
           "baseScore": 6.1,
           "baseSeverity": "MEDIUM"
         },
         "exploitabilityScore": 2.8,
         "impactScore": 2.7
       }
     ],
     "cvssMetricV2": [
       {
         "source": "nvd@nist.gov",
         "type": "Primary",
         "cvssData": {
           "version": "2.0",
           "vectorString": "AV:N/AC:M/Au:N/C:N/I:P/A:N",
           "accessVector": "NETWORK",
           "accessComplexity": "MEDIUM",
           "authentication": "NONE",
           "confidentialityImpact": "NONE",
           "integrityImpact": "PARTIAL",
           "availabilityImpact": "NONE",
           "baseScore": 4.3
         },
         "baseSeverity": "MEDIUM",
         "exploitabilityScore": 8.6,
         "impactScore": 2.9,
         "acInsufInfo": false,
         "obtainAllPrivilege": false,
         "obtainUserPrivilege": false,
         "obtainOtherPrivilege": false,
         "userInteractionRequired": true
       }
     ]
    }


.. code-block:: bash 

   curl https://raw.githubusercontent.com/cwise24/snopsy/wise_jsonfile/cvss.json | jq '.. | objects | .cvssData?|select(. != null)|{version, baseScore}'