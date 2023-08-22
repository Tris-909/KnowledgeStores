<h2>1. Features and Limitations of React</h2>

<h4> Pros:</h4>

- Using JSX so it’s easy to read and write and it is flexible as well
- Virtual DOM
- Server-side rendering
- One-way data flow
- Reusable components

<h4> Cons:</h4>

- React is a library not a framework meaning if you need extra function like routing you have to install and learn how to use packages related routing.
- A learning curve is required to learn how to use. But requires even higher learning curve to learn advanced methods to know almost anything about React.
- React on it owns doesn't support SEO well because it is a single page application.

<h2>2. What is JSX ? </h2>

- Javascript XML boils down to React.createElement(type, props, …children)
- Web browsers can't read JSX directly they can only read JS and HTML. So React uses Babel to transform JSX codes into JS code before sending it to the Browser

<h2>3. What is the Virtual DOM ? </h2>

- DOM stands for Document Object Model. The DOM represents an HTML model with a logical tree structure. Each branch ends in a node and each node contains objects.
- React keeps a lightweight representation of the actual DOM called Virtual DOM in memory and synced with the real DOM.
- When ever data changes and a component re-render it will cause Virtual DOM to reflect these changes as well. Then React will compare the Virtual DOM with the real DOM and updated the new DOM with change. See how we didn’t have to update the real DOM with a whole new DOM from scratch to bottom just to reflect some changes in some branches ? That is why virtual DOM is useful.

<h2>4. Differences between ES6 and ES5 ? </h2>

- Arrow functions. Functional Component using arrow function. Removing the `this` keyword ( Practical React )
- ES5 `exports` vs ES6 `export`
- ES5 `require` vs ES6 `import`

<h2>5. React events </h2>

- React events are actions that user or system can trigger like onClick, onSubmit, onPress or can even be a function that user create. They are all `camelCase`.
- Synthetic events combine the response of different browser's native events into one API so we can make sure the behaviour is the same accross different web browsers. One such event that is commonly used is `event.preventDefault()`.

<h2>6. Key prop in React array of elements ?</h2>

- React using keys in an array of elements to keep track which items have changed, added or removed from an array.
- Without “key” it will cause performance issues because React will try to create every single element in an array from scratch for every re-render.

<h2>7. React notes ?</h2>

- Comment in React using `#` or `/* */`
- React Context provides a way to pass data without having to pass it down as props to every single component above your desired component. Actual implementation: `https://react.dev/learn/passing-data-deeply-with-context`

<h2>8. React components ?</h2>

- Functional Component / Class Component.
- Stateful / Stateless Component.
- Each component needs `render()` method to display component to the screen ( if they get called correctly in the first place ofc )
- React state holds data of a component. Whenever state changes, component re-render. You can use `setState` hook in react to declare and update the state. You **have** to use `setState()` to update state otherwise the component won't re-render even if the state changes.
- `props` is used to pass data from one component to another. Passing `props` from parent component to child component.
- You can use `style={}` keyword and inside `{}` is a style object.
- `Fragment` is a React feature that allow user to return a list of component on the same level without the need to add another node into DOM tree by adding any actual parent component above it. The syntax is `<></>` wraps around child components.
- HoC ( Higher order component ) takes in a component and return a new component. HoC allows you to add additional functionality to a component without modifying the component’s code. For example a page component will have a HoC to check if the user who is accessing that page is authenticated or not. Or You can have a HoC to style or theme any page you pass into it.

- There are 3 cycles : Mounting, Updating, Unmouting. Each have different life cycle methods run on all phases of cycle

  - Mounting : constructor() -> getDerivedStateFromProps() -> render() -> componentDidMount()
  - Updating : getDerivedStateFromProps() -> shouldComponentUpdate() -> render() -> getSnapshotBeforeUpdate() -> componentDidUpdate()
  - Unmounting : componentWillUnmount()

- `constructor()` is called when `a component is first created`.
- `getDerivedStateFromProps(props, state)` (^16.3) is called after `constructor()` but before `render()`. It should return an updated state of the component or null if no changes required.
- `render()` is called `every time a component need to re-render` or it `load the component for the first time`.
- `componentDidMount()` is called `after the component mounted into the DOM`.
- `shouldComponentUpdate() true/false` is called on Updating Phase `before render() method`. It returns a boolean value to decide a component should update or not.
- `getSnapshotBeforeUpdate(prevProps, prevState)` it gets access to previous props and state before the update so it can manipulate that. The method when called has to be also called with `componentDidUpdate()`
- `componentDidUpdate(prevProps, prevState, snapShot)` is called after the component is updated in the DOM.
- `componentWillUnmount()` is called before the component is unmounted from the DOM.

<h2>9. React hooks ?</h2>

Important hooks :

- `useState()` https://react.dev/reference/react/useState
- `useEffect()` https://react.dev/reference/react/useEffect
- `useContext()` https://react.dev/reference/react/useContext

Less common hooks :

- `useId()` Generating unique ID -> https://react.dev/reference/react/useId
- `useMemo(func, [dependencies])` Cache the result of a calculation between each re-renders, and only trigger the function when dependencies change https://react.dev/reference/react/useMemo
- And many more...

<h2>10. React APIs ?</h2>

<h4>1. React.context</h4>

```
import { createContext } from 'react';

# ...

const ThemeContext = createContext('light');

# ...

const theme = useContext(ThemeContext);
<ThemeContext.Provider value={theme}>
  <Page />
</ThemeContext.Provider>
...
# Anything inside <Provider> can now access to `theme`
```

<h4>2. React.lazy</h4>

- `lazy` allows you defer loading component’s code until it is rendered for the first time.
- Call `lazy` outside of your component to declare a lazy-load React component :

```
// Declare in one file
import { lazy } from 'react';

const MarkdownPreview = lazy(() => import('./MarkdownPreview.js'));

// Using it in other file with <Suspense>
<Suspense fallback={<Loading />}>
  <h2>Preview</h2>
  <MarkdownPreview />
 </Suspense>
```

<h4>3. React.memo</h4>

- Allow you to skip re-rendering some components when it props unchanged. Mostly for performance optimization.
