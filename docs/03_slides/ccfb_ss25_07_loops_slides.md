name: inverse
layout: true
class: center, middle, inverse
---

# Creative Coding For Beginners

### Prof. Dr. Lena Gieseke | l.gieseke@filmuniversitaet.de  


<br />
#### Film University Babelsberg KONRAD WOLF


---
layout:false

## Today

--

.left-even[
* Re-Cap Variables

]



---


## Today

.left-even[
* Re-Cap Variables

* Loops
    * while Loops
    * for-Loops
    * 2D Loops
    * Grid-based Pattern

]





---


## Today

.left-even[
* Re-Cap Variables

* Loops
    * while Loops
    * for-Loops
    * 2D Loops
    * Grid-based Pattern

]

.right-even[

* Homework
    * Code understanding
    * Your adjustments
    * Animation examples

]




---

## Today

.left-even[
* Re-Cap Variables

* Loops
    * while Loops
    * for-Loops
    * 2D Loops
    * Grid-based Pattern

]

.right-even[

* Homework
    * Code understanding
    * Your adjustments
    * Animation examples

* Practicing examples

]



???

https://editor.p5js.org/legie/full/fYvij_ACr (TODO: clean and comment code)


---
template:inverse

# Variables

---
## Variables


???
.task[COMMENT:]  

* What is a variable?

--

With a variable you can store and re-use data.

--


```js
//Pseudo code

let variablename = value;
```

---
.header[Variables]

## Scope


???
.task[COMMENT:]  

* What is the scope of variable?

--

Scope refers to the area in the code where you can access the variable, meaning *where it exists*.  

The scope is defined by the surrounding `{}`, where you created the variable:

```js
{
    // Variable only exists inside the brackets
    let myDiameter = 10;
}
```


---
.header[Variables]

## Nesting Scopes

---

.center[<img src="../02_scripts/img/variables/ch03_17.png" alt="ch03_17" style="width:95%;">]

---
.header[Variables]

## Global Scope

--

Good for

* having your variable visible everywhere in your code 
* saving values between different function calls, e.g., different `draw` calls

--

Carful with keeping track of the value within a global variable.



---
template:inverse

# Loops

---
layout:false


.left-even[]
.right-even[]


.center[<img src="../02_scripts/img/loops/ten_print.png" alt="ten_print" style="width:92%;">]

--

.center[*What do we see? Can you find the underlying algorithm?*]

---
layout:false

## The `10 PRINT` Pattern


<img src="../02_scripts/img/loops/ten_print.png" alt="ten_print" style="width:50%;">


Algorithm
  
* Go row by row
* Place a `/` or a `\` randomly



---

![ten_print_commodore](../02_scripts/img/loops/ten_print_commodore.png)

The original BASIC program for the Commodore 64:

```bash
10 PRINT CHR$(205.5+RND(1)); : GOTO 10
```
<!-- ??? BASIC had its own character indices (not ASCII) -->

--

Bash:

```bash
f="╱╲";while :;do print -n ${f[(RANDOM % 2) + 1]};done
```


???
.task[TASK:]  

* Show terminal version

---

## The `10 PRINT` Pattern

```bash
10 PRINT CHR$(205.5+RND(1)); : GOTO 10
```

* BASIC program from the 1980s
* Considered a phenomenon of creative coding through its simplicity and visual appeal
* There is a whole [book](http://10print.org/) dedicated to this line of code
* You can watch the author talk about his work on [youtube](https://www.youtube.com/watch?v=34CXQr5OLas)

---

## The `10 PRINT` Pattern

*How could we modify the pattern? Which parameters do we have?*

![ten_print](../02_scripts/img/loops/ten_print.png)


---

## The `10 PRINT` Pattern

### Spacing

![ten_print_quadratic](../02_scripts/img/loops/ten_print_quadratic.png) ![ten_print_spacing](../02_scripts/img/loops/ten_print_spacing.png)

---

## The `10 PRINT` Pattern

### Probability

E.g. 90% probability for a backslash

![ten_print_quadratic](../02_scripts/img/loops/ten_print_quadratic.png)
![ten_print_prob](../02_scripts/img/loops/ten_print_prob.png)


???

* As we are repeatedly placing a `/` or a `\` we need to learn how to repeat code for creating such a pattern. And that is coincidentally what you are going to learn in this script 😁.


---


## Learning Objectives

With this chapter you 

* understand how to repeat code,
* know how to implement a `while` and a `for`-loop, 
* know how to implement a 2D `for`-loop, and
* understand how to create grid-based pattern.


---

## Looping

For repeating the same code multiple times, there are two types of loops,  

* `while-` loops 
* `for-`loops


---

## `while`-Loop

--

```js
// Pseudo code

