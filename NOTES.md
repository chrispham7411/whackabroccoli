# 📓 Notes — Whack-a-Broccoli

Our lesson plan, build log, and idea backlog. This is a **living** doc — we
add to it after every coding session.

---

## 🎯 The big objective

> Show the kids that an AI can turn **plain English** into **working code**,
> by building a game together one prompt at a time.

The game itself is the prize. The lessons happen *while* we build it.

### Three things we want the kids to take away

1. **You can make a computer do things by talking to it.** No magic words —
   just describe what you want.
2. **The clearer your words, the better the result.** Fuzzy in, fuzzy out.
3. **The AI makes choices you didn't ask for** (colors, speed, fonts). That's
   not a bug — that's the AI filling in the blanks. Decide if you like the
   choice, then *ask it to change* what you don't.

---

## 🎮 The game we're building

**Whack-a-Broccoli — 2-player edition.**

- 3×3 grid of holes on a kitchen-table background
- Broccoli on forks 🥦🍴 pop up at random — smash them with a cartoon hand ✋
- Candy 🍬 sometimes pops up — **don't** whack it or a bomb goes off (−1)
- Whacked broccoli explodes into green bits that **fall and pile up** at the
  bottom of the screen (gravity!)
- Splat sound 💥 + "YUCK!" text + hand slam animation + floating +1 / −1
- 30-second round
- Two players on one keyboard:
  - **Left:** A / S / D / F (their 4 holes)
  - **Right:** J / K / L / ; (their 4 holes)
  - Middle hole = bonus, either can hit it

---

## 🪜 Build order

Each row is **one prompt** the kids give. Tick the box when it's shipped.

| Step | The kids' prompt (in their own words) | Status |
|------|----------------------------------------|--------|
| v1 | "Make a 3×3 grid of holes on a kitchen-table background." | ✅ |
| v2 | "Make a broccoli on a fork pop up in a random hole every second." | ✅ |
| v3 | "When I click a broccoli, it disappears and a +1 floats up." | ✅ |
| v3.5 | "It works with mouse but not with keyboard." (Q/W/E A/S/D Z/X/C) | ✅ |
| v4 | "Sometimes candy pops up. If I hit it, a bomb goes off and −1." | ✅ |
| v5 | "Hand slam, YUCK!/YUM…NO! text, splat sound." | ✅ |
| v6 | "Add a 30-second timer and a 'Game Over' screen showing the winner." | ⏳ |
| v7 | "Make it two players: A/S/D/F vs J/K/L/;." | |
| v8 | "When broccoli explodes, the bits fall down and pile up at the bottom." | |
| v9 | Kids' wishlist (see below) | |

---

## 🖼️ Image prompts (for "art day")

When we're ready to swap emoji for real images, paste these into Claude.ai,
ChatGPT, or Gemini's image generator. Save the results into `images/` as:

- `broccoli.png`
- `fork.png`  *(or `broccoli-on-fork.png` if combined)*
- `hand.png`
- `candy.png`
- `bomb.png`
- `splat.png`

### Prompts to try

> A cute cartoon piece of bright green broccoli with a googly-eyed face, stuck
> on a shiny silver fork. Flat illustration style, transparent background,
> centered, no shadow. PNG.

> A cartoon human hand with a peach skin tone, open palm facing the viewer,
> ready to smack down. Bold black outline, flat colors, transparent
> background. PNG.

> A bright red and white striped peppermint candy with a smiley face. Flat
> cartoon illustration, transparent background. PNG.

> A small round black bomb with a lit fuse and a sparkle, cartoon style, flat
> colors, transparent background. PNG.

> A green splat/splash shape made of broccoli bits, like paint splatter,
> cartoon style, transparent background. PNG.

---

## 📒 Build log

### v1 — shipped
- 3×3 grid of dark holes on a wood-grain "kitchen table" background.
- Title bar across the top.
- Pure HTML + CSS, no JavaScript.
- **Kids' reaction:** *(fill in after they see it!)*

### v2 — shipped
- A broccoli-on-fork pops up in a random empty hole every ~0.9 seconds.
- Stays up for ~1.1 seconds, then drops back down and disappears.
- Made from emojis stacked together: 🥦 on top, 🍴 underneath rotated upside
  down to look like the broccoli is on a stick. (Hacky! We swap to a real
  image on art day.)
- First JavaScript in the project — `setInterval` keeps the game going.
- **Kids' reaction:** *(fill in after they see it!)*

### v3 — shipped
- Click a broccoli → it vanishes, a yellow "+1" floats up out of the hole,
  scoreboard at the top ticks up by 1.
- Cursor is now a crosshair so it feels like aiming.
- New keyframe animation `floatUp` for the +1 pop.
- Bug we already thought about: clicking *and* the auto-hide could fire at
  the same time and double-free the hole — guarded with a `_gone` flag.
- **Kids' reaction:** *(fill in!)*

### v3.5 — shipped (the "AI only does what you ask" lesson)
- Kids tried the keyboard. Nothing happened. We talked about why: nobody
  ever *asked* the AI for keyboard support — only mouse clicks. The plan
  in NOTES isn't the prompt!
- Then we added keyboard whacking. Keys map spatially to the grid:
  - **Q W E** → top row
  - **A S D** → middle row
  - **Z X C** → bottom row
- Refactored the whack action into a `whack()` function so both click and
  keydown share the same code.

### v4 — shipped
- 25% chance any given pop is a candy 🍬 instead of broccoli.
- Whack a candy → red "−1" floats up, a 💥 boom briefly fills the hole,
  score drops by 1.
- Score can now go negative.
- Code change worth noticing: the `whack()` function now *branches* on what
  kind of thing was whacked. Same function, different outcomes.
- **Kids' reaction:** *(fill in!)*

### v5 — shipped (the "feel" round)
- ✋ hand emoji slams down onto the hole on every whack — drops from above,
  rotates slightly, bounces, fades.
- Green **"YUCK!"** text pops up for broccoli, red **"YUM...NO!"** for candy.
- Splat sound effect! Synthesized in real-time with the **Web Audio API** —
  no audio file needed. It's a noise burst (texture) layered with a low
  sine-wave thud (impact). Candy splat is pitched higher than broccoli.
- Lesson worth telling the kids: *sound effects can be made with math*. The
  computer is literally calculating each tiny number that becomes the wave
  your speakers play. We didn't download a sound — we *generated* one.
- **Kids' reaction:** *(fill in!)*

### v6 — ⏳ next
- 30-second timer counts down at the top.
- When it hits 0: stop the broccoli/candy from spawning, freeze the score,
  show a "GAME OVER" overlay with the final score.
- A "Play Again" button to reset and start fresh.

---

## 💡 Kids' wishlist (v9 and beyond)

Add ideas here as the kids think of them. Anything goes.

- [ ]
- [ ]
- [ ]

---

## 🤖 What we noticed about the AI (lessons)

Add observations here whenever the AI surprises us (good or bad).

### Format
> **What we asked for:** ...
> **What the AI made:** ...
> **What we learned:** ...

#### Example
> **What we asked for:** "Make a 3×3 grid of holes on a kitchen-table background."
> **What the AI made:** Brown wood-grain background, dark circular holes with
> shadows so they look like real holes — but we never asked for shadows.
> **What we learned:** The AI fills in details on its own. If we don't like
> them, we just say so.
