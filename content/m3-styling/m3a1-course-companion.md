# Project 1 - Course Companion (docs reader + flashcard generator)

Build a small React app with two halves: a **docs reader** for course material,
and a **flashcard generator** you can study from. This is where your Module 2
React (components, state, lists, routing) meets your Module 3 styling.

You choose the styling approach and any UI library (see
[07-choosing-your-stack.md](07-choosing-your-stack.md)). The requirements below
are the same whatever you pick.

---

## What to build

### Part A - Docs reader

A simple documentation layout:

- a **navigation** area (a sidebar or top nav) listing at least **3 topics**,
- a **content area** that shows the selected topic's content,
- selecting a topic shows its content without a full page reload (use state or
  React Router).

Keep the topic content simple (a heading and a few paragraphs each). It can be
hard-coded data; the point is the layout and navigation, not a CMS.

### Part B - Flashcard generator

A study tool driven by data. A flashcard is an object like:

```js
{ id: 1, question: 'What is the Virtual DOM?', answer: 'An in-memory tree React diffs to update the real DOM' }
```

The app must let you:

- **add** a card by typing a question and an answer,
- see all cards in a **list**,
- **flip** a card to reveal/hide its answer,
- **delete** a card.

This exercises arrays of objects, `useState`, lists with keys, controlled
inputs, conditional rendering, and events, all from Module 2.

---

## The required contract (so it can be graded)

Style and structure the app however you like, **but expose these hooks** so the
automated tests can find and drive the flashcard feature. These are the only
fixed names; everything else is your choice.

> **Put the flashcard feature in `src/Flashcards.jsx`** (a default-exported
> component). The tests render that component directly, so the flashcards work
> the same however you lay out the rest of the app. Build the docs reader and
> wire everything together in `src/App.jsx`, using a `<nav>` for the topic list.

### Add-card form

| Element | Required marker |
| --- | --- |
| Question input | `placeholder="Question"` |
| Answer input | `placeholder="Answer"` |
| Add button | accessible name **"Add card"** (i.e. a `<button>Add card</button>`) |

Adding must **ignore empty input**: if either field is blank, no card is added.

### Each flashcard

| Element | Required marker |
| --- | --- |
| The card container | `data-testid="flashcard"` |
| The question text | visible on the card at all times |
| Flip button | accessible name **"Flip"** (one per card) |
| Delete button | accessible name **"Delete"** (one per card) |

- The **answer text must NOT be in the document until the card is flipped**
  (use conditional rendering, not just CSS `display:none`).
- Clicking **Flip** reveals the answer; clicking again hides it.
- Clicking **Delete** removes that one card.

Minimal example of a conforming card (your styling will differ):

```jsx
<div data-testid="flashcard">
  <p>{card.question}</p>
  {flipped && <p>{card.answer}</p>}
  <button onClick={flip}>Flip</button>
  <button onClick={remove}>Delete</button>
</div>
```

### Styling requirement

Use **one** real styling approach: CSS Modules, Tailwind, or styled-components
(a UI library counts). Styling everything with inline `style={{}}` does **not**
count.

---

## How to start (a suggested build order)

Do not try to build everything at once. Add one piece, watch a test go green,
then add the next. A good order:

1. **Get it running.** Create your repo from the template, `npm install`,
   `npm run dev`. You should see the placeholder page.
2. **Choose your styling approach** ([07-choosing-your-stack.md](07-choosing-your-stack.md))
   and install it. You do not have to style anything yet; just have it ready.
3. **Flashcards, part 1: add + list.** In `src/Flashcards.jsx`, build the
   add-card form (Question and Answer inputs + an "Add card" button) and render
   the cards as a list, each with `data-testid="flashcard"`. Run
   `npm run test:watch`; the "adds a card" and "ignores empty input" tests go
   green.
4. **Flashcards, part 2: flip.** Give each card a "Flip" button that
   conditionally shows the answer. Two more tests go green.
5. **Flashcards, part 3: delete.** A "Delete" button that removes the card.
6. **Docs reader.** In `src/App.jsx`, add a `<nav>` of at least 3 topics and a
   content area that swaps when you pick one. The App test goes green.
7. **Style it** with your chosen approach, then **push** and check the Actions
   tab.

By step 6 every automated test should be green. Steps 2 and 7 are what the
design rubric rewards.

## How it is graded

Out of **100 points: 50 automated + 50 a design rubric** (the full rubric, with
levels, is in [ASSESSMENT.md](ASSESSMENT.md)).

- **Automated (50):** it builds and runs (10), uses a real styling approach (5),
  the flashcard contract works (add / flip / delete) (25), and there is no
  horizontal scroll on mobile (10).
- **Design rubric (50):** visual design & hierarchy, responsive quality,
  consistency / design system, accessibility, code organization, and
  completeness / UX, scored by your instructor from your running app and the
  published screenshots.

## Set up your repo

1. **Use this template -> Create a new repository**, owner **`HAU-6APSI`**.
2. Name it `m3a1-<classcode>-yourname`, **Private**.
3. Clone it and `npm install`, then build your app in `src/`.

```bash
npm run dev     # build it (http://localhost:5173)
npm test        # run the contract tests locally (your self-check)
npm run build   # must succeed; the grader builds it too
```

## Submit

Pushing is submitting:

```bash
git add -A
git commit -m "✨ Project 1 - Course Companion"
git push
```

The **Actions** tab shows the test results, a build check, and screenshots of
your app at phone / tablet / desktop widths.
