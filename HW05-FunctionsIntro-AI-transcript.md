# HW05 AI Transcript: Functions in JavaScript and p5.js

---

## Question 1

> **We've been using `function setup()` and `function draw()` since day one. But what actually IS a function? Explain it to me like I'm learning this for the first time.**

A **function** is a **named set of instructions** that you can run whenever you want by using its name.

Think of a recipe card labeled **"Make Pancakes."** The card has steps on it: crack eggs, add flour, stir, cook. Once the card exists, you don't have to remember the steps. You just say "make pancakes" and someone follows the card.

A function works the same way:

1. **You write the recipe once.** This is called **defining** the function.
2. **You use it by name as many times as you want.** This is called **calling** the function.

### So what about `setup()` and `draw()`?

You've been writing functions since day one. `setup()` and `draw()` are functions **you define**, but **p5.js calls them for you**:

| Function | Who calls it? | When? |
|---|---|---|
| `setup()` | p5.js | **Once**, when the program starts |
| `draw()` | p5.js | **Over and over**, about 60 times per second |

You've also been **calling** functions the whole time. `createCanvas()`, `background()`, `fill()`, and `circle()` are all functions that someone else already wrote for you. When you write `circle(200, 200, 50)`, you're saying "run the circle recipe with these values."

### Why bother with functions?

- **Organization:** you can group related code under one meaningful name, like `drawHouse()` or `drawSun()`.
- **Reuse:** write the code once and use it many times.
- **Readability:** `drawTree()` is easier to understand than 15 lines of shapes.
- **Easier fixes:** if something is wrong, you fix it in one place, not everywhere you copied it.

> **Key idea:** A function is a named block of code that runs when it is called.

---

## Question 2

> **Annotate this program to help me learn function definitions and calls.**

```javascript
// ===== FUNCTION DEFINITION: setup =====
// "function" tells JavaScript we're defining a new function.
// "setup" is its name. The empty () means it takes no inputs.
// p5.js CALLS setup() for us automatically, ONE time, at the start.
function setup() {
  createCanvas(400, 400);   // FUNCTION CALL: run p5's createCanvas with arguments 400 and 400
}                           // closing curly brace = end of setup's body


// ===== FUNCTION DEFINITION: draw =====
// p5.js CALLS draw() for us automatically, about 60 times per second.
function draw() {
  background("lightgray");  // FUNCTION CALL: p5's background function, argument "lightgray"

  // Three FUNCTION CALLS to OUR OWN function, drawBall.
  // Each call sends three ARGUMENTS: an x value, a y value, and a color.
  drawBall(100, 200, "red");     // jumps to drawBall with ballX=100, ballY=200, ballColor="red"
  drawBall(200, 200, "gold");    // jumps to drawBall with ballX=200, ballY=200, ballColor="gold"
  drawBall(300, 200, "purple");  // jumps to drawBall with ballX=300, ballY=200, ballColor="purple"
}


// ===== FUNCTION DEFINITION: drawBall =====
// This is a function WE created. p5.js does NOT call it automatically.
// It only runs when our code calls it (see the three calls in draw above).
// ballX, ballY, and ballColor are PARAMETERS: placeholder variables
// that receive the values (arguments) sent in by each call.
function drawBall(ballX, ballY, ballColor) {
  fill(ballColor);              // FUNCTION CALL: set fill color to whatever ballColor holds
  circle(ballX, ballY, 50);     // FUNCTION CALL: draw a circle at (ballX, ballY), diameter 50
}                               // when this brace is reached, the program jumps back to the call
```

### What the program draws

Three circles in a row across the middle of the canvas: **red** on the left, **gold** in the middle, and **purple** on the right.

### Things to notice

- There are **3 function definitions** in this program: `setup`, `draw`, and `drawBall`.
- `drawBall` is **defined once** but **called three times**. That's the power of functions.
- The **order of the arguments matters**. The first argument goes into the first parameter (`ballX`), the second into the second (`ballY`), and the third into the third (`ballColor`).
- Without functions, we'd have to write `fill()` and `circle()` three separate times.

