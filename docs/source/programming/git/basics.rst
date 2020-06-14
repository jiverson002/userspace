.. highlight:: none

.. note::
   The following article is an adaptation of `How To Use Git Effectively <https://www.digitalocean.com/community/tutorials/how-to-use-git-effectively>`_ and `How To Use Git Branches <https://www.digitalocean.com/community/tutorials/how-to-use-git-branches>`_ by Jason Kurtz, available under a `Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License <https://creativecommons.org/licenses/by-nc-sa/4.0/>`_.

Basics
------

Before using git for your development, it's a good idea to plan out your
workflow. The workflow decision is typically based on the size and scale of your
project. To gain a basic understanding of git for now, a simple, single-branch
workflow will suffice. By default, the first branch on any git project is called
``master``. Later in this tutorial, you will learn how to create other branches.

Let's create our first project and call it ``testing``. (If you already have a
project that you want to import to git you can skip down to :ref:`init`.)

Just like you want to have a good, clean work environment, the same idea applies
to where you do your coding, especially if you're going to contribute to a
number of projects at the same time. A good suggestion might be to have a
directory called git in your home directory which has subdirectories for each of
your individual projects.

The first thing we need to do is create our workspace environment::

  $ mkdir -p ~/git/testing
  $ cd ~/git/testing

The above commands will accomplish two things: 1) it creates a directory called
``git`` in our home directory and then creates a subdirectory inside of that
called ``testing`` (this is where our project will actually be stored) and 2) it
brings us to our project's base directory.

Once inside that directory, we need to create a few files that will be in our
project. In this step, you can either follow along and create a few dummy files
for testing purposes or you can create files/directories you wish that are going
to be part of your project.

We are going to create a test file to use in our project::

  $ touch file

.. _init:

``init``
^^^^^^^^

Once all your project files are in your workspace, you need to start *tracking*
your files with git. To do this, you must tell git that you want to use your
current directory as a git environment::

  $ git init
  Initialized empty Git repository in /home/user/git/testing/.git/

From this point forward the ``testing`` project directory is considered a *Git
repository*, or *repo* for short.

``status``
^^^^^^^^^^

During the course of the development of your project, you may wish to know the
state of your project with respect to its underlying Git repository. This state
can be checked with the following::

  $ git status
  On branch master

  No commits yet

  Untracked files:
    (use "git add <file>..." to include in what will be committed)
      file

  nothing added to commit but untracked files present (use "git add" to track)

The output tells us a few things. First, we are on the branch ``master``.
You can read more about branches `later <branches>` in this article. Second,
that we have not made any commits yet, but we will make our first very soon! An
finally, that there are some *untracked* files in our repo, in this case, just
one. Untracked files are files whose history is not kept as part of the repo.

``add``
^^^^^^^

To start *tracking* a file, i.e., have its history maintained in the repo, we
must add said files to the repo. The following will add all files and
directories in your project to your newly created repo::

  $ git add .

In this case, no output is good output. Unfortunately, git does not always
inform you if something worked. If we check the status of our repo again, we
will see something slightly different than before::

  $ git status
  On branch master

  No commits yet

  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
      new file:   file

Now we see that git is reporting no untracked files, but there is a ``new
file`` in the repo.

``commit``
^^^^^^^^^^

Adding files alone does not mean that the history of changes to them is being
tracked. In fact, any time that you have made changes to your code that you wish
to be eternalized in the history of your project, you must *commit* these
changes to the repo.

Every time you commit changes, you need to write a commit message. A commit
message is a short message explaining the changes that you've made. It is
required before sending your coding changes off (which is called a push) and it
is a good way to communicate to your co-developers what to expect from your
changes.

Commit messages are generally rather short, between one and two sentences
explaining what your change did. It is good practice to commit each individual
change before you do a push. You can push as many commits as you like. The only
requirement for any commit is that it involves at least one file and it has a
message. A push must have at least one commit.

Continuing with our example, we are going to create the message for our initial
commit::

  $ git commit -m "Initial Commit"
  [master (root-commit) c1d1b05] Initial commit
  1 file changed, 0 insertions(+), 0 deletions(-)
  create mode 100644 file

