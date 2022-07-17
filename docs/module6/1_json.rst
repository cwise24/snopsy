JSON
=====

JSON data structure

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

2 styles used in parsing JSON data:
* dot notation       `$.data[0].gid`         response: 001
* bracket notation   `$.['data'][0]['gid']`  response: 001

.. note:: In Ansible, bracket notation is preferred