---

## Question 3

> **Explain how a function definition in JavaScript (and p5.js) is written. Be sure to describe the purpose of: the word `function`, the parentheses `()`, and the curly braces `{ }`.**

Here is the general pattern:

```javascript
function functionName(parameter1, parameter2) {
  // instructions go here (the "body")
}
```

And a real example:

```javascript
function drawBall(ballX, ballY, ballColor) {
  fill(ballColor);
  circle(ballX, ballY, 50);
}
```

### The parts

**1. The word `function`**
This is a **keyword**. It tells JavaScript, "I'm about to define a new function." It's like writing "RECIPE:" at the top of a recipe card. It is always lowercase.

**2. The name (`drawBall`)**
The name comes right after `function`. You'll use this name later to call the function. Good names describe what the function does, usually starting with a verb: `drawBall`, `drawSun`, `moveCar`. Names can't have spaces, so we use **camelCase**.

**3. The parentheses `( )`**
The parentheses hold the function's **parameters**, which are the **inputs** the function needs.
- In `drawBall(ballX, ballY, ballColor)`, there are three parameters, separated by commas.
- If the function needs no inputs, the parentheses are still required but left empty: `setup()`.

**4. The curly braces `{ }`**
The curly braces surround the **body** of the function, which is the actual instructions that run when the function is called.
- `{` marks where the function **starts**.
- `}` marks where the function **ends**.
- Everything between them belongs to the function. We indent that code so it's easy to see what's inside.

### Quick summary

| Part | Purpose |
|---|---|
| `function` | Keyword that says "I'm defining a function" |
| name | What we call it by later |
| `( )` | Holds the parameters (inputs); empty if there are none |
| `{ }` | Wraps the body: the instructions that run when it's called |

> **Common mistake:** forgetting a closing `}`. Every `{` needs a matching `}`. Missing one is one of the most common reasons a p5.js sketch won't run.

---

## Question 4

> **What's the difference between a function definition and a function call? Give a small code example that includes both.**

| | Function **Definition** | Function **Call** |
|---|---|---|
| What it does | **Creates** the function. Describes what it will do. | **Runs** the function. |
| Recipe analogy | Writing the recipe card | Actually cooking the recipe |
| Starts with `function`? | **Yes** | **No** |
| Has `{ }`? | **Yes**, it has a body | **No** |
| Ends with `;`? | No | Usually yes |
| How many times? | Written **once** | Can happen **many times** |

**Important:** Defining a function does **not** run it. The code inside a definition just sits there and waits until something calls it.

### Example

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background("skyblue");
  drawCloud(100, 100);   // ← CALL
  drawCloud(280, 150);   // ← CALL
}

// ↓ DEFINITION
function drawCloud(x, y) {
  fill("white");
  noStroke();
  ellipse(x, y, 80, 50);
  ellipse(x + 30, y, 60, 40);
}
```

- **Definition:** the block that starts with `function drawCloud(x, y) {` and ends with `}`.
- **Calls:** the two lines `drawCloud(100, 100);` and `drawCloud(280, 150);`.

### A quick way to tell them apart

- If you see the word **`function`** in front and **curly braces** after, it's a **definition**.
- If you see just the **name followed by parentheses** and a semicolon, it's a **call**.

---

## Question 5

> **My teacher keeps saying that a function call is like a "jump" command. What does that mean?**

Normally, a computer runs your code **from top to bottom, one line at a time**. A function call **breaks that pattern**.

When the computer reaches a function call, it:

1. **Jumps** to that function's definition.
2. **Runs** every line inside the function's `{ }`.
3. **Jumps back** to the line right after the call and keeps going.

### Example

```javascript
function draw() {
  background("lightgray");     // Step 1
  drawBall(100, 200, "red");   // Step 2: JUMP to drawBall
  drawBall(300, 200, "blue");  // Step 5: JUMP to drawBall again
}

