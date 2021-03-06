How to install python-rtmidi from source on Windows
===================================================

These instruction are only working for installing ``python-rtmidi`` from source
using Python 2.7 or Python 3.3 in the 32-bit versions (you can run these on
Windows 64-bit versions with no problems).

Please follow all the steps below in the exact order.


Installing required software
----------------------------

You probably need adminstrator rights for some or all of the following steps.

#. Install Python 2.7.x or Python 3.3 (32-bit!) from
   http://python.org/download/ to the default location (i.e. ``C:\Python27`` or
   ``C:\Python33``).

#. (Optional: add ``C:\Python27`` and ``C:\Python27\Scripts`` resp.
   ``C:\Python33`` and ``C:\Python33\Scripts`` to your PATH.)

#. Install setuptools_ (the following commands assume that you are using
   Python 2.7. If you are using Python 3.3, use ``C:\Python33`` in place of
   ``C:Python27`` in the commands given).

   - Download ez_setup.py_.

   - Open a command line and run it::

        > C:\Python27\python ez_setup.py

#. Install pip_::

        > C:\Python27\Scripts\easy_install pip

#. Install virtualenv_::

        > C:\Python27\Scripts\pip install virtualenv

#. Install Visual Studio Express (Microsoft Visual C++).

   - For Python 2.7 (and 3.2) install Visual Studio Express **2008**.

   - For Python 3.3 install Visual Studio Express **2010**.

   You'll have to use an internet search to find a current download link for
   the installer or an ISO with the whole distribution.

   Please make sure that you install the correct Visual Studio Express edition
   for the Python version you are using as detailed above. You can install
   Visual Studio Express 2008 *and* 2010 at the same time.

   After installation, use Windows Update to get any pending security updates
   and fixes.


Setting up a virtual environment
--------------------------------

#. Open a command line and run::

        > C:\Python27\Scripts\virtualenv rtmidi
        > rtmidi\Scripts\activate

#. Install Cython (still in the same command line window)::

        > pip install Cython


Download & unpack python-rtmidi source
--------------------------------------

Get the latest python-rtmidi distribution as a Zip archive from
https://pypi.python.org/pypi/python-rtmidi, unpack it somewhere, and, in the
command line window you opened above, change into ``python-rtmidi`` directory,
which you unpacked, e.g.::

    > pip install --no-install -d . "python-rtmidi>=0.4"
    > cd python-rtmidi

If you use a non-english version of Windows XP (or possibly Vista), adapt the
values of ``WINLIB_DIR`` and ``WININC_DIR`` at the top of file ``setup.py`` to
your system to point to the location of ``WinMM.lib`` and the Microsoft SDK
headers.


Build & install python-rtmidi
-----------------------------

Just run the usual setup command from within the source directory with the
active virtual environment, i.e. from still the same command line window::

    > python setup.py install

This might also download some version of setuptools in the process again. You
can also update setuptools within your virtual environment beforhand to the
latest version with::

    > pip install -U setuptools


Verify your installation
------------------------

Change out of the ``python-rtmidi`` source directory (important!) and run::

    > cd ..
    > python
    >>> import rtmidi
    >>> rtmidi.API_WINDOWS_MM in rtmidi.get_compiled_api()
    True
    >>> midiout = rtmidi.MidiOut()
    >>> midiout.get_ports()
    [u'Microsoft GS Wavetable Synth']

If you have any other MIDI outputs (hardware MIDI interfaces, MIDI Yoke etc.)
active, they should be listed by ``get_ports()`` as well.

*That's it, congratulations!*


Notes
-----

Windows Kernel Streaming support in RtMidi has been removed (it was broken
anyway) and consequently in ``python-rtmidi`` as well.

Compiling with MinGW also does not work out-of-the-box yet. If you have any
useful hints, please let the author know.


.. _ez_setup.py: https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py
.. _pip: https://pypi.python.org/pypi/pip
.. _setuptools: https://pypi.python.org/pypi/setuptools
.. _virtualenv: https://pypi.python.org/pypi/virtualenv
