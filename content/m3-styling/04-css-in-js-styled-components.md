# 04 - CSS-in-JS (styled-components)

**CSS-in-JS** writes your styles *in JavaScript*, tied directly to a component.
The most famous library is **styled-components**. The idea: a styled element is
itself a component, with its styles baked in and its class name auto-generated
(so, no clashes, ever).

## What it looks like

```jsx
import styled from 'styled-components'

const Card = styled.article`
  padding: 1rem;
  border-radius: 12px;
  background: white;
`
const Title = styled.h2`
  font-size: 1.25rem;
  font-weight: 600;
`

export default function ProductCard({ title }) {
  return (
    <Card>
      <Title>{title}</Title>
    </Card>
  )
}
```

`Card` is a real component that renders an `<article>` with those styles. You
write actual CSS inside the backticks (a tagged template literal), including
`:hover`, media queries, and nesting.

## Styling from props

The superpower: styles can read the component's **props**, so dynamic styling is
natural:

```jsx
const Button = styled.button`
  background: ${(props) => (props.$primary ? '#2563eb' : '#e5e7eb')};
  color: ${(props) => (props.$primary ? 'white' : '#111')};
  padding: 0.5rem 1rem;
`

<Button $primary>Save</Button>
<Button>Cancel</Button>
```

(The `$` prefix marks a prop as "for styling only", so it is not passed to the
DOM.)

## Theming

styled-components ships a `ThemeProvider` (it uses React Context, see
[`react-theory/06-state-management.md`](../react-theory/06-state-management.md)).
You define design tokens once and every styled component can read them:

```jsx
import { ThemeProvider } from 'styled-components'
const theme = { colors: { primary: '#2563eb' }, space: { md: '1rem' } }

<ThemeProvider theme={theme}>
  <App />
</ThemeProvider>

const Box = styled.div`
  padding: ${(p) => p.theme.space.md};
  color: ${(p) => p.theme.colors.primary};
`
```

This is a clean, real **design system** in code.

## Setup

```bash
npm install styled-components
```

That is it; no build config. (There are other CSS-in-JS libraries:
**Emotion** is very similar; newer "zero-runtime" options like vanilla-extract
move the work to build time.)

## Strengths and trade-offs

**Good:**
- Styles and component live together; delete the component, the styles go with it.
- Dynamic, prop-driven styles are effortless.
- Real theming via Context, with no naming and no clashes.

**Trade-offs:**
- A **runtime cost**: styles are generated as the app runs (smaller in newer
  versions, but real). This is why the ecosystem is drifting toward zero-runtime
  options and Tailwind.
- Styles defined inside a component re-create on each render unless defined
  outside it (a common beginner mistake; define `styled.x` at module top level).

## When to choose it

When you love writing CSS, want it colocated with components, and need dynamic,
theme-driven styling. Common in existing codebases; know it well even though the
trend is shifting.

## In one breath, for the exam

> CSS-in-JS (styled-components) writes CSS inside JavaScript as **styled
> components**: `styled.button\`...\`` returns a component with those styles and
> an auto-generated, clash-free class name. Styles can read **props** for dynamic
> styling, and a `ThemeProvider` (React Context) supplies design tokens. The cost
> is a runtime overhead, which is why newer projects lean toward Tailwind or
> zero-runtime CSS-in-JS.

## References

- styled-components. *Documentation*. https://styled-components.com/docs
- Emotion. *Introduction*. https://emotion.sh/docs/introduction
- MDN Web Docs. *Template literals*. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
