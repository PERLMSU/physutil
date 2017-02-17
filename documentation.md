---
layout: page
title: Documentation
permalink: /documentation/
---

PhysUtil has several tools that can help new modelers develop highly visual simulations:

* MotionMap
* PhysGraph
* PhysTimer
* PhysAxis
* csvFunctions

## MotionMap

In this section we describe the MotionMap class which assists students in constructing motion maps using either arrows (measuring a quantity) or “breadcrumbs” (with timestamps).

### Setting Up the Motion Map
Here is an example of how to set up a simple motion map:

```
from physutil import *

#Create the object to be in motion and set its velocity
cart = box(pos=vector(-1.0,0,0), size=(0.1,0.04,0.06), color=color.green)

vcart = vector(0.5,0,0)

#Set up timing data
deltat = 0.01
t = 0
tf = 4

#Set up motion map
motionMap = MotionMap(cart, tf, 5, markerScale=0.5)
```

Importing from physutil makes all the Physics utility tools including the MotionMap class available for use in the current program.

This example sets up a motion map set to track the “cart” object. The timing data is set up for when the cart is eventually put into motion. The variable ''tf'' represents the expected tFinal or the time when the motion is set to stop, and it is necessary in the motion map instantiation in order to space marker placement over time. The variable ''5'' designates the number of markers to be placed during the duration of the object’s motion. The variable ''markerScale'' designates the size of the markers to be placed (the default is ''markerScale=1''). If code were then added to this program that put the object in motion via a while loop and the program was run, the graphic display window display something similar to this at the end of the object’s motion:

![MotionMap Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/motionmap.png)

This motion map image shows that the green “cart” object has moved from left to right and dropped 5 red arrow markers throughout the duration of the motion. Notice that by default the motion map used red arrow markers labeled in numerical order. This next example shows how to set up a more complex motion map and how to change these defaults:


```
motionMap = MotionMap(cart, tf, 5, markerType=”breadcrumbs”, markerColor=color.blue, labelMarkerOrder=False, dropTime=true, timeOffset=vector(0,1,0))
```

In this example a motion map is created that tracks the motion of the “cart” object by dropping 5 blue “breadcrumbs.” The variable ''markerType'' designates the type of markers to be dropped on the motion map. The two marker types are ''“arrow”'' which are the default type, and ''“breadcrumbs”'' which are basically points. The variable ''markerColor'' sets the color of the markers being dropped. The variable ''labelMarkerOrder'' toggles on and off the numerical labeling of the order of the markers. The default value of ''labelMarkerOrder'' is ''True'' which turns the labels on, so in this example they are turned off. The variable ''dropTime'' determines whether a timestamp is placed along with the markers (this parameter is set to ''False'' by default). The variable ''timeOffset'' is only active if ''dropTime'' is set to ''True'' and it determines a vector by which to offset the timestamp label from the marker. If an object were set in motion within the motion map set up in this example then the graphic display window would look similar to the following:

![Breadcrumbs Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/breadcrumbs.png)

### Updating MotionMap in a Loop

In order to see your motion map you must update the motion map in a while loop. If your motion map is an arrow motion map, then your ''update'' function must have two parameters: the time ''t'' and the vector quantity being mapped by the arrows. The following is an example of what an ''update'' call would look like for the first example above:

```
motionMap.update(t, vcart)
```

In this example, the arrows map the vector quantity ''vcart'' representing the “cart” object’s velocity.

If your motion map is a breadcrumb map, then your ''update'' function only needs the time parameter. The following is an example of what an ''update'' call would look like for the second example above:

```
motionMap.update(t)
```

## PhysGraph

In this section we describe the PhysGraph class which assists students in creating dynamic graphs with advanced functionality.

### Setting Up the Graph

Here is an example of how to set up a simple graph:

```
from physutil import *
from visual.graph import *

graphExample = PhysGraph(numPlots=1)
```

Importing from physutil makes all the Physics utility tools including the PhysGraph available for use in the current program and visual.graph makes available all Visual objects plus the graph plotting module.

The variable ''numPlots'' represents the number of dependent variables that you want to plot in relation to the dependent variable.  However, this variable is optional.  If you do not type anything, the program will only make one plot by default.  The lines of code below are all synonymous and work equally well for only one plot.

```
graphExample = PhysGraph(numPlots=1)
graphExample = PhysGraph(1)
graphExample = PhysGraph()
```

### Updating PhysGraph in a Loop

In order to see your graph you will need to update PhysGraph in the while loop. To plot the cart object’s x-position vs. time (t) using PhysGraph, type this in the loop:

```
graphExample.plot(t, cart.pos.x)
```

![Graphing Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/graph.png)

### Creating Multiple Plots on Graph
If you want to create multiple plots, first specify how many plots you want PhysGraph to create.  In this example we want it to print two plots:

```
graphExample = PhysGraph(2)
```

Then, specify which values you want PhysGraph to plot in the while loop.  In this example it will plot the cart’s x-position (this values would have to be instantiated earlier in the code) compared to time (t).  It also draws a horizontal line at 2:

```
graphExample.plot(t, cart.pos.x, 2)
```

