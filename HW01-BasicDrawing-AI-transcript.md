# HW01: Basic Drawing in p5.js — AI Transcript


## Question 1

**What is the purpose of the setup() and draw() functions in p5.js? What are the curly braces used for?**

p5.js **calls** (runs) two special functions for you automatically — you never call them yourself.

- **`setup()`** runs **once**, at the very start. Use it for things that only need to happen one time, like `createCanvas()`.
- **`draw()`** runs **over and over**, about 60 times per second. This is what makes animation possible, and it's also what actually paints your shapes each frame.

**Curly braces `{ }`** mark the start and end of a block of code — here, everything that belongs to a function. Forgetting a closing brace will break your program.

```javascript
function setup() {
  // runs once
}

function draw() {
  // runs 60 times per second
}
```

---

## Question 2

**Describe the coordinate system that is set up when a p5.js program uses createCanvas(400, 400).**

`createCanvas(400, 400)` makes a canvas **400 pixels wide and 400 pixels tall**.

- **(0, 0)** is the **top-left corner** — not the center.
- **x increases going right**, same as a normal graph.
- **y increases going DOWN**, the opposite of a normal math graph.

On a 400×400 canvas: `(400, 0)` = top-right, `(0, 400)` = bottom-left, `(400, 400)` = bottom-right, and `(200, 200)` = dead center.

---

## Question 3

**Describe in words the shape `rect(100, 50, 250, 125)` and annotate what each number means.**

```
rect(x, y, width, height)
```

| Value | Meaning |
|---|---|
| `100` | x-coordinate of the top-left corner |
| `50` | y-coordinate of the top-left corner |
| `250` | width (extends right) |
| `125` | height (extends down) |

This draws a rectangle with its top-left corner at (100, 50), stretching 250 pixels right and 125 pixels down.

---

## Question 4

**On a 400x400 canvas, write a command for a rectangle that is centered on the canvas, the full height of the canvas, and half the width of the canvas.**

- Full height → height = `400`, starting at y = `0`
- Half width → width = `200`
- Centered horizontally → 100px of empty space on each side, so x = `100`

```javascript
rect(100, 0, 200, 400);
```

---

## Question 5

**Describe in words the shape `ellipse(300, 200, 50, 400)` and annotate what each number means.**

An **ellipse** is just an oval — a stretched-out circle. In fact, a circle *is* an ellipse where the width and height happen to be equal; as soon as width and height differ, it stretches into an oval shape.

```
ellipse(x, y, width, height)
```

Unlike `rect()`, the x and y here mark the **center** of the shape, not a corner.

| Value | Meaning |
|---|---|
| `300` | x-coordinate of the center |
| `200` | y-coordinate of the center |
| `50` | width (horizontal diameter) |
| `400` | height (vertical diameter) |

Centered at (300, 200), only 50px wide but 400px tall — so this is a tall, thin, vertical oval, not a circle.

---

## Question 6

**On a 400x400 canvas, write a command for a circle (via the ellipse command) that fills the bottom left quadrant.**

The bottom-left quadrant of a 400×400 canvas spans x: 0–200 and y: 200–400 — a 200×200 square centered at (100, 300).

Since a circle is an ellipse with equal width and height, set both to 200:

```javascript
ellipse(100, 300, 200, 200);
```

---

## Question 7

**Describe in words the shape `triangle(100, 100, 200, 0, 300, 100)` and annotate what each number means.**

```
triangle(x1, y1, x2, y2, x3, y3)
```

| Value | Meaning |
|---|---|
| `100, 100` | vertex 1 |
| `200, 0` | vertex 2 |
| `300, 100` | vertex 3 |

Vertices 1 and 3 share y = 100, so the base is a flat, horizontal line 200px long. Vertex 2 sits above the base's midpoint (smaller y = higher up), making an upward-pointing, symmetrical triangle near the top of the canvas.

---

## Question 8

**On a 400x400 canvas, write a command for a right triangle with one vertex in the center of the screen.**

Easiest approach: make one side purely horizontal and another purely vertical from the same vertex — they'll automatically meet at 90°.

```javascript
triangle(200, 200, 350, 200, 200, 50);
```

- **(200, 200)** — center of canvas
- **(350, 200)** — same y as vertex 1 → horizontal side
- **(200, 50)** — same x as vertex 1 → vertical side

The horizontal and vertical sides meet at 90° at (200, 200). (Many other answers also work.)

---

## Question 9

**Tell me about how to color the inside of shapes in p5.js. We will primarily be using shape names, but I want to hear about RGB too.**

`fill()` sets the color used for **every shape drawn after it**, until called again.

**Color names:**

```javascript
fill("red");
fill("lightblue");
```

**RGB** (Red, Green, Blue — the light your screen mixes to make color): three numbers from **0–255** each:

```javascript
fill(r, g, b);

fill(255, 0, 0);     // pure red
fill(255, 255, 255); // white
fill(0, 0, 0);        // black
```

RGB gives far more precise, unlimited color choices than the named list.

**Related:** `stroke()` colors a shape's outline the same way; `noStroke()` removes the outline entirely.

---

## Question 10

**Help me annotate this p5.js program.**

```javascript
function setup() {
  createCanvas(400, 400);
  noStroke();
  textAlign(CENTER, CENTER);
  textSize(20);
}

function draw() {
  background("lightgray");
  fill("white");
  rect(50, 100, 300, 200);
  fill("red");
  ellipse(200, 200, 100, 100);
  fill("black");
  text("Flag of Japan", 200, 350);
}
```

**`setup()` (called once):**

- `createCanvas(400, 400);` — makes a 400×400 canvas.
- `noStroke();` — turns off outlines on all shapes from now on.
- `textAlign(CENTER, CENTER);` — makes any `text()` coordinate refer to the text's center, not a corner.
- `textSize(20);` — sets text size to 20px.

**`draw()` (called 60 times per second):**

- `background("lightgray");` — repaints the whole canvas gray, clearing the previous frame.
- `fill("white");` then `rect(50, 100, 300, 200);` — draws a white rectangle (top-left at (50,100), 300×200) as the flag's background.
- `fill("red");` then `ellipse(200, 200, 100, 100);` — draws a red circle (equal width/height) centered on the canvas.
- `fill("black");` then `text("Flag of Japan", 200, 350);` — labels the image in black, centered at (200, 350).

**Big picture:** gray background → white rectangle → red circle centered on it (the flag of Japan) → text label below. Since `draw()` redraws this same image 60 times per second, nothing appears to move.
