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

    diff --staged

Compare ``modified`` to last commit:

.. code:: shell

    diff
