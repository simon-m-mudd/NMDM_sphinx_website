==============================================
Creating figures with python: Matplotlib
==============================================

Introduction
======================================

One requirement ubiquitous to all research is the production of figures that can effectively (this is unfortunately lost on some people!) relay your results to the research community, policy makers and/or general public.  In almost all cases, figures may need to be revised, and you may need to produce plots of multiple datasets that have consistent formatting.  Python is your friend in this regard, providing a powerful library of tools `Matplotlib <http://matplotlib.org/>`_.

Whilst a little awkward to start with, if you tenderly nourish your nascent relationship with Matplotlib, you will find that it will provide a comprehensive range of options for plotting and annotating, with the advantage that if you need to reproduce figures, you can do so at the touch of a button (or a single command for all you Linux types).  For some annotations, such as more complex annotations, it may still be necessary/easier for you to modify the figures in a graphics package.  Fortunately, `Inkscape <https://inkscape.org/en/>_` provides a nice package that deals with Scalar Vector Graphics (SVG) files, which enables it to sync nicely with your Matplotlib output.  We’ll deal with this later.

In this class, we will be using a python GUI called `Spyder <https://code.google.com/p/spyderlib/>_`, which also gets installed by default with `pythonxy <https://code.google.com/p/pythonxy/>_`.  All of this is available on the University of Edinburgh servers, but if you need to install it, we’d recommend installing Spyder via pythonxy, as for the same effort the latter will also install a whole bunch of useful libraries for scientific computing.

Before we begin, it is worth pointing out that there are many ways of producing the same figure, and there are an infinite number of possible permutations with regards to what kind of figure you might want to produce.  With this in mind, we will try to introduce you to as many different options as is feasible within the confines of this course.  The aim is to give you sufficient knowledge of the commonly used commands for plotting in Matplotlib, so that you can quickly move on to producing your own scripts.  The best way of becoming the proficient Matplotlib wizard that you aspire to be is to practice making your own.  You will never look at an Excel plot in the same way again!
On a final note, one of the wonderful things about Matplotlib is the wealth of information out there to give you a head start.  Check out the `Matplotlib gallery <http://matplotlib.org/gallery.html>_` for inspiration; source code is provided with each figure  just click on the one you want to use; there is also extensive online documentation, a whole load of other websites and blogs from which you can get more information, or if you are really stuck, an active community of Matplotlib users on `Stack Exchange <http://stackexchange.com/>_`.

OK, let’s begin…

PART 1- Plotting climate data
=====================================

Getting started
--------------------




PART 2- Producing fake data and serious statistical analysis
=================================================

In this section, we use a random number generator to create a dataset, and then learn how to plot the data with a maximum amount of information in one plot. Useful information such as error bars and a linear regression are detailed. 
For the adventurous ones, you may want to explore a bit more and create additional plots such as a probability density function of the data or a boxplot. 

The art of faking data
------------------------
Create a new, empty python file to write this code. 



Scatter plot, error bars and additional information
-----------------------------------------------------



Linear regression
--------------------




Boxplot, histogram and other stats
------------------------------------


