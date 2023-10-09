# React

**React** is a JavaScript library for building **User Interfaces**. It is responsible for the **view layer** of our application. This means it is only responsible for rendering our User Interface (such as the text, text boxes, buttons, etc.) as well as updating the UI whenever it changes.

- React uses a **component-based architecture** to create interfaces with an intuitive declarative approach. This also allows us to reuse this logic in another part of UI without having to re-write it.

- **React is a library and not a framework**.
  The difference between a library and a framework is that a library only helps us in one aspect. In contrast, a framework helps us in many aspects. For example:

  - **React** is a library because it only takes care of our UI.
  - **Angular**, on the other hand, is a framework because it handles much more than the UI (It handles Dependency Injection, CSS encapsulation, etc.)

- React itself is not a UI Library as in it does not give us beautifully designed buttons or cards. It helps us manage complicated UI but does not come with a design system. It will be up to us to choose a design library or use CSS to make it look nice and user-friendly.

## Component

A component is a reusable and self-contained piece of a user interface in React. Components can be functional (using functions) or class-based (using classes) and encapsulate both the UI and the logic related to that UI. They allow you to break down complex user interfaces into smaller, manageable parts.

## JSX

JSX is a syntax extension used in React to write UI components in a more declarative and readable way. It allows you to mix HTML-like code within your JavaScript code. JSX elements are transpiled to JavaScript by tools like Babel before being rendered by React.

## ReactDOM

ReactDOM is a package in React that provides the necessary methods to interact with the Document Object Model (DOM) of a web page. It acts as a bridge between React elements (created with JSX) and the actual DOM in the browser. The most commonly used ReactDOM function is ReactDOM.render(), which takes a React component and renders it to the specified DOM element, effectively adding it to the web page.

## React.Fragments

- React Fragments are a container component in React that allow you to group multiple elements without adding an extra parent div or any other unnecessary DOM element.
- They are particularly useful when you want to return multiple adjacent elements from a component's render method without wrapping them in a single container.
- React Fragments can be created using the <React.Fragment> syntax, for example:

```javascript
<React.Fragment>
  <h1>Hello World</hi>
  <p>React is awesome! </p>
</React.Fragment>
```

- React Fragments can also be created using an empty angle bracket syntax `<>...</>`, which is a shorter and more concise way to define fragments, for example:

```javascript
<>
  <h4>Hello World</h1>
  <p>React is Awesome! </p>
</>
```

## Conditional Rendering

- Conditional rendering refers to the process of displaying different elements or components in your React application based on specific conditions or criteria.
- In React, conditional rendering can be achieved in various ways, but two common approaches involve using ternary operators (`? :`) or short-circuit evaluation (`&&`).

```javascript
<React.Fragment>
  { myBool ? <hi>Hello World</h1> : null }
  { myOtherBool && <p>React is Awesome!</p> }
</React.Fragment>
```

- When using ternary operators, we conditionally render one element or another based on a boolean condition. In our example, if `myBool` is `true`, it renders an `<h1>` element, otherwise, it renders `null`. Similarly, with `myOtherBool &&`, the `<p>` element is rendered only if `myOtherBool` is `true`.
- The use of `null`, `undefined`, `true`, or `false` are used in JSX as they do not render anything.
  
## Props

- Props are JavaScript objects passed as parameters to functional components in React.
- They contain key-value pairs representing attributes that were passed to the component when it was used in JSX.
- Props are read-only and cannot be modified by the component receiving them; they are intended for data that is passed from parent to child.
- Consider an example:

```javascript
<MyComponent message-"hello” number={42} />
```

The `MyComponent` function would take in props with two key-value pairs:

```javascript
function MyComponent(props) {
  console.log(props.message); // “hello”
  console.log(props.number); // 42
  return <hi>Hello World!</h1>;
```

- In the above example, the `MyComponent` function receives `props` as an argument, and we can access the values of those props using dot notation, such as `props.message` and `props.number`.
- Props are a way to customize and configure child components based on data or settings provided by their parent components.

## State

- State in React refers to data that is specific to a particular instance of a component.
- It is used to store and manage information that can change over time and should persist between renders.
- When state data is modified, React automatically triggers a re-render of the component, ensuring that the user interface stays in sync with the data.
- State is typically initialized in the `constructor` of a class-based component or using the `useState` hook in a functional component.
- State allows components to be dynamic and responsive, as they can update their rendering based on changes in the state data.

## Hook

- In React, a hook is a JavaScript function that allows you to "hook" into React features such as state, lifecycle methods, context, and more.
- Hooks are functions that have names starting with "use" (e.g., `useState`, `useEffect`, `useContext`).
- They provide a way to add stateful logic to functional components, which traditionally didn't have access to state or lifecycle methods.
- Hooks must be called unconditionally at the top level of your functional component. They cannot be called conditionally or within nested functions.

## useState

