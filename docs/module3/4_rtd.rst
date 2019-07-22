ReadTheDocs 
===========

Sphinx
~~~~~~~

::

     pip3 install sphinx sphinx-autobuild 
     pip3 install sphinxcontrib-nwdiag  { requires extra configs }

First create a new directory to start your project::

    mkdir newproject
    mkdir docs 
    sphinx-quickstart
    sphinx-build -b html docs _build/html

To run the files/builds locally and see how the web links and pages are run

::

    sphinx-autobuild -b html docs/ _build/html 

From here you can navigate to localhost:8000 from your browser


::

    sphinx-build -b html docs/ _build/html

Bullets
~~~~~~

Bullets

* item
- item

::

    Bullets

    * item
    - item

Images/Figures
~~~~~~~~~~~~~

To place images or figures on pages.  I have found it better to use ``.. figure::`` and set a ``:scale:``, this way the image can be opened

.. figure:: imgs/rtd.png
   :scale: 50%
   :align: center

::

    .. figure:: imgs/rtd.png
       :scale: 50%
       :align: center

Code Blocks
~~~~~~~~~~~

Example below, `reference <www.sphinx-doc.org/es/stable/markup/code.html>`_

.. code-block:: html
   :linenos:
   :emphasize-lines: 2-4,6

   <html>
   <head>
   <link rel="stylesheet" type="text/css" href="mystyle.css">
   <title> Title</title>
   </head>
   <body>
   Text
   </body>
   </html>

You use the ``:emphasize-lines:`` directive to highlight a line or lines of code, and the ``:linenos:`` to add line numbers
::

    .. code-block:: html
       :linenos:
       :emphasize-lines: 2-4,6

       <html>
       <title> Title</title>
       <body>
       Text
       </body>
       </html>

Notes_Warnings
~~~~~~~~~~~~~~

.. note:: This is a note
.. seealso:: See also
.. warning:: Warning ``here``
.. todo:: Todo see the next section for extensions and todo_include_todos
.. important:: Important
.. versionadded:: 1.2
.. versionchanged:: 2.1
.. deprecated:: 1.1

::

    .. note:: This is a note
    .. seealso:: See also
    .. warning:: Warning ``here``
    .. todo:: Todo see the next section for extensions and todo_include_todos
    .. important:: Important
    .. versionadded:: 1.2
    .. versionchanged:: 2.1
    .. deprecated:: 1.1 

Network Diagrams
~~~~~~~~~~~~~~~~

Edit the conf.py file to include new extensions::

    extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.doctest',
    'sphinx.ext.todo',
    'sphinx.ext.coverage',
    'sphinx.ext.mathjax',
    'sphinx.ext.ifconfig',
    'sphinx.ext.viewcode',
    'sphinx.ext.graphviz',
    'sphinxcontrib.nwdiag',
    'sphinxcontrib.rackdiag',
    'sphinxcontrib.packetdiag',
     'sphinx.ext.todo'
     ]

     todo_include_todos=True

You must also create a ``requirements.txt`` file and add::

    sphinxcontrib-nwdiag

This now enables
::
    .. nwdiag:: 

        nwdiag {
          network dmz {
              web01;
              web02;
            }
        }

Example Diagrams

.. nwdiag::

    nwdiag {
      network dmz {
          web01;
          web02;
       }
    }

Or highlight groups

::

    .. nwdiag::

       nwdiag{
          network web_tier {
            address = "172.10.1.0/24";
              //define group
                group web {
                  web01 [ address = ".1 "];
                  web02 [address  = ".2"];
               }
            }
        network db {
           address = "172.20.1.0/24";
              web01 [ address = ".1"];
              web02 [ address = ".1"];
              db01 [ address = ".101"];
              db02 [ address = ".102"];
              group db {
                 db01;
                 db02;
                 }
            }
        }


.. nwdiag::

   nwdiag{
      network web_tier {
        address = "172.10.1.0/24";
          //define group
            group web {
              web01 [ address = ".1 "];
              web02 [address  = ".2"];
           }
        }
    network db {
       address = "172.20.1.0/24";
          web01 [ address = ".1"];
          web02 [ address = ".1"];
          db01 [ address = ".101"];
          db02 [ address = ".102"];
          group db {
             db01;
             db02;
             }
        }
    }

Rack El 
^^^^^^

::

    .. rackdiag::

   rackdiag {
       rack {
       //define height of rack
       8U;
        //define description
        description = "Rack A1";
       //define position of items
       1: UPS
       2: UPS
       7: TOR Switch
       8: Fuse Panel [-48 VDC]
      }
      
       rack {
       8U;
       description = "Rack A2";
       1: UPS
       2: UCS
       2: UCS
       3: N/A [4U];
       7: TOR Switch
       8: Fuse Panel [-48 VDC]
       }
   }

.. rackdiag::

   rackdiag {
       rack {
       //define height of rack
       8U;
        //define description
        description = "Rack A1";
       //define position of items
       1: UPS
       2: UPS
       7: TOR Switch
       8: Fuse Panel [-48 VDC]
       }

       rack {
       8U;
       description = "Rack A2";
       1: UPS
       2: UCS
       2: UCS
       3: N/A [4U];
       7: TOR Switch
       8: Fuse Panel [-48 VDC]
       }
   }
Links and References
~~~~~~~~~~~~~~~~~~

`Link <www.google.com>`_ 

::

    `Link <www.google.com>`_


Something quoted [#]_

.. rubric:: Footnote

.. [#] https://www.google.com/

Using the ``[#]`` will auto number the footnotes
::

    Something quoted [#]_

    .. rubric:: Footnote
    
    .. [#] https://www.google.com