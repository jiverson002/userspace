.. highlight:: none

.. note::
  The following article is a adaptation of `Basic Linux Navigation and File Management <https://www.digitalocean.com/community/tutorials/basic-linux-navigation-and-file-management>`_ by `Justin Ellingwood <https://www.digitalocean.com/community/users/jellingwood>`_, available under a `Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License <https://creativecommons.org/licenses/by-nc-sa/4.0/>`_.

File management
===============

You have probably seen some files when using the ``ls`` command in various
directories. In this section, we'll discuss different ways that you can use to
manage those files and the directories in which they are contained. In contrast
to some operating systems, Linux and other Unix-like operating systems rely on
plain text files for vast portions of the system.

``less``
--------
The main way that we view files is with the ``less`` command. This is what we
call a *pager*, because it allows us to scroll through pages of a file. While
the previous commands immediately executed and returned you to the command line,
``less`` is an application that will continue to run and occupy the screen until
you exit.

We will open the ``/etc/services`` file, which is a configuration file that
contains service information that the system knows about::

  $ less /etc/services

The file will be opened in ``less``, allowing you to see the portion of the
document that fits in the area of the terminal window::

  # Network services, Internet style
  #
  # Note that it is presently the policy of IANA to assign a single well-known
  # port number for both TCP and UDP; hence, officially ports have two entries
  # even if the protocol doesn't support UDP operations.
  #
  # Updated from http://www.iana.org/assignments/port-numbers and other
  # sources like http://www.freebsd.org/cgi/cvsweb.cgi/src/etc/services .
  # New ports will be added on request if they have been officially assigned
  # by IANA and used in the real-world or are needed by a debian package.
  # If you need a huge list of used numbers please install the nmap package.

  tcpmux          1/tcp                           # TCP port service multiplexer
  echo            7/tcp
  . . .

To scroll, you can use the up and down arrow keys on your keyboard. To page down
one whole screens-worth of information, you can use either the space bar, the
*Page Down* button on your keyboard, or the ``CTRL-f`` shortcut.

To scroll back up, you can use either the *Page Up* button, or the ``CTRL-b``
keyboard shortcut.

To search for some text in the document, you can type a forward slash ``/``
followed by the search term. For instance, to search for ``mail``, we would
type::

  /mail

This will search forward through the document and stop at the first result. To
get to another result, you can type the lower-case ``n`` key::

  n

To move backwards to the previous result, use a capital ``N`` instead::

  N

When you wish to exit the ``less`` program, you can type ``q`` to quit::

  q

While we focused on the ``less`` tool in this section, there are many other ways
of viewing a file that come in handy in certain circumstances. The ``cat``
command displays a file's contents and returns you to the prompt immediately.
The ``head`` command, by default, shows the first 10 lines of a file. Likewise,
the ``tail`` command shows the last 10 lines by default. These commands display
file contents in a way that is useful for *piping* to other programs. We will
discuss this concept in a future guide.

Feel free to see how these commands display the /etc/services file differently.

``touch``
---------
Many commands and programs can create files. The most basic method of creating a
file is with the ``touch`` command. This will create an empty file using the
name and location specified.

First, we should make sure we are in our home directory, since this is a
location where we have permission to save files. Then, we can create a file
called ``file1`` by typing::

  $ cd
  $ touch file1

Now, if we view the files in our directory, we can see our newly created file::

  $ ls
  file1

If we use this command on an existing file, the command simply updates the data
our filesystem stores on the time when the file was last accessed and modified.
This won’t have much use for us at the moment.

We can also create multiple files at the same time. We can use absolute paths as
well. For instance, if our user account is called ``demo``, we could type::

  $ touch /home/demo/file2 /home/demo/file3
  $ ls
  file1  file2  file3

``mkdir``
---------
Similar to the ``touch`` command, the ``mkdir`` command allows us to create
empty directories.

For instance, to create a directory within our home directory called ``test``,
we could type::

  $ cd
  $ mkdir test

We can make a directory within the ``test`` directory called example by typing::

  $ mkdir test/example

For the above command to work, the ``test`` directory must already exist. To
tell ``mkdir`` that it should create any directories necessary to construct a
given directory path, you can use the ``-p`` option. This allows you to create
nested directories in one step. We can create a directory structure that looks
like ``some/other/directories`` by typing::

  $ mkdir -p some/other/directories

The command will make the ``some`` directory first, then it will create the
other directory inside of that. Finally it will create the directories directory
within those two directories.

``mv``
------
We can move a file to a new location using the ``mv`` command. For instance, we
can move ``file1`` into the test directory by typing::

  $ mv file1 test

For this command, we give all of the items that we wish to move, with the
location to move them at the end. We can move that file *back* to our home
directory by using the special dot reference to refer to our current directory.
We should make sure we’re in our home directory, and then execute the command::

  $ cd
  $ mv test/file1 .

This may seem unintuitive at first, but the ``mv`` command is also used to
rename files and directories. In essence, moving and renaming are both just
adjusting the location and name for an existing item.

So to rename the ``test`` directory to ``testing``, we could type::

  $ mv test testing

.. warning::
  It is important to realize that your Linux system will not prevent you from
  certain destructive actions. If you are renaming a file and choose a name that
  *already* exists, the previous file will be **overwritten** by the file you
  are moving. There is no way to recover the previous file if you accidentally
  overwrite it.

.. _cp:

``cp``
------
With the ``mv`` command, we could move or rename a file or directory, but we
could not duplicate it. The ``cp`` command can make a new copy of an existing
item.

For instance, we can copy ``file3`` to a new file called ``file4``::

  $ cp file3 file4

Unlike a ``mv`` operation, after which ``file3`` would no longer exist, we now
have both ``file3`` and ``file4``.

.. warning::
  As with the ``mv`` command, it is possible to **overwrite** a file if you are
  not careful about the filename you are using as the target of the operation.
  For instance, if ``file4`` already existed in the above example, its content
  would be completely replaced by the content of ``file3``.

In order to copy directories, you must include the ``-r`` option to the command.
This stands for *recursive*, as it copies the directory, plus all of the
directory’s contents. This option is necessary with directories, regardless of
whether the directory is empty.

For instance, to copy the ``some`` directory structure to a new structure called
``again``, we could type::

  $ cp -r some again

Unlike with files, with which an existing destination would lead to an
overwrite, if the target is an *existing directory*, the file or directory is
copied *into* the target::

  $ cp file1 again

This will create a new copy of ``file1`` and place it inside of the ``again``
directory.

``rm``
------
To delete a file, you can use the ``rm`` command.

.. warning::
  Be extremely careful when using any destructive command like ``rm``. There is
  no *undo* command for these actions so it is possible to accidentally destroy
  important files permanently.

To remove a regular file, just pass it to the ``rm`` command::

  $ cd
  $ rm file4

To remove a directory, you will have to use the ``rm`` command again. Like
``cp``, when dealing with directories, you will have to pass the ``-r`` option,
which removes all of the directory's contents recursively, plus the directory
itself.

For instance, to remove the ``again`` directory and everything within it, we can
type::

  $ rm -r again

.. warning::
  Once again, it is worth reiterating that these are permanent actions. Be
  entirely sure that the command you typed is the one that you wish to execute.