- `useState` is a React hook used for creating and managing stateful components in functional components.
- It takes an initial state value (or a function that returns the initial state) as its argument and returns an array containing two elements:
  - The first element is the current state value, which we can read and use in our component.
  - The second element is a setter function, which we can use to update the state value.
- We typically destructure the array returned by `useState` to assign meaningful variable names to the current state and its corresponding setter function, for example:
  
```javascript
const [number, setNumber] = useState(10);
```

## useReducer

- `useReducer` is a React hook that is an alternative to `useState`, commonly used for managing more complex state in functional components.
- It takes two arguments: a reducer function and an initial state value. It returns an array with two elements:
  - The first element is the current state value.
  - The second element is a dispatch function, which is used to dispatch actions to update the state.

```javascript
const [state, dispatch] = useReducer(reducer, {
  count: 0
});

return (
  <button onClick={() => dispatch({
    type: 'increment',
    num: 1
  })}>Increment</button>
);
```  

- The dispatch function accepts an action object as its argument. The action object typically includes a `type` property, which is used in a switch statement inside the reducer function to determine how to update the state. For example:

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + action.num};
    case 'decrement':
      return {count: state.count - action.num};
    default:
      throw new Error("Unknown action type");
  }
}
```

- The reducer function is responsible for taking the previous state and the action, and it returns the new state based on the action type. It should be designed to be pure and deterministic.
- `useReducer` is especially useful when we have more complex state management needs, involving multiple state values that depend on each other or when state transitions are more intricate.

## Lifting State Up

- "Lifting State Up" is a common design pattern in React where we move the management of shared state from child components to a common ancestor or parent component in the component tree.
- This pattern is used to centralize and manage the state in a single location, making it the source of truth for the shared data.
- The parent component holds the state and passes it down to its child components as **props**, along with the functions to update that state.
- By lifting state up, we ensure that all child components that need access to this state receive it consistently and can interact with it through the provided props.
- This pattern promotes better data flow and simplifies the management of shared data, making our application more predictable and easier to maintain.

"Lifting State Up" is especially valuable when dealing with multiple components that depend on the same data or need to synchronize their behavior based on a shared state. It helps in keeping your application's state management organized and efficient.

## Controlled Component

- A controlled component is a React pattern where we use React state to control and manage the current state of an input element. Fro example, an input can be controlled via the `value` and `onChange` props (note that in React, `onChange` works the same as `onInput`):
  
```javascript
const [value, setValue] = useState("");
return <input value={value} onChange={e => setValue(e.target.value)} />;
```

- In a controlled component, we explicitly set the input element's value using the `value` prop, and we provide an `onChange` event handler to update the state whenever the input value changes.
- This pattern ensures that the React component's state and the input element's value are always in sync, and any changes to the input value are controlled by React.
- Controlled components are useful for maintaining strict control over the input's behavior and value, making it easier to perform validation, synchronization, or other custom logic when the input changes.

## React Component Lifecycle
The React component lifecycle consists of three primary stages:

1. **Mounting:**
   - This stage occurs when a component is being created and inserted into the DOM for the first time.
   - Key lifecycle methods during mounting include:
     - `constructor`: The component's constructor function is called.
     - `render`: The component's UI is rendered.
     - `componentDidMount`: This method is called after the component has been rendered into the DOM. It's often used for performing initial setup, data fetching, or interacting with external libraries.

2. **Updating:**
   - The updating stage occurs when a component is re-rendered due to changes in its state or props.
   - Key lifecycle methods during updating include:
     - `render`: The component's UI is re-rendered to reflect the new state or props.
     - `componentDidUpdate`: This method is called after the component has been updated in the DOM. It's commonly used for side effects or interactions based on the updated data.

3. **Unmounting:**
   - The unmounting stage occurs when a component is removed from the DOM.
   - The primary lifecycle method for unmounting is:
     - `componentWillUnmount`: This method is called just before the component is removed from the DOM. It's typically used for cleanup tasks, such as canceling network requests or removing event listeners.

Understanding the React component lifecycle is essential for managing component behavior, handling side effects, and optimizing performance in your React applications. However, it's worth noting that with the introduction of React Hooks, some of the traditional class-based lifecycle methods, such as `componentDidMount` and `componentDidUpdate`, can be replaced by equivalent functionality using hooks like `useEffect`.

## useEffect

- `useEffect` is a React hook used for managing side effects in functional components. Side effects can include data fetching, DOM manipulation, subscriptions, and more.
- It takes two arguments: a callback function and an optional dependency array.
- If no dependency array is provided, the callback function will run on every render.
- If a dependency array is provided, the callback function will run when the component mounts and whenever any of the dependencies in the array change.
- The dependency array is crucial for ensuring that the effect runs when it should and doesn't run when it shouldn't. It should include all values that the callback function relies on and can change between renders.
- The callback function can return a cleanup function, which will run before the main effect function runs again on unmount and before any re-renders.
- Using `useEffect` allows us to manage side effects in a declarative and controlled way, making it easier to handle asynchronous operations and keep our component's behavior in sync with its rendering.
- Let's explore the `useEffect` hook in React with an example where we'll create a simple React component that fetches data from an API when the component mounts.

```javascript
import React, { useState, useEffect } from 'react';

