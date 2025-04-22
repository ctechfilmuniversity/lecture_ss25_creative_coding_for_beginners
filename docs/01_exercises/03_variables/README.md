---
layout: default
title: Exercise 03
parent: Exercises
nav_order: 4
---

# Creative Coding For Beginners
  
Prof. Dr. Lena Gieseke \| l.gieseke@filmuniversitaet.de  
  
  
# Exercise 03 - Variables

This session is due on **April 29th** before class.  

* [Creative Coding For Beginners](#creative-coding-for-beginners)
* [Exercise 03 - Variables](#exercise-03---variables)
    * [Task 03.01 - Scripts](#task-0301---scripts)
    * [Task 03.02 - Program Understanding](#task-0302---program-understanding)
    * [Task 03.03 - Code adjustment](#task-0303---code-adjustment)
    * [Task 03.04 - Animation](#task-0304---animation)


## Task 03.01 - Scripts

Recap the scripts:

* [Variables](../../02_scripts/ccfb_ss25_06_variables_script.md)


*Submission*: -



## Task 03.02 - Program Understanding

Execute and understand the [following code](https://editor.p5js.org/legie/sketches/mfJiSQu4o). You might need to look stuff up in the reference, e.g. [`constraint()`](https://p5js.org/reference/#/p5/constrain)and [short-cuts for arithmetic operators](../../02_scripts/ccfb_ss25_06_variables_script.md#arithmetic-operators)

```js
// Based on https://happycoding.io/tutorials/p5js/animation/bouncing-line

let lineStartX;
let lineStartY;
let lineEndX;
let lineEndY;

let stepStartX;
let stepStartY;
let stepEndX;
let stepEndY;
let rangeStep = 8;
let rangeColor = 5;

let r;
let g;
let b;


function setup() {
    createCanvas(windowWidth, windowHeight);

    lineStartX = random(windowWidth);
    lineStartY = random(windowHeight);
    lineEndX = random(windowWidth);
    lineEndY = random(windowHeight);


    stepStartX = random(-rangeStep, rangeStep);
    stepStartY = random(-rangeStep, rangeStep);
    stepEndX = random(-rangeStep, rangeStep);
    stepEndY = random(-rangeStep, rangeStep);

    r = random(255);
    g = random(255);
    b = random(255);

    noFill();
    strokeWeight(3);
    background(32);
}

function draw() {

    // Draw a line
    stroke(r, g, b, 80);
    line(lineStartX, lineStartY, lineEndX, lineEndY);
    // bezier(0, 0, lineStartX, lineStartY, lineEndX, lineEndY, width, height);

    // Increase the color values by a random number
    r += random(-rangeColor, rangeColor);
    g += random(-rangeColor, rangeColor);
    b += random(-rangeColor, rangeColor);

    // Check the reference for the
    // constraint function!
    r = constrain(r, 0, 255);
    g = constrain(g, 0, 255);
    b = constrain(b, 0, 255);

    // Move the line a bit
    lineStartX += stepStartX;
    lineStartY += stepStartY;
    lineEndX += stepEndX;
    lineEndY += stepEndY;

    if(lineStartX < 0 || lineStartX > width){
        stepStartX *= -1;
    }

    if(lineStartY < 0 || lineStartY > height){
        stepStartY *= -1;
    }

    if(lineEndX < 0 || lineEndX > width){
        stepEndX *= -1;
    }

    if(lineEndY < 0 || lineEndY > height){
        stepEndY *= -1;
    }
}
```

If you are completely lost with the code, [check this website](https://happycoding.io/tutorials/p5js/animation/bouncing-line), it gives a lengthy explanation about similar code.

*Submission*: - (we will discuss the code in class)


## Task 03.03 - Code adjustment

Make at least one adjustment to the code in 03.02 to make it look different. 

Optional, more advanced task: [Refactor the code](https://en.wikipedia.org/wiki/Code_refactoring) to make the code itself more efficient, e.g. by using [vectors](https://p5js.org/reference/p5/p5.Vector/).

*Submission*: Add a link to your sketch in your OwnCloud file.


## Task 03.04 - Animation

Create a sketch up to your liking that animates certain properties of the visuals (see the [example from class](https://editor.p5js.org/legie/sketches/pA5Ddli51)). The goal is to practice the use of variables.
  
*Submission*: Add a link to your sketch in your OwnCloud file.


---

*Happy Animating!*
