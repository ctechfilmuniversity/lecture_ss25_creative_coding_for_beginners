---
layout: default
title: Tutorial Jumping Game
nav_exclude: true
---


# Tutorial Jumping Game


* [Tutorial Jumping Game](#tutorial-jumping-game)
    * [1. The Player](#1-the-player)
        * [1.1 Player Setup](#11-player-setup)
        * [1.2 Player Placeholder](#12-player-placeholder)
        * [1.3 Player Jumping](#13-player-jumping)
        * [1.4 Player Graphics](#14-player-graphics)
        * [1.5 Player Graphics Jumping](#15-player-graphics-jumping)
    * [2. The Background](#2-the-background)
        * [2.1. BG Setup](#21-bg-setup)
        * [2.2. BG Animation](#22-bg-animation)
    * [3. Coin](#3-coin)
        * [3.1. Coin Animation](#31-coin-animation)
        * [3.2. Coin Collection](#32-coin-collection)
        * [3.3. Coin Counting](#33-coin-counting)
    * [4. Enemies](#4-enemies)
        * [4.1 Enemies Animation](#41-enemies-animation)
        * [4.2 Enemies Collision](#42-enemies-collision)
    * [5. Game Logic](#5-game-logic)
        * [5.1. Stop](#51-stop)
    * [6. Sound](#6-sound)
        * [6.1 Sound BG](#61-sound-bg)
        * [6.2 Sound Effects](#62-sound-effects)
    * [7. Enemies Birds](#7-enemies-birds)



We start with an empty sketch.


## 1. The Player

We start with the basic functionality for the player, meaning its variables and its jumping. We do so for now with a circle and later add graphics.

### 1.1 Player Setup

To organize our code we will use multiple files. You can create and switch tabs under `Sketch Files` the editor.

* Create a new file `player.js`
* In `index.html` add the following line under `<script src="sketch.js"></script>`

```html
<script src="sketch.js"></script>
```

Now our sketch uses both files as source and behaves as if all code is in `sktech.js`.

Solution: [ccfb_jumpinggame_1-1_player-setup](https://editor.p5js.org/legie/sketches/nuSIRXHVW)

### 1.2 Player Placeholder


In `player.js` create the variables and functions to draw our player character.

```js
// Player variables and functions

let playerX = 0; // Current position
let playerY = 0;
let playerSize = 50;
let playerYOnGround = 0; // We need this position over and over again, so let's save it


function initPlayer() {

    // Place the player at the middle of the screen...
    // ...in width...
    playerX = width * 0.5;

    // ...and in height.
    playerYOnGround = height - playerSize * 0.5;
    playerY = playerYOnGround;
}


function animatePlayer() {
    fill(255, 0, 0);
    ellipse(playerX, playerY, playerSize);

}
```

In `sketch.js`, call the functions, we just created:

```js
function setup() {
    createCanvas(400, 400);

    initPlayer();
}

function draw() {
    background(220);

    animatePlayer();
}
```

We can now see our circle, meaning the placeholder for the player graphics at the bottom of our canvas.

Solution: [ccfb_jumpinggame_1-2_player-placeholder](https://editor.p5js.org/legie/sketches/oQQgp0ZlQ)


### 1.3 Player Jumping

Now, we want to add the key input for activating the "jumping". For that we add a global variable jumping, which is either false, if we are not jumping, or true, when we are jumping. We set that variable in a keyPressed() function and check for its value in draw (where we eventually want to do the jumping - which is adjusting the position of the player).

For the up arrow we need the system variable `keyCode` for special keys. You can find it in the [reference](https://p5js.org/reference/p5/keyPressed/).


For that, we need to add new global variables in `player.js`.

```js
...

// Jumping Variables
let jumpHeight = 0; // The current height of the player in each frame
let jumpStrength = 0; // Value that we add the the player's position for the jumping
let jumping = false; // Are we currently jumping? Set to true while the player is jumping
let jumpStrengthMax = 5; // Constant value, controlling the speed of the jumping

...
```


The actual jumping works as follows: we have a variable `jumpHeight`, which tracks the current jumping height of the player in each frame and a variable `jumpStrength`, which tracks the value that we want to add to the jumpHeight in each frame. The jumping is then computed in each frame by adjusting the jumpHeight with jumpStrength and subtracting the `jumpHeight` from `playerYOnGround` to get the final postion.
  
`jumpStrength` is zero when we are not jumping.


```js
function animatePlayer() {

    if (jumping) {
        jumpHeight += jumpStrength; // Add force to current height
    }

    // jumpHeight is zero when we are not jumping
    playerY = playerYOnGround - jumpHeight;

    fill(255, 0, 0);
    ellipse(playerX, playerY, playerSize);
}
```


The `jumpStrength` gets set to a positive value after the arrow key is pressed.

Let's implement the reading of the arrow key. As there is only one `keyPressed` function, which might affect different components later, we keep it in `sketch.js`. 
  
Also, we add the global variables jumpStrengthMax, which is a constant value for controlling the initial speed of the jumping.

```js

// INTERACTION
// Key input for controlling the jump:
// the up-arr0w key makes the
// player jump
function keyPressed() {

if (keyCode == UP_ARROW) {
        // This will trigger to compute the jumping movement in setup()
        jumping = true; 
        jumpStrength = jumpStrengthMax;
    }
}
```

We need to make sure that the player also comes down at some point. So, we need to make the value jumpStrength negativ at some point. With a negativ value, the direction of the movement is reversed and the player moves down again. For that we add the constant global variable `gravity` and subtract `gravity` each frame from jumpStrength. Then at some point jumpStrength will become negative and the direction of the jump in reversed.


```js
...
let gravity = 0.1;


function animatePlayer() {

    if (jumping) {

        // Eventually, jumpStrength will become negative
        // and by that the jumping direction is reversed.  
        // This brings the player back to the ground.
        jumpStrength = jumpStrength - gravity;
        jumpHeight += jumpStrength; // Add force to current height
    }

    // jumpHeight is zero when we are not jumping
    playerY = playerYOnGround - jumpHeight;

    fill(255, 0, 0);
    ellipse(playerX, playerY, playerSize);
}
```

Usually a "force" such as `jumpingStrength` is slightly reduced each frame to further slow the movement down. Adding a small factor to slow down the movement makes it look more natural. However, this step is really just cosmetics. We can make the movement look anyway we want.

```js
...
let gravity = 0.1;


function animatePlayer() {

    if (jumping) {

        // Eventually, jumpStrength will become negative
        // and by that the jumping direction is reversed.  
        // This brings the player back to the ground.
        jumpStrength = (jumpStrength * 0.99) - gravity;
        jumpHeight += jumpStrength; // Add force to current height
    }

    // jumpHeight is zero when we are not jumping
    playerY = playerYOnGround - jumpHeight;

    fill(255, 0, 0);
    ellipse(playerX, playerY, playerSize);
}
```


For making the player's coming down stop at the ground, we add a check whether `jumpHeight <= 0` (which it is when the player is back on the ground) and set `jumping` to `false` and `jumpHeight` and `jumpStrength` to zero. Then the jumping activity is over.


```js
...

function animatePlayer() {

    if (jumping) {

        // Eventually, jumpStrength will become negative
        // and by that the jumping direction is reversed.  
        // This brings the player back to the ground.
        jumpStrength = (jumpStrength * 0.99) - gravity;
        // Add force to current height
        jumpHeight += jumpStrength; 

        // Check if we are back on the ground 
        // and want to stop the jumping
        if (jumpHeight <= 0) {
            jumping = false;
            jumpHeight = 0;
            jumpStrength = 0;
        }
    }

    // jumpHeight is zero when we are not jumping
    playerY = playerYOnGround - jumpHeight;

    fill(255, 0, 0);
    ellipse(playerX, playerY, playerSize);
}
```


Solution: [ccfb_jumpinggame_1-3_player-jumping](https://editor.p5js.org/legie/sketches/g3L7rq5qS)



### 1.4 Player Graphics

In this step we are replacing the circle with the animated player graphics.

For that, add a folder called `guy` to your sketch and add the graphics in `jumping_game_guy` , namely `guy-X.png`, to that folder.

Now, let's display those images in sequence in `player.js`.


```js
...

// Image Variables
let numberPlayerImg = 6;
let playerImg = []; // Image array
let playerImgIndex = 1; // Index the image currently displayed
let animationSlowDown = 8; // The higher the value, the slower the animation

```

Loading the images:

```js

function loadPlayer() {

    // Store images of player in array
    for (let i = 0; i < numberPlayerImg; i++) {
        playerImg.push(loadImage("guy/guy-" + i + ".png"));
    }
}
```
Add `loadPlayer()` to a `preLoad()` function in `sketch.js`:

```js
// Preload external files before calling setup()
function preload() {
    loadPlayer();
}
```


Displaying and animating the images in `animatePlayer()`:

```js
    // fill(255, 0, 0);
    // ellipse(playerX, playerY, playerSize);

    // Walk cycle
    image(playerImg[playerImgIndex], playerX, playerY);

    // Walk images are images 0..3
    // We want to iterate the walking image for each draw call.
    // For that, we count up playerImgIndex up until 3
    // and then back to 0

    if (frameCount % animationSlowDown == 0) { // Every 8th frame
        playerImgIndex++; // Next image

        if (playerImgIndex > 3) { // Reached last walk cycle image
            playerImgIndex = 0 // Back to first image
        }
    }
```

As for an image the reference point is the upper-left corner, we have to adjust the player's positioning in `initPlayer()`:

```js
    // Place the player at the middle of the screen...

    // (for an image object the reference point
    // is the upper left corner)

    // ...in width...
    playerX = (width * 0.5) - (playerSize * 0.5);

    // ...and in height.
    playerYOnGround = height - playerSize;
    playerY = playerYOnGround;
```

There seems to be a strange offset, let's counterbalance that with a new variable that we also use for positioning the play in y.

```js
let bgGroundHeight = 45; // Visible ground height

...

playerYOnGround = height - playerSize - bgGroundHeight;
```

While we are here, lets also reset all used variables in the initPlayer function, which now looks in total as follows.

```js
function initPlayer() {

    // Place the player at the middle of the screen...

    // (for an image object the reference point
    // is the upper left corner)

    // ...in width...
    playerX = (width * 0.5) - (playerSize * 0.5);

    // ...and in height.
    // We also subtract the bgGroundHeight variable
    // to move the player up to the visible ground height
    playerYOnGround = height - playerSize - bgGroundHeight;
    playerY = playerYOnGround;

    jumping = false;
    jumpHeight = 0;
    jumpStrength = 0;
}
```

This is all we have to do for the player for now.

Solution: [ccfb_jumpinggame_1-4_player-graphics](https://editor.p5js.org/legie/sketches/g4PmnzKME)


### 1.5 Player Graphics Jumping

There is actually a different image for the little guy when he jumps. We need to use `guy-4.png` for the jumping in `animatePlayer()`.


```javascript
    // Choosing which player image to
    // draw based on the current
    // player activity
    if (jumping) {

        image(playerImg[4], playerX, playerY)

    } else {

        // Walk cycle
        image(playerImg[playerImgIndex], playerX, playerY);

        // Walk images are images 0..3
        // We want to iterate the walking image for each draw call.
        // For that, we count up playerImgIndex up until 3
        // and then back to 0

        if (frameCount % animationSlowDown == 0) { // Every 8th frame
            playerImgIndex++; // Next image

            if (playerImgIndex > 3) { // Reached last walk cycle image
        playerImgIndex = 0 // Back to first image
            }
        }
    }
```

Solution: [ccfb_jumpinggame_1-5_player-graphics-jumping](https://editor.p5js.org/legie/sketches/uf2bsNqf6)



## 2. The Background

For the background, we animated on image repeatedly in x.

### 2.1. BG Setup

* Create a new file `background.js`
* In `index.html` add the following line under `<script src="sketch.js"></script>`

```html
<script src="background.js"></script>
```

Solution: [ccfb_jumpinggame_2-1_bg_setup](https://editor.p5js.org/legie/sketches/Z-K9SEN7x)

### 2.2. BG Animation

We know all the steps we need to do from the player, hence we do everything at once now.

Add a folder called `bg` to your sketch and add the graphics `background.png` for the background to that folder.

Do the following steps in `background.js`


Global variables:

```js
// Background variables
let bgImg; // Background image
let bg1X = 0; // X position of first background
let bg2X = 0; // X position of second background
let bgSpeed = 1; // Speed of background animation
```

Loading the image file:

```js
function loadBackground() {
    bgImg = loadImage("bg/background.png");

}
```

Initializing the bg values:

```js
function initBackground() {

    bg1X = 0;
    // To get an infinite loop of the moving background
    // we display it two times and shift the second image
    // to the right end of the first.
    // For that we need to initialize its X position
    // as the width of the image:
    bg2X = bgImg.width;
}
```

Display and animate the background:

```js

function animateBackground() {
    // Draw background
    image(bgImg, bg1X, 0);
    image(bgImg, bg2X, 0);

    // Move both images to the left constantly
    // by subtracting the bgSpeed variable
    // from their X position
    bg1X -= bgSpeed;
    bg2X -= bgSpeed;

    // We need to put back the images to the right side
    // when they left the screen at the left side
    // by setting their X position to the image width
    if (bg1X <= -bgImg.width) {
        bg1X = bgImg.width;
    } else if (bg2X <= -bgImg.width) {
        bg2X = bgImg.width;
    }
}
```

Add all functions in `sketch.js` to `preload()`, `setup() `, and `draw()` before the player functions. Now you should have an animated background.

Our current canvas size must match the size of the background image, hence change `createCanvas()`:

```js
createCanvas(480, 360);
```

We also want the player to be walking on the ground, not on the bottom of the canvas anymore. We can re-use the variable `bgGroundHeight` for that. 

For tidiness reasons let move `let bgGroundHeight = 10; // Visible ground height` from `player.js` to `background.js`. Then adjust its value as needed, which is `55`.

Now we have the final graphics and animation for player and background.

Solution: [ccfb_jumpinggame_2-2_bg_animation](https://editor.p5js.org/legie/sketches/XPPxI7K9r)

## 3. Coin

The is always only one coin in the game. A coin is animated and can be collected. When a coin is collected it disappears and a new coin is created.

### 3.1. Coin Animation

We add a new file `coins.js` and add it to the sketch.

```html
<script src="coin.js"></script>
```

For that, add a folder called `coin` to your sketch and add the graphics in `jumping_game_coins` , namely `coin-X.png`, to that folder.

Then, coins are loaded, displayed and animated in `coin.js` as we did for the player and background.

```js
// Coin Variables
let coinX = 0; // Current position
let coinY = 0;
let coinSize = 48; // Coin images are 48x48

let coinCollected = false; // True when the player collected the coin

// Image Variables
let coinImg = []; // Image array
let numberCoinImg = 4;
let coinImgIndex = 0; // Index of the image currently displayed


function loadCoin() {
    for (i = 0; i < numberCoinImg; i++) {
        coinImg[i] = loadImage("coin/coin-" + i + ".png");
    }
}

function initCoin() {

    // Place the coin at the right side of the screen...
    coinX = bgImg.width;
    //coinX = (width * 0.5) - (coinSize * 0.5);

    // ...at a random height between
    // 100 (because we don't want the coin too high)
    // and
    // the sketch height minus the coin image size
    // minus the ground height visible at the background image
    coinY = random(100, height - coinSize - bgGroundHeight);
}


function animateCoin() {

    image(coinImg[coinImgIndex], coinX, coinY);

    // Display the image animation
    if (frameCount % animationSlowDown == 0) { // Every 8th frame
        coinImgIndex++; // Next image

        if (coinImgIndex == numberCoinImg) { // Reached last image
            coinImgIndex = 0 // Back to first image
        }
    }

    // Move the coin to the left (with the background)
    coinX -= bgSpeed;


    // Create a new coin when it left the screen
    if (coinX <= 0 - coinImg[1].width) {
        initCoin();
    }
}
```

Add all functions in `sketch.js` to `preload()`, `setup() `, and `draw()` after the player functions. Now you should have an animated coin.

Solution: [ccfb_jumpinggame_3-1_coins-animation](https://editor.p5js.org/legie/sketches/MfPBFSkQS)

### 3.2. Coin Collection

First, we need to detect a potential player-coin collision, to make the coin the disappear.

First, we create a two new variables: one for tracking a collision and with that a coin collection and one for tracking the number of collected coins:

```js
let coinCollected = false; // True when the player collected the coin
let coinCollectedNumber = 0;

...
```

In `animateCoin()` we check if the distance between player and coin is half of the player's size plus half of the coin's size. If the distance is smaller, they collide.



```js
function animateCoin() {

    ...

    // Check for collision between coin and player:
    // They collide if the distance between their positions is equal or less
    // than both of their "radiuses" (half their size)
    if (dist(coinX, coinY, playerX, playerY) <= playerSize / 2 + coinSize / 2) {
        coinCollected = true;
        coinCollectedNumber++;
    }
}
```

Next, we need to make the current coin disappear and create a new one. For that we can extend the "running out of screen" logic:

```js
    // Create a new coin when it left the screen or when it was collected
    if (coinX <= 0 - coinImg[1].width || coinCollected) {
        initCoin();
    }
```

In `initCoin()` we must also set `coinCollected = false;` for re-starting the coin creation.

Solution: [ccfb_jumpinggame_3-2_coin-collection](https://editor.p5js.org/legie/sketches/Rwp0jBOro)

### 3.3. Coin Counting

We are already tracking the number of the collected coins. Check it with ` print("Coins collected: " + coinCollectedNumber);`.


Now, we want to display the number of coins selected as text on the screen. For that we write a new coin function in `coin.js`, which puts text on the canvas.

```js
function displayCoins() {

    fill(0, 0, 0);
    textSize(20);
    text(coinCollectedNumber, 10, 20);
}
```

Add the function `displayCoins();` in `sketch.js` to `draw()`

We can load a font up to our liking. For that downloaded the font and add it in a new folder `font` to your sketch.

As the font is globally used, we load and set it gloablly for the whole game in `sketch.js`. This structure is once again a matter of taste.

```js
// This is needed in
// all tabs, hence I
// put it here
let gameFont;

...

function preload() {

    gameFont = loadFont('fonts/ka1.ttf');

    ...
}

function setup() {

    ...

    textFont(gameFont);
    textAlign(CENTER, CENTER);

    ...
}
```

Sets the way text is aligned when text() is called. Center puts the text's reference point for its position to the text's center.

We need to change the coin number text position, while doing that, let's also add a tiny coin image to the coin counter as well.

Add into the coin folder the small coin's image file.

```js
let coinSmallImg;

...

function loadCoin() {
    
    ...
    coinSmallImg = loadImage("coin/coin_small.png");
}

...


function displayCoins() {

    image(coinSmallImg, 10, 10);
    fill(0, 0, 0);
    textSize(20);
    text(coinCollectedNumber, 49, 19);
}

```

Solution: [ccfb_jumpinggame_3-3_coin-counting](https://editor.p5js.org/legie/sketches/apH1MHy_Y)


## 4. Enemies

Similar to the coins, there should be only ever one enemy on scree, walking on the ground like the player but in opposite direction. Upon player-enemy collision in x, the player dies. But if the player jumps "onto" the enemy, meaning the collision occurs when the player is jumping and coming down.


### 4.1 Enemies Animation

We add a new file `enemies.js` and add it to the sketch.

```html
<script src="enemies.js"></script>
```


For that, add a folder called `enemies` to your sketch and add the graphics in `jumping_game_enemies` , namely `baddie-X.png`, to that folder. Again, we have a walk cycle and an animation, for when the enemy dies.

Then, enemies are loaded, displayed and animated in `enemies.js` as we did for the player, background, and coins.

```js
// Enemy Variables
let enemyX = 0; // Current position
let enemyY = 0;
let enemySize = 48; // Coin images are 48x48

let enemyDead = false; // True when the player collected the coin
let enemySpeed = 1.5;

// Image Variables
let enemyImg = []; // Image array
let numberEnemyImg = 5;
let enemyImgIndex = 0; // Index of the image currently displayed

function loadEnemy() {
    for (i = 0; i < numberEnemyImg; i++) {
        enemyImg[i] = loadImage("enemies/baddie-" + i + ".png");
    }
}

function initEnemy() {

    // Place the coin at the right side of the screen...
    enemyX = bgImg.width;
    enemyY = height - enemySize - bgGroundHeight + 10;

}

function animateEnemy() {


    image(enemyImg[enemyImgIndex], enemyX, enemyY);

    // Display the image animation
    if (frameCount % animationSlowDown == 0) { // Every 8th frame
        enemyImgIndex++; // Next image

        if (enemyImgIndex == numberEnemyImg - 1) { // Reached last image
            enemyImgIndex = 0 // Back to first walk cycle image
        }
    }

    enemyX -= bgSpeed * enemySpeed;


    // Give the enemy a new position when it left the screen
    if (enemyX <= 0 - enemyImg[1].width) {
        initEnemy();
    }
}

```

Add all functions in `sketch.js` to `preload()`, `setup() `, and `draw()` after the player functions. Now you should have an walking enemy.

Solution: [ccfb_jumpinggame_4-1_enemies-animation](https://editor.p5js.org/legie/sketches/y5gcgmRX6)

### 4.2 Enemies Collision

We want two type of collisions: 
1. The player is walking and the player dies upon collision
2. The player is jumping and the enemy dies upon collision

The collision check in `animateEnemy()` identical to the coin collision.

```js

...

    // Check for collision between coin and player:
    // They collide if the distance between their positions is equal or less
    // than both of their "radiuses" (half their size)
    if (dist(enemyX, enemyY, playerX, playerY) <= playerSize / 2 + enemySize / 2) {

        print("dead player");
    }
...
```

Now, we add the two types of collisions:

```js

...

    // Check for collision between coin and player:
    // They collide if the distance between their positions is equal or less
    // than both of their "radiuses" (half their size)
    if (dist(enemyX, enemyY, playerX, playerY) <= playerSize / 2 + enemySize / 2) {

        if(jumpStrength < 0) {
            print("dead enemy");
        }
        else {
            print("dead player");
        }
    }
...
```

If the enemy dies, we need to show the graphics for that and then make the old enemy disappear and create a new one. 

For that we create a variable that tracks, if the enemy is dead or not and set that upon collision:

```js
let enemyDead = false; // True when the player collected the coin
...


function initEnemy() {

    ...
    enemyDead = false;
}

function animateEnemy() {

...

    // Check for collision between coin and player:
    // They collide if the distance between their positions is equal or less
    // than both of their "radiuses" (half their size)
    if (dist(enemyX, enemyY, playerX, playerY) <= playerSize / 2 + enemySize / 2) {

        if(jumpStrength < 0) {
            enemyDead = true;
        }
        else if(!enemyDead) {
            print("dead player");
        }
    }
...

}
```

Next we use the `enemyDead` variable to display the graphics for the dead enemy in `animateEnemy()`:

```js
    if(!enemyDead){
        image(enemyImg[enemyImgIndex], enemyX, enemyY);
    } else {
        image(enemyImg[numberEnemyImg - 1], enemyX, enemyY);
    }
```

For having the player dies, it is game over and the game should end. For that we add a global variable `gameOver` in `sketch.js`.

```js
let gameOver = false;
```

When the player dies, we set that variable to true in `enemies.js`:

```js

function animateEnemy() {

...

    // Check for collision between coin and player:
    // They collide if the distance between their positions is equal or less
    // than both of their "radiuses" (half their size)
    if (dist(enemyX, enemyY, playerX, playerY) <= playerSize / 2 + enemySize / 2) {

        if(jumpStrength < 0) {
            enemyDead = true;
        }
        else if(!enemyDead) {
            print("dead player");
            gameOver = true;
        }
    }
...

}
```

Then, in `player.js`, we set the graphic to the dead player and make it move with the background:

```js
function animatePlayer() {

    ...

    // Choosing which player image to
    // draw based on the current
    // player activity
    if (jumping && !gameOver) {

        image(playerImg[4], playerX, playerY)

    } else if(gameOver) {
      
        image(playerImg[5], playerX, playerY)
        playerX -= bgSpeed;

    }  else {

        ...
    }
}
```

Solution: [ccfb_jumpinggame_4-2_enemies-collision](https://editor.p5js.org/legie/sketches/NYUM3UMbG)

## 5. Game Logic

When the player dies the game should stop and the option to re-start the game should appear.

### 5.1. Stop

First, we make the game stop in `sketch.js`. When the game stops, player, enemies and coins should disappear and the while the background stays the same.

```js
function draw() {
    background(255);

    animateBackground();

    if (!gameOver) {

        animateCoin();
        animateEnemy();
        animateBirds();
    } else {

        print("GAME OVER");
    }
    animatePlayer();
    displayCoins();
}
```

Next, we display a "game over" and "play again" text on the screen:

```js
function draw() {
    background(255);

    animateBackground();

    if (!gameOver) {

        animateCoin();
        animateEnemy();
        animateBirds();
    } else {
        displayGameOver();
        print("GAME OVER");
    }
    animatePlayer();
    displayCoins();
}

...

function displayGameOver() {

    // The "game over" text
    fill(255, 0, 0);
    textSize(42);
    text("Game Over", width * 0.5, height * 0.5);

    // The "play again" text
    let textPlayAgain = "Play Again?";
    let textPlayAgainW = textWidth(textPlayAgain);
    let textPlayAgainX = (width * 0.5) - textPlayAgainW * 0.5;
    let textPlayAgainY = height * 0.5 + 30;

    textSize(32);
    text(textPlayAgain, width * 0.5, height * 0.5 + 50);
}
```


For enabling a selection of the "play again" option we manually detect a mouse click inside of the area of the "play again" text and change the text's color to red:


```js
function displayGameOver() {

    // The "game over" text
    fill(255, 0, 0);
    textSize(42);
    text("Game Over", width * 0.5, height * 0.5);

    // The "play again" text
    let textPlayAgain = "Play Again?";
    let textPlayAgainW = textWidth(textPlayAgain);
    let textPlayAgainX = (width * 0.5) - textPlayAgainW * 0.5;
    let textPlayAgainY = height * 0.5 + 30;

    // Is the mouse on the text?
    if (mouseX > textPlayAgainX && mouseX < textPlayAgainX + textPlayAgainW &&
        mouseY > textPlayAgainY && mouseY < textPlayAgainY + 50) {
        fill(63, 143, 110);

        // Restart the game if the mouse is clicked
        if(mouseIsPressed){

            print("RESTART");
        }
    } else {
        fill(0, 0, 0);
    }

    textSize(32);
    text(textPlayAgain, width * 0.5, height * 0.5 + 50);
}
```

For restarting the game, we can simply can call `setup()`, which initializes all elements. We also need to set `gameOver` to false and `coinCollectedNumber` to zero (that variable is not part of `initCoin()`).


```js
function displayGameOver() {

    ...

        // Restart the game if the mouse is clicked
        if(mouseIsPressed){

            gameOver = false;
            coinCollectedNumber = 0;
            setup();
        }

    ...
}
```

Now, the game should re-start afresh, when "play again" is selected.

Solution: [ccfb_jumpinggame_5-1_gamelogic_stop](https://editor.p5js.org/legie/sketches/Z6ebEmTJp)

## 6. Sound

We have three sounds: the background song and a jingle when a coin is selected or the player dies.


### 6.1 Sound BG

We will implement the theme loop as part of the `background.js` . Add the `theme_loop_small.wav` file to the `bg` folder.

```js
let soundBackground;

...


function loadBackground() {
    ...
    // Loading the soundfile
    soundBackground = loadSound('bg/theme_loop_small.wav');
}


function initBackground() {
    ...

    // Quick hack to restart
    // when game over
    soundBackground.stop();
    soundBackground.play();

    // Repeating the sound file
    soundBackground.loop();

    // Reducing the volume with 
    // a value between 0 (no sound) to 1 (full volume)
    soundBackground.setVolume(0.1);
}
```

Now you should have a background song repeating.

Solution: [ccfb_jumpinggame_6-1_sound-bg](https://editor.p5js.org/legie/sketches/bF6EKt7bb)


### 6.2 Sound Effects

First let's add a sound to the coin collection in `coin.js`. Add the `coin_collected.wav` file to the `coin` folder.

```js
let soundCollected;

...

function loadCoin() {

    ...

    // Loading the sound file, saving it in soundCollected
    soundCollected = loadSound('coin/coin_collected.wav');
    soundCollected.playMode('restart');
}



function animateCoin() {

    ...

    if (dist(coinX, coinY, playerX, playerY) <= playerSize / 2 + coinSize / 2) {
        coinCollected = true;
        coinCollectedNumber++;
        // Playing the sound effect
        soundCollected.play();
    }

    ...

}
```



Let's repreat the steps for a sound upon enemy collosion in `enemies.js`. Add the `enemy_collision.wav` file to the `enemies` folder.

```js
let soundCollision;


function loadEnemy() {


    soundCollision = loadSound('enemies/enemy_collision.wav');
    soundCollision.playMode('restart');
}

...

function animateEnemy() {

    ...
        // Check for collision between coin and player:
    // They collide if the distance between their positions is equal or less
    // than both of their "radiuses" (half their size)
    if (dist(enemyX, enemyY, playerX, playerY) <= playerSize / 2 + enemySize / 2) {

        if(jumpStrength < 0) {
            enemyDead = true;
        }
        else if(!enemyDead) {
            print("dead player");
            gameOver = true;

            soundCollision.play();
        }
    }

    ...
}
```

Solution: [ccfb_jumpinggame_6-2_sound-effects](https://editor.p5js.org/legie/sketches/PcX8yjOgd)

## 7. Enemies Birds

Add the flying enemies yourself. You can use the `cherry-X.png` files in folder `jumping_game_birds`.

Solution: [ccfb_jumpinggame_7-1_birds](https://editor.p5js.org/legie/sketches/MEVmLtqGa)

---

*The End*