function MyComponent() {
  // State to store the fetched data
  const [data, setData] = useState(null);

  // useEffect for fetching data when the component mounts
  useEffect(() => {
    // Define the URL of the API
    const apiUrl = 'https://jsonplaceholder.typicode.com/posts/1';

    // Fetch data from the API using the Fetch API
    fetch(apiUrl)
      .then((response) => response.json())
      .then((result) => {
        // Update the data state with the fetched data
        setData(result);
      })
      .catch((error) => {
        console.error('Error fetching data:', error);
      });
  }, []); // Empty dependency array means this effect runs only on mount

  return (
    <div>
      <h1>Fetching Data Example</h1>
      {data ? (
        <div>
          <h2>Title: {data.title}</h2>
          <p>Body: {data.body}</p>
        </div>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
}

export default MyComponent;
```

In this example:

1. We import the `useState` and `useEffect` hooks from React.

2. Inside the `MyComponent` functional component, we declare a `data` state variable using `useState`. This state will be used to store the fetched data.

3. We use the `useEffect` hook to define a side effect. This effect is responsible for fetching data from an API when the component mounts.

4. Inside the `useEffect` callback function:
   - We define the URL of the API we want to fetch data from.
   - We use the `fetch` function to make the API request, parse the response as JSON, and update the `data` state with the fetched data.

5. The empty dependency array `[]` as the second argument to `useEffect` ensures that the effect runs only once when the component mounts. If you were to provide dependencies in the array, the effect would run whenever any of those dependencies change.

6. In the component's render function, we conditionally render the fetched data or a loading message based on the `data` state.

- Consider another example where we'll use the `useEffect` hook to log messages when a state variable called `count` changes and when the component unmounts. The effect will run when the `count` variable changes.

```javascript
useEffect(() => {
  console.log("count changed");

  // Cleanup function (runs when the component unmounts or when `count` changes)
  return () => {
    console.log("cleanup count changed effect");
  };
}, [count]);
```

In this code:

1. We're using the `useEffect` hook to define an effect that should run when the `count` state variable changes. We specify `[count]` as the dependency array, which means the effect runs whenever `count` changes.

2. Inside the effect's callback function, we log the message `"count changed"` whenever the effect is triggered due to a change in the `count` state.

3. Additionally, we return a cleanup function from the `useEffect`. The cleanup function is executed when the component unmounts or when the `count` variable changes.

4. The cleanup function logs the message `"cleanup count changed effect"` to indicate that it's being executed when the effect is cleaned up.

Here's how this code behaves:

- When the component first mounts, the effect is triggered because `count` is considered changed from its initial state (if it started as `undefined` or `null`).

- If `count` changes during the component's lifecycle, the effect runs again and logs `"count changed"` each time.

- When the component unmounts or when `count` changes again, the cleanup function logs `"cleanup count changed effect"`.

## useLayoutEffect

- `useLayoutEffect` is a React hook used for performing side effects around the component lifecycle, similar to `useEffect`.
- The primary difference between `useLayoutEffect` and `useEffect` is that `useLayoutEffect` runs synchronously, whereas `useEffect` runs asynchronously.
- Because `useLayoutEffect` runs synchronously, it ensures that the effects it contains always finish running before the browser repaints the screen. This can be crucial when we need to make visual changes to the DOM that should be reflected immediately.
- It's recommended to use `useLayoutEffect` only for effects that directly manipulate the DOM or require synchronous updates, as it may impact performance negatively if used unnecessarily.
- When we don't need synchronous updates, we can generally prefer `useEffect` because it doesn't block the rendering pipeline and provides better performance for non-visual side effects.

In summary, `useLayoutEffect` is a specialized hook for cases where we need synchronous, immediate updates to the DOM, but it should be used judiciously to avoid unnecessary performance overhead.

## References

- <https://react.dev/>
- <https://react.dev/learn/writing-markup-with-jsx>
- <https://react.dev/reference/react/Fragment>
- <https://react.dev/learn/conditional-rendering>
- <https://react.dev/learn/passing-props-to-a-component>
- <https://react.dev/reference/react-dom/components/common#react-event-object>
- <https://react.dev/learn/state-a-components-memory>
- <https://react.dev/reference/react/useState>
- <https://react.dev/reference/react/useReducer>
- <https://react.dev/reference/react/useEffect>
- <https://react.dev/reference/react/useLayoutEffect>
- <https://react.dev/learn/sharing-state-between-components#lifting-state-up-by-example>
- <https://react.dev/learn/sharing-state-between-components#controlled-and-uncontrolled-components>
- <https://react-tutorial.app/app.html>
- [Create React App](https://github.com/facebook/create-react-app)
