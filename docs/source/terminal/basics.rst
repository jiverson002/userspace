.. highlight:: none

.. note::
  The following article is an adaptation of `An Introduction to the Linux Terminal <https://www.digitalocean.com/community/tutorials/an-introduction-to-the-linux-terminal>`_ by `Chris Zabriskie <https://www.digitalocean.com/community/users/manicas>`_, available under a `Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License <https://creativecommons.org/licenses/by-nc-sa/4.0/>`_.

Basics
======

This tutorial is intended to teach Linux basics to get new users on their feet.
It covers getting started with the terminal, the Linux command line, and
executing commands. If you are new to Linux, you will want to familiarize
yourself with the terminal, as it is the standard way to interact with a Linux
machine. Using the command line may seem like a daunting task but it is actually
very easy if you start with the basics, and build your skills from there.

Let's get started by going over what a terminal emulator is.

Terminal emulator
-----------------

A terminal emulator is a program that allows the use of the terminal in a
graphical environment. As most people use an OS with a graphical user interface
(GUI) for their day-to-day computer needs, the use of a terminal emulator is a
necessity to become a more efficient Linux user. The efficiency and flexibility
of the terminal is so desirable, that most modern operating systems have some
terminal emulator available for their platform.

Here are some free, commonly-used terminal emulators by operating system:

- **MacOS**: Terminal (default), iTerm 2
- **Windows**: PuTTY
- **Linux**: Terminal, KDE Konsole, XTerm

Each terminal emulator has its own set of features, but all of the listed ones
work great and are easy to use.

Shell
-----

In a Linux system, the shell is a command-line interface that interprets a
user's commands and script files, and tells the server's operating system what
to do with them. There are several shells that are widely used, such as *Bourne
shell* (``sh``), *Bourne-Again shell* (``bash``), and *Z shell* (``zsh``). Each
shell has its own feature set and intricacies, regarding how commands are
interpreted, but they all feature input and output redirection, variables, and
condition-testing, among other things.

This tutorial was written using the *C shell* (``csh``), which is the default
shell for users of the CSB/SJU Linux systems.

Command prompt
--------------

When you first open a terminal emulator in Linux, you will be dropped into the
command prompt, or shell prompt, which is where you can issue commands to the
server. The information that is presented at the command prompt can be
customized by the user, but here is an example of the default CSB/SJU command
prompt::

  [sammy@vplinssh2 5001 ~]$

Here is a breakdown of the composition of the command prompt:

- ``sammy``: The *username* of the current user
- ``vplinssh2``: The *hostname* of the server
- ``5001``: The *event number* of the current history
- ``~``: The *current directory*. In ``bash``, which is the default shell, the
  ``~``, or tilde, is a special character that expands to the path of the
  current user's *home directory*; in this case, it represents ``/home/sammy``
- ``$``: The prompt symbol. This denotes the end of the command prompt, after
  which the user's keyboard input will appear

Here is an example of what the command prompt might look like, if logged in as
``root`` and in the ``/var/log`` directory::

  root@vplinssh2:/var/log#

Note that the symbol that ends the command prompt is a ``#``, which is the
standard prompt symbol for ``root``. In Linux, the ``root`` user is the
*superuser* account, which is a special user account that can perform
system-wide administrative functions---it is an unrestricted user that has
permission to perform any task on a server.

.. note::

  From this point forward and for the entirety of this collection of
  documentation articles, the command prompt will be shortened to a single
  ``$``, except when there is a specific reason to show a more verbose
  command prompt.

Executing commands
------------------

Commands can be issued at the command prompt by specifying the name of an
executable file, which can be a binary program or a script. There are many
standard Linux commands and utilities that are installed with the OS, that allow
you navigate the file system, install and software packages, and configure the
system and applications.

An instance of a running command is known as a **process**. When a command is
executed in the *foreground*, which is the default way that commands are
executed, the user must wait for the process to finish before being returned to
the command prompt, at which point they can continue issuing more commands.

It is important to note that almost everything in Linux is case-sensitive,
including file and directory names, commands, arguments, and options. If
something is not working as expected, double-check the spelling and case of your
commands!

We will run through a few examples that will cover the basics of executing
commands.

Without arguments or options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To execute a command without any arguments or options, simply type in the name
of the command and hit ``RETURN``.

If you run a command like this, it will exhibit its default behavior, which
varies from command to command. For example, if you run the ``cd`` command
without any arguments, you will be returned to your current user's home
directory. The ``ls`` command will print a listing of the current directory's
files and directories. The ``ip`` command without any arguments will print a
message that shows you how to use the ``ip`` command.

