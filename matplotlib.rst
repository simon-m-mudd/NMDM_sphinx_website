==============================================
Creating figures with python: Matplotlib
==============================================

Introduction
======================================

One requirement ubiquitous to all research is the production of figures that can effectively relay your results to the research community, policy makers and/or general public (this fact is unfortunately lost on some people!).  In almost all cases, figures may need to be revised, and you may need to produce plots of multiple datasets that have consistent formatting.  Python is your friend in this regard, providing a powerful library of tools `Matplotlib <http://matplotlib.org/>`_.

Whilst a little awkward to start with, if you tenderly nourish your nascent relationship with Matplotlib, you will find that it will provide a comprehensive range of options for plotting and annotating, with the advantage that if you need to reproduce figures, you can do so at the touch of a button (or a single command for all you Linux types).  For some annotations, such as more complex annotations, it may still be necessary/easier for you to modify the figures in a graphics package.  Fortunately, `Inkscape <https://inkscape.org/en/>`_ provides a nice package that deals with Scalar Vector Graphics (SVG) files, which enables it to sync nicely with your Matplotlib output.  We’ll deal with this later.

In this class, we will be using a python GUI called `Spyder <https://code.google.com/p/spyderlib/>`_, which also gets installed by default with `pythonxy <https://code.google.com/p/pythonxy/>`_.  All of this is available on the University of Edinburgh servers, but if you need to install it, we’d recommend installing Spyder via pythonxy, as for the same effort the latter will also install a whole bunch of useful libraries for scientific computing.

Before we begin, it is worth pointing out that there are many ways of producing the same figure, and there are an infinite number of possible permutations with regards to what kind of figure you might want to produce.  With this in mind, we will try to introduce you to as many different options as is feasible within the confines of this course.  The aim is to give you sufficient knowledge of the commonly used commands for plotting in Matplotlib, so that you can quickly move on to producing your own scripts.  The best way of becoming the proficient Matplotlib wizard that you aspire to be is to practice making your own.  You will never look at an Excel plot in the same way again!

On a final note, one of the wonderful things about Matplotlib is the wealth of information out there to give you a head start.  Check out the `Matplotlib gallery <http://matplotlib.org/gallery.html>`_ for inspiration; source code is provided with each figure  just click on the one you want to replicate; there is also extensive online documentation, a whole load of other websites and blogs from which you can get more information, or if you are really stuck, an active community of Matplotlib users on `Stack Exchange <http://stackexchange.com/>`_.

OK, let’s begin…

Getting Started
=====================================

There are two parts to this tutorial, which can be undertaken independently, so feel free to start whichever one you like the look of.  In Part 1, you will discover the art of 'faking data' and learn to do some basic statistical analyses in addition to some further plotting options.  In Part 2, you will be learning to adjust and annotate figures within matplotlib, and progresses from basic formatting changes to more complex commands that give you an increasing amount of control in how the final figure is laid out and annotated.


Saving Files For Adjusting In Inkscape
=====================================

You have previously been introduced to the savefig() function.  If you save your figures using “.svg” format, then you should be able to reopen and edit your figures in Inkscape or another graphics package::

	plt.savefig(<filename.svg>, format =”svg”)

We are not going to go into much detail on how to use Inkscape specifically as the possibilities are endless and most of you will have prior knowledge of using graphics packages.  However, if you have questions you’d like to ask about this, please see us at the computer lab session.


PART 1- Producing fake data and serious statistical analysis
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




PART 2- Plotting Climate Data
=====================================

Downloading the data
--------------------

