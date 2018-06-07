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


.. _Macros:

Macro Substitution
------------------

PyDM has support for macro substitution, which is a way to make a .ui template
for a display, and fill in variables in the template when the display is opened.

The macro system is also a good way to supply data to python-based displays when
launching them from the command line, related display button, or as an embedded
display.

Inserting Macro Variables
^^^^^^^^^^^^^^^^^^^^^^^^^

Anywhere in a .ui file, you can insert a macro of the following form: ``${variable}``.
Note that Qt Designer will only let you use macros in string properties, but you
can insert macros anywhere in a .ui file using a text editor.

Replacing Macro Variables at Launch Time
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When launching a .ui file which contains macro variables, specify values for each
variable using the '-m' flag on the command line:

.. code-block:: bash

  python pydm.py -m '{"variable": "value"}' my_file.ui

Macros in Python-based Displays
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you open a python file and specify macros (via the command line, related display
button, or embedded display widget), the macros will be passed as a dictionary to
the Display class initializer, where they can be accessed and used to generate the
display.

In addition, if the Display class specifies a .ui file to generate its user
interface, macro substitution will occur inside the .ui file.

Macro Behavior at Run Time
^^^^^^^^^^^^^^^^^^^^^^^^^^
PyDM will remember the macros used to launch a display, and re-use them when
navigating with the forward, back, and home buttons. When a new display is opened,
any macros defined on the current window are also passed to the new display.
This lets you cascade macros to child displays.