Try running the ``ls`` command with no arguments to list the files and
directories in your current directory (there may be none)::

  $ ls

With arguments
^^^^^^^^^^^^^^

Many commands accept *arguments*, or *parameters*, which can affect the behavior
of a command. For example, the most common way to use the ``cd`` command is to
pass it a single argument that specifies which directory to change to. For
example, to change to the ``/usr/bin`` directory, where many standard commands
are installed, you would issue this command::

  $ cd /usr/bin

The ``cd`` component is the command, and the first argument ``/usr/bin`` follows
the command. Note how your command prompt's current path has updated.

If you would like, try running the ``ls`` command to see the files that are in
your new current directory.

With options
^^^^^^^^^^^^

Most commands accept *options*, also known as *flags* or *switches*, that modify
the behavior of the command. As they are special arguments, options follow a
command, and are indicated by a single ``-`` character followed by one or more
options, which are represented by individual upper- or lower-case letters.
Additionally, some options start with ``--``, followed by a single,
multi-character (usually a descriptive word) option.

For a basic example of how options work, let's look at the ``ls`` command. Here
are a couple of common options that come in handy when using ``ls``:

- ``-l``: print a "long listing", which includes extra details such as
  permissions, ownership, file sizes, and timestamps
- ``-a``: list *all* of a directory's files, including hidden ones (that start
  with ``.``)

To use the ``-l`` flag with ``ls``, use this command::

  $ ls -l

Note that the listing includes the same files as before, but with additional
information about each file.

As mentioned earlier, options can often be grouped together. If you want to use
the ``-l`` and ``-a`` option together, you could run ``ls -l -a``, or just
combine them like in this command::

  $ ls -la

Note that the listing includes the hidden ``.`` and ``..`` directories in the listing, because of the ``-a`` option.

With options and arguments
^^^^^^^^^^^^^^^^^^^^^^^^^^

Options and arguments can almost always be combined, when running commands.

For example, you could check the contents of ``/home``, regardless of your
current directory, by running this ``ls`` command::

  $ ls -la /home

``ls`` is the command, ``-la`` are the options, and ``/home`` is the argument
that indicates which file or directory to list. This should print a detailed
listing of the ``/home`` directory, which should contain the home directories of
all of the normal users on the server.

Command help
------------

Often, you may know the command that you want to execute, but may not know
exactly the combination of arguments and options to give the desired results. In
that case, there are a variety of ways to get information about commands in a
Linux system.

``man``
^^^^^^^

*Manual pages*, or *man pages* for short, are the traditional way to get more
information about a command. To view the man page for the command ``ls``, type::

  $ man ls

which will open the *pager application* to display something like::

  LS(1)                            User Commands                           LS(1)

  NAME
         ls - list directory contents

  SYNOPSIS
         ls [OPTION]... [FILE]...

  DESCRIPTION
         List  information  about  the FILEs (the current directory by default).
         Sort entries alphabetically if none of -cftuvSUX nor --sort  is  speci‐
         fied.
  . . .

It is possible to navigate text with the arrow keys, but the pager application
used to display man pages typically provides faster ways of moving around a
document. You can use the ``j`` and ``k`` down and up, respectively.

These direction keys may seem confusing and unintuitive at first, but they were
chosen for a reason. They are in the home-row of a QWERTY keyboard. This means
that a user's hand moves from the resting position significantly less than with
the traditional arrow keys.

``info``
^^^^^^^^

Some commands, particularly those maintained as part of the GNU utilities, offer
man pages, but also include more complete documentation in the form of info
pages.

To view the info page for the command ``ls``, which is a GNU utility, type::

  $ info ls

which will open the info application to display something like::

  File: coreutils.info,  Node: ls invocation,  Next: dir invocation,  Up:
  Directo\
  ry listing

  10.1 'ls': List directory contents
  ==================================

  The 'ls' program lists information about files (of any type, including
  directories).  Options and file arguments can be intermixed arbitrarily,
  as usual.

This is not the standard pager application, but rather a distinct one for
displaying documentation in the texinfo format. As such, it has its own keyboard
navigation.

``--help``
^^^^^^^^^^

Some commands, especially those installed by you, the user, may not have formal
documentation in man or info format. In those cases, there are a few things to
try to get more information about the command, which I typically try in this
order:

#. Try executing the command with each of the following options:

   * ``-h``
   * ``--help``

#. Do a web search for the command
#. Look at the source code to see if any documentation is available there or if
   the code is commented.
