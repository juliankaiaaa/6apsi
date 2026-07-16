# Module 2 - React

You know JavaScript now (Module 1). React is *just* JavaScript: components are
functions, props are objects, and lists are rendered with `.map()`. This unit
turns those fundamentals into real user interfaces.

This is the **reading** that pairs with the six Module 2 activities. Each
section below maps to one activity and explains every idea that activity leans
on, with a small example of the *same* idea (never the answer to an exercise).

- **Activity 1 (`m2a1`)** - Hello React: write your very first component.
- **Activity 2 (`m2a2`)** - JSX, components, and props. Build static UI from data.
- **Activity 3 (`m2a3`)** - `useState`, events, conditional rendering, lists.
- **Activity 4 (`m2a4`)** - `useEffect`, lifting state, controlled inputs, forms.
- **Activity 5 (`m2a5`)** - routing and navigation with React Router.
- **Activity 6 (`m2a6`)** - reusability: folders, custom hooks, layouts, Context.

> **The theory companion.** For the *why* behind React (what the Virtual DOM is,
> how rendering works, component architecture, design systems, atomic design,
> project structure), read the [`react-theory/`](../react-theory/) library. This
> file is the hands-on *how*; that library is the conceptual *why*. They are
> meant to be read together.

> **How to read this:** skim a section, try the matching activity, come back when
> you get stuck. You do not need to memorize APIs; understanding *what* each tool
> does is enough. Every section links to the official React docs.

---

## What's new in your workflow

Module 1 was pure JavaScript: you wrote functions and ran them in Node. React is
still JavaScript, but the way you work shifts a little. None of this is hard;
just know what to expect so nothing feels surprising:

- **`npm install` pulls more this time.** A React project needs React, a build
  tool (Vite), and the test tools, so the first install takes a minute or two.
  That is normal.
- **`npm run dev` is new.** It starts a live dev server: open the printed
  `http://localhost:5173` and your app updates as you save. This is how you
  *see* your work.
- **Your code runs in a browser now, not the terminal.** You are building a user
  interface, so you look at a page instead of `console.log` output.
- **The tests look different.** Instead of calling a function and checking its
  return value, they *render your component* and check what appears on screen
  (you will see things like `getByText`). You do not write these; you make them
  pass, exactly like Module 1.
- **What stays the same:** write your code in `src/`, run `npm test` until it is
  green, and push to submit.

> **Styling comes later.** Module 2 is about making things *work*. You make them
> *look good* in Module 3, so plain, unstyled components are completely fine
> here. Focus on behavior.

## Setup: creating a React app

React on its own is just a library. To build an app you need a **build tool**
that bundles your components, serves them while you develop, and produces files
a browser can run. The modern standard is **Vite**.

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev        # starts a dev server with hot reload
```

**System requirements:** Node.js 18+ and npm (check with `node -v`). That is it.
You will recognize the project layout from Module 1: a `package.json`, a `src/`
folder, and `npm` scripts.

> **Create React App is deprecated.** You may see older tutorials run
> `create-react-app`. It is no longer maintained; use Vite. The React code you
> write is identical either way; only the tooling around it differs. See
> [`react-theory/11-the-react-ecosystem.md`](../react-theory/11-the-react-ecosystem.md).

📖 [React: Start a New Project](https://react.dev/learn/build-a-react-app-from-scratch) ·
[Vite Guide](https://vite.dev/guide/)

---

## Activity 1 - Hello React

Your warm-up. A **component** is a function that returns **JSX** (markup). The
app's entry file renders your component into the page, so you only write the
component. Here is the *idea* on a different example (not the exercise):

```jsx
function Welcome() {
  const course = 'APSI'
  return (
    <div>
      <h2>Welcome</h2>
      <p>You are taking {course}</p>   {/* { } drops a JS value into JSX */}
    </div>
  )
}
```

Two rules you meet here: a component returns **one** root element (wrap siblings
in a `<div>` or an empty `<>...</>` fragment), and **curly braces `{ }`** drop a
JavaScript value into the markup. Run `npm run dev` and watch it appear in the
browser.

📖 [Your First Component](https://react.dev/learn/your-first-component) ·
[Writing Markup with JSX](https://react.dev/learn/writing-markup-with-jsx)

---

## Activity 2 - JSX, components, and props

### Components are functions

A **component** is a function that returns UI. Its name must start with a capital
letter so React tells it apart from a plain HTML tag:

```jsx
function Greeting() {
  return <h1>Hello</h1>
}
```

You then *use* it like a tag: `<Greeting />`.

### JSX

**JSX** lets you write HTML-looking markup inside JavaScript. It is not HTML and
it is not a string; it is syntax that compiles to function calls. A few rules
that trip everyone up at first:

- Return **one** root element. Wrap siblings in a `<div>` or an empty `<>...</>`
  fragment.
- `class` becomes **`className`**; `for` becomes `htmlFor`.
- Drop JavaScript into markup with **curly braces**: `{ }`.

```jsx
const name = 'Ana'
const ui = <p className="hi">Hello, {name}!</p>   // {name} is real JS
```

### Props

**Props** are the inputs to a component: an object of values the parent passes
in. You read them by destructuring (Module 1, objects):

```jsx
function Card({ title, price }) {
  return <article><h2>{title}</h2><p>${price}</p></article>
}

