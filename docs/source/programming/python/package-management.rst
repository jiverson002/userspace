Package management
==================

.. _virtual-environments:

Virtual environments
--------------------

.. todo:: pip can install packages in a users home directory with ``pip install
   packagename --user``, should this be preferred and we ignore virtual
   environments?

Virtual environments are useful for many reasons. Most relevant for us is their
ability manage Python packages independent of packages installed system-wide.
For example, maybe there is a Python package that you would like to use, but has
not been installed by the system administrator. In that case, Python virtual
environments give you a mechanism to install the package without system
administrator intervention.

Setting up a Python virtual environment is easy and need only be done once
(possibly once per project, depending on your needs). In the following
demonstration, I will be working from a directory called ``sandbox`` which is in
my home directory. Inside of that directory, I have created another directory
called ``new-project`` which will represent the new Python project that I will
be creating. In this case, I will be installing the Python virtual environment
within that project directory.

.. code-block:: none

  $ pwd
  .../sandbox
  $ ls
  new-project
  $ cd new-project
  $ ls
  $ python --version
  Python 2.7.5

The last command that was executed was checking the version of Python installed
on the machine. In this case, the Python version is **2.7**. Since Python 2.7 is
no longer officially supported and has been deprecated for quite some time, we
will strongly prefer a more recent version of Python on which to base our
virtual environment. On a university computer, it turns out that a more recent
version of Python is installed and can be used as so::

  $ python3 --version
  Python 3.6.8

This will be much more suitable for any development that we plan to do in
Python. So, at this point we can create the virtual environment::

  $ python3 -m venv env

where ``env`` is the "*name*" of the virtual environment. This name is
arbitrary. Assuming no errors were reported, you should see something like::

  $ ls
  env

At this point, the virtual environment has been *created*, but in order to use
it, it must be *activated*. Activating a virtual environment is something you
must do each time that you enter the terminal and plan to use the virtual
environment, so you will want to commit the necessary command to memory. The
command to activate a virtual environment will depend on the type of shell that
your terminal is running. To find that out issue the following command::

  $ echo $SHELL
  /bin/tcsh

On a university machine you should get the same output that I did. This means
that the shell that we are using is a derivative of the `C
shell <https://en.wikipedia.org/wiki/C_shell>`_. As a result, the correct
command to activate our virtual environment is::

  $ source env/bin/activate.csh
  [env] $

Executing this command should report no errors. If that is the case, then you
have successfully activate your new Python virtual environment. You should
notice that the command prompt is now decorated with the name of your virtual
environment.

At this point, everything you do using the Python interpreter will be relative
to this virtual environment. Test this for yourself by checking the version of
Python like so::

  [env] $ python --version
  Python 3.6.8

Notice that although the command was ``python`` and not ``python3``, the version
is 3.6.8 rather than 2.7.5. To *deactivate* a virtual environment and return to
the system-wide Python environment, execute the following command::

  [env] $ deactivate
  $

Package installation
--------------------

Since using :ref:`Python virtual environments<virtual-environments>` is strongly
recommended, the following discussion assumes their use. However, apart from the
command prompt, the following instructions should work regardless of your using
them or not.

To install Python packages one can use the program ``pip``, which is installed
alongside Python and will already be available in your virtual environment.
For example, to install the `NumPy <https://numpy.org/>`_ package to do
some numerical computing in Python, execute the command::

  [env] $ pip install numpy