while (condition is true) {

    statement;
}
```

--


* Closely related to the if-statement

--
* Executed **as long as** (*while*) the condition is true


---

## `while`-Loop

```js
// https://editor.p5js.org/legie/sketches/swLARHfUn
// While Loop

let counter = 0;    // Iteration counter

while (counter < 3) { // Loop condition
  
    print('wow');     // Loop activity

    counter += 1;       // Increase counter
}

print('All done…');
```


???
* https://editor.p5js.org/legie/sketches/IpQYBo_YUU
* 

---

## `while`-Loop

.center[<img src="../02_scripts/img/loops/ch02_04.png" alt="ten_print" style="width:60%;">.imgref[[[michaelkipp]](http://michaelkipp.de/processing/07%20schleifen.html)]]

---

## `while`-Loop

```js
// https://editor.p5js.org/legie/sketches/P9nGLtSJq
...

function draw() {

    let counter = 0; // Iteration counter

    while (counter < 30) { // Loop condition
    
        ellipse(mouseX + random(100), mouseY + random(100), 10, 10);
        counter += 1; // Increase counter
    }
}
```

What is exactly happening here? What is repeated when?

---

## `while`-Loop

* The `draw()` function is called by default 60 times per second.
* For each `draw()` call, we execute the loop, hence we draw 30 ellipses 60 times per second.

???

.task[COMMENT:]  

* Even though the while-loop works just fine with setting up a counter and increasing it manually, it is there is another way of creating loops which gives us more control and is less error prone.
* Before we have a look into `for`-loops, let's review the general loop logic.
* https://www.geeksforgeeks.org/find-if-a-point-lies-inside-or-on-circle/
* https://stackoverflow.com/questions/481144/equation-for-testing-if-a-point-is-inside-a-circle

---
template:inverse

### Quick Detour

## Test If A Point Is Inside A Circle

---

## Test If A Point Is Inside A Circle

.left-even[<img src="../02_scripts/img/loops/circle_01.png" alt="circle_01" style="width:100%;">.imgref[[[wiki]](https://www.wikiwand.com/en/Circle)]]

--

.right-even[
A circle with the

* centre coordinates $(a, b)$
* radius $r$

is the set of all points $(x, y)$ such that

$(x-a)^2 + (y-b)^2 = r^2$

]


---


## Test If A Point Is Inside A Circle

To test if a point is *inside* a circle we have to test for

<br />

$(x-centerX)^2 + (y-centerY)^2 <= r^2$

--

```js
// https://editor.p5js.org/legie/sketches/q53DdC1ul

if ((x - centerX) * (x - centerX) +
    (y - centerY) * (y - centerY) <= r * r) {

        // Points are inside
    }
```


???

* https://editor.p5js.org/legie/sketches/q53DdC1ul


---

## `while`-Loop

# 🚨 
**You have to make sure that the condition becomes `false` at some point!**
  
--
  
Otherwise you have created an **infinity loop** 🤬 ♾️


---
template:inverse

# Loop Logic

---
## Loop Logic

Independently from the specific syntax both loops follow the same logic and include the same components.

--

For repeating code you need to

--
* Create a variable (e.g. `i`) as iterator
    * Initialize the iterator with a start value
--
* Give a termination condition

--
* Increase the iterator in each loop

--
* Check for the termination condition


???

The last two points can also happen in reversed order (hence, first check the termination condition and then increase the iterator).


---


## Loop Logic

`while`-loop:

```js
let counter = 0;    // INITIALIZATION
while (counter < 3) { // CONDITION
    // code
    counter += 1;   // STEP
}
```

--

`for`-loop:

```js
// Pseudo Code

