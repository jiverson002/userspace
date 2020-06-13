.. highlight:: none

.. note::
   The following article is a adaptation of `How To Use Git: A Reference Guide
   <https://www.digitalocean.com/community/cheatsheets/how-to-use-git-a-reference-guide>`_
   by `Lisa Tagliaferri
   <https://www.digitalocean.com/community/users/ltagliaferri>`_, available
   under a `Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License <https://creativecommons.org/licenses/by-nc-sa/4.0/>`_.

Basics
------

Teams of developers and open-source software maintainers typically manage their
projects through Git, a distributed version control system that supports
collaboration.

This cheat sheet-style guide provides a quick reference to commands that are
useful for working and collaborating in a Git repository.

There are many more commands and variations that you may find useful as part of
your work with Git. To learn more about all of your available options, you can
run::

  $ git --help

You can also read more about Git and look at Git's documentation from the
`official Git website <https://git-scm.com/>`_.

Set Up and Initialization
^^^^^^^^^^^^^^^^^^^^^^^^^

Check your Git version with the following command, which will also confirm that
Git is installed.

.. code-block:: none

  $ git --version

You can initialize your current working directory as a Git repository with
``init``.

.. code-block:: none

  $ git init

To copy an existing Git repository hosted remotely, you'll use ``git clone``
with the repo's URL or server location (in the latter case you will use
``ssh``).

.. code-block:: none

  $ git clone https://www.github.com/username/repo-name

Show your current Git directory's remote repository.

.. code-block:: none

  $ git remote

For a more verbose output, use the ``-v`` flag.

.. code-block:: none

  $ git remote -v

Add the Git upstream, which can be a URL or can be hosted on a server (in the
latter case, connect with ``ssh``).

.. code-block:: none

  $ git remote add upstream https://www.github.com/username/repo-name

Staging
^^^^^^^

When you've modified a file and have marked it to go in your next commit, it is
considered to be a staged file.

Check the status of your Git repository, including files added that are not
staged, and files that are staged.

.. code-block:: none

  $ git status

To stage modified files, use the ``add`` command, which you can run multiple
times before a commit. If you make subsequent changes that you want included in
the next commit, you must run ``add`` again.

You can specify the specific file with ``add``.

.. code-block:: none

  $ git add my_script.py

With ``.`` you can add all files in the current directory including files that
begin with a ``.``.

.. code-block:: none

    git add .

You can remove a file from staging while retaining changes within your working
directory with ``reset``.

.. code-block:: none

  $ git reset my_script.py

Committing
^^^^^^^^^^

Once you have staged your updates, you are ready to commit them, which will
record changes you have made to the repository.

To commit staged files, you'll run the ``commit`` command with your meaningful
commit message so that you can track commits.

.. code-block:: none

  $ git commit -m "Commit message"

You can condense staging all tracked files with committing them in one step.

.. code-block:: none

  $ git commit -am "Commit message"

If you need to modify your commit message, you can do so with the ``--amend``
flag.

.. code-block:: none

  $ git commit --amend -m "New commit message"

Branches
^^^^^^^^

A branch in Git is a movable pointer to one of the commits in the repository, it
allows you to isolate work and manage feature development and integration. You
can learn more about branches by reading the `Git branch documentation
<https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell>`_.

List all current branches with the ``branch`` command. An asterisk (``*``) will
appear next to your currently active branch.

.. code-block:: none

  $ git branch

Create a new branch. You will remain on your currently active branch until you
switch to the new one.

.. code-block:: none

  $ git branch new-branch

Switch to any existing branch and check it out into your current working
directory.

.. code-block:: none

  $ git checkout another-branch

You can consolidate the creation and checkout of a new branch by using the
``-b`` flag.

.. code-block:: none

  $ git checkout -b new-branch

Rename your branch name.

.. code-block:: none

  $ git branch -m current-branch-name new-branch-name

Merge the specified branch's history into the one you're currently working in.

.. code-block:: none

  $ git merge branch-name

Abort the merge, in case there are conflicts.

.. code-block:: none

  $ git merge --abort

You can also select a particular commit to merge with ``cherry-pick`` with the
string that references the specific commit.

.. code-block:: none

  $ git cherry-pick f7649d0

When you have merged a branch and no longer need the branch, you can delete it.

.. code-block:: none

  $ git branch -d branch-name

If you have not merged a branch to master, but are sure you want to delete it,
you can **force** delete a branch.

.. code-block:: none

  $ git branch -D branch-name

Collaborate and update
^^^^^^^^^^^^^^^^^^^^^^

To download changes from another repository, such as the remote upstream, you'll
use ``fetch``.

.. code-block:: none

  $ git fetch upstream

Merge the fetched commits.

.. code-block:: none

  $ git merge upstream/master

Push or transmit your local branch commits to the remote repository branch.

.. code-block:: none

  $ git push origin master

Fetch and merge any commits from the tracking remote branch.

.. code-block:: none

  $ git pull

Inspecting
^^^^^^^^^^

Display the commit history for the currently active branch.

.. code-block:: none

  $ git log

Show the commits that changed a particular file. This follows the file
regardless of file renaming.

.. code-block:: none

  $ git log --follow my_script.py

Show the commits that are on one branch and not on the other. This will show
commits on a-branch that are not on b-branch.

.. code-block:: none

  $ git log a-branch..b-branch

Look at reference logs (``reflog``) to see when the tips of branches and other
references were last updated within the repository.

.. code-block:: none

  $ git reflog

Show any object in Git via its commit string or hash in a more human-readable
format.

.. code-block:: none

  $ git show de754f5

Show changes
^^^^^^^^^^^^

The ``git diff`` command shows changes between commits, branches, and more. You
can read more fully about it through the `Git diff documentation
<https://git-scm.com/docs/git-diff>`_.

Compare modified files that are on the staging area.

.. code-block:: none

  $ git diff --staged

Display the diff of what is in ``a-branch`` but is not in ``b-branch``.

.. code-block:: none

  $ git diff a-branch..b-branch

Show the diff between two specific commits.

.. code-block:: none

  $ git diff 61ce3e6..e221d9c

Stashing
^^^^^^^^

Sometimes you'll find that you made changes to some code, but before you finish
you have to begin working on something else. You're not quite ready to commit
the changes you have made so far, but you don't want to lose your work. The
``git stash`` command will allow you to save your local modifications and revert
back to the working directory that is in line with the most recent ``HEAD``
commit.

Stash your current work.

.. code-block:: none

  $ git stash

See what you currently have stashed.

.. code-block:: none

  $ git stash list

Your stashes will be named ``stash@{0}``, ``stash@{1}``, and so on.

Show information about a particular stash.

.. code-block:: none

  $ git stash show stash@{0}

To bring the files in a current stash out of the stash while still retaining the
stash, use ``apply``.

.. code-block:: none

  $ git stash apply stash@{0}

If you want to bring files out of a stash, and no longer need the stash, use
``pop``.

.. code-block:: none

  $ git stash pop stash@{0}

If you no longer need the files saved in a particular stash, you can ``drop``
the stash.

.. code-block:: none

  $ git stash drop stash@{0}

If you have multiple stashes saved and no longer need to use any of them, you
can use ``clear`` to remove them.

.. code-block:: none

  $ git stash clear

Ignoring files
^^^^^^^^^^^^^^

If you want to keep files in your local Git directory, but do not want to commit
them to the project, you can add these files to your ``.gitignore`` file so that
they do not cause conflicts.

Use a text editor to add files to the ``.gitignore`` file.

To see examples of ``.gitignore`` files, you can look at `GitHub's gitignore
template repo <https://github.com/github/gitignore>`_.
