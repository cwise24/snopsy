Parsing with JQ
===============

In these examples, you'll be working with **jq** to extract specific JSON data. For more inforamtion please see the **jq** documentation
located `here`_

.. _here: https://jqlang.github.io/jq/manual/

.. code-block:: json 

    {
      "data": [
        {
          "gid": "001",
          "name": "project_1",
          "data_type": "json"
        },
        {
          "gid": "002",
          "name": "project_2",
          "data_type": "json"
        },
        {
          "gid": "003",
          "name": "project_3",
          "data_type": "json"
        }
      ]
    }

Using the example data above, you can use either of the 2 styles in parsing JSON data noted below.

.. list-table:: JSON Notations
   :align: center
   :header-rows: 1

   * - Notation Name 
     - Example 
     - Output 
   * - dot notation 
     - `$.data[0].gid`
     - 001
   * - bracket notation 
     - `$.['data'][0]['gid']`
     - 001

.. note:: In Ansible, bracket notation is preferred

Both of these examples reference the same value **(001)**. Bracket notation always works. Dot notation can cause problems because
some keys collide with attributes and methods of python dictionaries. Use bracket notation if you use keys which start and end 
with two uderscores (which are reserved for special meaning in python) or are any of the known public attributes. (add link from Ansible)

For this first lab, you'll need to copy the below and create a new file *datacenter.json*. 

.. literalinclude:: ../../datacenter.json
   :caption: datacenter.json
   :language: json

Bracket Notation
++++++++++++++++

Print out the json file starting at the root level object *dataCenter*

.. code-block:: bash 
   
   cat datacenter.json | jq '.["dataCenter"]'

Print out the array of objects under *switch*, notice that you must include the full array of objects in dataCenter as switch is found in 
that array:

.. code-block:: bash 

   cat datacenter.json | jq '.["dataCenter"][]["switch"]'

Another way we could express this, is to return only the first element of the *dataCenter* array:

.. code-block:: bash 

   cat datacenter.json | jq '.["dataCenter"][0]'

.. code-block:: json
   :caption: Example Output

   [
     {
       "id": 1,
       "manufacturer": "Cisco",
       "model": "9600"
     },
     {
       "id": 6,
       "manufacturer": "Cisco",
       "model": "9400"
     },
     {
       "id": 2,
       "manufacturer": "Juniper",
       "model": "4300"
     }
   ]


Create a custom JSON object output based on keys:

.. code-block:: bash
   
   cat datacenter.json | jq '.["dataCenter"][]["switch"][] | {manufacturer,model}'

.. code-block:: json
   :caption: Key Output

   {
       "manufacturer": "Cisco",
       "model": "9600"
     }
     {
       "manufacturer": "Cisco",
       "model": "9400"
     }
     {
       "manufacturer": "Juniper",
       "model": "4300"
    }


Only output switches where the **manufacturer** is *Cisco*:

.. code-block:: bash
  
   cat datacenter.json | jq '.["dataCenter"][]["switch"][] | select(.["manufacturer"] == "Cisco")'

.. code-block:: json 
   :caption: Filter Output

   {
     "id": 1,
     "manufacturer": "Cisco",
     "model": "9600"
   }
   {
     "id": 6,
     "manufacturer": "Cisco",
     "model": "9400"
   }

Output only the model numbers 

.. code-block:: bash 
   
   cat datacenter.json | jq '.["dataCenter"][]["switch"][] | select(.["manufacturer"] == "Cisco")["model"]'

.. code-block:: json
   :caption: Model Only 

   "9600"
   "9400"

Using  variable substitution with **jq** 

 * **\-\-arg** - treats the variable as a string (Example \-\-arg foo 123 will bind $foo to "123")
 * **\-\-argjson** - treats the variable as integer (Example \-\-argjson foo 123, $foo will have the value 123)
 * **-r** - raw output - will directly to standard out; unformated 

.. code-block:: bash 
   :caption: arg

   cat datacenter.json | jq --arg idnum Cisco '.["dataCenter"][]["switch"][] | select(.["manufacturer"] == $idnum)'

.. code-block:: json
   :caption: arg output

   {
     "id": 1,
     "manufacturer": "Cisco",
     "model": "9600"
   }
   {
     "id": 6,
     "manufacturer": "Cisco",
     "model": "9400"
   }

.. code-block:: bash 
   :caption: argjson

   cat datacenter.json | jq --argjson idnum 4 '.["dataCenter"][]["routing"][] | select(.["id"] == $idnum)'

.. code-block:: json 
   :caption: argjson Output

   {
     "id": 4,
     "name": "isis",
     "dynamic": true
   }

Dot Notation
+++++++++++++

.. code-block:: bash
   :caption: dot notation

   cat datacenter.json| jq --arg idnum Cisco '.dataCenter[].switch[] | select(.manufacturer == $idnum)'