<Card title="Coffee" price={3} />   // title & price arrive as props
```

Props are **read-only**. A component never changes its own props; it only reads
them. Data flows **one way**: from parent down to child. This is *component
reuse*: the same `Card` renders any product you pass it.

> **Render a list** by mapping data to elements. Give each a stable `key` so
> React can track them (more in Activity 3):
> `products.map(p => <Card key={p.id} title={p.title} price={p.price} />)`

📖 [Your First Component](https://react.dev/learn/your-first-component) ·
[Passing Props](https://react.dev/learn/passing-props-to-a-component) ·
[Writing Markup with JSX](https://react.dev/learn/writing-markup-with-jsx)

---

## Activity 3 - State, events, conditional rendering, and lists

### `useState`

**State** is data that changes over time and that React should *re-render* when
it changes. Props come from outside; state lives inside the component.
`useState` returns the current value and a setter:

```jsx
import { useState } from 'react'

function Counter() {
  const [count, setCount] = useState(0)        // 0 is the initial value
  return <button onClick={() => setCount(count + 1)}>{count}</button>
}
```

Calling `setCount` does two things: it remembers the new value, and it schedules
a re-render so the screen catches up. **Never reassign the variable directly**
(`count = 5` does nothing); always call the setter.

### Events

You attach handlers with camelCase props that take a **function** (not a call):

```jsx
<button onClick={handleClick}>      {/* pass the function */}
<button onClick={handleClick()}>    {/* WRONG: calls it during render */}
```

### Updating state immutably

Because state must be replaced, not mutated, you use the immutable patterns from
Module 1: spread to copy an object, `.filter()`/`map()` to change arrays.

```jsx
setUser({ ...user, name: 'Ben' })          // new object, one field changed
setItems([...items, newItem])              // new array with one more
setItems(items.filter(i => i.id !== id))   // new array with one removed
```

### Conditional rendering

Show different UI from a condition, using the operators from Module 1:

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}    // either/or
{error && <p className="err">{error}</p>}   // show only when truthy
```

> **The `&&` footgun:** `count && <List />` renders `0` when `count` is `0`,
> because React renders the number. Guard with `count > 0 && <List />`.

### Lists and keys

Render a collection with `.map()`. Each item needs a **`key`**: a stable, unique
id so React can match items across re-renders. Use a real id, not the array
index, when items can be reordered or removed.

```jsx
{todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
```

