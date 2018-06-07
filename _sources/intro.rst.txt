Setting up the Environment
==========================

Virtual Machine
---------------

We provide a virtual machine disk that can be used to follow the tutorial section.

You can download the disk using this `Link <https://drive.google.com/file/d/1ZrcDf2oMj_PwVFFQN-y1-ZwR_bp_5aur/view?usp=sharing>`_.

After downloading it, extract the ``.tar.gz`` file and create a new Virtual Machine at the virtualization client of your preference.
We used `Oracle VirtualBox <https://www.virtualbox.org/wiki/Downloads>`_ to create this machine and it is available for Windows, OS X and Linux hosts.

Useful Virtual Machine Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

User Account
++++++++++++
========    ========
Username    Password
========    ========
user        tutorial
========    ========

Python Environment
++++++++++++++++++

On this machine we are using Miniconda to handle our Python environment and dependencies.
To have access to the environmnet please do:

.. code-block:: bash

    source activate tutorial

Simulated EPICS IOCs
++++++++++++++++++++

This machine comes with simulated motors and cameras.
The IOCs can be started through their launcher scripts available at:

.. code-block:: bash

    cd ~/tutorial/iocs_launcher

    # For the AreaDetector (cameras) simulation use
    ./simDetector

    # For the simulated motor axis use
    ./simMotor

    # For the linking IOC
    ./simLinker

For AreaDetector (cameras):

-  The prefix for the PVs is ``13SIM1:`` so we have: ``13SIM1:cam1`` as well as ``13SIM1:cam2`` available.

For Motor Axis:

- The prexif for the PVs is ``IOC:`` so we have: ``IOC:m1 .. IOC:m8``


Creating your own environment
-----------------------------

- You will need Python 2.7 or newer (Python 3.6 is the recommended version since in the future Python 2.7 will be deprecated).

   **If the version is less than 2.7, please update it to meet the minimal requirements.**

- You will also need Qt 5.7 or newer and PyQt 5.7 or newer available and pyqtgraph >= 0.10.0 for the plot widgets.


- Different Data Plugins require different dependencies. E.g:

   - When using the Channel Access data plugin with PyEpics you will also need:
      - PyEpics >= 3.2.7
      - Epics Base >= 3.14.12

   - When using the Archiver Appliance data plugin you will also need:
      - requests >= 1.1.0

For up-to-date dependency list as well as detailed installation instructions please
refer to the `PyDM Documentation Website <http://slaclab.github.io/pydm/>`_

.. note::

    If you are a `conda <https://conda.io/docs/user-guide/install/download.html>`_ user,
    you can create a conda environment and easily run PyDM with the following:

    .. code-block:: bash

       conda create -n pydm-env "python >= 3.6" pydm -c pydm-tag
       source activate pydm-env

Checking dependencies version
-----------------------------

From a Terminal window, check your Python version doing the following:

.. code-block:: bash

   # For Python 2.7.x
   python --version

   # For Python 3.x
   python3 --version

In order to check your Qt and PyQt version, open a python or ipython shell and run the following code:

.. code-block:: python

   from PyQt5.QtCore import QT_VERSION_STR
   from PyQt5.Qt import PYQT_VERSION_STR
   print("Qt Version: ", QT_VERSION_STR)
   # Output should be something like... Qt Version:  5.9.4
   print("PyQt Version: ", PYQT_VERSION_STR)
   # Output should be something like... PyQt Version:  5.9.2


