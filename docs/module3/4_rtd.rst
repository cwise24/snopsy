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

Code Blocks
^^^^^^^^^^

Example below, `reference <www.sphinx-doc.org/es/stable/markup/code.html>`_

.. code-block:: html
   :linenos:
   :emphasize-lines: 2

   <html>
   <title> Title</title>
   <body>
   Text
   </body>
   </html>

::

    .. code-block:: html
       :linenos:
       :emphasize-lines: 2

       <html>
       <title> Title</title>
       <body>
       Text
       </body>
       </html>

Notes_Warnings
^^^^^^^^^^^^^^^^

.. note:: This is a note
.. seealso:: See also
.. warning:: Warning ``here``
.. todo:: Todo 
.. important:: Important
.. versionadded:: Upgrade to 1.X
.. versionchanged:: Newer Version is available
.. deprecated:: Since version 2.X 

::

    .. note:: This is a note
    .. seealso:: See also
    .. warning:: Warning ``here``
    .. todo:: Todo 
    .. important:: Important
    .. versionadded:: Upgrade to 1.X
    .. versionchanged:: Newer Version is available
    .. deprecated:: Since version 2.X 

Network Diagrams
^^^^^^^^^^^^^^

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
       //define height of rack
       8U;

       //define position of items
       1: UPS
       2: UPS
       7: TOR Switch
       8: Fuse Panel
   }

.. rackdiag::

   rackdiag {
       //define height of rack
       8U;

       //define position of items
       1: UPS
       2: UPS
       7: TOR Switch
       8: Fuse Panel
   }