📖 [State: A Component's Memory](https://react.dev/learn/state-a-components-memory) ·
[Responding to Events](https://react.dev/learn/responding-to-events) ·
[Conditional Rendering](https://react.dev/learn/conditional-rendering) ·
[Rendering Lists](https://react.dev/learn/rendering-lists)

---

## Activity 4 - Effects, lifting state, and forms

### `useEffect`

Most of your code runs *during* render and just returns UI. But some work has to
happen *after* render and touches the world outside React: fetching data,
setting a timer, subscribing to an event. That is an **effect**.

```jsx
import { useEffect, useState } from 'react'

function Clock() {
  const [now, setNow] = useState(Date.now())
  useEffect(() => {
    const id = setInterval(() => setNow(Date.now()), 1000)
    return () => clearInterval(id)   // cleanup: runs before re-run / unmount
  }, [])                             // [] = run once, after first render
}
```

The **dependency array** controls when the effect re-runs: `[]` runs it once;
`[userId]` re-runs it whenever `userId` changes; omitting it runs it after
*every* render (rarely what you want). The **cleanup function** you return
undoes the effect (clear the timer, cancel the subscription).

> **You need fewer effects than you think.** Do not use an effect to compute a
> value from props/state (just compute it during render) or to respond to a
> click (do it in the handler). Effects are for *synchronizing with an external
> system*. See [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect).

### Lifting state up

When two components need the same data, you do not duplicate it. You move the
state **up** to their closest common parent and pass it down: the value as a
prop, plus a setter (or callback) so the child can request a change. Data flows
down, events flow up. See
[`react-theory/05-component-architecture.md`](../react-theory/05-component-architecture.md).

### Controlled vs uncontrolled inputs

A **controlled** input gets its value from state, so React is the single source
of truth:

```jsx
const [email, setEmail] = useState('')
<input value={email} onChange={e => setEmail(e.target.value)} />
```

An **uncontrolled** input keeps its own value in the DOM and you read it later
with a `ref`. Prefer controlled inputs: they make validation and conditional
buttons trivial.

### Forms and validation

A form is controlled inputs plus an `onSubmit` that calls
`e.preventDefault()` (so the browser does not reload), validates, and either
shows errors or proceeds:

```jsx
function onSubmit(e) {
  e.preventDefault()
  if (!email.includes('@')) return setError('Enter a valid email')
  setError('')
  // ...submit
}
```

📖 [Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects) ·
[Sharing State Between Components](https://react.dev/learn/sharing-state-between-components) ·
[React Forms (MDN)](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Forms)

---

## Activity 5 - Routing and navigation

A single-page app does not reload the page when you "navigate". A **router**
swaps which component renders based on the URL, so it *feels* like separate pages
while staying one app. The standard is **React Router (v6+)**.

```bash
npm install react-router-dom
```

```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom'

<BrowserRouter>
  <nav><Link to="/">Home</Link> <Link to="/about">About</Link></nav>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/products/:id" element={<Product />} />   {/* dynamic */}
    <Route path="*" element={<NotFound />} />              {/* 404 catch-all */}
  </Routes>
</BrowserRouter>
```

- **`<Link>`** navigates without reloading. Use it instead of `<a href>` for
  internal links.
- **Route params** (`:id`) read with `useParams()`: `const { id } = useParams()`.
- **Nested routes** render a parent layout plus an `<Outlet />` for the child.
- **Redirects** use `<Navigate to="/login" />`; the `path="*"` route is your
  **404** page.
- **Programmatic navigation** (after a form submit, say) uses
  `const navigate = useNavigate()` then `navigate('/success')`.

📖 [React Router: Tutorial](https://reactrouter.com/start/library/installation) ·
[Routing concepts](https://reactrouter.com/start/library/routing)

---

## Activity 6 - Component reusability

### Component structure and folders

As an app grows, *how* you organize files matters as much as the code. Group by
**feature** (a `products/` folder with its components, hooks, and styles) rather
than by type once a project is real. See
[`react-theory/07-project-structure-and-organization.md`](../react-theory/07-project-structure-and-organization.md)
and [`react-theory/08-atomic-design.md`](../react-theory/08-atomic-design.md).

### Custom hooks

When two components share **logic** (not markup), extract it into a function
whose name starts with `use`. It can call other hooks. This is how you reuse
stateful behavior:

```jsx
function useToggle(initial = false) {
  const [on, setOn] = useState(initial)
  const toggle = () => setOn(o => !o)
  return [on, toggle]
}

// in any component:
const [open, toggleOpen] = useToggle()
```

### Layout components

A **layout** component holds the shared frame (header, nav, footer) and renders
whatever page goes inside it, usually via `children` or React Router's
`<Outlet />`:

```jsx
function Layout({ children }) {
  return <><Header /><main>{children}</main><Footer /></>
}
```

### Context API

When data is needed by many components at different depths (the logged-in user,
the theme), passing props through every level gets painful ("prop drilling").
**Context** lets a provider publish a value and any descendant read it with
`useContext`, no prop threading:

```jsx
const ThemeContext = createContext('light')

<ThemeContext.Provider value="dark">
  <App />            {/* anything inside can read the theme */}
</ThemeContext.Provider>

const theme = useContext(ThemeContext)   // in a deep child
```

Use Context for *low-frequency, app-wide* values. For heavy or fast-changing
state, see [`react-theory/06-state-management.md`](../react-theory/06-state-management.md).

📖 [Reusing Logic with Custom Hooks](https://react.dev/learn/reusing-logic-with-custom-hooks) ·
[Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)