for(INITIALIZATION; CONDITION; STEP) {
    // code
}
```

???

* The `for`-loop also executes a block of code the given number of times. It is used more often than the while loop because it gives you more control.

---


## Loop Logic


```js
// Pseudo Code

for(INITIALIZATION; CONDITION; STEP) {
    // code
}
```

```js
for(let i = 0; i < numberOfTimes; i++) {

    // code

}
```


???

.task[COMMENT:]  

* You can chose any variable name as iterator
    * `i` as short for iterator is just typical
* You can chose any start value
    * Most times it will be `0` though
* You can chose any end value `numberOfTimes`
    * This can be a direct value or a variable
* `i++` is a shortcut for `i=i+1` and represents the step size, meaning how the value of the iterator changes from iteration to iteration
    * You can chose any step size you want, e.g. `i+=12`

---

## For Loop

```js
let counter = 0;
while (counter < 3) {
 
    print('wow');
    counter += 1;
}
```

--

```js
// https://editor.p5js.org/legie/sketches/QcpJQ9fMR
// For Loop

for(let i = 0; i < 3; i++){
    print('wow');
}
```

---

## For Loop

Or with a different variable name:

```js
for(let counter = 0; counter < 3; counter++){
    print(“wow”);
}
```

---

## For Loop

The for loop follows the same logic as the while loop:

.center[<img src="../02_scripts/img/loops/ch02_04.png" alt="ten_print" style="width:60%;">.imgref[[[michaelkipp]](http://michaelkipp.de/processing/07%20schleifen.html)]]


---

## For Loop


```js
// https://editor.p5js.org/legie/sketches/9kusxGMGp
// The For-Loop Inside Draw

...

function draw() {
    // let counter = 0; // Iteration counter
    // while (counter < 30) { // Loop condition 
    //     ellipse(mouseX + random(30), mouseY + random(30), 2, 2);
    //     counter += 1; // Increase counter
    // }

    for (let i = 0; i < 30; i++) {
        ellipse(mouseX + random(30), mouseY + random(30), 2, 2);
    }
}

```

---

## For Loop

What is the scope of the iteration variable?  

--

The scope is **local** within the loop code block, meaning it is only visible inside the loop:

```js
// Pseudo Code

for(let i = 0; i < numberOfTimes; i++) {

    // i only exists here

}
print(i); //gives an error
```

---

## For Loop

*How to create something like the following?*

.center[<img src="../02_scripts/img/loops/ch05_04.png" alt="name" style="width:55%;">]

---
template:inverse

# 2D Loops

---

## 2D Loops

???

In the following, we are not learning any new syntax but only apply what we have learned above.

--

As we are working on a 2D canvas in x and y, often times a 2D loop is used to fill a space, for example the canvas. You can imagine this as the filling of a grid.

---

## 2D Loops

**For every row, look at every element…**

--

![ch01_06](../02_scripts/img/loops/ch05_05.png)  


---

## 2D Loops

**For every row, look at every element…**

![ch01_06](../02_scripts/img/loops/ch05_06.png)  

---

## 2D Loops

**For every row, look at every element…**

![ch01_07](../02_scripts/img/loops/ch05_07.png)  

---

## 2D Loops

**For every row, look at every element…**

![ch01_08](../02_scripts/img/loops/ch05_08.png)  

---

## 2D Loops

**For every row, look at every element…**

![ch01_09](../02_scripts/img/loops/ch05_09.png)  

---

## 2D Loops

For implementing this, we **nest** two loop as follows

```js
// Pseudo Code

For every row {
    For every column {

    }
}
```
---

## 2D Loops

```js
// https://editor.p5js.org/legie/sketches/lpStDBNUC
// 2D For-Loop

