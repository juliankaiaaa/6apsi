# Project 2 - Portfolio (single-page website)

Build a personal, single-page portfolio you would be happy to link on a CV. This
project is about **styling and responsive design**: it must look good and work on
a phone and a wide screen. Use everything from
[01](01-styling-in-react.md)-[07](07-choosing-your-stack.md) and the design
theory in [`react-theory/`](../react-theory/).

You choose the styling approach and any UI library. The requirements below are
the same whatever you pick.

---

## What to build

A single page (one route is fine) with clear, well-designed sections:

- a **hero / intro** with your name as the main heading,
- an **About** section,
- a **Projects** section (show a few projects, real or sample, as cards),
- a **Contact** section with a way to reach you (an email link or a form).

It must be **responsive** (mobile-first), use a **Flexbox and/or Grid** layout,
and apply the design ideas you have learned: visual hierarchy, consistent
spacing and color, and accessibility.

---

## The required contract (so it can be graded)

Design it however you like, **but include these landmarks** so the automated
checks can confirm the structure. Everything else (layout, colors, content,
components) is your choice.

> Your portfolio is rendered by `src/App.jsx` (a default-exported component).
> Split it into as many components as you like; `App` just has to render the
> whole page.

| Requirement | Required marker |
| --- | --- |
| Page name / hero | a level-1 heading (`<h1>`) with your name |
| Navigation | a `<nav>` element (role "navigation") |
| Main content | a `<main>` element (role "main") |
| About section | a heading whose text contains **"About"** |
| Projects section | a heading whose text contains **"Projects"** |
| Contact section | a heading whose text contains **"Contact"** |
| Contact method | a `mailto:` link, an external link, or a contact form |

### Styling and responsive requirements

- Use **one** real styling approach (CSS Modules, Tailwind, or
  styled-components; a UI library counts). Not all-inline styles.
- Use **Flexbox and/or Grid** for layout
  ([05](05-responsive-layout-flexbox-grid.md)).
- **No horizontal scrolling on a 375px-wide phone** (the grader checks this in a
  real browser). Use fluid units and `max-width: 100%` on media.
- The layout should genuinely adapt between phone and desktop (e.g. a single
  column on mobile, multiple columns on desktop).

---

## How to start (a suggested build order)

Build the structure first, get it green, then make it beautiful. A good order:

1. **Get it running.** Create your repo from the template, `npm install`,
   `npm run dev`.
2. **Choose your styling approach** ([07-choosing-your-stack.md](07-choosing-your-stack.md))
   and install it.
3. **Lay out the skeleton** in `src/App.jsx` with plain markup first (replace the
   placeholder): an `<h1>` with your name, a `<nav>`, a `<main>`, headings for
   About, Projects, and Contact, and a contact link. Run `npm run test:watch`;
   the structure tests go green.
4. **Add your real content** to each section.
5. **Style it mobile-first** ([05-responsive-layout-flexbox-grid.md](05-responsive-layout-flexbox-grid.md)):
   base styles for a phone, then add columns and spacing for wider screens with
   media queries (or Tailwind's `md:` prefixes). Check there is no sideways
   scroll at a narrow width.
6. **Polish:** visual hierarchy, consistent spacing and color, accessible
   contrast.
7. **Push** and check the phone / tablet / desktop screenshots in the Actions
   tab.

By step 3 the automated structure checks pass. Steps 5 and 6 are what the design
rubric rewards.

## How it is graded

Out of **100 points: 50 automated + 50 a design rubric** (the full rubric, with
levels, is in [ASSESSMENT.md](ASSESSMENT.md)).

- **Automated (50):** it builds and runs (10), uses a real styling approach (5),
  the required section landmarks exist (25), and there is no horizontal scroll on
  mobile (10).
- **Design rubric (50):** visual design & hierarchy, responsive quality,
  consistency / design system, accessibility, code organization, and
  completeness / UX, scored by your instructor from your running app and the
  screenshots captured at phone / tablet / desktop widths.

> The automated part is a floor, not the goal. The rubric rewards a genuinely
> polished, thoughtful, accessible design. Build something you are proud of.

## Set up your repo

1. **Use this template -> Create a new repository**, owner **`HAU-6APSI`**.
2. Name it `m3a2-<classcode>-yourname`, **Private**.
3. Clone it and `npm install`, then build your portfolio in `src/`.

```bash
npm run dev     # http://localhost:5173 - check it at narrow and wide widths
npm test        # run the structure checks locally
npm run build   # must succeed
```

## Submit

```bash
git add -A
git commit -m "✨ Project 2 - Portfolio"
git push
```

The **Actions** tab shows the checks and screenshots of your portfolio at phone /
tablet / desktop widths.
