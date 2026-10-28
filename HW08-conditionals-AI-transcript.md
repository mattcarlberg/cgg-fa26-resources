# HW08 AI Transcript: If Statements in p5.js

---

## Question 1

**Student:** Show a first example of an if statement that might appear in p5.js.

**AI:** Here's a simple one. On a 400 × 400 canvas, a circle shows up only when your mouse is on the right half.

```javascript
if (mouseX > 200) {
  ellipse(300, 200, 80, 80);
}
```

In plain English: *"If the mouse's x-position is greater than 200, draw a circle."*

This code goes inside `draw()`, after `background()`. Move your mouse left and right across the canvas. The circle appears when you cross the middle (x = 200) and disappears when you go back. `draw()` runs about 60 times per second, so the computer asks this question 60 times per second.

---

## Question 2

**Student:** What goes inside the parentheses? What goes inside the curly braces?

**AI:**

**Inside the parentheses `( )`** goes the **condition**. A condition is a question whose answer is either `true` or `false`. For example:

- `mouseX > 200`: Is the mouse past x = 200?
- `mouseIsPressed`: Is the mouse button being held down?
- `score == 10`: Is the score exactly 10?

**Inside the curly braces `{ }`** goes the **code to run when the condition is true**. It can be one line or many lines.

```javascript
if (mouseIsPressed) {          // condition goes here
  fill(255, 0, 0);             // code that runs
  ellipse(200, 200, 100, 100); // only when the
}                              // condition is true
```

If the condition is false, the computer skips everything inside the curly braces.

**Two common mistakes:**

1. **Don't put a semicolon after the parentheses.** `if (mouseX > 200);` ends the if statement right there, so the code in the braces runs every time no matter what.
2. **Match your braces.** Every `{` needs a matching `}`. Indenting the code inside the braces makes it much easier to see where the if statement starts and stops.

---

## Question 3

**Student:** Show a first example of an if/else statement that might appear in p5.js.

**AI:** This one makes the background blue when the mouse is on the right half and red when it's on the left half.

```javascript
if (mouseX > 200) {
  background(0, 0, 255);   // blue
} else {
  background(255, 0, 0);   // red
}
```

(This goes inside `draw()` on a 400 × 400 canvas.)

In plain English: *"If the mouse is past x = 200, make the background blue. Otherwise, make it red."*

The `else` part has **no condition** of its own. It means "in every other case." Notice that `else` comes right after the closing `}` of the if part.

---

## Question 4

**Student:** Explain the "flow" of an if/else statement.

**AI:** "Flow" means the order in which the computer runs your code. Here's what happens when the computer reaches an if/else:

1. **It checks the condition** in the parentheses.
2. **If the condition is true**, it runs the code in the **first** set of curly braces and skips the else part.
3. **If the condition is false**, it skips the first set of curly braces and runs the code in the **else** braces.
4. **Either way, it moves on** to whatever code comes after the if/else.

The key idea: **exactly one of the two blocks runs. Never both, and never neither.** It's a fork in the road where you have to take one path or the other, and both paths meet up again afterward.

```
          check condition
           /           \
        true           false
         |               |
   run "if" block   run "else" block
           \           /
        continue with the rest of the code
```

In p5.js, because `draw()` repeats about 60 times per second, the computer goes through this fork 60 times per second. That's why the result changes instantly when you move the mouse.

---

## Question 5

**Student:** What if I need the computer to choose between three or four or more options?

**AI:** Use **else if**. You can chain as many as you need.

This example splits the canvas into three sections and gives each one its own background color:

```javascript
if (mouseX < 133) {
  background(255, 0, 0);     // red on the left
} else if (mouseX < 266) {
  background(0, 255, 0);     // green in the middle
} else {
  background(0, 0, 255);     // blue on the right
}
```

(This goes inside `draw()` on a 400 × 400 canvas.)

**How the flow works:**

- The computer checks the conditions **from top to bottom**.
- As soon as it finds one that is **true**, it runs that block and **skips all the rest**.
- If none of them are true, it runs the final `else` block. (The final `else` is optional. Without it, possibly nothing runs.)

So just like a plain if/else, **only one block runs**.

**Order matters!** Look at the middle condition: `mouseX < 266`. A mouse at x = 50 is also less than 266, but it never gets there because the first condition already caught it. If you put the conditions in the wrong order, some of them may never get a chance to run.

For four or more options, add more `else if` lines:

```javascript
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else if (score >= 70) {
  grade = "C";
} else {
  grade = "F";
}
```

---

## Question 6

**Student:** Tell me about these four things: > and >= and == and !=
My teacher says we won't use ===

**AI:** These are **comparison operators**. Each one compares two values and gives back `true` or `false`, which makes them perfect for the parentheses of an if statement.

| Operator | Meaning | Example | True when... |
|---|---|---|---|
| `>` | greater than | `mouseX > 200` | mouseX is 201, 250, 400... (but **not** 200) |
| `>=` | greater than **or equal to** | `mouseX >= 200` | mouseX is 200, 201, 250... (200 counts!) |
| `==` | equal to | `lives == 0` | lives is exactly 0 |
| `!=` | **not** equal to | `lives != 0` | lives is anything except 0 |

**Tips:**

- The difference between `>` and `>=` only matters at the exact boundary value. `x > 10` is false when x is 10, but `x >= 10` is true.
- With `>=`, the `=` always goes **second**. Write `>=`, not `=>`.
- `!` means "not" in JavaScript, so `!=` reads as "not equal."
- `==` is great for things that count in whole steps, like a score or number of lives, or for checking which key was pressed: `if (key == 'a')`. It's less useful with `mouseX`, because the mouse is rarely at one *exact* pixel.
- There are also `<` (less than) and `<=` (less than or equal to). They work the same way, just in the other direction.

