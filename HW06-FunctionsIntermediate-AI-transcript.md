# COMPUTING HW06: AI Transcript

---

## Question 1

**Student:** Here's an almost complete p5.js program. Write the `draw()` function that draws three houses in different areas of the canvas.

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  //WHAT GOES HERE
}

function house(hx, hy) {
  rect(hx, hy, 60, 60);
  triangle(hx, hy, hx + 30, hy - 30, hx + 60, hy);
}
```

**AI:** Here's one way to do it:

```javascript
function draw() {
  background("skyblue");
  house(50, 100);
  house(250, 100);
  house(150, 300);
}
```

Each line **calls** `house()` with different **arguments**. The first number becomes `hx` and the second becomes `hy`.

**Tip:** (hx, hy) is the **top-left corner** of the house's body, and the roof sticks up **30 pixels above** it. So `hy` must be at least 30, or the roof goes off the top of the canvas.

---

## Question 2

**Student:** What needs to change about the program to have ONE house that moves to the right?

**AI:** You need three changes:

```javascript
let hx = 0;                // 1. Create a variable ABOVE setup()

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background("skyblue");
  house(hx, 200);          // 2. Use the variable as an argument
  hx = hx + 2;             // 3. Change the variable every frame
}

function house(hx, hy) {
  rect(hx, hy, 60, 60);
  triangle(hx, hy, hx + 30, hy - 30, hx + 60, hy);
}
```

**Common mistake:** Writing `let hx = 0;` *inside* `draw()`. Then `hx` resets to 0 every frame, so the house never moves.

---

## Question 3

**Student:** Show me a trace table for this p5.js program for the first two times `draw()` runs. The trace table should include columns for "step number", "line number", "what happens", and "console". Use one short phrase per row, and whenever a variable changes, show its new value. After the table, show the final console output and give a brief description of the animation.

| Line | Code |
|---|---|
| 1 | `let x = 50;` |
| 2 | |
| 3 | `function setup() {` |
| 4 | &nbsp;&nbsp;&nbsp;&nbsp;`createCanvas(400, 400);` |
| 5 | `}` |
| 6 | |
| 7 | `function draw() {` |
| 8 | &nbsp;&nbsp;&nbsp;&nbsp;`background("lightgray");` |
| 9 | &nbsp;&nbsp;&nbsp;&nbsp;`ellipse(x, 200, 40, 40);` |
| 10 | &nbsp;&nbsp;&nbsp;&nbsp;`console.log(x);` |
| 11 | &nbsp;&nbsp;&nbsp;&nbsp;`x = x + 10;` |
| 12 | `}` |

**AI:**

| Step | Line | What happens | Console |
|---|---|---|---|
| 1 | 1 | x = 50 | |
| 2 | 3 | p5 calls `setup()` (runs only once) | |
| 3 | 4 | creates a 400×400 canvas | |
| 4 | 7 | p5 calls `draw()`: frame 1 | |
| 5 | 8 | paints gray background | |
| 6 | 9 | draws ball at (50, 200) | |
| 7 | 10 | prints x | 50 |
| 8 | 11 | x = 50 + 10 = 60 | |
| 9 | 7 | p5 calls `draw()` again: frame 2 | |
| 10 | 8 | paints gray background (covers the old ball) | |
| 11 | 9 | draws ball at (60, 200) | |
| 12 | 10 | prints x | 60 |
| 13 | 11 | x = 60 + 10 = 70 | |

**Console output after two frames:**
```
50
60
```

**The animation:** A ball 40 pixels wide moves to the right across the middle of a gray canvas, 10 pixels per frame. It never stops or comes back. It slides off the right edge and keeps going forever (x keeps getting bigger). Since p5 runs about 60 frames per second, the ball crosses the whole canvas in well under a second!

**Notice:** You never wrote `setup()` or `draw()` in a line of your own code to call them. **p5 calls them for you.** It calls `setup()` once, then `draw()` over and over. That's why the line numbers jump from 4 to 7, and from 11 back to 7.

---

## Question 4

**Student:** Show me a trace table for this JavaScript program (not p5.js). The trace table should include columns for "step number", "line number", "what happens", and "console". Use one short phrase per row, and whenever a variable changes, show its new value. After the table, show the final console output.

| Line | Code |
|---|---|
| 1 | `let answer = addTen(5);` |
| 2 | `console.log(answer);` |
| 3 | |
| 4 | `function addTen(n) {` |
| 5 | &nbsp;&nbsp;&nbsp;&nbsp;`console.log("adding");` |
| 6 | &nbsp;&nbsp;&nbsp;&nbsp;`return n + 10;` |
| 7 | `}` |

**AI:**

| Step | Line | What happens | Console |
|---|---|---|---|
| 1 | 1 | calls `addTen(5)` → jump, n = 5 | |
| 2 | 5 | prints "adding" | adding |
| 3 | 6 | returns 5 + 10 = 15 → jump back to line 1 | |
| 4 | 1 | answer = 15 | |
| 5 | 2 | prints answer | 15 |

**Final console output:**
```
adding
15
```

**Notice:** Line 1 couldn't finish right away. It had to jump to the function, wait for the answer, and *then* store 15 in `answer`. That's why "adding" prints before 15.

**Why can line 1 call `addTen()` before it's defined?** Before running anything, JavaScript reads the whole program and remembers every function definition. So all the functions are ready to use from the very first line.

---

## Question 5

**Student:** Show me a trace table for this JavaScript program (not p5.js). The trace table should include columns for "step number", "line number", "what happens", and "console". Use one short phrase per row, and whenever a variable changes, show its new value. After the table, show the final console output.

| Line | Code |
|---|---|
| 1 | `let a = 3;` |
| 2 | `let b = 5;` |
| 3 | `a = mix(b);` |
| 4 | `b = stir(a);` |
| 5 | `console.log(a);` |
| 6 | `console.log(b);` |
| 7 | |
| 8 | `function mix(x) {` |
| 9 | &nbsp;&nbsp;&nbsp;&nbsp;`console.log("mixing");` |
| 10 | &nbsp;&nbsp;&nbsp;&nbsp;`return x * 2;` |
| 11 | `}` |
| 12 | |
| 13 | `function stir(y) {` |
| 14 | &nbsp;&nbsp;&nbsp;&nbsp;`console.log("stirring");` |
| 15 | &nbsp;&nbsp;&nbsp;&nbsp;`return y + 1;` |
| 16 | `}` |

**AI:**

| Step | Line | What happens | Console |
|---|---|---|---|
| 1 | 1 | a = 3 | |
| 2 | 2 | b = 5 | |
| 3 | 3 | calls `mix(b)` → jump, x = 5 | |
| 4 | 9 | prints "mixing" | mixing |
| 5 | 10 | returns 5 * 2 = 10 → jump back to line 3 | |
| 6 | 3 | a = 10 (b is still 5) | |
| 7 | 4 | calls `stir(a)` → jump, y = 10 | |
| 8 | 14 | prints "stirring" | stirring |
| 9 | 15 | returns 10 + 1 = 11 → jump back to line 4 | |
| 10 | 4 | b = 11 (a is still 10) | |
| 11 | 5 | prints a | 10 |
| 12 | 6 | prints b | 11 |

**Final console output:**
```
mixing
stirring
10
11
```

**Common mistakes:**
- **Using the old value of a.** By line 4, `a` is already 10, not 3. So `stir` gets 10.
- **Leaving out "mixing" and "stirring."** They print while the functions run, so they come *before* the numbers.

---

## Question 6

**Student:** What does the word `return` do inside a function? Then explain the difference between a function that uses `console.log` and a function that uses `return`.

**AI:** `return` does two things:

1. It **sends a value back** to the line that called the function.
2. It **ends the function** right away. That's the "jump back."

The returned value takes the place of the function call, so you can store it in a variable and use it later:

```javascript
let total = addTen(5);   // addTen(5) becomes 15, so total = 15
```

**`console.log` vs. `return`:**

| | `console.log` | `return` |
|---|---|---|
| What it does | shows a message in the console | sends a value back to your program |
| Who can use it | only *you*, the person reading the console | the *program*, which can store and reuse it |
| Ends the function? | no | yes |

Here's an example where you can see the difference:

```javascript
let a = sayIt();
let b = giveIt();
console.log(a);
console.log(b);

