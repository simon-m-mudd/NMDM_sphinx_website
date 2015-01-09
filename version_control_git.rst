.. _version-control-git:

========================================
Version control with git
========================================

  In this section we'll take you through some software call `git <http://git-scm.com/>`_. 
  It is version control software. This lesson will rely heavily on the lessons at `Software Carpentry <http://software-carpentry.org/>`_

What is version control
========================================

  Very briefly, version control software allows you to keep track of revisions so that you can very 
  easily see what changes you have made to your notes, data, scripts, programs, papers, etc. 
  It is also very useful for collaboration. 
  
  In this course we are going to use it to keep track of your progress,
  and in doing so we hope that techniques for producing reproducible research (see section :ref:`background-head`)
  become second nature to you. 
  
  If you want a more detailed explanation of version control, written in plain English, 
  see the outstanding lesson `available at software carpentry <http://software-carpentry.org/v5/novice/git/00-intro.html>`_.
  
git basics
=======================================

  The videos introduce you to the most basic operations in git, and if you want more written detail you can
  look at the `git documentation on Software Carpentry <http://software-carpentry.org/v5/novice/git/index.html>`_.
  
  We are going to start by making a markdown document. Markdown is a kind of shorthand for writing html pages. 
  You don't really need to worry too much about markdown at this point, since we'll go through the basics in the videos. 
  However, if you yearn to learn more, here are `some <https://help.github.com/articles/markdown-basics/>`_
  `websites <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>`_
  `with <https://guides.github.com/features/mastering-markdown/>`_ the
  `basics <http://whatismarkdown.com/>`_.
  
A note on configuration
---------------------------------------

  **You need to set your username and email** on git, if you don't it will insert a username and email for you. 
  This becomes slightly important if you want a consistent commit record on github the user.name and user.email need to be the same as your github account. 
  
  So, for example::
  
    git config --global user.name John Doe
    git config --global user.email John@Doe.com
    
  I've sometimes had trouble with this in the University of Edinburgh environment, 
  I'm not quite sure why but if you start getting warning mesages try a local config::
  
    git config --local user.name John Doe
    git config --local user.email John@Doe.com  
  
  
Videos
---------------

  * `git basics <http://www.geos.ed.ac.uk/~smudd/export_data/EMDM_videos/DTP_NMDMcourse_video_012_gitbasic.mp4>`_.
  * `looking at changes using git <http://www.geos.ed.ac.uk/~smudd/export_data/EMDM_videos/DTP_NMDMcourse_video_013_gitlog.mp4>`_.
  * `creating a repository on github <http://www.geos.ed.ac.uk/~smudd/export_data/EMDM_videos/DTP_NMDMcourse_video_014_github.mp4>`_.
  