The ``-m`` flag signifies that our commit message (in this case ``"Initial
Commit"``) is going to follow.

``remote``
^^^^^^^^^^

Up until this point, we have done everything on our local server. That's
certainly an option to use git locally, if you want to have any easy way to have
version control of your files. If you want to work with a team of developers,
however, you're going to need to push changes to a remote server. This section
will explain how to do that.

The first step to being able to push code to a remote server is providing the
URL where the repository lives and giving it a name. To configure a *remote
repository*, or *remote* for short::

  $ git remote add origin git@git.domain.tld/repository.git
  $ git remote -v
  origin	git@git.domain.tld/repository.git (fetch)
  origin	git@git.domain.tld/repository.git (push)

The first command adds a remote, called ``origin``, and sets the URL to
``git@git.domain.tld/repository.git``. You can name your remote whatever you'd
like, but the URL needs to point to an actual remote repository. For example, if
you wanted to push code to GitHub, you would need to use the repository URL that
they provide.

The second command lists any remotes that are configure for the repo. A repo may
have many remotes.

``push``
^^^^^^^^

Once you have a remote configured, you are now able to *push* your code. You can
push code to a remote by typing the following::

  $ git push origin master
  Counting objects: 4, done.
  Delta compression using up to 2 threads.
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 266 bytes, done.
  Total 3 (delta 1), reused 1 (delta 0)
  To git@git.domain.tld/repository.git
     0e78fdf..e6a8ddc  master -> master

``git push`` tells git that we want to push our changes, ``origin`` is the name
of our newly-configured remote and ``master`` is the name of the branch.

In the future, when you have commits that you want to push to the server, you
can simply type ``git push``.

``branch``
^^^^^^^^^^
A branch, at its core, is a unique series of code changes with a unique name.
Each repository can have one or more branches. By default, the first branch is
called ``master``.

Prior to creating new branches, we may want to see all the branches that exist.
We can view all existing branches by typing the following::

  $ git branch -a
  * master
  remotes/origin/master

Adding the ``-a`` flag tells git that we want to see all branches that exist,
including ones that we do not have in our local workspace.

The asterisk next to ``master`` in the first line of output indicates that we
are currently on that branch. The second line simply indicates that on our
remote, named origin, there is a single branch, also called master.

Now that we have a well established project, we may wish to improve the way that
we manage the source code. One small, but impactful improvement, is to create a
second branch in addtion to ``master``. We will call this branch ``develop`` and
it is where we will actively develop the project. Only after we are satisfied
with changes made to branch ``develop`` will we merge them into branch
``master``. This means that branch ``master`` will "*always*" contain code that
is production quality.

To create a new branch named ``develop``, type the following::

  $ git branch develop

In the case of a branch by that name already existing, git would tell us so::

  fatal: A branch named 'develop' already exists.

``checkout``
^^^^^^^^^^^^

You can switch back and forth between your two branches, by using the ``git
checkout`` command::

  $ git checkout master

or

.. code-block:: none

  $ git checkout develop
  Switched to branch 'master'

If you try to switch to a branch that doesn't exist, such as

.. code-block:: none

  $ git checkout nosuchbranch
  error: pathspec 'nosuchbranch' did not match any file(s) known to git.

Now that we have multiple branches, we need to put them to good use. In our
scenario, we are going to use our ``develop`` branch for testing out our changes
and the ``master`` branch for releasing them to the public.

To illustrate this process, we need to switch back to our ``develop`` branch::

  $ git checkout develop

On this branch, we are going to create a new blank file, named ``dosiero``.
Until we merge it to the ``master`` branch (in the following step), it will not
exist there.

.. code-block:: none

  $ touch dosiero
  $ git status
  On branch develop
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
      dosiero

  nothing added to commit but untracked files present (use "git add" to track)
  $ git add dosiero
  $ git status
  On branch develop
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
      new file:   dosiero

  $ git commit -m "Adds the file dosiero"
  [develop 3922da9] Adds the file dosiero
   1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 dosiero

The above set of commands will create a blank file named ``dosiero``, add it
to be tracked in the repo, and commit it to the history on branch ``develop``.

The ``git checkout`` command can be used to create a new branch and switch to it
immediately. For example, the following sequence of commands::

  $ git branch develop
  $ git checkout develop
  Switched to branch 'develop'

can be accomplished with a single invocation of the ``git checkout`` command by
passing the ``-b`` flag as so::

  $ git checkout -b develop
  Switched to a new branch 'develop'

Notice the message reported by git now indicates that the branch is a ``new
branch``.

``merge``
^^^^^^^^^

The interesting part comes after we switch back to our master branch, which we
can do with the git checkout command::

  $ git checkout master
  Switched to branch 'master'

Now if we execute ``ls``, it will appear that our new file is missing::

  $ ls
  file

However, it's not missing --- it's just on our ``develop`` branch and we are on
our ``master`` branch.

In this scenario, this file represents any change to any file (or a whole new
file) that has passed all testing on our development branch, and is ready to be
in production. The process of moving code between branches (often from
development to production) is known as merging.

It is important to remember when merging, that we want to be on the branch that
we want to merge to. In this case, we want to merge from our ``develop`` branch,
where the ``dosiero`` file exists, to our ``master`` branch.

Keeping that in mind, considering that we are already on the ``master`` branch,
all we have to do is run the ``git merge`` command. To merge the changes from
the ``develop`` branch to the ``master`` branch, type the following::

  $ git merge develop
  Updating c1d1b05..ef52230
  Fast-forward
   dosiero | 0
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 dosiero

Running the ``ls`` command again will confirm that our ``dosiero`` file is now
on our ``master`` branch::

  $ ls
  dosiero file
