==================================================================
Instructions specific to the University of Edinburgh
==================================================================


The documentation available on this page is specific to University of Edinburgh users. 
It includes information on how to access our servers and how to compile the code on
our systems. 

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

  If you are a user at the University of Edinburgh, you can donate some of your
  `DataStore <http://www.geos.ed.ac.uk/it/DataStore.html>`_ allocation to the group. 
  
  Our groupname is LSDTopoData. 

Donating storage to the DataStore (this gives you access to it)
---------------------------------------------------------------------------
  
  To register, you need to:
  
    #. Go to the web page: https://registration.ecdf.ed.ac.uk/storage/  
    #. Under My DataStore Personal Space Allocations select `allocate to shared space`.
    #. Select  datastore_geos_groups_LSDTopoData and assign some quota to it.

Creating a shortcut to the datastore from your home directory in Linux
----------------------------------------------------------------------------
  
  It is very annoying to have to remember the path name to your DataStore 
  directories, so you can create a shortcut to these. 
  
  To do this, just go into the directory from which you want the link 
  in a terminal (this will probably be your home directory) and type::
  
    ln -s /exports/csce/datastore/geos/groups/LSDTopoData NameOfLink 
    
  Where `NameOfLink` is just the name you want for the link (I used LSDTopoData).
  
  You could also do this for your personal DataStore folder::
  
    ln -s /exports/csce/datastore/geos/users/UUN NameOfLink
    
  where `UUN` is your university username. If you are a student this is your
  student number. 
  
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
  