About `===`: you'll see it in a lot of JavaScript examples online. It's a stricter version of `==`. Your teacher has decided the class will stick with `==`, and `==` works for everything we'll do, so you can set `===` aside for now.

---

## Question 7

**Student:** The symbols == and = seem similar, but my teacher says they're totally different. Huh?

**AI:** Your teacher is right. They look alike but do completely different jobs.

**One equals sign `=` is assignment. It *stores* a value.**

```javascript
let score = 0;     // put 0 into score
score = score + 1; // put a new value into score
```

Read `=` as **"gets"** or **"becomes"**: *"score gets 0."*

**Two equals signs `==` is comparison. It *asks a question*.**

```javascript
if (score == 10) {
  text("You win!", 150, 200);
}
```

Read `==` as **"is equal to?"**: *"Is score equal to 10?"* It doesn't change `score` at all. It only checks it and gives back `true` or `false`.

**Quick summary:**

| | `=` | `==` |
|---|---|---|
| Job | stores a value | asks a question |
| Read it as | "gets" | "is equal to?" |
| Changes the variable? | yes | no |
| Where you see it | `let` lines, updating variables | inside if statement parentheses |

**A classic bug:** writing `if (score = 10)` by mistake. Instead of asking "Is score 10?", this *sets* score to 10, and the if statement treats that as true. The code inside runs every time, and your score is wrecked. If an if statement seems to always run no matter what, check for a single `=` in the parentheses.

---

## Question 8

**Student:** Tell me about these two things: && and ||

**AI:** These are **logical operators**. They let you combine two (or more) conditions into one.

**`&&` means AND. *Both* conditions must be true.**

```javascript
if (mouseX > 200 && mouseY > 200) {
  background(0, 255, 0);
}
```

This turns the background green only when the mouse is on the right side **and** in the bottom half, which means the bottom-right quarter of the canvas.

**`||` means OR. *At least one* condition must be true.**

```javascript
if (mouseX < 50 || mouseX > 350) {
  background(255, 0, 0);
}
```

This turns the background red when the mouse is near the left edge **or** near the right edge. Either one is enough.

(The `|` key is usually above the Enter/Return key. Press Shift + backslash.)

**Cheat sheet:**

| A | B | A && B | A \|\| B |
|---|---|---|---|
| true | true | **true** | **true** |
| true | false | false | **true** |
| false | true | false | **true** |
| false | false | false | false |

**Common mistake:** each side has to be a complete comparison.

```javascript
if (mouseX > 100 && < 200)          // WRONG: the right side is missing mouseX
if (mouseX > 100 && mouseX < 200)   // RIGHT
```

You can chain more than two, too: `if (a && b && c && d)` is true only when all four are true. You'll use that in Question 10.

---

## Question 9

**Student:** What is a nested if statement? Tell me about its flow.

**AI:** A **nested if statement** is an if statement *inside* another if statement's curly braces.

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  if (mouseIsPressed) {
    if (mouseX > 200) {
      fill(0, 0, 255);   // pressed on the right: blue
    } else {
      fill(255, 0, 0);   // pressed on the left: red
    }
    ellipse(mouseX, mouseY, 50, 50);
  }
}
```

**The flow:**

1. The computer checks the **outer** condition first: is the mouse pressed?
2. If it's **false**, the computer skips *everything* inside the outer braces, including the inner if. It never even checks `mouseX`.
3. If it's **true**, the computer goes inside and checks the **inner** condition: is the mouse on the right?
4. It picks blue or red based on the inner condition, then draws the circle.

Think of it as asking questions in order: *"Is the mouse pressed? If yes, **then** which side is it on?"* The inner question only matters if the outer answer was yes.

**Tip:** indent each level so you can see which braces belong to which if statement.

**Connection to `&&`:** a simple nested if can often be rewritten with `&&`. These two do the same thing:

```javascript
if (mouseIsPressed) {
  if (mouseX > 200) {
    background(0);
  }
}

if (mouseIsPressed && mouseX > 200) {
  background(0);
}
```

Nesting is most useful when the outer condition controls several decisions at once, like in the example above where it controls both the color choice and drawing the circle.

---

## Question 10

**Student:** I have a rect(20, 30, 75, 25). How do I make it yellow if the mouse is inside the rectangle and gray otherwise?

**AI:** First, figure out where the rectangle's edges are. In `rect(x, y, width, height)`, the first two numbers are the **top-left corner**:

- **Left edge:** x = 20
- **Right edge:** 20 + 75 = **95**
- **Top edge:** y = 30
- **Bottom edge:** 30 + 25 = **55**

The mouse is inside the rectangle when **all four** of these are true:

- `mouseX > 20` (right of the left edge)
- `mouseX < 95` (left of the right edge)
- `mouseY > 30` (below the top edge)
- `mouseY < 55` (above the bottom edge)

"All four must be true" means **`&&`**. Since we want yellow *or* gray, we use **if/else**:

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  if (mouseX > 20 && mouseX < 95 && mouseY > 30 && mouseY < 55) {
    fill(255, 255, 0);   // yellow
  } else {
    fill(128);           // gray
  }

  rect(20, 30, 75, 25);
}
```

**Things to notice:**

- **`fill()` comes before `rect()`.** Fill sets the color for the shapes drawn *after* it, so the if/else has to pick the color first.
- Remember that **y gets bigger going down** in p5.js. That's why "below the top edge" is `mouseY > 30`.
- If you want the very edge pixels to count as inside, use `>=` and `<=` instead of `>` and `<`.
- p5.js also understands color names, so `fill('yellow')` and `fill('gray')` work too.

This pattern (left edge, right edge, top edge, bottom edge, all joined with `&&`) works for **any** rectangle. It's how you make buttons that light up when you hover over them.
