# Turtle Drawing
## Start with drawing some shapes. 

Let's examine the draw.py program in the window on the left:<br>
`import turtle` tells Python to load a whole bunch of functions that allow us to create turtles and move them around. <br>
`win = turtle.Screen()` creates and opens a new window that we are calling **win**. Every window contains a canvas that is the part of the window a turtle can move around in and draw on.<br>
`alex = turtle.Turtle()` creates a turtle that we are calling **alex**. Technically, alex is a variable that refers to this new turtle.<br>
`turtle.done()` tells the computer that the program is finished and that the turtle should start drawing. Put all your code before this line.<br> 
<br>
<h4>Turtle commands</h4>
`forward (`distance in pixels`)` makes a turtle go forward some distance. <br>
example: `alex.forward(50)` will make the turtle called alex move forward 50 pixels<br>
`backward` works in much the same way<br>
<br>
`right (`degrees`)` makes a turtle turn to the right some number of degrees<br>
example: `alex.right(45)` will make the turtle called alex turn right 45 degrees<br>
`left` works in much the same way<br>
<br>
[Click here for more Turtle commands](https://lab.cs50.io/martybillingsleyucls/uclsPython/master/turtleDraw/turtleReference.pdf) <br>
<br>
<h4>Try it out</h4>
Add commands to make alex move and turn and move again.<br>
To run your program, type `python draw.py` in the terminal window at the bottom of your screen.<br>


{% spoiler "Help" %}
Add these lines to the program draw.py, after the line `alex = turtle.Turtle()` and before the line `turtle.done()`:<br><br>
`alex.forward(50)`<br>
`alex.right(90)`<br>
`alex.forward(30)`<br>
`alex.left(45)`<br>
`alex.forward(50)`<br>
The turtle should draw a shape that looks like this:<br>
![First drawing](https://raw.githubusercontent.com/martybillingsleyucls/uclsPython/master/images/turtleDraw1.png) <br>
{% endspoiler %}



{% next  %}

## Make the turtle draw a square

Change your commands so that the turtle named alex draws a square.
{% spoiler "Help" %}
The answers to these questions might help you:  
how many sides does a square have?  
how many degrees is each angle in a square?  

{% endspoiler %}

<h4>How many lines of code did you have to write?</h4>
Did you find yourself typing the same lines over and over again?  
In Python, you can use a loop to do something over and over again.  
(point to intro/review of for loops)
