# Introduction To Processing
## History, Context And The First Lines Of Code

> This Lesson introduces Processing as a programming language and environment. After a brief overview over the origin of the project at the MIT Media Lab the Processing software will be introduced. This will be followed by a crash course covering Processing’s very basics such as the coordinate system, primitive shapes and the use of color.

---


This Lesson covers the design of generative and interactive systems using the Open-Source environment [Processing](http://www.processing.org). Processing enables people with no background in computer science to quickly and easily start working with code creatively. Without a complex setup, Processing will enable you to draw graphical elements, manipulate digital images, use your computer’s mouse and keyboard in your own programms and many things more.

The project was initiated in 2001 by [Ben Fry](http://www.benfry.com) and [Casey Reas](http://www.reas.com). Inspired by [John Maeda’s](http://www..com) [Design by Numbers](http://www..com) project, which he created in 1999, it was built as a tool for designers and artists to allow a more flexible approach to using software and technology. But Processing was quickly adapted by many artists and used not only in the sketching process but also in production of installations and exhibitions.

Processing is based on the [Java](https://en.wikipedia.org/wiki/Java_(programming_language)) programming language. It simplifies Java’s syntax and thus significantly reduces the amount of code you need to write during development. So, strictly speaking, Processing would be more a kind of dialect of Java rather than a programming language of its own. This has indeed many advantages. If you later want (or need) to look beyond the boundaries of the Processing environment, you will find it relatively easy to pick up other programming languages similar to Java, such as [ActionScript](https://en.wikipedia.org/wiki/ActionScript) or [JavaScript](https://en.wikipedia.org/wiki/Javascript). In recent years, Processing has also begun to expand from the Java platform to other environments. The most well know representative of this development is [ProcessingJS](http://processingjs.org) which is natively supported in the most recent versions of Processing. ProcessingJS is based on JavaScript, which makes it very easy to integrate Processing into full-featured webpages.

The key to learning programming is the ability to express instructions in the programming language’s syntax as well as to order and combine these instructions into a logical sequence, basically the design of an [algorithm](https://en.wikipedia.org/wiki/Algorithm). Many state-of-the-art programming languages are similar in this regard and hence can be learned quite easily with some experience in Processing. This is the main reason - besides the strong visual focus, of course - why Processing is our tool of choice for introducing software programming to artists and designers.

### The Application
Processing consists of two parts: The actual programming language (or dialect) on the one hand and the application on the other, which was built to make using Processing as simple as possible.

This application is basically a text editor with added tools for the essential tasks related to programming. In comparison with full-featured integrated development environments ([IDEs](https://en.wikipedia.org/wiki/Integrated_development_environment)) such as [Eclipse](http://eclipse.org) or [Netbeans](http://netbeans.org/), Processing projects are set up and confirgured easily and quickly, requiring only a minimum number of steps to get you started. You can download it for free from the [download section](http://processing.org/download) of the Processing website for Mac, Linux and Windows systems. The only requirements are a recent Java version and Quicktime, which come preinstalled on most operation systems or they are included in the download. Some additional components (called *[Libraries](http://www.processing.org/learning/libraries)*) also depend on specific software, but it is ususally included in their download as well.

*It is worth noting at this point that Processing is currently undergoing a major step in its evolution towards its second version. While the current download is labeled **Beta** – an equivalent to ‘testing’ in software development – we consider this as stable enough for use with all lessons on Creative Coding.*

The application window consists mainly of the text editing area. Inserted text will be highlighted in different colors for improved recognition of important passages in the code. A standard application menu with entries such as *open* or *save* is located above the editor. There you will also find more advanced options like adding *Libraries* or exporting your application. Applications are called ‘sketches’ in Processing which refers to the often iterative development process that can be seen as ‘sketching out’ an idea. The most essential tools are located between the application menu and text editor area and are represented as icons. If you press the *Run* button (the ‘play’ icon) a second window appear that shows your actual running programm. Alternatively, you can run your sketch with the Cmd (Ctrl) + r shortcut. It can happen later in the development of your sketch that your sketch contains more than one file. Thus, you will find an additional tab bar right above your editor window to manage multiple files.

### The Canvas
The canvas of your sketch (your application window’s content) is represented by a [Cartesin coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system) which describes element position and dimensions for drawing. The horizontal *x*-axis can be seen as being the top border of the window, the vertical *y*-axis as the left. The **origin** of this **coordinate system** with an (x,y)-position of **(0,0)** is located at the **upper left corner**. From this point, the coordinate system extends to the right on the *x*-axis and downwards on the *y*-axis. The position and dimension of an object is usually defined in pixel units with the result that the x-value for the point in the upper-right corner is equal to the width of the window in pixels. Both axes do also extend to the left and top into the negative value domain. For example, a point with an (x,y)-position of (-10, 10) would be located 10 pixels to the left and to the top of the upper-left corner, practically being outside of the application window. Hence, it is important to keep in mind that visual elements can be outside the visible canvas area and, as a consequence, will not be displayed.

We can also extend this two-dimensional space by a *z*-axis to display **three-dimensional** objects. This third axis would also have its origin in the upper-left corner and it would extend *perpendicularily* (in a right angle) to the screen. Positive values on this axis would be located in front of the screen, negative values behind it. However, in the following Lessons we will only focus on creative coding in 2D.

#### The Size Of Your Sketch’s Window
Your canvas’ size can be defined using the `size()` command. Processing will set a default canvas size of 100x100 pixels, if your sketch does not contain the `size()` command. To make this command work, you need to supply two pieces of information along with the command: the desired width and height of the canvas. In two-dimensional space we always provide the value on the *x*-axis first, followed by the value on the *y*-axis. Thus, for the `size` command the first piece of information will be the width, the second piece will be the height. We can provide both values as parameters inside the parentheses (‘round brackets‘) following the `‘size’` keyword.

* **`size(width, height)`** – sets the size of the visible canvas area (your sketch’s window). The example below sets the sketch size to be 800x600 pixel:
```processing
size (800, 600);
```

### Basic Shapes
#### Point
![Point](/files/documents/b01_point.jpg "Point")
The point is the most simple basic shape. It only requires an *x* and *y*-coordinate to fill a pixel on the screen. You can choose the color for a point using the [`stroke()`](lesson9#flaechen_fuellen_raender_einfaerben)-command.

* **`point(x, y)`** draws a point on the canvas using the specified *x* and *y*-coordinates.
```processing
point (0, 0);   // upper-left corner
point (43, 89);  // x = 43 & y = 89
```

#### Line
![Line](/files/documents/b01_line.jpg "Line")
The second element is the line. It connects a start with an endpoint. Use the `line()` command to draw a line. It requires exactly 4 arguments, consisting of an *x* and *y*-coordinate for the start and endpoint.

* **`line(x1, y1, x2, y2)`** draws a line on the canvas between two points. Point 1 & 2 are defined by a *x* and *y*-coordinate each.
```processing
line (10, 20, 80, 60);
```

#### Rectangle
![Rectangle](/files/documents/b01_rect.jpg "Rectangle")
The `rect()` command enables you to draw rectangular shapes. The shape’s position is defined relative to its upper-left corner. Its size is defined by specifying the extend to the right and bottom. Hence, you need to provide the width and height in addition to the *x* and *y*-coordinates to draw a rectangle.

* **`rect(x, y, width, height)`** draws a rectangle to the sketch’s canvas with a given *width* and *height* at position (*x*,*y*).
```processing
rect (20, 20, 60, 40);
```

There is also the [`quad()`](lesson1#viereck)-command, if you want to draw a quadrangle which interior angles are not limited to 90 degrees.

#### Ellipse
![Ellipse](/files/documents/b01_ellipse.jpg "Ellipse")
The `ellipse()` command enables you to draw ellipses and circles to the canvas.
In the basic configuration, the ellipse is draw relative to its *center* as given by the *x* and *y*-coordinates. The second pair of values defines the width and height of the ellipse, similarily to the `rect() command. If these values are equal the command will draw a circle. Please note that by defining the width and height we actually define the *diameters* of the ellipse and not its *radii*!

* **`ellipse(x, y, width, height)`** draws an ellipse to the sketch’s canvas given the *width* and *height* at position (*x*,*y*).
```processing
ellipse (50, 50, 45, 55);
```

#### Quadrilaterals
![Quadrilateral](/files/documents/b01_quad.jpg "Quadrilateral")
The `quad()` command enables you to draw quadrilaterals like [parallelograms](https://en.wikipedia.org/wiki/Parallelogram), [rhombi](https://en.wikipedia.org/wiki/Rhomb) or arbitrary quadrilaterals. You can draw them by defining its 4 corners:

* **`quad(x1, y1, x2, y2, x3, y3, x4, y4)`** draws a quad to the sketch’s canvas. Requires 4 corner vertices defined by an *x* and *y*-coordinate each.
```processing
quad (12, 19, 31, 85, 67, 74, 80, 19);
```

### Grey Tones
![Grey Tones](/files/documents/b01_grey.jpg "Grey Tones")
Within the [RGB color space](https://en.wikipedia.org/wiki/RGB_color_space), grey tones are all ‘colors’ for which its three components, **R**ed, **G**reen and **B**lue share the same value. Each component’s (*channel*) value is specified in the range from 0 to 255. Based on the principle of [additive color mixing](https://en.wikipedia.org/wiki/Additive_color) you will get a plain white if all channels are fully active (255) and black if they are off (0). Luckily, Processing provides a shortcut for specifying grey tones by allowing you to write the value for each channel only once, since they are the same anyways. So, instead of providing three values for *R*ed, *G*reen and *B*lue you can provide only one value for all three at once, resulting in a grey tone. Hence, the statements `fill(38, 38, 38);` and `fill(38);` will have the same result.

```processing
background (110);  // grey
fill (0);          // black
stroke (255);      // white
```

In addition to the grey value, you can provide an *A*lpha value to define an object’s transparency. This value is specified in the range of 0-255 as well.

```processing
background (110);  // grey
fill (0, 90);      // black, transparent
stroke (255, 200); // white, transparent
```

You can read calls to `fill()` and `stroke()` commands as follows:

* **1 value** grey tone, opaque
* **2 value** grey tone, with transparency
* **3 value** RGB color, opaque
* **4 value** RGB color, with transparancy

### Colors
![RGB Color Model](/files/documents/b01_rgb_system.jpg "RGB Color Model")
Processing uses the [RGBA Color Model](https://en.wikipedia.org/wiki/RGB_color_model) (**R**ed, **G**reen, **B**lue, **A**lpha) by default. Every *channel* in this model has a value in the range from 0 to 255 resulting in a mix of color channel intensities creating an actual color. This color model is also called [additive color mixing](https://en.wikipedia.org/wiki/Additive_color). A value of 0 means the color component is not present at all in the color mixing process, a value of 255 means the component is fully present in the mixing process.

Processing provides three commands to set colors for different properties in your sketch: `background()` to color the entire background of you sketch, `fill()` to set a fill color and `stroke()` to set a stroke color of any visual element to be drawn.

#### Background Color
Processing draws a grey background by default. We can use the `background()` command if we want to fill the background with a color of our choice as specified by the one to four color components. Additionally, this clears the sketch of all elements drawn so far.

* **`background(r, g, b)`** clears the sketch’s canvas replacing anything drawn so far by a solid color. The color is specified either by one grey value or three **R**, **G**, **B** components
```processing
background(231, 0, 89);
```

#### Stroke And Fill Colors
So far, we have not learned a way to specify stroke and fill colors for the graohical elements we would like to draw. For this purpose, Processing provides color commands to set the stroke and fill colors individually. Think of it as a ‘paint bucket’ which you can control using two commands: `fill()` and `stroke()`. They set the respective color for *all* subsequently drawn visual elements. You can use `noFill()` and `noStroke()` if you do not want strokes or fills to be drawn. The settings you make this way remains set until you change them again using `fill()` or `stroke()`.

* **`fill(r, g, b)`** sets the fill color for *all* subsequently drawn elements. The color is specified either by one grey value or three **R**, **G**, **B** components. Additionally, a fourth **A**lpha component can be specified to make the object transparent. All values must be between 0 and 255.
```processing
fill (255, 0, 0); // solid red
fill (0, 255, 0); // solid green
fill (0, 0, 255); // sollid blue
```
* **`noFill()`** all subsequently drawn elements will be drawn without a fill color.
```processing
noFill();
```
* **`stroke(r, g, b)`** sets the stroke color for *all* subsequently drawn elements. The color is specified either by one grey value or three **R**, **G**, **B** components. Additionally, a fourth **A**lpha component can be specified to make the object (i.e. point or line) or the object’s outline stroke transparent. All values must be between 0 and 255.
```processing
stroke (255, 0, 0); //volles Rot
stroke (0, 255, 0); //volles Grün
stroke (0, 0, 255); //volles Blau
```
* **`noStroke()`** all subsequently drawn elements will be drawn without a outline stroke. **WARNING:** points and lines will not be drawn if this is set!
```processing
noStroke();
```