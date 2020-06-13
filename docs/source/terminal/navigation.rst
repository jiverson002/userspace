.. highlight:: none

.. note::
  The following article is a adaptation of `Basic Linux Navigation and File Management <https://www.digitalocean.com/community/tutorials/basic-linux-navigation-and-file-management>`_ by `Justin Ellingwood <https://www.digitalocean.com/community/users/jellingwood>`_, available under a `Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License <https://creativecommons.org/licenses/by-nc-sa/4.0/>`_.

Navigation
==========

If you do not have much experience working with Linux systems, you may be
overwhelmed by the prospect of controlling an operating system from the command
line. In this guide, we will attempt to get you up to speed with the basics.

This guide will not cover everything you need to know to effectively use a Linux
system. However, it should give you a good jumping-off point for future
exploration. This guide will give you the bare minimum you need to know before
moving on to other guides.

``pwd``
-------

When you log into your server, you are typically dropped into your user
account's *home directory*. A home directory is a directory set aside for your
user to store files and create directories. It is the location in the filesystem
where you have full dominion.

To find out where your home directory is in relationship to the rest of the
filesystem, you can use the ``pwd`` command. This command displays the directory
that we are currently in::

  $ pwd

You should get back some information that looks like this::

  /home/demo

The home directory is named after the user account, so the above example is what
the value would be if you were logged into the server with an account called
``demo``. This directory is within a directory called ``/home``, which is itself
within the top-level directory, which is called *root* but represented by a
single slash ``/``.

``ls``
------

Now that you know how to display the directory that you are in, we can show you
how to look at the contents of a directory.

Currently, your home directory that we saw above does not have much to see, so
we will go to another, more populated directory to explore. Type the following
in your terminal to move to this directory (we will explain the details of
moving directories in the next section). Afterward, we'll use ``pwd`` to confirm
that we successfully moved::

  $ cd /usr/share
  $ pwd
  /usr/share

Now that we are in a new directory, let's look at what's inside. To do this, we
can use the ls command::

  $ ls
  adduser            groff                          pam-configs
  applications       grub                           perl
  apport             grub-gfxpayload-lists          perl5
  apps               hal                            pixmaps
  apt                i18n                           pkgconfig
  aptitude           icons                          polkit-1
  apt-xapian-index   info                           popularity-contest
  . . .

As you can see, there are *many* items in this directory. We can add some
optional flags to the command to modify the default behavior. For instance, to
list all of the contents in an extended form, we can use the ``-l`` flag (for
"long" output)::

  $ ls -l
  total 440
  drwxr-xr-x   2 root root  4096 Apr 17  2014 adduser
  drwxr-xr-x   2 root root  4096 Sep 24 19:11 applications
  drwxr-xr-x   6 root root  4096 Oct  9 18:16 apport
  drwxr-xr-x   3 root root  4096 Apr 17  2014 apps
  drwxr-xr-x   2 root root  4096 Oct  9 18:15 apt
  drwxr-xr-x   2 root root  4096 Apr 17  2014 aptitude
  drwxr-xr-x   4 root root  4096 Apr 17  2014 apt-xapian-index
  drwxr-xr-x   2 root root  4096 Apr 17  2014 awk
  . . .

This view gives us plenty of information, most of which looks rather unusual.
The first block describes the file type (if the first column is a ``d`` the item
is a directory, if it is a ``-``, it is a normal file) and permissions. Each
subsequent column, separated by white space, describes the number of hard links,
the owner, group owner, item size, last modification time, and the name of the
item. We will describe some of these at another time, but for now, just know
that you can view this information with the ``-l`` flag of ``ls``.

To get a listing of all files, including *hidden* files and directories, you can
add the ``-a`` flag. Since there are no real hidden files in the ``/usr/share``
directory, let's go back to our home directory and try that command. You can get
back to the home directory by typing ``cd`` with no arguments::

  $ cd
  $ ls -a
  .  ..  .bash_logout  .bashrc  .profile

As you can see, there are three hidden files in this demonstration, along with
``.`` and ``..``, which are special indicators. You will find that often,
configuration files are stored as hidden files, as is the case here.

For the dot and double dot entries, these aren't exactly directories as much as
built-in methods of referring to related directories. The single dot indicates
the current directory, and the double dot indicates this directory's parent
directory. This will come in handy in the next section.

``cd``
------

We have already made two directory moves in order to demonstrate some properties
of ``ls`` in the last section. Let's take a better look at the command here.

Begin by going back to the ``/usr/share`` directory by typing this::

  $ cd /usr/share

This is an example of changing a directory by giving an *absolute path*.
Remember, in Linux, every file and directory is under the top-most directory,
which is called the *root* directory, but referred to by a single leading slash
``/``. An absolute path indicates the location of a directory in relation to
this top-level directory. This lets us refer to directories in an unambiguous
way from any place in the filesystem. Every absolute path **must** begin with a
slash.

The alternative is to use *relative paths*. Relative paths refer to directories
in relation to the current directory. For directories close to the current
directory in the hierarchy, this is usually easier and shorter. Any directory
within the current directory can be referenced by name without a leading slash.
We can change to the ``locale`` directory within ``/usr/share`` from our current
location by typing::

  $ cd locale

We can likewise move multiple directory levels with relative paths by providing
the portion of the path that comes after the current directory's path. From
here, we can get to the ``LC_MESSAGES`` directory within the ``en`` directory by
typing::

  $ cd en/LC_MESSAGES

To go back up, traveling to the parent of the current directory, we use the
special double dot indicator we talked about earlier. For instance, we are now
in the ``/usr/share/locale/en/LC_MESSAGES`` directory. To move up one level, we
can type::

  $ cd ..

This takes us to the ``/usr/share/locale/en`` directory.

A shortcut that you saw earlier that will always take you back to your home
directory is to use ``cd`` without providing a directory::

  $ cd
  $ pwd
  /home/demo
