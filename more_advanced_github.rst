.. _more_advanced_github:

Working with GitHub repositories on more than one computer
============================================================

In this section we will explain the basics of woring with a repository on more than one computer. 
The basic case is that you want to work on something from your work computer and from your home computer. 
The lesson assumes you have already set up a `GitHub <https://github.com/>`_ repository. 
If you haven't, start here: :ref:`version-control-git`.

This section complenets the always outstanding instructions at `Software carpentry <http://www.software-carpentry.org/v5/novice/git/>`_.

Pulling, fetching, merging and cloning
========================================

If you have made a repository, you should already be familiar with the ``git push`` command. 
This command tells ``git`` to "push" all your commits to a remote repository
(which is usually `GitHub <https://github.com/>`_ or `Bitbucket <https://bitbucket.org/>`_.

But what if you have an up to date repository on GitHub and you want to start working on this repository on your home computer?
For this, you will need to learn about the ``git`` commands ``pull``, ``fetch``, ``merge`` and ``clone``.

We will discuss these commands below, but you can also read about them on
`GitHub help <https://help.github.com/articles/fetching-a-remote/>`_ and at
`Software Carpentry collaboration lesson <http://www.software-carpentry.org/v5/novice/git/02-collab.html>`_.

Cloning a repository
-----------------------------

If you want to reproduce a repository on your home computer, the place to start is probably by using the ``clone`` command. 

This command copies all the files in a repository to your computer, and begins tracking them in git. 
You do this by typing in::

  git clone https://github.com/USERNAME/REPOSITORY.git
  
Where you need to update the ``USERNAME`` and ``REPOSITORY`` to the appropriate names. 


