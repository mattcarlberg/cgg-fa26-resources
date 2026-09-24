# HW02: Color & Text in p5.js — AI Transcript

## Question 1

**In p5.js, should `fill()` go before or after the shape I am trying to draw? Why? As a reminder, I like to see `fill()` commands with color names.**

**Before.** p5.js runs your code from top to bottom, in order. `fill()` doesn't color a specific shape — it sets the fill color that will be used for **whatever gets drawn next**. If you put `fill()` after a shape, that shape has already been drawn with the *previous* fill color, so the new color does nothing to it.

```javascript
fill("orange");
rect(50, 50, 100, 100); // this rectangle is orange
```

---

## Question 2

**Is it the same for `stroke()`?**

Yes — `stroke()` (the outline color) works exactly the same way as `fill()`. It must go **before** the shape you want it to affect, since it also just sets a value that applies to whatever is drawn next.

---

## Question 3

**If I need BOTH a `stroke()` and a `fill()`, does it matter which one comes first?**

No. `fill()` and `stroke()` set two separate, independent settings — a fill color and a stroke color. They don't interact with or overwrite each other, so you can list them in either order. What *does* matter is that **both** come before the shape:

```javascript
fill("yellow");
stroke("black");
// or the reverse order — both work the same:
stroke("black");
fill("yellow");

rect(50, 50, 100, 100);
```

---

## Question 4

**What about if I have multiple shapes that have the same coloring?**

You only need to call `fill()` (and/or `stroke()`) **once** — it stays active for every shape drawn afterward until you call it again with a different color.

```javascript
fill("blue");
ellipse(100, 100, 50, 50);
rect(200, 200, 80, 80); // still blue — no need to repeat fill()
```

---

## Question 5

**How do I change the thickness of an outline? Sometimes I want a shape with no outline, sometimes I want a thin outline, and sometimes I want a thick outline?**

Use `strokeWeight(n)`, where `n` is the outline thickness in pixels. Like `fill()`/`stroke()`, it must be called **before** the shape and stays active until changed again.

| Goal | Command |
|---|---|
| No outline | `noStroke();` |
| Thin outline | `strokeWeight(1);` (or a small number) |
| Thick outline | `strokeWeight(10);` (or a larger number) |

```javascript
strokeWeight(8);
stroke("black");
ellipse(200, 200, 100, 100); // thick 8px black outline
```

---

## Question 6

**Here's some code. I wanted ONLY my ellipse to have a thick outline, but both shapes do. What gives?**

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  rect(150, 50, 100, 100);
  strokeWeight(5);
  ellipse(200, 300, 100, 100);
}
```

The problem: **`draw()` runs in a loop**, and settings like `strokeWeight()` do **not** automatically reset between frames. So here's what actually happens:

- **Frame 1:** `rect()` is drawn with the default (thin) stroke weight, since `strokeWeight(5)` hasn't run yet. *Then* `strokeWeight(5)` runs, and `ellipse()` is drawn thick.
- **Frame 2:** `draw()` starts over. `background(220)` clears the canvas — but `strokeWeight` is still `5` from last frame, because that setting was never reset! So now `rect()` *also* gets drawn with a weight of 5.
- Every frame after that, both shapes stay thick.

**Fix:** reset the stroke weight back to normal before drawing the rectangle:

```javascript
function draw() {
  background(220);
  strokeWeight(1);          // reset first
  rect(150, 50, 100, 100);
  strokeWeight(5);          // now increase just for the ellipse
  ellipse(200, 300, 100, 100);
}
```

**Takeaway:** style settings (`fill`, `stroke`, `strokeWeight`, etc.) carry over between shapes *and* between frames until you explicitly change them again.

---

## Question 7

**Tell me about `rectMode(CENTER)` and when/why I should consider using it.**

By default, `rect(x, y, w, h)` treats `(x, y)` as the **top-left corner**. `rectMode(CENTER)` changes that so `(x, y)` is treated as the **center** of the rectangle instead.

```javascript
rectMode(CENTER);
rect(200, 200, 100, 60); // now centered ON (200, 200), not cornered there
```

This is especially useful when you want to **center a rectangle** on a specific point (like the canvas center) without doing the math to find its top-left corner yourself. It's a setting, so it usually belongs in `setup()` if you want it to apply for the whole sketch — but it can go in `draw()` if you need to switch modes partway through.

---

## Question 8

**Tell me about how to display text on screen. Some text I will need to be small, and some I will need to be big.**

Two functions work together:

- **`text(string, x, y)`** — draws the given text at position `(x, y)`. By default, `(x, y)` is the text's top-left, unless you've changed that with `textAlign()`.
- **`textSize(n)`** — sets the font size (in pixels) for any text drawn afterward, same rule as `fill()`/`stroke()`: it stays active until changed again.

```javascript
textSize(12);
text("small label", 50, 50);

textSize(48);
text("BIG TITLE", 50, 150);
```

Call `textSize()` right before each `text()` call if you need different sizes for different labels in the same sketch.

---

## Question 9

**I often see `textAlign(CENTER, CENTER)` in people's code. What does that do? Should it go in setup() or draw()?**

`textAlign(CENTER, CENTER)` changes how the `(x, y)` coordinate in `text()` is interpreted. Instead of `(x, y)` marking the top-left of the text, it marks the **center** — both horizontally (first `CENTER`) and vertically (second `CENTER`). This makes it easy to perfectly center a label on a point without measuring the text's width yourself.

It usually belongs in **`setup()`**, since it's a one-time style setting, not something that needs to change every frame — put it in `draw()` only if you actually need to switch alignment modes partway through your sketch.

---

## Question 10

**My teacher is so inconsistent. Some lines of code end with a semicolon; some don't. What's up?**

The rule: a semicolon `;` ends a **statement** — a single instruction, like calling a function (`rect(50, 50, 100, 100);`) or declaring a variable. Lines that **don't** get a semicolon are usually lines that open or close a **block** with curly braces, like:

```javascript
function draw() {   // no semicolon — this line opens a block
  background(220);  // semicolon — this is a statement
}                    // no semicolon — this line just closes a block
```

So it's not actually random: statements need semicolons, but lines that are just `{` or `}` (defining where a function, loop, or `if` block starts/ends) don't. If you see a missing semicolon somewhere it should be, it may be a small typo — JavaScript is sometimes forgiving about it, but it's good practice to include them on every statement.
