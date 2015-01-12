.. _getting-on-servers:

==================================================================
Instructions specific to the University of Edinburgh
==================================================================


The documentation available on this page is specific to University of Edinburgh users. 
It includes information on how to access our servers


Videos
==============

  * `Getting onto our servers using nx and putty <http://www.geos.ed.ac.uk/~smudd/export_data/EMDM_videos/DTP_NMDMcourse_video_002_nx_putty.mp4>`_.
  * `Getting onto our servers using x2go <http://www.geos.ed.ac.uk/~smudd/export_data/EMDM_videos/DTP_NMDMcourse_video_003_x2go.mp4>`_.

Getting onto our servers using x2go
===================================================

  x2go is a remote desktop client that will in the future be the primary client for the school of GeoSciences. 
  
  You can set up an x2go client for Edinburgh's School of GeoSciences by following
  `these instructions <https://www.geos.ed.ac.uk/it/FAQ/x2go.html>`_ (note you will have to log in to see them).




.. _getting-onto-servers:

Getting onto our servers using NX
=================================

  A number of our topographic tools have been designed to be run in the Linux operating environment. 
  You can actually get your windows computer to act a bit like a Linux terminal by downloading the `Cygwin <https://www.cygwin.com/>`_ package,  
  If you work on a Mac you can also get Linux because the Mac operating system is built on top of Linux: 
  to get there you need to call the 'terminal' application.
  However, the way we mostly operate is via the School of GeoSciences Linux servers. 
  The main one is called 'burn'. The preferred way to get into it is via an NX window.


  #. In the windows menu, type nx, and you will see the nx client:

     .. image:: ./_images/Edinburgh_specific/nx1.jpg

  #. The 'host' is burn.geos.ed.ac.uk

     .. image:: ./_images/Edinburgh_specific/nx2.jpg

  #. You then need to enter your username and password. 
  
  #. You will get a sort of blank looking blue desktop. 
     If you right click on this desktop you get the option to start a terminal: 
   
     .. image:: ./_images/Edinburgh_specific/get_terminal.jpg

  #. Once you start a terminal you will see little screen that tells you what account you are on, where you are (so in the below image, 
     I am smudd and I am '@' burn, followed by the directory (if it is the '~' symbol that means it is your home directory).
   
     .. image:: ./_images/Edinburgh_specific/terminal.jpg   

  #. At this stage, you need to familiarise yourself with some linux commands for moving around in directories. 
     I'll wait while you read this: 
     http://www.ee.surrey.ac.uk/Teaching/Unix/
     and this:  
     http://www.skorks.com/2009/09/bash-shortcuts-for-maximum-productivity/
     
  #. The main commands you will need are 'cd', 'cd ..' and 'ls'. Also, the tab key, ctrl-r, ctrl-a and ctrl-e will save you vast amounts of time. 
 
Using NX from your home computer
----------------------------------------------------------

  You can get NX for your home computer in order to work on your files sitting on your home directory. 
  
  You'll want to set up a VPN on your computer. 
  
  Information on the University's VPN service can be found here: 
  http://www.ed.ac.uk/schools-departments/information-services/services/computing/desktop-personal/vpn
  
  NX software is free, so if you manage your own computer, you can get it here: http://www.nomachine.com/download
  
  If you are on a university laptop, NX should already be installed. 
 



Some notes on file storage for staff and postgraduates (as of 18/9/2014 undergraduates do not have access)
============================================================================================================

  Every staff member and PhD student at the University of Edinburgh has access to 500GB of storage on the `Edinburgh datastore <http://www.ed.ac.uk/schools-departments/information-services/research-support/data-management/data-storage>`_. 
  
  This is a very good place to put all of your files since it is backed up regularly (no losing your PhD if you spill coffee on your laptop!!). 

Donating storage to the DataStore (this gives you access to it)
---------------------------------------------------------------------------
  
  To register, you need to:
  
    * Go to the web page: https://registration.ecdf.ed.ac.uk/storage/  
    
  If you are in a group with a group page, you can allocate data to this group:  
    
    #. Under My DataStore Personal Space Allocations select `allocate to shared space`.
    #. Select your groups shared space and allocate some data to it. 

Creating a shortcut to the datastore from your home directory in Linux
----------------------------------------------------------------------------
  
  It is very annoying to have to remember the path name to your DataStore 
  directories, so you can create a shortcut to these. 
  
  To do this, just go into the directory from which you want the link 
  in a terminal (this will probably be your home directory) and type::
  
    ln -s /exports/csce/datastore/geos/users/UUN NameOfLink
    
  or if you are in, say, biology is will be::
  
    ln -s /exports/csce/datastore/biology/users/UUN NameOfLink
    
  where `UUN` is your university username. If you are a student this is your
  student number. Note that the `csce` in the above link is for the College of Science and Engineering.
  If you are in another college you will have to modify the link. 
      
  *WARNING!!!* If you sync your laptop or home computer to your M drive this will 
  result in your home computer syncing to BOTH your M drive and your DataStore drive.
     

A note on file permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~

  The source code should not have execute permission. 
  In a terminal window, you can check this with ``ls -l``. 
  There should be no ``x`` permission. 
  You can remove execute permission with ``chmod`` a ``-x filename``. 
  The reason for this is that in a terminal window you want to be able to easily see which files are executable. 
  
  Another way to do this is with the ``664`` option on ``chmod``. For example::
  
    chmod 664 LSDIndexChannelTree.cpp
  
  If you check this file you get this::
  
    -rw-rw-r-- 1 smudd smudd 37823 Apr  5 14:20 LSDIndexChannelTree.cpp
  
  This means that the owner can read and write to the file, the group can read and write, and anyone else can just read the file. 
  Remember, if you make changes to permissions you've got to commit the changes!
  



