JSON
=====

JSON data structure
Objects and Arrays
Working JSON data in VIM

Using the ``set paste`` command in VIM

.. figure:: imgs/setpaste.png
   :scale: 50%
   :align: center
.. centered:: Fig 1

What about when you use set paste and the formatting is still a mess?  No worries, use this python command in VIM   
``%!python -m json.tool``

.. figure:: imgs/json_tool.png 
   :scale: 50%
   :align: center
.. centered:: Fig 2


Parsing
--------

In these examples, you'll be working with **jq** to extract specific JSON data.

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

`` cat datacenter.json | jq \'.[datacenter]\' ``

`` cat datacenter.json | jq '.[datacenter][]["switch"]' ``

Create a custom JSON object output based on keys:

`` cat datacenter.json | jq '.[datacenter][]["switch"] | {manufacturer,model}' ``



`` cat datacenter.json | jq '.[datacenter][]["switch"][] | select(.["manufacturer == "Cisco")' ``