// Nested loop to run through the grid
for (let gridY = 0; gridY < numberRows; gridY++) {

    for (let gridX = 0; gridX < numberColumns; gridX++) {

        print("Row: " + gridY + " Column: " + gridX);
    
    }
}
```

---

## 2D Loops

```js
// 2D For-Loop

// Nested loop to run through the grid
for (let y = 0; y < numberRows; y++) {

    for (let x = 0; x < numberColumns; x++) {

        print("Row: " + y + " Column: " + x);

    }
}
```

???

* But as said before, you normally used shorter names. The following is the same as this above but with different variable names. If the variables refer to x,y coordinate, you often also use x and y as iterator variable names:

---
.header[2D Loops]

## A Grid

Now, we can, for example, draw a `rect` at each x,y coordinate within the 2D loop to create a grid. 

---
.header[2D Loops]

## A Grid

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
let rectSize = 50;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(255);

    noLoop();
}

function draw() {

    // Nested loop to run through the grid
    for (let y = 0; y < windowHeight; y++) {
        for (let x = 0; x < windowWidth; x++) {
        
            rect(x, y, rectSize, rectSize);
        
        }
    }
}
</script>


???
.task[COMMENT:]  

* We need to take larger steps to draw fewer rectangles. We can create a nice continuos grid, when taking the size of the rectangle also as the step size.

---
.header[2D Loops]

## A Grid

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
let rectSize = 50;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(255);

    noLoop();
}

function draw() {

    // Nested loop to run over
    // all pixels of the canvas
    // We are using the rectSize variable
    // to control the step size of the
    // loop
    for (let y = 0; y < windowHeight; y+=rectSize) {
        for (let x = 0; x < windowWidth; x+=rectSize) {


            rect(x, y, rectSize, rectSize);


        }
    }
}
</script>


???
.task[COMMENT:]  

* Now, we can for example also draw ellipses along the grid.


---
.header[2D Loops]

## A Grid

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
let rectSize = 50;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(255);

    noLoop();
    noFill();
}

function draw() {

    // Nested loop to run over
    // all pixels of the canvas
    // We are using the rectSize variable
    // to control the step size of the
    // loop
    for (let y = 0; y < windowHeight; y+=rectSize) {
        for (let x = 0; x < windowWidth; x+=rectSize) {

            rect(x, y, rectSize, rectSize);
            ellipse(x, y, rectSize, rectSize);
        }
    }
}

</script>


???
.task[COMMENT:]  

* Why is there this strange offset around the border?
* Because we are drawing the ellipses at the left upper corner (0,0) of each cell.
* For that we add to the above example rectangle with `stepSize` as size to visualize the grid structure we are working with:

---
.header[2D Loops]

## A Grid

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
let rectSize = 50;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(255);

    noLoop();
    noFill();
}

function draw() {

    // Nested loop to run over
    // all pixels of the canvas
    // We are using the rectSize variable
    // to control the step size of the
    // loop
    for (let y = 0; y < windowHeight; y+=rectSize) {
        for (let x = 0; x < windowWidth; x+=rectSize) {

            rect(x, y, rectSize, rectSize);
            ellipse(x + rectSize * 0.5, y + rectSize*0.5, rectSize, rectSize);
        }
    }
}

</script>


???
.task[COMMENT:]  

* Shifting the drawing of the ellipse to the center of the grid cell.

---
.header[2D Loops]

## A Grid

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
let rectSize = 50;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(255);

    noLoop();
    noFill();
}

function draw() {

    // Nested loop to run over
    // all pixels of the canvas
    // We are using the rectSize variable
    // to control the step size of the
    // loop
    
    
    
    for (let y = 0; y < windowHeight; y += rectSize) {

        for (let x = 0; x < windowWidth; x += rectSize) {

            // My smiley
            strokeWeight(1);
            fill(255, 180, 225);

            ellipse(x + rectSize * 0.5, y + rectSize * 0.5, rectSize);

            noFill();
            arc(x + 18, y + rectSize * 0.45, 10, 20, radians(180), radians(360));

            arc(x + rectSize * 0.5 + 8, y + rectSize * 0.45, 10, 20, radians(180), radians(360));

            arc(x + 25, y + rectSize * 0.6, 30, 20, 0, radians(180));

        } // END for (let x...

    } // END for (let y...

} // DRAW

</script>


---
.header[2D Loops]

## A Grid

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
let rectSize = 50;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(255);

    // For interaction don't forget
    // to turn on the loop again!
    //noLoop();
    noFill();
    stroke(180, 0, 255);
    strokeWeight(2);
}

function draw() {
    
    // Clearing the background in each
    // draw call
    background(255);

    
    
    // Mapping the value range mouseX, and mouseY
    // can have to 5..500 with the map function
    // https://p5js.org/reference/#/p5/map
    let diameterX = map(mouseX, 0, windowWidth, 5, 250);
    let diameterY = map(mouseY, 0, windowHeight, 5, 250);


    // Nested loop to run over
    // all pixels of the canvas
    // We are using the rectSize variable
    // to control the step size of the
    // loop
    for (let y = 0; y < height; y+=rectSize) {
        for (let x = 0; x < width; x+=rectSize) {

            // rect(x, y, rectSize, rectSize);
            ellipse(x + rectSize*0.5, y + rectSize*0.5, diameterX, diameterY);
        }
    }
}
</script>


???
.task[COMMENT:]  

* For making the pattern more interesting, we  control the width and height of the ellipses with mouseX and mouseY. 
* For that we need to map the possible value range of 0..1000 that mouseX and mouseY can have to a smaller range, e.g., 5..500 for having a reasonable sizes for the ellipse:

---


## The 10 PRINT Example

Remember this intro? Now we know how to implement the 10 PRINT example!

![ch05_01](../02_scripts/img/loops/ch05_01.png)  
[[10print.org]](https://10print.org/)

---

## The 10 PRINT Example

--

We need to place randomly either a slash or backslash in each cell of our grid.  

--

In order to have a simple 50-50 decision maker, you can use the following:

```js
let probability = 0.5;

