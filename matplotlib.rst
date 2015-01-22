==============================================
Creating figures with python: Matplotlib
==============================================

Introduction
======================================

One requirement ubiquitous to all research is the production of figures that can effectively (this is unfortunately lost on some people!) relay your results to the research community, policy makers and/or general public.  In almost all cases, figures may need to be revised, and you may need to produce plots of multiple datasets that have consistent formatting.  Python is your friend in this regard, providing a powerful library of tools `Matplotlib <http://matplotlib.org/>`_.

Whilst a little awkward to start with, if you tenderly nourish your nascent relationship with Matplotlib, you will find that it will provide a comprehensive range of options for plotting and annotating, with the advantage that if you need to reproduce figures, you can do so at the touch of a button (or a single command for all you Linux types).  For some annotations, such as more complex annotations, it may still be necessary/easier for you to modify the figures in a graphics package.  Fortunately, `Inkscape <https://inkscape.org/en/>`_ provides a nice package that deals with Scalar Vector Graphics (SVG) files, which enables it to sync nicely with your Matplotlib output.  We’ll deal with this later.

In this class, we will be using a python GUI called `Spyder <https://code.google.com/p/spyderlib/>`_, which also gets installed by default with `pythonxy <https://code.google.com/p/pythonxy/>`_.  All of this is available on the University of Edinburgh servers, but if you need to install it, we’d recommend installing Spyder via pythonxy, as for the same effort the latter will also install a whole bunch of useful libraries for scientific computing.

Before we begin, it is worth pointing out that there are many ways of producing the same figure, and there are an infinite number of possible permutations with regards to what kind of figure you might want to produce.  With this in mind, we will try to introduce you to as many different options as is feasible within the confines of this course.  The aim is to give you sufficient knowledge of the commonly used commands for plotting in Matplotlib, so that you can quickly move on to producing your own scripts.  The best way of becoming the proficient Matplotlib wizard that you aspire to be is to practice making your own.  You will never look at an Excel plot in the same way again!
On a final note, one of the wonderful things about Matplotlib is the wealth of information out there to give you a head start.  Check out the `Matplotlib gallery <http://matplotlib.org/gallery.html>`_ for inspiration; source code is provided with each figure  just click on the one you want to use; there is also extensive online documentation, a whole load of other websites and blogs from which you can get more information, or if you are really stuck, an active community of Matplotlib users on `Stack Exchange <http://stackexchange.com/>`_.

OK, let’s begin…

PART 1- Plotting climate data
=====================================

Getting started
--------------------




PART 2- Producing fake data and serious statistical analysis
=================================================

In this section, we use a random number generator to create a dataset, and then learn how to plot the data with a maximum amount of information in one plot. Useful information such as error bars and a linear regression are detailed. By doing this exercise, you will also learn more about moles, their needs and dreams, and their potential impact on the environment.

For the adventurous ones, you may want to explore a bit more and create additional plots such as a probability density function of the data or a boxplot. 

The art of faking data
------------------------
Let's say I want to study the influence of moles on stress-related health issues in a part of the human population, gardeners for instance. Collecting this type of data can be very complex and will surely take a lot of time and money. So we will just assume that we did the study and fake the data instead. 

At this point, I should probably point out that "fake data" can be a very serious topic and that is is the basis of many useful and relevant research branches, like stochastic hydrology for instance.

In the following, ``av_mole`` refers to the average number of moles per square meter of garden. We want to know if this variable is correlated to the health index of gardeners, commonly denoted ``HIG``. This index varies between zero (optimal health condition, bliss) and 10 (extreme health issues due to stress, eventually leading to premature death). 
 

To begin, create a new, empty python file to write this code. 
Add a few import commands that will be needed for this exercise::

     import numpy as np
     import matplotlib.pyplot as plt
     from scipy import stats

Now, to generate the data, you could simply use a vector of values with a linear increment (for ``av_mole``) and transform this using a given function. But the result would be way too smooth and nobody will believe you. Real data is messy. This is mostly due to the multitude of processes that interact in the real world and inluence your variable of interest to varying degrees. For instance, the mole population will be subject to worm availability, soil type, flooding events, vegetations and so on. All these environmental parameters add a noise to the signal of interest, that is ``av_mole``. 

So to generate noisy data, we will use a random number generator::

     N = 50
     av_mole = np.random.rand(N)

The function ``random.rand(N)`` create an array of size N and propagate it with random samples from a uniform distribution over [0, 1).

Now let's create the ``HIG`` variable::

      HIG = 1+2*np.exp(x)+x*x+np.random.rand(N)
      area = np.pi * (15 * np.random.rand(N))**2     

A third variable called ``area`` (also fake, of course) gives the size of the 50 fields that were studied to provide the data. We now create the error associated to each variable::

      mole_error = 0.1 + 0.1*np.sqrt(x)
      hig_error = 0.1 + 0.2*np.sqrt(y)/10


Scatter plot, error bars and additional information
-----------------------------------------------------
We now want to plot ``av_mole`` against ``HIG`` to see if these two varaibles are correlated. 
First create the figure by typing::

      fig = plt.figure(1, facecolor='white',figsize=(10,7.5))    
      ax = plt.subplot(1,1,1)

Then use the ``scatter`` function to plot the data. You can play with the different options such as the color, size of the points and so on. Here I define the color of each data point according to the area of the field studied::

      obj = ax.scatter(av_mole, HIG, s=70, c=area, marker='o',cmap=plt.cm.jet, zorder=10)
      cb = plt.colorbar(obj)
      cb.set_label('Field Area (m2)',fontsize=20)

Then we add the error bars using this function::

      ax.errorbar(x, y, xerr=mole_error, yerr=hig_error, fmt='o',color='b')   

And add labels and title::

      plt.xlabel('Average number of moles per sq. meter', fontsize = 18)
      plt.ylabel('Health Index for Gardeners (HIG)', fontsize = 18)
      plt.title('Mole population against gardeners health', fontsize = 24)  


Linear regression
--------------------




Boxplot, histogram and other stats
------------------------------------