function sayIt() {
  console.log(7);    // shows 7, but doesn't send anything back
}

function giveIt() {
  return 7;          // sends 7 back, but doesn't show anything
}
```

Console output:
```
7
undefined
7
```

`sayIt()` printed 7 but returned nothing, so `a` is `undefined`. `giveIt()` printed nothing, but it returned 7, so `b` is 7.

**Not every function needs `return`.** A function like `house()` just draws. It does its job and doesn't need to send anything back.

---

## Question 7

**Student:** I am tasked with writing a function named `drawFace()` with two parameters, `fx` and `fy`. It draws a face centered at (fx, fy) with:
- **head:** a circle 60 pixels wide
- **eyes:** circles 7 pixels wide, 10 pixels left/right of center, 5 pixels above center
- **mouth:** a horizontal line 30 pixels wide, centered left-to-right, 15 pixels below center

First, sketch a labeled face based on this description. Second, write a p5.js JavaScript function for it.

**AI:**

**Step 1: Sketch**

```
                ← head: 60 px wide →

                  .-~~~~~~~~~~-.
                /                \
               |    o        o    |   ← eyes at (fx - 10, fy - 5) and (fx + 10, fy - 5)
               |         •        |   ← center (fx, fy)
               |    ──────────    |   ← mouth from (fx - 15, fy + 15) to (fx + 15, fy + 15)
                \                /
                  '-__________-'
```

**Step 2: Figure out each shape**

Two rules to remember:
- **Left is minus, right is plus:** `fx - something` or `fx + something`.
- **Up is minus, down is plus:** `fy - something` or `fy + something`. (On the canvas, y gets *bigger* as you go *down*.)

| Part | Command | Why |
|---|---|---|
| Head | `circle(fx, fy, 60)` | centered exactly at (fx, fy) |
| Left eye | `circle(fx - 10, fy - 5, 7)` | 10 left (minus), 5 up (minus) |
| Right eye | `circle(fx + 10, fy - 5, 7)` | 10 right (plus), 5 up (minus) |
| Mouth | `line(fx - 15, fy + 15, fx + 15, fy + 15)` | 30 wide means 15 on each side; 15 down (plus) |

A `line` needs **two endpoints**: `line(x1, y1, x2, y2)`. The mouth is horizontal, so both endpoints have the same y.

**Step 3: The function**

```javascript
function drawFace(fx, fy) {
  circle(fx, fy, 60);
  circle(fx - 10, fy - 5, 7);
  circle(fx + 10, fy - 5, 7);
  line(fx - 15, fy + 15, fx + 15, fy + 15);
}
```

To use it, call it from `draw()`:

```javascript
function draw() {
  background("lightgray");
  drawFace(200, 200);
  drawFace(100, 300);
}
```

**Order matters:** Draw the head *first*. p5 draws shapes in order, so if the head came last, it would cover up the eyes and mouth.
