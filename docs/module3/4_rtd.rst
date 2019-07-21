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
    'sphinxcontrib.packetdiag'
     ]

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