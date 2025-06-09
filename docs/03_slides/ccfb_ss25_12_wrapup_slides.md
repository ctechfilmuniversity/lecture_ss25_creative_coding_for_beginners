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



???
  

* Algorithmic Thinking Example?


--

* Re-Cap

--
* The Jumping Game

--
* Course Summary

--
* Follow-Up Topics

--
* Administration

---
template:inverse

# Libraries


---

## Libraries

--
* Extend p5 regarding specific topics

--
* Have their own documentation

--
* Might vary in quality
  
--
  
You must link a library file in your `index.html`

```html
<script src="path"></script>
```

--

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.js"></script>
```

--

```html
<script src="p5.scribble.js"></script>
```

  
---

## The Sound Library

[p5.sound](https://p5js.org/reference/p5.sound/)

  
---

## The Sound Library

Loading a sound file:

```js 
let song;

function preload() {
    song = loadSound('song.mp3');
}
```

--

```js
song.playMode('restart');
song.setVolume(0.1);
song.play();
...

if(song.isPlaying() == true){
    song.stop();
}
```
---
template:inverse

# Homework


---
template:inverse

# The Jumping Game

---
## The Jumping Game

**Download**:
  
Code Examples -> Week 9 -> [Tutorial Jumping Game - Assets](./assets.zip)

<br />


**Open**:   
Code Examples -> Week 9 -> [Tutorial Jumping Game - Steps](./ccfb_ss25_tutorial_jumping_game.md)

<br />

**Hands On!**


---
template: inverse

# Course Summary


---
.header[Course Summary]

## Commands

* Functions define functionality blocks within `{}`
    * Commands are *function calls*.
--
* You can define what should happen in given functions, e.g., `setup()`

--
* You can write your own functions and call them

```javascript
function functionname([parameter1,...]) {

    // Code that is executed when we call the function

    [return value;]
}
```

---
.header[Course Summary]

## Program Flow

* p5's environment
    * `preload()`
    * `setup()`
    * `draw()`
--
* Structuring the program flow
    * `if(condition is true)`
    * `while(condition is true)`

---
.header[Course Summary]

## User Input

* User Input from
    * `keyPressed()`
    * `mouseX`, `mouseY`

---
.header[Course Summary]

## Variables

We use variables to save and access data

--
* `let hue = 0;`
    * Variables have a data type
    * Variables live inside `{}` and have a scope


---
.header[Course Summary]

## Operators

* Arithmetic
    * `+`, `-`, `*`, `/`, `--`, `++`
* Comparison
    * `>`, `>=`, `<`, `<=`, `==`, `!=`
* Logical Operators
    * `&&`, `||`, `!`

---
.header[Course Summary]

## Color Systems

* Two color systems available
    * RGBA
    * HSB
    * `colorMode(HSB);`
    * `colorMode(HSB, windowWidth, 100, 100);`

---
.header[Course Summary]

## Loops

```js
let myCounter = 0;
while(myCounter < numberOfTimes)…
```

```js
for(let i = 0; i < numberOfTimes; i++)…
```


```js
for(let element of myArray)…
```


---
.header[Course Summary]

## Loops

2D Loop

*For every row look at every element…*

```js
for (let y = 0; y < numberRows; y++){

    for (let x = 0; x < numberColumns; x++){

        print("Row: " + y + " Column: " + x);
    }
}
```

---
.header[Course Summary]

## Objects

* Have properties and functions that *belong to* them
* You access those properties and functions with the `.` notation
    * `myImage.width`
    * `myImage.resize(100, 100);`
--
* p5.Image, p5.sound, arrays


---
.header[Course Summary]

## Arrays

With arrays we can save multiple values in one variable.

--

```js
let myArray = [2, 4, 6, 8, 'done']

myArray.push(100) // -> [2, 4, 6, 8, 'done', 100]
myArray[1] = 'hello' // -> [2, 'hello', 6, 8, 'done', 100]

myArray.length // -> 5
```

--

Arrays are accessed with `[]` and an index, starting at `0`.

--

```js
print(myArray[2]) // 6
```



---
.header[Course Summary]

## Images

```js
let imgPanda;