OK, so first up we are going to have to download some data.  The figure that we will be generating will display some of the paleo-climate data stretching back over 400kyr, taken from the famous Vostok ice core and first published by Petit et al. (1999).  Conveniently, this data is now freely available from the National Oceanic and Atmospheric Administration (NOAA; http://www.ncdc.noaa.gov/).  It is easy enough to download the data manually, but now that you have been inducted into the wonderful world of Linux, we will do so via the command line.

    * Open a terminal and navigate to your working directory – you may want to create a new directory for this class.

    * Within this working directory, make a subsidiary directory to host the data. I’m going to call mine “VostokIceCoreData”. **Note that you might (should) think about using Version Control for this class, to keep track of changes to your files**.

    * Change directory to the data directory you’ve just created.  In Linux one way (of many) to quickly download files directly from an html link or ftp server is to use the command ``wget``.  We are going to download the Deuterium temperature record::

        - wget ftp://ftp.ncdc.noaa.gov/pub/data/paleo/icecore/antarctica/vostok/deutnat.txt

    * And the oxygen isotope record::

        - wget ftp://ftp.ncdc.noaa.gov/pub/data/paleo/icecore/antarctica/vostok/o18nat.txt

    * And finally the atmospheric CO2 record::

        - wget ftp://ftp.ncdc.noaa.gov/pub/data/paleo/icecore/antarctica/vostok/co2nat.txt

    * The deutnat.txt file has a bunch of information at the start.  For simplicity, it is easiest just to delete this extra information, so that the text file contains only the data columns with the column headers.

    * To get you started we’ve written a starting script that already has functions to read in these data files and produce a basic plot of the data.  Note that there are many ways of doing this, so the way we have scripted these may be different to the way that you/others do so.  If you have a niftier way of doing it then that is great!  Let’s download this script now from my GitHub repository::

	- git clone https://DTMilodowski@bitbucket.org/DTMilodowski/numerical-modelling-and-data-management.git .

The next step is to make some plots.  There are two parts to this: the first will be to plot the ice core data you have just downloaded; the second will be to plot data that you will yourself create alongside some common statistical procedures…


Basic plot
--------------------

Make sure that the data is in the same directory as the plotting script you’ve just downloaded.  Open up Spyder and load the plotting script.  Hit “F5” or click the select “Run” on the drop-down menu and then select the “Run” button.  It should now produce a nice enough looking graph – adequate you might think – but definitely possible to improve on before sharing with the wider world.
Before moving on, make sure that you understand what is going on in each line of the code!


Making this look better
--------------------

Setting axis limits
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First up, we can clip the axes so that they are fitted to the data, removing the whitespace at the right hand side of the plots.  This is easy to do – for each axis instance (e.g. ``ax1``, ``ax2`` … etc.) possible commands are ``set_xlim(<min>,<max>)``, or ``set_xlim(xmin=<value>)`` and ``set_xlim(xmax=<value>)`` for to set one limit only.  ``set_ylim()`` gives you the equivalent functionality for the y axis.  For each of the subplots, use the command::

	ax1.set_xlim(0,420)

You will need to update ``ax1`` for each subplot.

Grids
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Another quick improvement might be to add a grid to the plots to help improve the visualisation.  This is pretty easy once you know the command.  For each axis::

	ax1.grid(True)

Tick Markers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some of the tick markers are too close for comfort.  To adjust these, for the subplot axis that you want to change:

    * First decide on the repeat interval for your labels using the MultipleLocator() function.  Note that this is part of the matplotlib.ticker library, which we imported specifying the prefix tk::

	majorLocator = tk.MultipleLocator(0.5)

    * Setting the major divisions is then easy, once you know the command::

	ax4.yaxis.set_major_locator(majorLocator)

Repeat this for any axes you aren’t happy with.

Labelling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It would also be good to label the subplots with a letter, so that you can easily refer to them if you were to write a caption or within the text of a larger document.  You could do this in Inkscape or another graphics package, but it is easy with Matplotlib too.
We are going to use the annotate tool::

	ax1.annotate('a', xy=(0.05,0.9),  xycoords='axes fraction', backgroundcolor='none', horizontalalignment='left',  verticalalignment='top',  fontsize=10) 

This member function applies the label to the axis we designated ``ax1`` (i.e. the first subplot).  The first argument is the label itself, followed by a series of keyword arguments (``kwargs``).  The first is the xy coordinate, followed by a specification of what these coordinates refer to; in this instance the fraction of the x and y axes respectively.  We then specify the background colour, alignment and font size.  These latter four arguments are optional, and would be replaced by default values if you missed them out.
Try adding labels the rest of the subplots.  Experiment with varying the location etc. until you are happy with the results.


Making this look good
--------------------

The above commands will help improve the quality of your figure, but there are still some significant improvements that can be made.  

Layout Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As the subplots have identical x axes, we can be more efficient with our space if we stack the subplots together and only label the lowermost axis.  To do this there are three steps.

    * First, make an object that contains a reference to each of the tick labels that we want to remove::
	
	xticklabels = ax1.get_xticklabels()+ax2.get_xticklabels()+ax3.get_xticklabels()

    * Next turn these off::

	plt.setp(xticklabels, visible=False)

    * Finally we can use the subplots_adjust() function to reduce the spacing of the subplots::

	plt.subplots_adjust(hspace=0.001)


For some reason we can’t set hspace to 0, hence I have chosen an arbitrarily small number.  Note that using other kwargs here we could change the column spacing (cspace) or the margins.  Ask google for more details if you want to do this.

Switching sides
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now we have stacked the subplots, we have issues with overlapping labels.  This is easily fixed by alternating the axes labels between the left and right hand sides.  To label the second subplot axis on the right hand side rather than the left, use the commands::

	ax2.yaxis.tick_right()
	ax2.yaxis.set_label_position("right")

If we so desired, a similar set of commands could be easily be used for labelling the x axis using the top or bottom axes.

Repeat this for the fourth subplot.

We now have a pretty decent figure, which you might well be happy sharing.  Note that many of these alterations could have been done in Inkscape.  This would almost definitely have been faster in the first iteration.  However, as soon as you need to reproduce anything, the advantages of automating this should hopefully be obvious.


Now let’s zoom into the last Glacial-Interglacial cycle
--------------------

Now we are going to add another subplot to the figure, except this time, we are going to use a subplot that has different dimensions to the previous ones.   Specifically we are going to make a final subplot, in which both the temperature and CO2 data, spanning 130ka-present, are plotted on the same set of axes.  We’ll also include a legend for good measure.

Adding a new subplot with a different size – layout control with the subplot2grid function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

subplot2grid is the new way in which we are going to define the subplots.   It is similar in functionality to the previous subplot, except that we declare a grid of cells, and then tell matplotlib which cells should be used for each subplot.  This gives us more flexibility in terms of the figure layout.   ``I’d suggest scanning this page to get a better idea <http://matplotlib.org/users/gridspec.html>`_.

Now I reckon that in my ideal figure, the above subplots should fit into the upper two thirds of the page.  As a result, we should change the subplot declarations, so that rather than::

	ax1 = plt.subplot(411)

We have::

	ax1 = plt.subplot2grid((6,4),(0,0),colspan=4)

Here, our reference grid has 6 rows and 4 columns.  Each plot fills one row (default) and four columns.  The following subplot axis can then be declared as::
	
	ax2 = plt.subplot2grid((6,4),(1,0),colspan=4)

It now fills the second row (remember that python is 0 indexing)

Try adding the third and fourth rows; plot the results to get an idea for what is going on.

To plot the most recent glacial cycle, I’d like to use a figure that has different dimensions.  Specifically, I want it only to take up three quarters of the total figure width, so that I have space to the side to add a legend.  I also want it to be a bit taller, occupying 5/8ths of the height of the page. I am going to define a new grid with eight rows, rather than six, which we used before.  I guess it would be best to have consistent grid dimensions for everything, but I am feeling lazy at this point. (Note that because of this slight shortcut we can no longer use the ``tight_layout()`` function, so make sure you remove it!)

The subplot declaration looks like this::
	
	ax5 = plt.subplot2grid((8,4),(6,0),colspan=3,rowspan=3)

Run the program again to see where this new axis plots.

Now we will plot the temperature data for 130ka-present::

	ax5.plot(ice_age_deut[ice_age_deut<130000]/1000,deltaTS[ice_age_deut<130000], '-', color="blue", linewidth=1, label=u'$\Delta TS$')

Note that we are using **conditional indexing** here to plot only the data for which the corresponding ice age is < 130ka.  Now you can add axis labels and label the subplot as we did earlier.  Note that we include a label here as the final ``kwarg`` in the list.  This is necessary for producing the legend.

Plotting dual axes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We also want to plot the CO2 data on the same set of axes.  This can be done as follows: rather than making a new subplot, we can use the ``twinx()`` function::

	ax6 = ax5.twinx()

This will now plot ``ax6`` in the same subplot frame as ``ax5``, sharing the x axis, but the y axis for each will be on opposing sides.  Other examples where this is useful are climate data (precipitation and temperature) and discharge records (precipitation/discharge) to name but a couple.

We can now easily plot the CO2 data, again using conditional indexing::

	ax6.plot(ice_age_CO2[ice_age_CO2<130000]/1000,CO2[ice_age_CO2<130000], ':', color="green", linewidth=2, label='$CO_2$')

All that remains is for you to label the axes, adjust the tick locations, set the limits of the x axis and label the subplot and you are almost there.

I find that the following y-limits are pretty good::

	ax6.set_ylim(ymin=150,ymax=300)
	ax5.set_ylim(ymin=-10,ymax=10)

Legends for multiple axes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

One of the last things is to add a legend for this last subplot.  Legends are a little fiddly in matplotlib, especially if you want to make a single legend to cover the lines produced in multiple axes.
Firstly we need to make a couple of adjustments to some earlier code, so that we now give the lines we’d like included in the legend a specific name i.e.::

	line1 = ax5.plot(ice_age_deut[ice_age_deut<130000]/1000,deltaTS[ice_age_deut<130000], '-', color="blue", linewidth=1, label=u'$\Delta TS$')

and::

	line2 = ax6.plot(ice_age_CO2[ice_age_CO2<130000]/1000,CO2[ice_age_CO2<130000], ':', color="green", linewidth=2, label='$CO_2$')

The legend can then be constructed in ax5 with the following three lines of code::

	lines_for_legend=line1+line2
	labels=[l.get_label() for l in lines_for_legend]
	ax5.legend(lines_for_legend,labels,bbox_to_anchor=(1.36,0.66))

VERY nearly finished!  We can do better though!

Annotations – making this look awesome!
--------------------

You might decide to make any further adjustments and annotations manually in Inkscape or another graphics package.  This is fine, and depending on your purposes might actually be better/more efficient, especially if you are going to need to do extensive and complex annotations, as it gets progressively more fiddly to do this in matplotlib.  However, I list below a few examples highlighting some of the tools that matplotlib provides for making your figures shine.

Highlighting a period of interest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The last glacial lasted from ~115ka to ~12ka.  Let’s make the final subplot more exciting by shading this time period a nice, icy cyan colour::

	ax5.axvspan(12, 115, alpha = 0.2, color='cyan')

The ``axvspan()`` function above shades a region between two specified limits on the x axis.  The alpha argument specifies the level of opacity (0=transparent, 1=opaque).

Also, it might be helpful to show on subplot (a) exactly which time period is covered in the final subplot we’ve just created.  We can use the same function to do this::

	ax1.axvspan(0, 130, ymin=0, ymax=0.2, color = '0.0',alpha=0.7)

This time I have added a ``ymin`` and ``ymax`` to restrict the shading to the lowermost 20% of the figure.  Note that the y limits in the axvspan() function must be in terms of axis fraction.
A similar function - ``axhspan()`` – can be used to produce horizontally delimited shaded regions

Written annotations and arrows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can also annotate the plots.  First up, it would be useful to right an annotation into the shaded region in ``ax1`` to refer the reader to the final subplot, which has the zoomed in data::

	ax1.annotate('Panel (e)', xy=(65,-9), xycoords='data', color='white', horizontalalignment='center',  verticalalignment='center',  fontsize=10) 

Unlike the subplot labels, I am using the data coordinates to position the text in this case.  The choice of ``data`` vs. ``axes fraction`` is often pretty arbitrary and will depend on the purpose of the annotation.

Finally, on the final subplot, I’d like to put an arrow marking the location of the LGM at ~26.5ka.  The annotation is identical to before, except that (i) the first ``xy`` coordinates refer to the end points of the arrow, (ii) the text positioning is now given be ``xytext`` and we have to add some info determining the arrow characteristics.  I’m not going to go into the details of these.  The best way of getting a feel for this is experimentation if you need to use this level of annotation::

	ax5.annotate('Last Glacial Maximum', xy=(26.5, -7), xycoords='data', xytext=(0.5, 0.7), textcoords='axes fraction', horizontalalignment='right', verticalalignment='top', fontsize = 10, arrowprops=dict(arrowstyle="fancy", facecolor="gold", edgecolor="black", linewidth=0.25, shrinkB=4, connectionstyle="arc3,rad=0.1",))

Filling between two lines using fill_between
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The very last thing that I am going to take you through is an introduction to the ``fill_between()`` function.  This essentially enables you to shade between two regions.  For example, you might wish to shade the region bounding the uncertainty in your model output.  In this case, I am going to shade between the x axis and the relative temperature change shown in subplot (a).
Specifically areas that are negative (colder than present) will be shaded beneath the x axis, and coloured blue; areas that are positive (warmer than present) will be shaded red.  We need two lines of code::

	ax1.fill_between(ice_age_deut/1000, 0, deltaTS, where=deltaTS<=0, color="blue", alpha = 0.5) 
	ax1.fill_between(ice_age_deut/1000, 0, deltaTS, where=deltaTS>0, color="red", alpha = 0.5)

Essentially I am filling along the x axis (first argument), between 0 and the line deltaTS, for regions where deltaTS meets the given criteria.  A bit fiddly, but the results are good!
Well done for making it this far!





