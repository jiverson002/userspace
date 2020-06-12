Remote access
=============

``ssh``
-------

.. todo:: Find out if connections can be made to hpc0 from CSB/SJU wifi on
   personal computer.
.. todo:: Add section about common configuration options.

SSH is a program that allows one to log on to a university owned machine from
off-campus using only the terminal.

At CSB/SJU there are two *categories* of machines: those which are only
accessible from a computer connected to the *secure network* and those which are
accessible from any computer connected to the internet. There is only one
"*machine*" that falls into the second category and its name is
``ssh.csbsju.edu``. It turns out that the name actually refers to multiple
physical machines, each of which can be accessed directly, but for our purposes,
that only complicates matters, so we will stick with the name mentioned.

.. todo:: Include graphic illustrating categories of machines at CSB/SJU.

In order to connect to ``ssh.csbsju.edu``, you will need to be on a machine with
an *SSH client* installed. Most versions of Linux as well as MacOS, come with
one installed by default. In either case, you will be running the SSH client
from the terminal. If you are on Windows, I have used `PuTTY
<https://putty.org/>`_ successfully, but cannot say whether or not it is the
best SSH client available. PuTTY is not a terminal application, as a result, the
following instructions will not be usable directly, but should provide the
necessary information to connect successfully. To connect to ``ssh.csbsju.edu``
using a terminal, type::

   $ ssh username@ssh.csbsju.edu

where ``username`` should be replaced by your university username. The first
time that you connect, you will likely be warned about the ``authenticity of
host 'ssh.csbsju.edu'``. **You should indicate ``yes`` to continue
connecting,** after which you should be prompted for you password. This will be
your university password. Assuming no typos in either the command or your
password input, you should not be logged-in to ``ssh.csbsju.edu``. You can
verify this for yourself with the following::

  $ dnsdomainname

which should report ``ad.csbsju.edu``, indicating that the machine that your
terminal is now executing commands on is a machine on the CSB/SJU network. The
machine to which you are now connected is, in most respects, the same as a
machine to which you might connect using Horizon View. As such, anything you
could do from the terminal in Horizon View, you can do in the terminal used to
connect to ``ssh.csbsju.edu``.

Proxy jumping
^^^^^^^^^^^^^

Oftentimes you are connecting to ``ssh.csbsju.edu`` for the sole purpose of
connecting to one of the machines that belongs to the first category of machines
described above, i.e., those which are only accessible from the CSB/SJU secure
network. If that is the case, it can easily done by executing another ssh
command after connecting to ``ssh.csbsju.edu`` to whichever machine is your
final destination. However, with modern SSH clients, there is a shortcut that
collapses both commands into a single one. The technique is called proxy jumping
and the command is as follows::

  $ ssh -J jiverson002@ssh.csbsju.edu jiverson002@hpc0

In this case the final destination is the machine named ``hpc0`` which is not
accessible from outside of the CSB/SJU secure network. So to access it we must
*pass-through* or *proxy jump* by way of ``ssh.csbsju.edu`` first. The above
command is functionally equivalent to::

  $ ssh jiverson002@ssh.csbsju.edu
  ...
  $ ssh jiverson002@hpc0

``scp``
-------

``rsync``
---------
