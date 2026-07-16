# 03 - Tailwind CSS

**Tailwind** takes a different bet: stop writing CSS files and naming things at
all. Instead you compose small, single-purpose **utility classes** directly in
your markup. `p-4` is `padding: 1rem`, `flex` is `display: flex`, `text-center`
is `text-align: center`.

## What it looks like

```jsx
function Card({ title }) {
  return (
    <article className="rounded-xl bg-white p-4 shadow">
      <h2 className="text-xl font-semibold text-slate-800">{title}</h2>
    </article>
  )
}
```

No `Card.css`, no class names to invent. The styling lives next to the markup it
applies to, and you never leave the component.

## The mental model

Each class does one thing, and they read in a consistent shorthand:

| Class | CSS | Family |
| --- | --- | --- |
| `p-4` | `padding: 1rem` | spacing |
| `mt-2` | `margin-top: 0.5rem` | spacing |
| `flex` / `grid` | `display: flex/grid` | layout |
| `gap-4` | `gap: 1rem` | layout |
| `text-xl` | `font-size: 1.25rem` | typography |
| `bg-slate-800` | a background color | color |
| `rounded-xl` | `border-radius` | borders |

Numbers come from a **spacing scale** (`1` = 0.25rem, `4` = 1rem), so spacing
stays consistent across the whole app by default. The color names (`slate-800`)
come from a built-in palette. This *is* a small design system handed to you.

## Responsive and states are just prefixes

This is where Tailwind shines. Prefix a class to apply it only at a breakpoint or
in a state. It is **mobile-first**: an unprefixed class is the base, and
`md:` applies from medium screens up.

```jsx
<div className="grid grid-cols-1 gap-4 md:grid-cols-3">...</div>
{/* one column on phones, three from medium screens up */}

<button className="bg-blue-600 hover:bg-blue-700">Save</button>
{/* darker on hover */}
```

## Setup (Vite)

Tailwind needs a build step. The current versions install a Vite plugin and a
single CSS import:

```bash
npm install tailwindcss @tailwindcss/vite
```

```js
// vite.config.js
import tailwindcss from '@tailwindcss/vite'
export default { plugins: [tailwindcss()] }
```

```css
/* src/index.css */
@import "tailwindcss";
```

Then import that CSS once in `main.jsx`. (Always follow the current
[official install guide](https://tailwindcss.com/docs/installation/using-vite),
since setup details change between versions.)

## Strengths and trade-offs

**Good:**
- Extremely fast to build with once you know the classes.
- Built-in spacing/color scales keep things consistent.
- No naming, no separate files, no unused CSS (it strips what you do not use).
- Responsive and hover/focus states are trivial.

**Trade-offs:**
- The markup gets **long and noisy** (`className` with a dozen utilities).
- There is a learning curve: you must learn the class vocabulary.
- Repeated patterns should be extracted into a **component** (not copied), or it
  gets unmaintainable.

## When to choose it

When you want to move fast and like keeping styles next to markup. Hugely popular
in industry. Pairs well with shadcn/ui ([06](06-ui-component-libraries.md)),
which is built on Tailwind.

## In one breath, for the exam

> Tailwind is **utility-first**: instead of writing CSS and naming classes, you
> compose single-purpose classes (`p-4`, `flex`, `text-xl`) directly in your
> markup. Built-in spacing and color scales enforce consistency, and responsive
> or state styles are just prefixes (`md:`, `hover:`), mobile-first. The cost is
> verbose markup; repeated patterns should be extracted into components.

## References

- Tailwind CSS. *Documentation*. https://tailwindcss.com/docs
- Tailwind CSS. *Install with Vite*. https://tailwindcss.com/docs/installation/using-vite
- Tailwind CSS. *Responsive design*. https://tailwindcss.com/docs/responsive-design
