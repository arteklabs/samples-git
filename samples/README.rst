Git Cheatsheet
==============

Get the status of your checked out files:

.. code:: shell

   # untracked: ??
   # indexed: A
   # modified: M
   $ git status --short
   ?? samples/README.rst

Ignore files:

.. code:: shell

   # nested dirs: matches a/b/z, a/b/d/z, a/b/d/.../z
   a/**/z

   # ignore all lib files except
   *.lib
   !exception.lib

   # ignore all build files but persist build dir
   build/

   # ignore all html files
   docs/**/*.html

Compare ``indexed`` to last commit:

.. code:: shell

   git diff --staged

Compare ``modified`` to last commit:

.. code:: shell

   git diff

Index change:

.. code:: shell

   git add file
   git add dir

Index and commit with message:

.. code:: shell

   git commit -a -m "commit-message"

Remove from the index and from the working directory (the docs forgot ``-f``, add to the public repo). Even if the files have been committed already, it will remove them from the index, that is, index their removal.

.. code:: shell

   # removes file
   git rm -f file

   # removes dir (add to public repo)
   git rm -f dir

   # removes all html files in docs recursively
   git rm -f docs/\*.html

   # removes all html files in the subdirs only of docs recursively
   git rm -f docs/**/\*.html

   # removes all html files in the level 2 subdirs only of docs recursively
   git rm -f docs/**/**/\*.html

Remove from the index but keep in the working dir:

.. code:: shell

   git rm --cached

Rename indexed file:

.. code:: shell

   git mv file FILE

Log branch commits:

.. code:: shell

   # log last N commits in a single line with commit stats (line changes count
   # per file)
   git log -N --oneline --stats

   # show branch commit origin (oneline)
   git log --oneline --graph

   # format
   git log --pretty=format:"commit %h by %an, %ar --> %s"

   # log commits to file
   git log --oneline -- file

   # ignore merges
   git log --oneline --no-merges

Fix last commit message (of unpushed commit)

.. code:: shell

   git commit --amend

Unindex:

.. code:: shell

   git restore --cached file

Remove unindexed changes:

.. code:: shell

   git restore file

List remotes:

.. code:: shell

   # origin is the remote you've cloned from. Each remote can have its own
   # protocol: ssh, https, ...
   $ git remote -v
   origin  github:arteklabs/samples-git (fetch)
   origin  github:arteklabs/samples-git (push)

List local branches:

.. code:: shell

   git branch

List remote branches (requires ``pull`` first)

.. code:: shell

   git branch -r

List all branches (``*`` denotes current branch)

.. code:: shell

   $ git branch -a
   * latest
   remotes/origin/HEAD -> origin/latest
   remotes/origin/latest

Get changes made to remote branches without merging them with the local branches. In the example below, changes were fetched onto ``origin/latest`` but not to ``latest``.

.. code:: shell

   $ git fetch origin
   $ git branch
   * latest
   $ tree test
   test
   └── test
       ├── test
       │   └── test.html
       └── test.html
   $ git branch
   * (HEAD detached at origin/latest)
   latest
   $ tree test
   test
   ├── test
   │   ├── test
   │   │   └── test.html
   │   └── test.html
   └── test.html

Get changes made to remote branches and merge them with the local branches.

.. code:: shell

   $ git pull origin

Push changes to remote branch

.. code:: shell

   $ git pull origin


FAQ
===

difference between fetch and pull
---------------------------------

Difference between restore and rm
---------------------------------

``restore`` reverts the uncommitted indexed changes. ``rm`` removes the indexed files, whether they've been committed or not.

Exercises
=========

E1
--

If you've indexed changes to ``file``, can you restore them with ``git restore file``?

No, it is required to ``restore --staged`` and then ``restore``.

E2
--

How to remove locally a branch that has been removed remotely?

.. code:: shell

   git remote update origin --prune