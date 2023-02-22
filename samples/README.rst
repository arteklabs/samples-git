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

Index and commit with message:

.. code:: shell

   git commit -a -m "commit-message"

Remove from the index and from the working directory (the docs forgot ``-f``, add to the public repo):

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

