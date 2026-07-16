# 06 - UI component libraries

So far you have learned how to *style your own* components. A **UI component
library** flips that: it hands you a set of ready-made, accessible, good-looking
components (buttons, inputs, modals, menus, tabs) so you assemble a UI instead of
building every piece from scratch. This is the design-system idea from
[`react-theory/09-design-systems.md`](../react-theory/09-design-systems.md),
delivered as an npm package.

## What you get

```jsx
import Button from '@mui/material/Button'

<Button variant="contained" color="primary">Save</Button>
```

One import, and you have a polished, accessible, themeable button: focus rings,
keyboard support, hover states, and consistent styling, all already handled.
Multiply that across dozens of components and you build real UIs fast.

## The three you should know

| Library | Style | Feel | Notes |
| --- | --- | --- | --- |
| **Material UI (MUI)** | Google's Material Design | comprehensive, opinionated | huge component set, strong theming; looks "Material" out of the box |
| **Chakra UI** | clean, neutral | friendly, simple API | great defaults, style via props (`<Box p={4}>`), accessible by design |
| **shadcn/ui** | unstyled + Tailwind | you own the code | not an npm dependency: you **copy components in** and they use Tailwind |

### Material UI (MUI)

The most established. A massive catalog (data grids, date pickers, everything),
themed through a `ThemeProvider`. If you want batteries included and do not mind
the Material look, this is it.

```bash
npm install @mui/material @emotion/react @emotion/styled
```

### Chakra UI

Lighter and more neutral than MUI, with a lovely developer experience: you style
via props, and accessibility is baked in.

```jsx
import { Button, Box } from '@chakra-ui/react'
<Box p={4}><Button colorScheme="blue">Save</Button></Box>
```

### shadcn/ui

A different philosophy. It is **not** an installed dependency; a CLI **copies the
component source into your project**, where the components are built on Tailwind
([03](03-tailwind-css.md)) and **Radix UI** primitives (accessible, unstyled
building blocks). You own and edit the code. Maximum control, very popular, but
it assumes you are already using Tailwind.

## Headless / unstyled libraries

A related category worth knowing: **headless** libraries like **Radix UI** and
**Headless UI** give you the *behavior and accessibility* of complex components
(a dropdown, a dialog) with **no styling at all**, so you style them yourself.
shadcn/ui is essentially "Radix behavior + Tailwind styling, pre-assembled".

## The trade-off

**Good:** speed, consistency, and accessibility you would struggle to get right
by hand. You focus on your app, not on re-inventing a date picker.

**Cost:**
- **Bundle size and lock-in:** you ship the library's code and adopt its
  conventions.
- **Sameness:** apps built with default MUI look like every other MUI app.
  Theming helps, but escaping the default look takes effort.
- **A learning curve** per library's API.

## How it fits the projects

For the **portfolio**, a UI library is optional but can raise the polish quickly.
For the **flashcard app**, components like cards, buttons, and inputs map neatly
onto a library. Either way: **pick one**, do not mix three. Mixing libraries is a
common beginner mistake that produces an inconsistent, bloated UI.

## In one breath, for the exam

> A UI component library gives you ready-made, accessible, themeable components so
> you assemble a UI instead of building each piece. **MUI** is comprehensive and
> Material-styled; **Chakra** is lighter with a prop-based API; **shadcn/ui**
> copies Tailwind + Radix components into your project so you own the code.
> **Headless** libraries (Radix, Headless UI) provide behavior and accessibility
> with no styling. The trade-off is bundle size, lock-in, and visual sameness.

## References

- Material UI. *Documentation*. https://mui.com/material-ui/getting-started/
- Chakra UI. *Documentation*. https://chakra-ui.com/docs
- shadcn/ui. *Documentation*. https://ui.shadcn.com/docs
- Radix UI. *Primitives*. https://www.radix-ui.com/primitives