![Graphing Window 2](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/graph2.png)

By default, colors for each plot are chosen in this order: starting with red, green, blue, yellow, orange, cyan, magenta, and finally white.

### Formatting the Plots
Many of the vPython plotting options have been enumerated in PhysGraph.
By adding the following arguments to the initial call to PhysGraph you can change those parameters.

**title='...some text...'**<br>
Use this parameter to add a title to the plotting window.<br>
<br>
<b>xlabel='...some text...'</b><br>
Use this parameter to add a title to the x-axis.<br>
<br>
<b>ylabel='...some text...'</b><br>
Use this parameter to add a title to the y-axis.<br>
<br>
<b>backgroundColor = XXX</b><br>
Use this parameter to change the background color of the plots.  The default color is white.  You can either specify some standard colors using the color.white, color.red, etc. key-words or by specifying an RGB tupple [0-1,0-1,0-1].<br>
<br>
<b>graphColors=</b><br>
Use this parameter to specify the color order of the plots being displayed.  The list may include color key-words (color.red, etc.) or RGB tupples [0-1,0-1,0-1].<br>
<br>
<b>radius= ###</b><br>
Size of the curve being drawn in the plot.  The units are in terms of the scale of the window.  The default is radius=0.015.  A value of radius=0 will tell the plotting system to simply plot a 1 pixel wide line, independent of the plot scale.<br>
<br>
<b>dot= True/False</b><br>
Specify if the data points should be plotted.<br>
<br>
<b>dot_size= #</b><br>
Size, in pixels, of data points if dot=True is specified.  Default is dot_size=8.

## PhysTimer


In this section we will describe the PhysTimer class which keeps track of the current time and displays it in the simulation's window.

### Setting up the Timer

Here is an example of how to set up the timer:

```
from physutil import *

# Sets timer in top right of screen
timerDisplay = PhysTimer(2, 5, useScientific=False)
```

Importing from physutil makes all the Physics utility tools including the PhysTimer available for use in the current program.

In this example, the timer will be displayed at x-coordinate “2” and y-coordinate “5.”  By default, the timer is displayed in HH:MM:SS:DD format -- hours, minutes, seconds, and 1/100 of a second format. This format is communicated to the computer when you type ''useScientific=False''.  The timer will appear in a similar fashion to the screenshot below.

![Timer Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/timer.png)

Since only the first two variables are expected it isn’t necessary to type ''useScientific=False'' when trying to display the timer in HH:MM:SS:DD format.  The line of code:

```
timerDisplay = PhysTimer(2, 5, useScientific=False)
```

works exactly the same as:

```
timerDisplay = PhysTimer(2, 5)
```

because this representation is the default behavior.

### Update PhysTimer in Loop

In order to display the current time in the simulation window, the timer has to be updated within the while loop.  Here is how you update timerDisplay:

```
timerDisplay.update(t)
```

### Displaying Timer in Scientific Notation

PhysTimer can also be displayed in scientific notation instead of HH:MM:SS:DD format.  To do this, type:

```
timerDisplay = PhysTimer(2, 5, useScientific=True)
```

In the simulation window you will see a timer displayed at x-position 2 and y-position 5.  Changing ''useScientific=True'' to ''useScientific=False'' will make the timer display in HH:MM:SS:DD format (this is the default).  A screenshot of how the scientific notation format will look can be seen below.



![Scientific Timer Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/scitimer.png)

## PhysAxis

In this section we describe the PhysAxis class which assists students in creating dynamic axes for their models.

### Setting Up the Axis

Here is an example of how to set up a simple axis:

```
from physutil import *

track = box(pos=vector(0,-0.05,0), size=(5.0,0.05,0.10), color=color.white)
axis = PhysAxis(track, 10)
```

Importing from physutil makes all the Physics utility tools including the PhysAxis available for use in the current program.

In this example an axis is created that is oriented based on the “track” object and has “10” labels on it. The following image shows what this should look like in the graphic display window:

![X-Axis Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/x-axis.png)

PhysAxis has many more parameters than just the object that it is based on and the number of labels that it has. Here is a more complex example:

```
axis2 = PhysAxis(track, 10, axisType="arbitrary", labels=(1,2,3,"four",5,6,7,8,9,10), axis=vector(1,1,0))
```

which creates the following in the graphic display window:

![45 Degree Axis Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/axis-45.png)

In this example an “arbitrary” axis with 10 labels based on the “track” object is created. The parameter ''axisType=”arbitrary”'' makes the axis arbitrary meaning that the user can set arbitrary labels to be displayed along the axis and set an arbitrary orientation for the axis. The parameter ''labels=(1,200,3,”four”,5,6,70,8,9,10)'' defines the values to be displayed as the 10 labels along the axis. As you can see, these values may be strings as well as numbers. The ''labels'' parameter may also be set equal to zero if no labels are desired. The parameter ''axis=vector(1,1,0)'' sets (1,1,0) as the unit vector that defines the orientation of the axis.