function preload() {
    imgPanda = loadImage("panda.jpg");
}

function draw() {
    image(imgPanda, 50, 50);
}
```

--
* Like any other object, e.g. change the positions...
* Store sequence in array and display them sequentially to animate
* `get(x, y)` and `set(x, y, color)` for, e.g., custom filter

???

* Animate images e.g. by changing their position like any other shape
* Store images in arrays and display them sequentially to animate image series
* Use `get(x, y)` and `set(x, y, color)` to return or set the color of the image at a specific pixel


---
.header[Course Summary]

## Libraries

* Libraries extend the p5 library in regard to one specific topic.
* You have to activate a library for a sketch in openProcessing.  
* For knowing how to use a library you have to refer to the library's given documentation, it is not necessarily on the p5 page.  
  
--

[p5.sound](https://p5js.org/reference/#/libraries/p5.sound)

---
.header[Course Summary]

## Libraries

Loading a sound file:

```js 
let song;

function preload() {
    song = loadSound('song.mp3');
}
```

--

```js
song.playMode('restart');
song.setVolume(0.1);
song.play();
...

song.stop();
```

---
.header[Course Summary]

# Use the [Reference](https://p5js.org/) 🚒

--

* [Open Processing](https://www.openprocessing.org)
* [Happy Coding](https://happycoding.io/tutorials/p5js/)
* [Generative Gestaltung](http://www.generative-gestaltung.de)
* [Creative Applications](https://www.creativeapplications.net/tools/framework/p5js/)
* The fairest of them all: [Daniel Shiffmann](https://shiffman.net/) 🤴🏼
* [Nature of Code](https://natureofcode.com/)


???
  

* https://happycoding.io/tutorials/p5js/


---
.header[Course Summary]

## Code Organization

--

* Good layout matters!!

--
* Write your own functions
* Split your code into different files

---
.header[Course Summary]

## Algorithmic Thinking

--

The goal is an **algorithm** that defines a list of steps to finish a task.

.footnote[[[code.org]](https://code.org/curriculum/course3/1/Teacher)]

--
  
* **Decomposition**: Break a problem down into smaller pieces

--
* **Pattern Matching**: Find similarities

--
* **Abstraction**: Reduce specific differences and make one solution work for multiple cases

---
.header[Course Summary]

## Learning Objectives

With this course, you hopefully gained

--
* An understanding of programming

--
* **Skills to develop simple programs from scratch**
    * Knowledge about resources
    * Guidance towards and learning through self-studies
--
* Skills to apply programming as (an expressive) tool


???
  

* But it is like a poetry class in Japanese

---
template:inverse

# Follow-Up Topics

---
.header[Follow-Up Topics]

## Coding Environments

For now, it is perfectly fine to continue with coding on the p5 Editor.  


???
  

* For each sketch you can control to whom the sketch is visible. With the option "Anyone can see your sketch" anyone with the URL can see your results - which is very handy of you want to share your work.

--
* Eventually you should move on to a more flexibel and adjustable IDE (Integrated Development Environment)


???
* Integrated Development Environment

--

I like [Visual Studio Code](https://code.visualstudio.com/) (in short VSCode). The editor is

* Free
* Multi-purpose
* Extensively adjustable

???

I like it because I can write different types of languages with it while still having many language specific features. Also, I am totally addicted to customizing my working environments to exactly the way I like it and VSCode let's me do so in a convenient way (enabled through *extensions*). In summary, it is:

---
.header[Follow-Up Topics]

## Coding Environments

But how can you develop and run a website on you local computer?

???

This will need a bit more learning on your side.

---
.header[Follow-Up Topics]

## Coding Environments

### Local Webserver

* Simulate the www locally on your computer

???
With a so-called local webserver you can build a "mini-Internet" on your computer. That is what professional web developers do, when working on a website.

--

<br />

Workflow

* Start a webserver
* Write code on your computer, e.g. with Visual Studio Code
* Look at the results in a browser

???

.task[TASK:]  

* Download game
* Start VSCode webserver
* Make it run locally

---
.header[Follow-Up Topics]

## Object Oriented Programming

--

```js
let myVector;