function drawBall(ballX, ballY, ballColor) {
  fill(ballColor);             // Step 3 (and Step 6)
  circle(ballX, ballY, 50);    // Step 4 (and Step 7), then JUMP BACK
}
```

The order the lines actually run is:

```
background("lightgray")
→ jump to drawBall (red)
    fill("red")
    circle(100, 200, 50)
← jump back
→ jump to drawBall (blue)
    fill("blue")
    circle(300, 200, 50)
← jump back
end of draw()
```

### An analogy

Imagine you're reading a textbook and you see: *"See page 112 for a diagram."* You **jump** to page 112, look at the diagram, and then **return** to the exact spot where you were reading. That's what a function call does.

> **Key idea:** The order lines appear in your file is **not** always the order they run. A function call makes the program jump to the definition and then return.

---

## Question 6

> **Here's some code. Why doesn't the ellipse show up? What's the fix?**

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background("lightgray");
}

function drawSun() {
  fill("yellow")
  ellipse(350, 50, 100, 100);
}
```

### Why it doesn't work

The function `drawSun()` is **defined**, but it is **never called**.

Remember: p5.js automatically calls `setup()` and `draw()`, but it does **not** know about your custom functions. Writing a definition is like writing a recipe card and putting it in a drawer. Nothing gets cooked unless someone uses it.

So the program draws a gray background 60 times a second and never runs the code inside `drawSun()`.

### The fix

Add a **call** to `drawSun()` inside `draw()`, **after** `background()`:

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background("lightgray");
  drawSun();                   // ← the missing function CALL
}

function drawSun() {
  fill("yellow");
  ellipse(350, 50, 100, 100);
}
```

### Why it has to go *after* `background()`

`background()` paints over the entire canvas. If you called `drawSun()` **before** `background()`, the sun would be drawn and then immediately covered up, so you still wouldn't see it. In p5.js, **later code draws on top of earlier code**.

### Small bonus fix

The original line `fill("yellow")` is missing a semicolon. JavaScript usually lets this slide, so it isn't what broke the program, but it's a good habit to end each statement with `;`.

---

## Question 7

> **What are arguments? How are they different from parameters? Show me a simple example of each using pure JavaScript (not p5.js).**

These two words are related but mean different things:

- A **parameter** is a **variable name** listed in a function's **definition**. It's a placeholder for a value the function will receive.
- An **argument** is the **actual value** you send into the function when you **call** it.

### Example in pure JavaScript

```javascript
// DEFINITION: name and age are PARAMETERS
function greet(name, age) {
  console.log("Hi " + name + "! You are " + age + " years old.");
}

// CALLS: "Maya", 15, "Leo", and 16 are ARGUMENTS
greet("Maya", 15);
greet("Leo", 16);
```

**Output in the console:**

```
Hi Maya! You are 15 years old.
Hi Leo! You are 16 years old.
```

### What happens step by step

When `greet("Maya", 15)` runs:
1. The argument `"Maya"` is stored in the parameter `name`.
2. The argument `15` is stored in the parameter `age`.
3. The body runs using those values.

When `greet("Leo", 16)` runs, the **same parameters** get **new values**.

### Another example

```javascript
// a and b are PARAMETERS
function add(a, b) {
  console.log(a + b);
}

add(3, 4);    // 3 and 4 are ARGUMENTS  → prints 7
add(10, 25);  // 10 and 25 are ARGUMENTS → prints 35
```

### Comparison

| | **Parameter** | **Argument** |
|---|---|---|
| What it is | A variable name (placeholder) | An actual value |
| Where it appears | In the function **definition** | In the function **call** |
| Example | `name`, `age`, `a`, `b` | `"Maya"`, `15`, `3`, `4` |
| Analogy | An empty labeled box | The thing you put in the box |

### Memory trick

- **P**arameter = **P**laceholder (in the definition)
- **A**rgument = **A**ctual value (in the call)

### Connecting back to p5.js

In `function drawBall(ballX, ballY, ballColor)`, the names `ballX`, `ballY`, and `ballColor` are **parameters**. In `drawBall(100, 200, "red")`, the values `100`, `200`, and `"red"` are **arguments**. Arguments are matched to parameters **by position**: first to first, second to second, and so on.
