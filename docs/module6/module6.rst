Module 6
=========

JSON 
+++++

JavaScript Object Notation or simply called *JSON* is a very simple data structure. The primary compenents of this structure is
"key: value" pairs house in *objects* or *arrays* or **both**.

**Object**

An object in JSON is indicated by ``{}`` and contains key:value pairs.

**Array**

An array in JSON is indicated by ``[]`` and it's elements can be accessed by it's index(elements start at zero).

Let's use an exaple to demonstrate how to access parts of a JSON file. 

.. literalinclude:: ../../indices.json
   :caption: indices.json
   :language: json

.. code-block:: bash
   :caption: Get First Element 

   cat indices.json | jq '.["index"][0]'

In this example, *index* is an object with an array of values. We have accessed the first element of the array **"zero": 0**

.. code-block:: bash
   :caption: Get object letter

   cat indices.json | jq '.["letter"]'

This will produce the value of object **letter** which is **a**

Working JSON data in VIM

Using the ``set paste`` command in VIM

.. figure:: imgs/setpaste.png
   :scale: 50%
   :align: center
.. centered:: Fig 1

What about when you use set paste and the formatting is still a mess?  No worries, use this python command in VIM   
``%!python -m json.tool``

``%`` - References current fiile name   
``!python`` - Run python in shell calling module ``-m`` *json.tool*   

.. figure:: imgs/json_tool.png 
   :scale: 50%
   :align: center
.. centered:: Fig 2
This modules focus is on parsing JSON data.


.. toctree::
   :maxdepth: 1
   :glob:

   1_json
   2_recursion
