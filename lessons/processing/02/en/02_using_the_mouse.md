# Using your computer’s mouse
## The basics for designing interactive programmes

> After a short introduction to the concept of the draw-loop for creating infinitely running programmes, this lesson will focus on mouse interactions, especially the use of the mouse position and mouse buttons.

---

### Setting the stage: The draw-loop

Processing essentially differentiates between two application modes: _static_ and _active_. So far, we have only worked in the _static_ mode, which is why all applications we have written until now ended on completition. Your sketch’s visual result was shown in its window, but there was no way of manipulating the content afterwards. We have to add new components to our programme in order to create continuously running applications. These components are called _blocks_:

 * block 1: **setup()** runs once, immediately after the programme starts
 * block 2: **draw()** runs in a loop after **setup()** finishes and until the user ends the application

If both blocks are present in the programme it will first execute everything between the curly braces of the **setup()** block. After this has finished, the programme will move on to the **draw()** block and execute its contents in a continuous loop. Effectively, this means if the execution has arrived at the last line within the block, it will start again at the first.

###### Example: continously running programmes (loops)
```processing
// run in a loop until the
// user ends the execution
void draw () {
  fill (255, 0, 0, 1);
  rect (10, 10, 80, 80);
}
```

This programme will draw an almost completely transparent red square to the canvas, 60 times a second. The transparent rectangles are overlayed on top of each other, slowly adding up to one opague shape.

###### Example: Initialization & loop
```processing
// run once when the
// programme starts
void setup () {
  fill (0, 125, 0, 50);
  rect (40, 40, 20, 20);
}

// run in a loop until the
// user ends the execution
void draw () {
  fill (255, 0, 0, 4);
  rect (10, 10, 80, 80);
}
```

In the **setup()** block, the fill color is first set to green and a rectangle is drawn once using this color. After this has finished, the programme continues to execute the **draw()** block in a loop until the user ends the application. With the effect that a very transparent red rectangle is repeatedly drawn to the canvas until the green rectangle gets almost completely covered.

Without using **setup()** and **draw()** this would could be expressed as follows:

```processing
// all commands from the setup() block
fill (0, 125, 0, 50);
rect (40, 40, 20, 20);
// iterations from the draw() loop, one after the other
// iteration 1
fill (255, 0, 0, 4);
rect (10, 10, 80, 80);
// iteration 2
fill (255, 0, 0, 4);
rect (10, 10, 80, 80);
// iteration 3
// ...
```

We can refer to one iteration as a [frame](https://en.wikipedia.org/wiki/Film_frame) (originating from film and animation). Processing will try to create and draw 60 frames per second to the sketch’s canvas. This rate is simply referred to as: [frameRate](http://processing.org/reference/frameRate_.html) in Processing.

  * **frameRate** contains the approximate frame rate of a running sketch.
  * **frameRate()** specifies the number of frames to be displayed every second. This effectively refers to the number of times the **draw()** block is being run per second. Processing will try to stay as close to the requested frameRate as possible.

###### Example.: frameRate
```processing
void setup () {
  // festlegung der Bildrate auf ein 
  // Bild pro Sekunde
  frameRate (1);
}

void draw () {
   fill (255, 0, 0, 15);
   rect (20, 20, 60, 60);
}
```

### Mouse Interaction
#### Mouse Position
Users can interact with your programs in multiple ways. This section focuses on using the mouse, more specifically its position within the canvas. Processing offers four keywords to access different mouse positions: [mouseX](http://processing.org/reference/mouseX.html), [mouseY](http://processing.org/reference/mouseY.html) for the current mouse position and [pmouseX](http://processing.org/reference/pmouseX.html), [pmouseY](http://processing.org/reference/pmouseY.html) for the mouse’s position in the previous frame. All four keywords represent the numerical value of the distance of the mouse on each axis from the center of the coordinate system (top left) in pixels.

###### Example: current mouse position 1
```processing
void draw() {
  ellipse(mouseX, mouseY, 20, 20);
}
```

A circle will be drawn in every **draw()** loop at the current mouse position. Newer circles will overlap older ones.

###### Example: current mouse position 2
```processing
void draw() {
  background(255, 255, 255);
  ellipse(mouseX, mouseY, 20, 20);
}
```

Through the use of the [background()](http://processing.org/reference/background_.html) command the canvas will be painted completely white before each circle is drawn. This gives the impression of one circle following the mouse.

###### Example: current and previous mouse position
```processing
void setup() {
    frameRate(5);
}

void draw() {
  background(255, 255, 255);
  line(pmouseX, pmouseY, mouseX, mouseY);
}
```

If the mouse is moved quickley a black line will appear. This line will be drawn between the current and the previous mouse position and represents the distance of the mouse position between two successive frames. The "p" in both keywords, pmouseX and pmouseY, is short for *previous*.

#### Mouse Buttons
In Processing, we can simply "request" a mouse button’s state in order to determine if it is pressed or not. To do so we can use a new type of command:

  * **[if](http://processing.org/reference/if.html) (** *condition* **) {...}**, literally meaning "if" a certain condition is "true", execute all the code between the curly brackets

To determine if a mouse button is pressed or not, we can use another new keyword similar to the [width](http://processing.org/reference/width.html) or [height](http://processing.org/reference/height.html) keywords.

* **[mousePressed](http://processing.org/reference/mousePressed.html)**, is the left mouse button pressed or not.

The following example illustrates it usage:

###### Example: mouse button pressed 1
```processing
// we’ll simply add the conditional to determine 
// the mouse button state to the drawing block
void draw() {
  // paint the background white
  background(255, 255, 255);

  // if the left mouse button is pressed:
  if (mousePressed) {
    // draw an ellipse at the mouse’s position
    ellipse(mouseX, mouseY, 10, 10);
  }

  // this part will be executed regardless of 
  // the mouse button’s state
  rect(90, 90, 10, 10);
}
```

An [if](http://processing.org/reference/if.html)-conditional always distinguishes between either "yes" ("true") or "no" ("false"). There is no "maybe" obviously, since such a case is highly unlikely for a simple mouse button. In the example above we have given the mouse button state as the condition for the if-clause and will draw a circle this the condition happens to be "true". We can also define a block of code which is only executed if the mouse button is not pressed ("false").

  * **[else](http://processing.org/reference/else.html) {...}** defines a code block which is executed if the [if](http://processing.org/reference/if.html)-condition evaluates to "false". This block is also enclose by two curly brackets.

###### Bsp.: mouse button pressed 2
```processing
void draw() {
  // paint the background white
  background(255, 255, 255);

  // if the left mouse button is pressed:
  if (mousePressed) {
    // draw an ellipse at the mouse’s position
    ellipse(mouseX, mouseY, 10, 10);
  // if it is not pressed:
  }else{
    // draw a rectangle at the mouse’s position
    rectMode(CENTER);
    rect(mouseX, mouseY, 30, 30);
  }
}
```

### Application Examples: Mouse Interaction
Mouse interactions often require code to determine if a specific position is within a certain area. For this it does not really matter whether this area is a simple shape, such as a circular button, or a complex shape such as a character in a computer game. The basic principle of to determine this is a software program stays the same.

*MISSING EXAMPLE LINKS (9) (10)*