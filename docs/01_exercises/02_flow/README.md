---
layout: default
title: Exercise
nav_exclude: true
---


layout: default
title: Exercise 02
parent: Exercises
nav_order: 2



# Creative Coding For Beginners
  
Prof. Dr. Lena Gieseke \| l.gieseke@filmuniversitaet.de  
Elena Vasilkova \| elena.vasilkova@filmuniversitaet.de
  

# Exercise 02 - Program Flow & Interaction

This session is due on **Tuesday, April 22nd** before class.  


* [Creative Coding For Beginners](#creative-coding-for-beginners)
* [Exercise 02 - Program Flow \& Interaction](#exercise-02---program-flow--interaction)
    * [Task 02.01 - Scripts](#task-0201---scripts)
    * [Task 02.02 - Errors](#task-0202---errors)
    * [Task 02.03 - Interaction](#task-0203---interaction)


## Task 02.01 - Scripts

Recap the scripts:

* [Program Flow and Interaction](../../02_scripts/ccfb_ss25_04_flow_script.md)
* [Color Systems](../../02_scripts/ccfb_ss25_05_colorsystems_script.md)

*Submission*: -


## Task 02.02 - Errors

[This code](https://editor.p5js.org/legie/sketches/2wzE7ba4V) has three errors. Can you find and fix them? Make sure to read the error messages, they might (or might not) help you find the issues.

Briefly explain what the code does.


```js
function setup() {createCanvas(400, 400);colorMode(HSB);noStroke();
  // Properties for the
  // text() command
  // https://p5js.org/reference/p5/text/
  // https://p5js.org/reference/p5/textAlign/
  textAlign(CENTER, CENTER);textSize(36);}

function draw() // hour() returns the current hour

  // from 0..23
  // https://p5js.org/reference/p5/hour/
  if( hour() < 5 ) {
    
    // Night
    background(240, 100, 40);fill(50, 40, 100);text('⭐️ Good Night! ⭐️', 200, 200);} else if (hour() < 12) { // Morning
    background(200, 20, 100);fill(42, 100, 100);text('☀️ Good Morning! ☀️, 200, 200);} else if (hour() < 16) {
    
    //Midday
    background(210, 60, 100);    
    
    fill(42, 60, 100);text('🌼 Good Afternoon! 🌼', 200, 200);} else {
    
    //Evening
    background(210, 100, 80);    
    fill(100);
    text('🍿 Good Evening! 🛋️', 200);
  }}
```

*Submission*: Add in your OwnCloud file a link to your sketch and a brief explanation about what the code does.


## Task 02.03 - Interaction

Create a sketch up to your liking and that uses interaction and conditionals. You could also add interaction to your homework from last week. The goal is to practice the learned functionalities.

  

*Submission*: Add a link to your sketch in your OwnCloud file.

---

*Happy Flowing!*