if (random(1) < probability) {

    //...
}
else {
    //...
}
```


???
.task[COMMENT:]  

* Can someone explain how this works?

---

## The 10 PRINT Example

We need to place randomly either a slash or backslash in each cell of our grid.  

In order to have a simple 50-50 decision maker, you can use the following:

```js
let probability = 0.5;

if (random(1) < probability) { //all random numbers between 0..0.49

    //...
}
else { //all random numbers between 0.5..0.99

    //...
}
```

---

## The 10 PRINT Example

<script type="text/p5" data-p5-version="1.6.0" data-autoplay data-height="450" data-preview-width="500" >
//https://editor.p5js.org/legie/sketches/Gd7jHe9WZ

let cellSize = 10;

// Threshold for which
// slash to draw
let probability = 0.5;


function setup() {
	createCanvas(1000, 1000);
	background(255);

	noLoop();
}

function draw() {

	// Nested loop to run over
	// all pixels of the canvas
	// We are using the rectSize variable
	// to control the step size of the
	// loop
	for (let y = 0; y < height; y += cellSize) {
		for (let x = 0; x < width; x += cellSize) {


			// Switch which "character" to draw
			// based on probability
			if (random(1) < probability) {

				line(x, y, x + cellSize, y + cellSize);

			} else {

				line(x, y + cellSize, x + cellSize, y);

			}
		}
	}
}
</script>


???
* https://editor.p5js.org/legie/sketches/nrfQTzxMI

* TODO: https://editor.p5js.org/legie/sketches/fYvij_ACr
* 



---
template:inverse

## Summary

---
## Summary

### Loops

```js
while(i < numberOfTimes)…
```

```js
for(int i = 0; i < numberOfTimes; i++)…
```

---
## Summary

### 2D Loop

*For every row look at every element…*

```js
for (let y = 0; y < numberRows; y++)
{
    for (let x = 0; x < numberColumns; x++)
    {
        print("Row: " + y + " Column: " + x);
    }
}
```

--

Use the [reference](https://p5js.org/reference/) 🚒



---
template:inverse

## The End

## 🎨 🎡 🔗 

