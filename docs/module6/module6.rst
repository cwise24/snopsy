Module 6
=========

JSON 
+++++

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
