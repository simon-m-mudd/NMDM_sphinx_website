==========================================================================
Getting the tools working outside of the University of Edinburgh network
==========================================================================

  Ideally, users of our software will not come exclusively from the University of Edinburgh. 
  In addition, even if you are at the University of Edinburgh you might not have access to our servers. 

  These instructions are intended to get you set up on your home computer. You will need administrator privileges to get this working.  

Operating systems
=====================================

  The development of our software is done in a Linux environment. 
  There is a prosaic reason for this: our servers at Edinburgh GeoSciences and our supercomputers run linux so it is the fastest option, 
  and our code uses a large amount of memory and is computationally expensive.
  
  I (`SMM <http://www.geos.ed.ac.uk/homes/smudd>`_) have managed to get components of the code to run on the Windows operating system using something called `cygwin <https://www.cygwin.com/>`_.
  This is perhaps not ideal, however, since I've never managed to get the `FFTW <http://www.fftw.org/>`_ package working on my Windows computers via cygwin, 
  and a number of our routines rely on this package. 
  
  My group does not use Apple products, so we have no expertise in getting the software to run on Apple computers.
  Apple uses a linux operating system "under the hood" of its proprietary operating systems, 
  so theoretically one should be able to get our code to run on a Mac natively. We haven't tried this so can't provide documentation. 
  
  A perhaps simpler way to do things, if you don't have an existing Linux operating system, is to use a `virtual machine <http://en.wikipedia.org/wiki/Virtual_machine>`_.
  Basically this is to get a Linux operating system running within your Windows or Apple computer. This page walks you through that process. 
  
Creating a Linux virtual machine on your Windows or Apple computer
-----------------------------------------------------------------------

  So to get Linux running (relatively) painlessly on your windows or Apple computer, you will need some software that allows you to run a `virtual machine <http://en.wikipedia.org/wiki/Virtual_machine>`_.
  
  There are a number of options, popular ones include:
  
    * `Parallels <http://www.parallels.com/uk/>`_ This software is proprietary. 
    * `VMWare <http://www.vmware.com/uk>`_ There are several flavours of this. The free version is VMware Player. 
    * `VirtualBox <https://www.virtualbox.org/>`_ This is open source. 
    
  Here I'll walk you through setting up Linux using VMware. 
  I have no better reason for choosing this software other than a `former PhD student <http://www.bgs.ac.uk/staff/profiles/41289.html>`_ has used it and it works.
  One disadvantage is it doesn't seem to have an Apple version. If you use Apple you'll need to try to go through a similar process using `VirtualBox <https://www.virtualbox.org/>`_, 
  which does have a version for Mac operating systems.
  
  But, here is how you set up the VMware player. 
  You will need a reasonable amount of storage and RAM. So a very old computer won't work.
  If you've got a computer purchased in the last few years things will probably be fine.  
  You will also need a reasonable amount of storage on your hard disk. 
  The virtual machine permanently takes up some component of your hard disk.
  
    #. First, download VMware player. The download is currently `here <https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/7_0>`_. 
    #. Run the installation package. Brew a cup of tea while you wait for it to install. `Maybe surf the internet a bit <http://www.bbc.co.uk/sport/football/teams/hibernian>`_. 
    #. **BEFORE** you set up a virtual machine, you will need to download a linux operating system!
        
        #. We are going to use `Ubuntu <http://www.ubuntu.com/>`_, just because it is stable, popular and has good documentation.
        #. I first attempted an installation with 64-bit Ubuntu, but it turns out my computer doesn't allow guest 64 bit operating systems. 
           To fix this I just downloaded the 32 bit version of Ubuntu:
           
             .. image:: ./_images/Outside_edin/Ubuntu32.jpg
           
        #. Find the downloads link and download the latest version. It will be an `iso` disk image. This will take a while. Put that time to `good use <https://www.youtube.com/user/HibernianTV>`_. 
        
    #. Once that finishes downloading, you can set up your virtual box. First, open VMware Player.
    
    #. Now click on the "Create a New Virtual Machine" option. 
       
        .. image:: ./_images/Outside_edin/Create_VM.jpg

    #. It will ask you how you want to install the operating system. Tell it you want to use the Ubuntu disk image you just downloaded:
    
        .. image:: ./_images/Outside_edin/Pick_OS_install.jpg
        
    #. You will need to add some username information, and then you will have to pick a location for the Virtual Machine. I made a folder called `c:\Ubuntu` for it:
    
        .. image:: ./_images/Outside_edin/Ubuntu.jpg
        
    #. Now allocate disk space to the virtual machine. **This disk space cannot be used by your windows operating system!!**. I decided to use a single file to store the disk since it should be faster:
    
        .. image:: ./_images/Outside_edin/Disk.jpg
    
    #. The next page will say it is ready to create the virtual machine, but it has a default Memory (in my case 1GM) allocated. I wanted more memory so I clicked on the customize hardware button:
    
        .. image:: ./_images/Outside_edin/CutomizeHardware.jpg
        
       This allowed me to increase the memory to 2GB. Note that this will be used when the virtual  machine is on, but when not in use the memory will revert to your original operating system. 
       
   #. You might be asked to install some VMware Linux tools. You should do this, as some things won't work if it isn't installed.
   
   #. Installing the operating system within the virtual machine will take ages. You might schedule this task for your lunch hour, which is what I did. 
   
   #. When Ubuntu has installed, it will look for software updates. You should install these. This will also take ages. Maybe you have a book to read?
   
   #. Finally, you should be aware that the default keyboard layout is US. Getting a different keyboard is a bit of a pain.
   
       #. First go to system settings. 
       #. Then click on language support. 
       #. It will need to install some stuff. 
       #. Go to text entry. 
       #. In the lower left corner click on the `+` button. 
       #. Add your country's input source. 
   
        
        
Setting up your Linux virtual machine: essentials
----------------------------------------------------

  You will need to spend some time setting up common tools for your new Ubuntu virtual machine. 
  
  Before you do anything, you need to know how to open a terminal. Click on the search tool (on mine it is in the upper left corner, and looks like a little red whirlpool)
  and then find terminal. Once you start a terminal, you can right click on its symbol on the 'launcher' (the stuff on the right hand side of you Ubuntu desktop)
  and lock it there with the 'lock to launcher` command
    
  Now you will need to install the essential tools. This all  needs to be done in a terminal window.  
  
  #. To install git::
  
      sudo apt-get install git
    
  #. To install subversion::
  
      sudo apt-get install subversion 
    
  #. To install a c++ compiler::
  
      sudo apt-get install g++
    
     This seems to install `g++`, `gdb` and `make`, so that is nice. 
     
  #. Get the python package installer, `pip <https://pypi.python.org/pypi/pip>`_::
  
      sudo apt-get install python-pip
      
  #. Install all the really useful python packages (this will take a while)::
  
      sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose
  
  
      