function setup() {
    createCanvas(300, 300);
    myVector = new p5.Vector(150, 200);
}

function draw() {
    background(50);
    circle(myVector.x, myVector.y, 100);
}
```

--
Creating object instances with `myInstance = new Classname();`

---
.header[Follow-Up Topics]

## Object Oriented Programming


Bad:
```
let positionX = [];
let positionY = [];

let stepX = [];
let stepY = [];

let hue = [];
```



---
.header[Follow-Up Topics]

## Object Oriented Programming

Good: Create your own objects!

---
.header[Follow-Up Topics | OOP]

```js
class Confetto {
    constructor(x, y, stepX, stepY, hue, size) {
        this.x = x;
        this.y = y;
        this.stepX = stepX;
        this.stepY = stepY;
        this.hue = hue;
        this.size = size;
        this.trail = [];
        this.trailIndex = 0;
    }

    update() {
        ...
    }
}
```

--
```js
let c = new Confetto(...);
```


---
.header[Follow-Up Topics | OOP]


```js
...

let confetti = [];

// Initalization of the values
for (let i = 0; i < numCircles; i++) {

    let x = random(width);
    let y = random(height);
    let stepX = random(-5, 5);
    let stepY = random(-5, 5);
    let hue = random(360);
    let size = random(5, 50);
    
    confetti.push(new Confetto(x, y, stepX, stepY, hue, size));
}

...
```

---
.header[Follow-Up Topics | OOP]

```js

...
function draw() {

...

    for (let i = 0; i < confetti.length; i++) {
        confetti[0].update();
    }
...
}

...
```

???
* todo: make sketch


---

## Follow-Up Topics

* Video

???
  

* https://p5js.org/reference/p5/createCapture/

--
* Working with AI as helper

--
* Machine Learning with ml3

--
* Web Development



???

* Data Visualization?
* Sound

---
template: inverse

# Where Should You Go From Here?
# 🤔

---

## Where Should You Go From Here?

--
* Do the final project

--
* Pick a direction you want to focus on
    * Generative designs
    * Games
    * Tools
    * etc.
--
* Watch tutorials and courses

--
* Look through other people's and professional code

--
* Create your own projects

---
## Where Should You Go From Here?

Once you stop to practice coding your will lose the skill. 😨 

--

<br />
But it will come back much faster once you are coding again! 😁


---
## Where Should You Go From Here?

I am happy to advise projects, theses, etc.  
  
Just get in touch.

---
template:inverse

# Administration

---
## Administration

* 4 SWS + 2 ECTS for attending lectures and exercises
* 1-2 ECTS for completing 70 % of the homework assignments 
* 1-3 ECTS for the final project


???
* Over 70% (without today's homeowork): Bente, Maksim, Celine, Siri, Carla
* https://owncloud.gwdg.de/index.php/apps/onlyoffice/3440037979?filePath=%2F03_teaching%2Flecture_ss25_creative_coding_for_beginners%2FTotal_Points.xlsx

--

VFX

* *Programmierkonzepte: Grundlagen der Programmierung*
    * Modul 7 - Programmierung und Entwicklung
    * 4 SWS + 5 ECTS
* Final Project: ~4 days of work = 1 ECTS

---
.header[Administration]

## Homework

You can hand in homework until **July 25th** to make it count. This is a hard deadline.

---
.header[Administration]

## The Final Project

You can do anything you like as a final project. 

--

<br />
**Hard Deadline: September 30st**


???

You have to hand in the final project in your Owncloud file until **September 30st**. This is a hard deadline.

---
.header[Administration]

## The Final Project

* Concept
* Implementation
* Results
    * At least three representative image a
* Lessons Learned
* Time spent on the project


???
* Moreover, submit at least one representative image and a short project description covering the following aspects:
  
--
  

> Feel free to get in touch for any questions.



---
template:inverse

## The End

# 👋🏻

