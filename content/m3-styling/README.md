# Module 3 - Styling, UI Frameworks, and Projects

Module 2 made things *work*. Module 3 makes them *look good* and pulls
everything together into two real projects you can show people.

You will learn the modern ways to style a React app (CSS Modules, Tailwind,
styled-components), how to build responsive layouts with Flexbox and Grid, and
how to use a UI component library (Material UI, Chakra, or shadcn/ui). Then you
apply all of it, plus everything from Module 2, in two projects.

## The reading

Read these in order. They are hands-on: lots of code, and you pick what fits
your project.

| # | File | Covers |
| --- | --- | --- |
| 01 | [Styling in React](01-styling-in-react.md) | the landscape, why "just a CSS file" stops scaling |
| 02 | [CSS Modules](02-css-modules.md) | locally scoped CSS, zero new syntax |
| 03 | [Tailwind CSS](03-tailwind-css.md) | utility-first styling in your markup |
| 04 | [CSS-in-JS (styled-components)](04-css-in-js-styled-components.md) | styles as components |
| 05 | [Responsive layout: Flexbox and Grid](05-responsive-layout-flexbox-grid.md) | the two layout systems, mobile-first |
| 06 | [UI component libraries](06-ui-component-libraries.md) | Material UI, Chakra, shadcn/ui |
| 07 | [Choosing your stack](07-choosing-your-stack.md) | trade-offs and a decision guide |

This builds on the design theory you already have:
[`react-theory/09-design-systems.md`](../react-theory/09-design-systems.md),
[`react-theory/10-design-methodologies.md`](../react-theory/10-design-methodologies.md),
and the styling overview in
[`react-theory/11-the-react-ecosystem.md`](../react-theory/11-the-react-ecosystem.md).

---

## The two projects

You choose **one** styling approach and (optionally) **one** UI library per
project. The choice is yours; the requirements are the same whatever you pick.
Full briefs and the grading details:

- [m3a1-course-companion.md](m3a1-course-companion.md) - docs reader + flashcard generator
- [m3a2-portfolio.md](m3a2-portfolio.md) - single-page portfolio
- [ASSESSMENT.md](ASSESSMENT.md) - how the projects are graded (automated + rubric)

### Project 1 - Course Companion (docs reader + flashcard generator)

A small app with two halves:

1. **A docs reader** for course material: a sidebar of topics and a content area
   that shows the selected topic. This is your Module 2 routing and components in
   action.
2. **A flashcard generator**: build decks of flashcards from data, then study
   them. You add cards (a question and an answer), the app lists them, you can
   **flip** a card to reveal the answer, move between cards, and remove a card.

This project is about **data and state**: a deck is an array of card objects
like `{ id, question, answer }`. You will use `useState`, lists with keys,
controlled inputs, and conditional rendering, all styled with your chosen
approach.

### Project 2 - Portfolio (single-page website)

A personal, single-page portfolio that demonstrates **styling and responsive
design**:

- Clear sections: a hero/intro, about, projects, and contact.
- Built with your chosen styling approach (CSS Modules, Tailwind, or
  styled-components) and, if you like, a UI library.
- A **responsive layout** using Flexbox and/or Grid: it must look right on a
  phone *and* a wide screen (mobile-first, no horizontal scrolling on mobile).
- Good use of the design ideas from `react-theory`: hierarchy, spacing,
  consistency, accessibility.

> **How these are graded: 100 points, split 50 / 50.** Fifty are automated (it
> builds and runs, the required behavior works, it is responsive, it uses a real
> styling approach); fifty are a **design rubric** your instructor scores (visual
> design, responsive quality, consistency, accessibility, code organization, and
> completeness). The full rubric with levels is in
> [ASSESSMENT.md](ASSESSMENT.md). Build something you are proud to link on a CV.

---

> **A note on scope.** You are not learning *new* React here, you are combining
> what you know with real styling. If you find yourself stuck on a React concept,
> go back to the Module 2 reading; if you are stuck on a *layout*, doc 05 is your
> friend.
