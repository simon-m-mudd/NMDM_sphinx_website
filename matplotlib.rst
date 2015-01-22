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

In the following, ``av_mole`` refers to the average number of moles per square meter of garden. We want to know if this variable is correlated to the Health Index of Gardeners, commonly denoted ``HIG``. This index varies between zero (optimal health condition, bliss) and 10 (extreme health issues due to stress, eventually leading to premature death). 
 

To begin, create a new, empty python file to write this code. 
Import the packages (using the ``import`` command) that will be needed for this exercise::

     import numpy as np
     import matplotlib.pyplot as plt
     from scipy import stats

Now, to generate the data, you could simply use a vector of values with a linear increment (for ``av_mole``) and transform this using a given function. But the result would be way too smooth and nobody will believe you. Real data is messy. This is mostly due to the multitude of processes that interact in the real world and inluence your variable of interest to varying degrees. For instance, the mole population will be subject to worm availability, soil type, flooding events, vegetations and so on. All these environmental parameters add a noise to the signal of interest, that is ``av_mole``. 

So to generate noisy data, we will use a random number generator::

     N = 50
     av_mole = np.random.rand(N)

The function ``random.rand(N)`` creates an array of size N and propagate it with random samples from a uniform distribution over [0, 1).

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

      ax.errorbar(av_mole, HIG, xerr=mole_error, yerr=hig_error, fmt='o',color='b')   

And add the labels and title::

      plt.xlabel('Average number of moles per sq. meter', fontsize = 18)
      plt.ylabel('Health Index for Gardeners (HIG)', fontsize = 18)
      plt.title('Mole population against gardeners health', fontsize = 24)  


Now we clearly see that the mole population seems to be linearly correlated with the HIG. The next step is to assess this correlation by performing a linear regression. 


Linear regression
--------------------
Fortunately, the great majority of the most commonly used statistical functions are already coded in python. You just need to know the name of the tool you need. For the linear regression, there are several functions that would do the job, but the most straightforward is ``linregress`` from the ``stats`` package. This is one way to call the function, and at the same time define the parameters associated with the linear regression::

      slope, intercept, r_value, p_value, std_err = stats.linregress(av_mole, HIG)

The linear regression tool will find the equation of the best fitted line for your dataset. This equation is entirely defined by the ``slope`` and ``intercept``, and can be written as: HIG = slope * av_mole + intercept.

You can display these parameters on your workspace in python using the ``print`` command::

      print 'slope = ', slope
      print 'intercept = ', intercept
      print 'r value = ', r_value
      print  'p value = ', p_value
      print 'standard error = ', std_err

The values of r, p and the standard error evaluate the quality of the fit between your data and the linear regression. To display the modeled line on your figure::
 
      line = slope*av_mole+intercept
      plt.plot(av_mole,line,'m-')
      plt.title('Linear fit y(x)=ax+b, with a='+str('%.1f' % slope)+' and b='+str('%.1f' % intercept), fontsize = 24) 


Boxplot, histogram and other stats
------------------------------------
If you want to learn more about your data, it can be very useful to plot the histogram or probability density function associated to your dataset. You can also plot the boxplots to display the median, standard deviation and other useful information.
Try to create one (or both) of these plots, either in a subplot under your first figure, or in an embedded plot (figure within the figure). 
 
You can use ``plt.boxplot`` to create the boxplot and ``plt.hist`` for the histogram and probability density function (depending on the parameters of the function). 

