Creating custom functions makes your sketch modular, easier to debug, and allows you to reuse code without rewriting it.

1. Basic Function Syntax

A custom function is built using the function keyword, a descriptive name, parentheses, and curly brackets containing the body of your code: 

```javascript
function nameOfFunction() {
  // The code you want to run goes here
}
```

2. A Simple Step-by-Step Example

Unlike built-in p5.js functions like `setup()` and `draw()` which run automatically, you must explicitly call your custom functions to execute them. 

Here is how you define a function that draws a basic emoji face, and how you call it inside draw():

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 2. Call your custom function
  drawHappyFace(); 
}

// 1. Define your custom function
function drawHappyFace() {
  fill(255, 204, 0); // Yellow
  circle(200, 200, 100); // Face
  
  fill(0); // Black eyes
  circle(180, 190, 10);
  circle(220, 190, 10);
  
  noFill();
  arc(200, 210, 50, 30, 0, PI); // Smile
}
```


3. Adding Parameters (Passing Inputs)

To make your function flexible, you can add parameters inside the parentheses. Parameters act like local placeholder variables that let you customize the function every time you call it. 

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // Call the function multiple times with different coordinates and sizes!
  drawCustomFlower(100, 150, 40); 
  drawCustomFlower(300, 200, 80);
  drawCustomFlower(200, 300, 60);
}

// Custom function with 3 parameters: x position, y position, and diameter
function drawCustomFlower(x, y, diameter) {
  fill(255, 100, 150);
  // Center petal
  ellipse(x, y, diameter, diameter);
  // Top, bottom, left, right petals using basic offsets
  ellipse(x - diameter/2, y, diameter/2, diameter/2);
  ellipse(x + diameter/2, y, diameter/2, diameter/2);
  ellipse(x, y - diameter/2, diameter/2, diameter/2);
  ellipse(x, y + diameter/2, diameter/2, diameter/2);
}
```

4. Returning Values

Functions can also calculate a value and send it back to whoever called it using the return statement. 

```javascript
function draw() {
  background(220);
  
  // Call the function to calculate the average width
  let middlePoint = calculateMiddle(0, width);
  
  line(middlePoint, 0, middlePoint, height); // Draws a line down the middle
}

// This function takes two numbers, calculates the average, and outputs it
function calculateMiddle(num1, num2) {
  let result = (num1 + num2) / 2;
  return result; // Outputs the value
}
```

Best Practices 💡

* Naming: Use camelCase for your function names (e.g., drawSpookyGhost, checkCollision). 
* Placement: Define your custom functions outside of setup() or draw(), usually at the very bottom of your sketch.js file. 
* Scope: Variables created inside your custom function cannot be accessed outside of it (local scope). 