The ''axisType'' parameter may also be set to ''“x”'' (which causes axis labels to be the x-coordinates and orients the axis along the vector (1,0,0)) or ''“y”'' (which causes the axis labels to be the y-coordinates and orients the axis along the vector (0,1,0)).

The default ''axisType'' is ''“x”'' thus making the ''axis'' parameter equal to ''vector(1,0,0)'' by default. Because these are the default values, they do not need to be explicitly stated every time you want to create a PhysAxis of ''axisType= “x”''. Therefore all three of the following lines are equivalent:

```
axis = PhysAxis(track, 10, axisType=”x”, axis=vector(1,0,0))

axis = PhysAxis(track, 10, axisType=”x”)

axis = PhysAxis(track, 10)
```

Here is an example of how to create an axis with a different start position:

```
axis = PhysAxis(track, 10, startPos=vector(-1, 1, 0))
```

In this example an axis with 10 labels based along the “track” object is created starting at (-1, 1, 0). By default ''startPos=vector(-obj\_size(obj).x/2,-4\*obj\_size(obj).y,0)'' ((The “obj” object refers to the object that the PhysAxis is oriented along, so in these examples the “track” object.)).

The following screenshot displays the default position of the axis below the “track” object and then the altered axis position above the “track” object from the example above:


![Axis 2 Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/axis2.png)

The following example shows how to change the length of the axis being created:

```
axis = PhysAxis(track, 10, length=7.5)
```
![Long Axis Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/axis-long.png)

In this example an axis with 10 labels oriented along the “track” object is created that is 10 units long. The ''length'' parameter may be used to define how long the axis created is. By default ''length'' is set to the length of the object along which the axis is oriented, in this case ''obj-size(track).x''.

The following example demonstrates how to change how labels are placed relative to axis markers along the axis:

```
axis = PhysAxis(track, 10, labelOrientation=”up”)
```

![Axis Label Window](https://raw.github.com/perlatmsu/python-physutil/master/screenshots/axis-label.png)

In this example an axis with 10 labels oriented along the “track” object is created with the labels oriented above the markers along the axis. The parameter ''labelOrientation=”up”'' places the labels above the markers. The options for labelOrientation are ''“down”'', ''“up”'', ''“left”'', or ''“right”'' which orient the labels accordingly. The default ''labelOrientation'' is ''“down”''.

### Updating PhysAxis in a Loop

In order to determine if the reference object has shifted and therefore whether the PhysAxis should be shifted as well, the PhysAxis must be updated within the while loop. Here is how to update the axis:

```
axis.update()
```

### Reorienting PhysAxis

The ''reorient()'' function allows axes to be modified during a simulation to reflect various aspects of the object they are serving as an axis for. For example, if one wanted an axis which points in the direction of the force of an object and whose length matches the force's magnitude, calling ''axis.update()'' would be insufficient as this would merely move the existing axis as a whole; this is where ''reorient()'' comes in.

The ''reorient()'' function takes a subset of the parameters that can be given to the initial constructor of PhysAxis, specifically:

```
axis=None, startPos=None, length=None, labels=None, labelOrientation=None
```

As you can see all of these parameters are set to ''None'' by default meaning that their default behavior is to not change any of the current values of the axis that ''reorient()'' is called on. This means that if you were to call ''axis.reorient()'' with no parameters this would effectively recreate the axis without changing anything about it. The following example shows how the axis works to alter certain parameters of the axis:

```
axis.reorient(length=50, labelOrientation=”left”)
```

In this example the ''reorient'' call updates the ''length'' parameter to 50 making the axis 50 units long and it updates the ''labelOrientation'' parameter to ''“left”'' moving the axis labels to the left of the markers. These are the only two parameters that ''reorient'' changes in this example.

The ''reorient()'' function allows you to change any or all of the parameters ''axis'', ''startPos'', ''length'', ''labels'', and ''labelOrientation'' during a simulation and recreates the axis with the updated parameters.

## csvFunctions

PhysUtil has built in functions for easily reading and writing csv (comma-separated-value) files.  Unlike the cvs library included with python, these functions have a simplified syntax that is independent of python version ( i.e. they work for both python 2.x and 3.x).


#### Reading from and Writing to CSV

**readcsv()**

[Col1, ...] = readcsv(filename, cols=1, IgnoreHeader=False, startrow = 0, NumericData=True)

To read data from a csv file, the user simply specifies the file and the number of columns.  If the csv file has a header in the first row they can included IgnoreHeader = True (default=False).  Alternatively the can use the startrow to specify the row the data starts in (default=0).  NumericData allows the user to specify if the data should be converted to a float or left as text (default=True, i.e. convert to float).

**writecsv()**

writecsv('filename.csv', [X,Y,...], header=['one','two',...])

To save a csv file, the user first specifies the location/name of the file to be saved.  Next, in the second parameter, they supply the lists of values (numeric or text) that they want to form the columns of the file.  Alternatively, they can specify a numpy array (see numpy documentation for details on that structure).  If desired, they can pass a header to be included at the top of the columns.
The function is smart enough to make sure that the number of rows in
each list are the same, and that the number of headers match the
number of lists.  If either of those conditions aren't met, it will
display some errors telling the user what they did wrong.
