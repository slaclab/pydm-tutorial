Important Concepts
==================

PyDM Launcher
-------------

PyDM provides a launcher that makes it easier for users to quickly run UI files as well as code based screens.
The launcher is responsible for setting up the Python logging module but it mainly parses the command line parameters
and send them to the instantiated PyDMApplication.

The Launcher is available for Linux, OSX and Windows and it can be called using the command line:

.. code-block:: bash

   pydm

This will result in the PyDM Main Window being displayed.

.. figure:: /_static/intro/main_window.png
   :scale: 75 %
   :align: center
   :alt: PyDM Main Window

.. note::
   It is not mandatory for you to use the PyDM Launcher to run your screen but keep in mind that not using it means that
   you will need to handle command line arguments, logging setup and the instantiation of the PyDMApplication at your own
   code.

.. _Channel:

Channels
--------

**Channels** are the bridge between PyDM Widgets and the different Data Plugins provided.

Usually channels are specified on the following format:

.. code-block:: python

   <protocol>://<channel address>

Where ``protocol`` is a unique identifier for a given Data Plugin used with PyDM and ``channel address`` will vary
depending on the data plugin and every plugin should have in its documentation the expected format for users.

Here are some examples:

.. code-block:: python

   ca://MTEST:Float

Where ``ca`` means the Channel Access plugin and ``MTEST:Float`` is the PV name in this case.

Another example is the Archiver Appliance plugin in which channels are specified as:

.. code-block:: python

   archiver://pv=test:pv:123&donotchunk

In which everything at the ``channel address`` section is the same as what is sent to the ``retrieval`` part of the Archiver
as specified at the **Retrieving data using other tools** section of the `Archiver Appliance User Guide <https://slacmshankar.github.io/epicsarchiver_docs/userguide.html>`_

.. _DataArchitecture:

Data Architecture
-----------------

* PyDM widgets are data-source agnostic, and communicate with the PyDM Application through Qt signals and slots.

* The PyDM application routes data between the widgets and data source plugins.

* A data source plugin speaks to a particular source of data (EPICS, HTTP, databases, etc).

* This system makes it possible to mix-and-match different data sources within the same display, using the same widget set.

.. figure:: /_static/intro/architecture.png
   :scale: 25 %
   :align: center
   :alt: PyDM Data Plugin Architecture