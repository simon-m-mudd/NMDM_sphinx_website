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
  
videos
-----------------------------------------------

  
  
Getting started with Git
==============================================

  Git is already installed on our servers. You can call it with::
  
    $ git
    
  Much of what I will descrbe below is also described in the
  `Git book <http://git-scm.com/book/en/>`_.
  
  The first thing you want to do is set the username and email for the session::
  
    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com   
    
  I'm not acutally sure if this will affect other users, as it is sitting on the 
  GeoScience server. So you might choose to not use the --global flag, and 
  so the name and email will only apply to the specific project you are working 
  on that session::
  
    $ git config --local user.name "John Doe"
    $ git config --local user.email johndoe@example.com     

  You can check all your options with::
  
    git config --list
    
Setting up a git repository
-----------------------------------------
  
  First, I'll navigate to the directory that holds my
  prospective git repository::
  
    smudd@burn markdown_test $ pwd
    /home/smudd/SMMDataStore/Courses/Numeracy_modelling_DM/markdown_test
    
  Now I'll initiate git here::
  
    smudd@burn OneD_hillslope $ git init
    Initialized empty Git repository in /home/smudd/SMMDataStore/Courses/Numeracy_modelling_DM/markdown_test.git/


Adding files and directories to the repository
------------------------------------------------------

  So now you have run ``git init`` in some folder to initiate a repository. 
  You will now want to add files with the add command::
  
    git add README.md
    
  You can also add folders and all their contianing files this way. 
 
Committing to the repository
------------------------------------------------------

  Adding files **DOES NOT** mean that you are now keeping track of changes. You do this by "commitng" them. 
  A ``commit`` command tells git that you want to store changes. 
  
  You need to add a message with the ``-m`` flag. Like this::

    commit -m "Initial project version" .
    
  Where the . indicates you want everything in the current directory including subfolders.
  You could also commit an individual file with::
  
    commit -m "Initial project version" README.md  
  
Pushing your repository to Github
=============================================================

  `Github <https://github.com/>`_ is a resource that hosts git repositories. 
  It is a popular place to put open source code. 
  
  To host a repository on `Github <https://github.com/>`_, you will need to set up the repository before
  synching your local repository with the github repository. 
  
  You can place your repository on 
  `Github <https://github.com/>`_ by using the ``push`` command::
  
    smudd@burn OneD_hillslope $ git remote add origin https://github.com/simon-m-mudd/markdown_test.git
    smudd@burn OneD_hillslope $ git push -u origin master
    Counting objects: 36, done.
    Delta compression using up to 64 threads.
    Compressing objects: 100% (33/33), done.
    Writing objects: 100% (36/36), 46.31 KiB, done.
    Total 36 (delta 8), reused 0 (delta 0)
    To https://github.com/simon-m-mudd/markdown_test.git
    * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
    
         
Problems with Setting up repos on github
==========================================
  
 Git is not entirely intuitive, so I've found quite a number of problems in setting up github repos. 
 Here are some examples and (hopefully) their fixes. 
 
    
Creating local repo and then Github repository
------------------------------------------------

  I made a local github repository using::
  
    git init
    
  And then tried to push to a github repo, but the first error message is you need to make a repository on github first. 
  I added a readme file on Github, but this seemed to lead to errors::
  
    Updates were rejected because the tip of your current branch is behind
    hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
    
    
  So what I did to fix this was:
  
    #. On the local repo, I used::
    
        touch README.md
	git add README.md
        git commit -m "Trying to add readme" .
    
    #. Then I pulled from the master::
    
        git pull origin master
        
        
    #. Then I pushed to the master. That seemed to fix things::
    
        git push -u origin master

 
 


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
  
