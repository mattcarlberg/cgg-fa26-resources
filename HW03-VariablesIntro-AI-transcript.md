# HW03: Intro to Variables in p5.js — AI Transcript

## Question 1

**What is the bare minimum I should know about how computer memory works to understand variables in a programming language?**

Think of computer memory as a huge wall of **labeled boxes**. Each box can hold one value. A **variable** is just a named box: the name is the label on the outside, and the value is whatever's currently stored inside.

Two key ideas:

- You can **look at** what's in the box (use the variable) without changing it.
- You can **replace** what's in the box (reassign the variable) — the old value is gone, overwritten by the new one.

That's really it for the "bare minimum" — a variable is a labeled, reusable storage spot, and its contents can change while your program runs.

---

## Question 2

**Describe what this command does: `let bard = 3020;`**

This **declares** (creates) a new variable named `bard` and immediately stores the value `3020` in it.

- `let` — the keyword that tells p5.js/JavaScript "I'm creating a new variable."
- `bard` — the variable's name (the label on the box).
- `= 3020` — sets its starting value to 3020.
- `;` — ends the statement.

After this line runs, anywhere you write `bard` later in your code, it will be treated as the value `3020` — until it's changed.

---

## Question 3

**Can I name a variable anything I want? What are the rules and recommendations for naming variables?**

**Rules (break these and your code won't run):**

- Can't start with a number (`2cool` is invalid, `cool2` is fine).
- No spaces (use `myScore`, not `my score`).
- Can't be a reserved word already used by the language, like `let`, `function`, or `draw`.
- Names are **case-sensitive** — `score` and `Score` are two different variables.

**Recommendations (not required, but good practice):**

- Use **descriptive names** that say what the variable holds (`playerScore`, not `x`, unless it really is just a coordinate).
- Use **camelCase** for multi-word names: lowercase first word, capitalize the start of each word after that (`ballSpeed`, `backgroundColor`).

---

## Question 4

**Describe what this command does: `bard = bard + 1;`**

This is a **reassignment**, not a declaration — notice there's no `let`, so it assumes `bard` already exists.

Here's the order of operations: p5.js first looks at the **right side** of the `=` sign and figures out the current value of `bard`, adds `1` to it, and only *then* stores that new result back into `bard` on the left side.

So if `bard` was `3020` before this line, it becomes `3021` after. This pattern — "take a variable's current value, do some math, save it back to itself" — is extremely common for things like counters or animation.

---

## Question 5

**Are there other ways to write code that adds one to a variable?**

Yes — `bard = bard + 1;` can be shortened two ways:

| Style | Code | Meaning |
|---|---|---|
| Full | `bard = bard + 1;` | most explicit, easiest to read as a beginner |
| Shorthand | `bard += 1;` | "add 1 to bard, save it back" |
| Increment | `bard++;` | adds exactly 1, nothing else |

All three do the exact same thing. `+=` also works with other numbers (`bard += 5;`) and other operators (`-=`, `*=`, `/=`).

---

## Question 6

**What is stored in the variable queens when this code finishes running from top to bottom? Please provide annotations to help explain.**

```javascript
let queens = 4;
queens = queens + 3;
queens = queens * 2;
queens -= 5;
```

Tracing through it line by line:

| Line | What happens | Value of `queens` after |
|---|---|---|
| `let queens = 4;` | creates `queens`, sets it to 4 | `4` |
| `queens = queens + 3;` | 4 + 3 | `7` |
| `queens = queens * 2;` | 7 × 2 | `14` |
| `queens -= 5;` | 14 − 5 | `9` |

**Final value: `queens` is `9`.**

---

## Question 7

**Write for me the simplest program that defines a variable and uses it to create vertical motion in p5.js.**

```javascript
let y; // declared here so both setup() and draw() can use it

function setup() {
  createCanvas(400, 400);
  y = 0; // starting position
}

function draw() {
  background(220);
  ellipse(200, y, 50, 50);
  y = y + 2; // move down a little each frame
}
```

Every time `draw()` runs (60 times per second), `y` increases by 2, so the circle's vertical position keeps changing — creating smooth downward motion.

---

## Question 8

**Why do we always seem to put the let statement above the setup function?**

A variable declared with `let` can only be used by code that comes **after** it and is allowed to "see" it — this is called **scope**. If you declare a variable *inside* `setup()`, only `setup()` can use it; `draw()` won't know it exists.

By declaring it **above both** `setup()` and `draw()` (in the global scope — outside of any function), both functions can read and change it. This matters a lot for animation, since you typically set a variable's *starting* value in `setup()` but need to keep *updating* it in `draw()`.

---

## Question 9

**What would this animation look like (assuming it was coded inside of the `draw()` function)?**

```javascript
ellipse(x, y, 20, 20);
x = x + 3;
y = y - 1;
```

Each frame:

- A small circle (20×20) is drawn at the current `(x, y)`.
- `x` increases by 3 → the circle moves **right**.
- `y` decreases by 1 → the circle moves **up** (remember, smaller y = higher on the canvas).

Combined, the circle would appear to drift diagonally — **up and to the right** — moving faster horizontally (3px/frame) than vertically (1px/frame), so the motion would look shallow and mostly sideways rather than a steep diagonal.

---

## Question 10

**Tell me about console.log(). Give me an example. Why would I use it?**

`console.log()` prints a value to the **console** (also called the developer console/output panel — not the canvas itself) so you can see what's going on inside your program while it runs.

```javascript
let score = 10;
console.log(score); // prints: 10
```

**Why use it:** it's one of the most useful debugging tools available. If a variable isn't behaving the way you expect, adding a `console.log()` lets you check its actual value at that exact moment in the code — without it showing up anywhere on your canvas.

---

## Question 11

**In console.log() and text() commands, I see my teacher using tick marks and $ signs. Huh?**

That's a **template literal** — a string written with backticks (`` ` ``) instead of regular quotes. Backticks let you drop a variable's value directly inside a string using `${ }`:

```javascript
let score = 10;
console.log(`Your score is ${score}`); // prints: Your score is 10
```

Anything inside `${ }` gets evaluated and inserted into the string automatically — no need to manually glue pieces of text and variables together. This works the same way inside `text()`:

```javascript
text(`Score: ${score}`, 200, 200);
```

Note the difference: `` ` `` (backtick, next to the 1 key) is not the same character as `'` (a regular single quote) — only backticks support the `${ }` trick.

---

## Question 12

**Variables can store values that are non-numerical. Talk me through a really simple example in p5.js when that might happen?**

Variables can also hold **strings** (text) — not just numbers. A common example is storing a color as a string so you can reuse or change it easily:

```javascript
let bgColor = "lightblue";

function draw() {
  background(bgColor);
  // ... later, elsewhere in your code ...
  bgColor = "black"; // change it, and background() will use the new color next frame
}
```

Here, `bgColor` isn't holding a number — it's holding the text `"lightblue"`. This is useful because if you want to change the background color, you only need to update it in one place, and anywhere else in the code that uses `bgColor` will automatically use the new value too.
