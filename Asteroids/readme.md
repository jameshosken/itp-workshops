# Asteroids in p5.js

## Complete Code
https://editor.p5js.org/hosken/sketches/k93xnkA3X


## Housekeeping
The easiest way to follow along with this workshop is to use the [p5 web editor](https://editor.p5js.org/). It's free and open to anyone; to save you'll need to create an account.

We have a lot to cover in 2 hours. For the sake of flexibility this workshop has 3 checkpoints, each of which constitutes a noble goal. After each checkpoint we'll evaluate where we are and whether to spend time reviewing material or moving forwards.

Ask questions at any time. I will either try anwser directly, or ask you to wait for a checkpoint (usually because your question will be forthcomingly answered). If I cannot answer you question I shall refer you to a [higher authority](https://www.google.com/). Which leads to:

Everything we do here is googlable. I don't expect you'll absorb everything in 2 short hours, rather I hope to demonstrate some of the fundamental concepts so that you know what to google later. In addition to google the [p5 reference](https://p5js.org/reference/) is an important and valuable resource.

If I go to fast please slow me down. If I'm going too slow for you feel free to experiment ahead using this guide.

## Prologue: A quick review of p5 concepts 

### The default sketch
- **setup()**: Runs once at the beginning of your sketch
- **draw()**: Runs over and over, about 60 times a second
- **createCanvas(x,y)**: Determines the size of your sketch in pixels
- **background(c)**: fills the whole canvas with c

### Numbers
There are only 2 numbers we care about today: **0** and **255**. When they are used as colour, 0 is pure black and 255 is pure white. 

### Variables

Variables are like a box you can put stuff in.

- **Local** variables exist within 2 {brackets} and cannot be accessed outside of those brackets
- **Global** variables exist within 2 {brackets} and cannot be accessed outside of those brackets

## Section 1: Making a starfield


### Making a single star (the stupid way)

*What shape is a star?*

- **point(x,y)**: draws a point at x and y
- **stroke(n)**: determines colour of what comes next
- **strokeWeight(n)**: determines thickness of stroke

```javascript
stroke(255);
strokeWeight(3);
point(200,200);
```

I know all this in my brain, but if you're new you can find this info on the [reference](https://p5js.org/reference/)

### Making lots of stars (the stupid way)

*Copy, paste, repeat until you die*

There are two major problems with this method: it's **hard-coded** and **tedious**. Code can help solve both of these problems by **randomising** our star location and then **automating** the generation of stars.

First let's focus on randomisation

### Making a single star (the clever way)

We can randomise the placement of our stars so that we don't have to manually input a position for each star.

- **random(min, max)** provides a random value

```javascript
let x = random(0,width);
let y = random(0,height);  
point(x, y);
 ```

We're on the right track, but stars don't bounce randomly around the screen. We need a way to store the values consistently between frames. This is where **global** variables come in handy!

If we put the xy variables *outside* of the function, the sketch will remember them between frames.

But, there's a problem! For reasons a little too handwavy for this moment, special p5 functions, like **random()** only work during and after **setup()**. So, we need to *define* the variable before setup, but *assign* it in setup. 

This pattern will be repeated a lot throughout this workshop.

```javascript
let x ;
let y ;

function setup() {
  createCanvas(500, 500);

  x = random(0,width);
  y = random(0,height);
}
```
---

Now we can make a few of them using the stupid way. However, to avoid something that looks very clunky like this:

```javascript
//Bad way: do not use:
let x1;
let y1;
let x2;
let y2;
let x3;
let y3;
```

Wouldn't it be nice to store all the information about a star in one variable? 

- **{brackets}** allow us to store many variables in one, and name them (technically knownn as **Objects** in javascript). For instance:

```javascript
//Better way: use this for now
let star = {} 	//Create an object to store info about our star

function setup() {
  createCanvas(500, 500);

  // Add information to the star object:
  star.x = random(0,width); 		
  star.y = random(0,height);
}
```

This way when we think about a 'star', we're not thinking about many things all over the place, we're thinking about one single thing (albeit with many things inside it).

### Making lots of stars (the clever way)

*Programming is inherently lazy. When you see patterns of repetition, think about how you can reduce redundancy. Aim for the least amount of work possible.*

The next steps requires two new programming concepts, so hold on to your seats.

#### Storing lots of things (lists)

- **Lists []** allow us to store many variables. At first they may seem confusingly like objects, but a key difference is that lists in JavaScript are **ordered**.

Using the box metaphor, an **object** is a big box that you throw a bunch of other boxes jumbled in, whereas a **list** is a neat row of boxes.

```javascript
let stars = []	//create empty list of stars

function setup(){
	createCanvas(500, 500);

	let star = {};				//Define star locally
  	star.x = random(0,width);	//Add info as before
  	star.y = random(0,height);
  	stars.push(star);			//Now add the star to the list
  
}
```

To access the values in a list, we use `listName[index]` where *index* is the position of the value in the list, **staring at zero**.

From above, we now have a list of **stars** with a single star in it. To display that star:

```javascript
function draw() {

  background(0);

  stroke(255);  strokeWeight(3);

  //Use stars[0] to access the first (and only) item of stars.
  point(stars[0].x, stars[0].y);	

}
```

*Why did we do that? We're back where we started?? Nothing has changed!*

#### Repeating things (loops)

Having a list means that we can easily add more stars to our sketch. 

```javascript
	//Adding more stars involves repeating this chunk of code 
	let star = {}; //Define star locally
	star.x = random(0, width); //Add info as before
	star.y = random(0, height);
	stars.push(star); //Now add the star to the list
```

Since we have everthing to do with adding a star in one place, automating that process is relatively simple

- **Loops** allow us to repeat a chunk of code a certain number of times. 

A loop works like such:
1. Start a counter, called *i*, from zero
2. Set a max number to stop counting at
3. Set the increment you want to count by (usually 1)
4. Execute the code in {brackets} until i reaches the max number.

```javascript
	
for (let i = 0; i < 10; i++) {
	let star = {}; 
	star.x = random(0, width); 
	star.y = random(0, height);
	stars.push(star); 
}
```

Now we can display the stars using the same type of loop. In the last case we didn't really care what *i* was, but in this case we can use *i* as the *index* for our list, essentially counting through each item!

```javascript	
for (let i = 0; i < 10; i++) {
	point(stars[i].x, stars[i].y);
}
```

Imagine how long it'd have taken us to copy/paste these 10 values. What about 100? 

### Bonus Features 

#### Depth
Since all the info for our star is contained within a single 'star' object, we can add and use more information about each star easily.

E.g. what if we add information about size?

#### Adjustability
One last thing to clean up the code a bit: add a tweaking variable for number of stars


## Checkpoint 1
How are we doing? *Save your sketch!*

---

---

## Section 2: Adding a ship

### Custom Functions
*setup(), draw(), background(), etc are all p5.js functions. We can make our own functions, which will help us become the laziest programmers we can be!*

As you're coding, look for chunks of code that do *one definable thing*. Generally speaking, if a chunk of code is more than a few lines, and does one specific thing, you can turn it into a function!

```javascript
for (let i = 0; i < numOfStars; i++) {
    let star = {}; //Define star locally
    star.x = random(0, width); //Add info as before
    star.y = random(0, height);
    star.diam = random(1,3);
    stars.push(star); //Now add the star to the list
  }
```
The above is a hefty chunk, but all it does is *generate a starfield*. So I'm going to put it in a function called **generateStars()**.
```javascript

function generateStars(){
	for (let i = 0; i < numOfStars; i++) {
	    let star = {}; //Define star locally
	    star.x = random(0, width); //Add info as before
	    star.y = random(0, height);
	    star.diam = random(1,3);
	    stars.push(star); //Now add the star to the list
	}
}
```

now my setup() looks like:

```javascript
function setup() {
  createCanvas(500, 500);
  generateStars();
}
```

The benefits of this become vast down the road, but for now this change has the simple benefit of making it a lot easier to read the flow of your code, and keep track of what happens when. 

Do the same with displayStars() and we're ready to make a ship!

*Keep track of the {brackets}; a 'SyntaxError' might mean you have too many or too few.*

### Generating a ship

Building on the concepts above, we know we'll need an object to store all the information about our ship.

```javascript
let ship = {};
```

Now let's make a function **generateShip()**, and call it in setup().

```javascript
function generateShip() {
  
}
```

### Turning the ship
What do we put in this function? We know we want a ship, and we want it to turn. Let's store its position and rotation:

```javascript
function generateShip() {
  ship.x = width/2;
  ship.y = height/2;
  ship.rotation = 0; //start with no rotation
}
```

To handle the turning of the ship, we'll make a new function called **turnShip()**. Inside it we'll add some keyboard interaction to determine when to add and when to subtract rotation.

**keyIsDown(key)** tells us if a key is being pressed. If you want to use alphanumeric keys you'll need to know the [keycode](https://p5js.org/reference/#/p5/keyCode), but there are some special keys (such as LEFT_ARROW) that have their own identifiers.

```javascript
function turnShip() {

  if (keyIsDown(LEFT_ARROW)) {
    ship.rotation -= .1;
  }
  if (keyIsDown(RIGHT_ARROW)) {
    ship.rotation += .1;
  }

}
```

Now let's write a **displayShip()** function so we can see the results of our work. We need to be able to display the ship at its position, and rotate it by its rotation. 

Luckily, p5 has a [rotate(r)](https://p5js.org/reference/#/p5/rotate) function we can use! The tricky thing is that it can only rotate around the origin (0,0), which is at the top left of the canvas. 

Luckily again, there's a way to solve that, by moving the origin! [translate(x,y)](https://p5js.org/reference/#/p5/translate)

When we use translate or rotate it's good practice to use **push()** and **pop()** as well. **push()** essentially saves the current settings of the sketch, and **pop()** reverts to those settings. This prevents unwanted rotation of future objects.

```javascript

function displayShip(){
  push();
  strokeWeight(1);
  stroke(255);
  
  translate(ship.x, ship.y);	//Translate the origin to where the center of the ship should be
  rotate(ship.rotation);		// Rotate round that new origin
  
  //Draw a triangle around this new, rotated, origin
  beginShape();
  vertex(0, -25);
  vertex(15, 15);
  vertex(-15, 15);
  endShape();
  pop();
}
```

### Moving the ship

#### Introducting Vectors

A vector is a way of representing 2 ordered numbers. In p5 there are some handy functions we can perform on vectors which make them great to use for position, rotation, and acceleration.

Rather than storing ship.x and ship.y, we can store location as one vector, ship.pos.

*Don't forget to change the displayShip() function accordingly!*

```javascript
function generateShip() {
  ship.pos = createVector(width / 2, height / 2);
  ship.vel = createVector(0, 0);
}
```

#### Position, Velocity, Acceleration

- **Position** is where the spaceship is on screen
- **Velocity** is change in that position over time (so position = position + velocity)
- **Acceleration** is a change in that velocity over time (velocity = velocity + acceleration)

We only want to add acceleration when we tell the ship to go forward, but we want to add velocity each frame.

For more insight on these concepts I strongly recommend [Nature of Code](https://natureofcode.com/)

In a new function, **moveShip()**, we'll register the keypress for accelerate, and then apply the above algorithm.

We'll also need to rotate the acceleration vector by the ship's rotation, which can be done using the vector function **vector.rotate(r)**

I've also added a new ship variable, ship.thrust, so we can tweak the amount of acceleration
```javascript

function moveShip(){
  
  let acc = createVector(0,0);
  
  if(keyIsDown(UP_ARROW)){
     acc = createVector(0, ship.thrust );	//Add acceleration pointin along ship's axis (up)
     acc.rotate(ship.rotation);		//Rotate by ship's rotation
  }
  
  ship.vel.add(acc);
  ship.pos.add(ship.vel);
  
}
```

### Wrapping the ship around the screen

The ship flies off the screen pretty quickly, let's make sure it will wrap back around when it does.

Wrapping around is something that I may want other things to do in the future (such as asteroids), so I'm going to make this function generic to any object with a position vector, and when I call the function pass in what I want to check edges on. 

``` javascript
function checkEdges(obj) {
  if (obj.pos.x < 0) {
    obj.pos.x = width;
  }
  if (obj.pos.x > width) {
    obj.pos.x = 0;
  }

  if (obj.pos.y < 0) {
    obj.pos.y = height;
  }
  if (obj.pos.y > height) {
    obj.pos.y = 0;
  }
}

// call with checkEdges(ship);

```


### Add parallax motion to stars

For consistency's sake, let's change the star object to use position as well.
```javascript
function moveStars(){
  
  for (let i = 0; i < numOfStars; i++) {
    vel = createVector(ship.vel.x, ship.vel.y);
    vel.mult(-.1 * stars[i].diam);
    stars[i].pos.add(vel);
    checkEdges(stars[i]);
  }
}
```

## Checkpoint 2
How are we doing? *Save your sketch!*

---

---

## Adding Asteroids

*Here we'll add asteroids to float around in space, detect whether we've hit them, then do something about it*

### Like stars, only bigger

We'll start by taking inspiration from the stars code

We're changing up the code by adding a velocity vector, increasing the size, and obviously changing the names.
```javascript
function generateAsteroids(){
  for (let i = 0; i < numOfAsteroids; i++) {
    let asteroid = {}; //Define star locally
    asteroid.pos = createVector(random(0, width), random(0, height));
    asteroid.vel = createVector(random(-1, 1), random(-1, 1))
    asteroid.diam = random(10, 50);
    asteroids.push(asteroid); //Now add the star to the list
  }
}
```

### Move them and display them

Similar to the way stars move, except using their own velocity information rather than the ship's.

```javascript
function moveAsteroids(){
 
  for (let i = 0; i < asteroids.length; i++){
    asteroids[i].pos.add(asteroids[i].vel);
    checkEdges(asteroids[i]);
  }
  
}

function displayAsteroids() {
  stroke(255);
  for(let i = 0; i < asteroids.length; i++){
    ellipse(asteroids[i].pos.x, 
            asteroids[i].pos.y, 
            asteroids[i].diam,
            asteroids[i].diam);
  }
}
```


### Checking for collisions

Collision detection can be a nightmare, so to simplify things we're going to pretend everything in our scene is a circle. We can detect if two circles are colliding by asking whether the sum of their radii is greater than the distance between their two centers. 

We need to check each asteroid against the ship for collision. We could either:
- put a detection algorithm in each asteroid and chack it against the ship, or
- put a detection algorithm in the ship and check it against each asteroid. 

At this point the decision is arbitrary but I can imagine in the future I'll want to check the ship for collisions against other things (powerups?, bullets?) so I'll attach it to the ship.

To make our lives a *little* easier I'm going to rename targets[i] to t, so we don't have to do so much typing.

Don't forget to add a **ship.diam** variable to make this work!

```javascript
//pass in a list of objects to check against
function checkShipForCollisions(targets){
  
  //Note this will crash if the target object does not contain a 'pos' vector.
  for (let i = 0; i < targets.length; i++){
    let t = targets[i];
    let distance = dist(ship.pos.x, ship.pos.y, t.pos.x, t.pos.y);

    let sumOfRadii = ship.diam/2 + t.diam/2;

    if(sumOfRadii > distance){
      //We have a collision!
      print("HIT");
    }
  }
}

```


A quick and dirty way to end the game is have a global variable called 'isGameOver', set to false in the beginning. In the draw loop, if isGameOver, then do nothing else. One a hit is detected, set isGameOver to true.

```javascript

let isGameOver = false;

function draw(){
  background(0);
  if(isGameOver){
    return; //Ends the current function.
  }
}
```

Add text here for extra effect.

## Checkpoint 3
How are we doing? *Save your sketch!*

---

---


## Extra Effects

### Parallax for asteroids too
The ship's velocity influnces the backdrop of the stars, so it makes sense that it would influence the asteroids too. This makes the game far more difficult and, hopefully, fun!

```javascript
    // Add this line to the moveAsteroids function.
    v = createVector(ship.vel.x, ship.vel.y); // This copies the variable so that we are not changing the ship velocity directly.
    asteroids[i].pos.add(v.mult(-1));
    
```

### Prevent collision within first second of game
Right now the asteroids spawn totally randomly. This means that they could start right on the ship. That's not a fun game to play. If we're a bit smarter about where the asteroids start we could give the player some breathing room at the start.


Inside the asteroid generation function, we'll choose a random spot for the asteroid, but if it's within a certain distance of the ship, we'll choose another random position, and check again. We'll keep doing this until the asteroid is out of the 'danger zone'

```javascript
    //Inside generateAsteroids()
    let pos = createVector(random(width), random(height));
    //A while loop will keep repeating while the given condition is true. 
    //In this case the given condition is that the distance between the ship and 
    // the asteroid is less than 200. ONce that is no longer true, the while loop ends.
    while (dist(pos.x, pos.y, ship.pos.x, ship.pos.y) < 200) {
      pos = createVector(random(width), random(height));
    }
    //While loop has ended, thus the position is a safe distance away from the ship.
    asteroid.pos = pos;

    ```

### Thruster feedback
We can keep track of whether we are thrusting, and display that info in a meaningful way.

Keep track of **ship.isThrusting** and use it to display an engine.


## Moving Forward & Review

You have all the tools required to create a bullet system with collision detection if that's what you wish to do, or you could leave the game as is and have the challenge be to avoid the asteroids for as long as possible. 

Take a moment to reflect on what we've covered, if you're new to javascript this was likely a lot of info. As I said before, the goal here is not to absorb everything, rather get a sense of what patterns to looks for and how to ask google what you want to know. 