

Hooks Let you use different react features from your components. You can either use built in hooks or combine them to build your own. These are all the hooks


https://react.dev/reference/react/hooks


## State Hooks

State lets a component remember information like user input. For example a form component can use state to store the input value while and image gallery component can use state to store the selected image index.

To add state to a component use one of these hooks:

useState Declares a state variable that you can update

useReducer declares a state variable with the updated logic inside a reducer function.

```
function ImageGallery(){
	const[index, setIndex] = useState(0);
}
```



## Context Hooks

Context lets a component receive information from distant parents without passing it as props. For example your apps top-level component can pass the current UI theme to all components below no matter how deep.

useContext Reader and subscribes to a context.

```
function Button(){
	const theme = useContext(ThemeContext)
}
```



## Ref Hooks


Refs let a component hold some information that isnt used for rendering like a DOM node or a timeout ID. Unlike with state, updating a ref does not re-render your component. Refs are an "escape hatch" from the React paradigm. They are useful when working with non-react systems like a browser API.

- [`useRef`](https://react.dev/reference/react/useRef) declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.
- [`useImperativeHandle`](https://react.dev/reference/react/useImperativeHandle) lets you customize the ref exposed by your component. This is rarely used.

```
function Form() {  
const inputRef = useRef(null);  
}

```



## Effect Hooks[](https://react.dev/reference/react/hooks#effect-hooks "Link for Effect Hooks")

_Effects_ let a component [connect to and synchronize with external systems.](https://react.dev/learn/synchronizing-with-effects) This includes dealing with network, browser DOM, animations, widgets written using a different UI library, and other non-React code.

- [`useEffect`](https://react.dev/reference/react/useEffect) connects a component to an external system.

```
function ChatRoom({roomId}){
	useEffect(() => {
	const connection = createConnection(roomId);
	connection.connect();
	return () => connection.disconnect();
	}, [roomId]);
}
```


return () => if true

Effects are an “escape hatch” from the React paradigm. Don’t use Effects to orchestrate the data flow of your application. If you’re not interacting with an external system, [you might not need an Effect.](https://react.dev/learn/you-might-not-need-an-effect)

There are two rarely used variations of `useEffect` with differences in timing:

- [`useLayoutEffect`](https://react.dev/reference/react/useLayoutEffect) fires before the browser repaints the screen. You can measure layout here.
- [`useInsertionEffect`](https://react.dev/reference/react/useInsertionEffect) fires before React makes changes to the DOM. Libraries can insert dynamic CSS here.

## Performance Hooks[](https://react.dev/reference/react/hooks#performance-hooks "Link for Performance Hooks")

A common way to optimize re-rendering performance is to skip unnecessary work. For example, you can tell React to reuse a cached calculation or to skip a re-render if the data has not changed since the previous render.

To skip calculations and unnecessary re-rendering, use one of these Hooks:

- [`useMemo`](https://react.dev/reference/react/useMemo) lets you cache the result of an expensive calculation.
- [`useCallback`](https://react.dev/reference/react/useCallback) lets you cache a function definition before passing it down to an optimized component.

```
function TodoList({ todos, tab, theme }) {  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);  // ...}
```

Sometimes, you can’t skip re-rendering because the screen actually needs to update. In that case, you can improve performance by separating blocking updates that must be synchronous (like typing into an input) from non-blocking updates which don’t need to block the user interface (like updating a chart).

To prioritize rendering, use one of these Hooks:

- [`useTransition`](https://react.dev/reference/react/useTransition) lets you mark a state transition as non-blocking and allow other updates to interrupt it.
- [`useDeferredValue`](https://react.dev/reference/react/useDeferredValue) lets you defer updating a non-critical part of the UI and let other parts update first.

---

## Other Hooks[](https://react.dev/reference/react/hooks#other-hooks "Link for Other Hooks")

These Hooks are mostly useful to library authors and aren’t commonly used in the application code.

- [`useDebugValue`](https://react.dev/reference/react/useDebugValue) lets you customize the label React DevTools displays for your custom Hook.
- [`useId`](https://react.dev/reference/react/useId) lets a component associate a unique ID with itself. Typically used with accessibility APIs.
- [`useSyncExternalStore`](https://react.dev/reference/react/useSyncExternalStore) lets a component subscribe to an external store.

- [`useActionState`](https://react.dev/reference/react/useActionState) allows you to manage state of actions.

---

## Performance Hooks[](https://react.dev/reference/react/hooks#performance-hooks "Link for Performance Hooks")

A common way to optimize re-rendering performance is to skip unnecessary work. For example, you can tell React to reuse a cached calculation or to skip a re-render if the data has not changed since the previous render.

To skip calculations and unnecessary re-rendering, use one of these Hooks:

- [`useMemo`](https://react.dev/reference/react/useMemo) lets you cache the result of an expensive calculation.
- [`useCallback`](https://react.dev/reference/react/useCallback) lets you cache a function definition before passing it down to an optimized component.

```
function TodoList({ todos, tab, theme }) {  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);  // ...}
```

Sometimes, you can’t skip re-rendering because the screen actually needs to update. In that case, you can improve performance by separating blocking updates that must be synchronous (like typing into an input) from non-blocking updates which don’t need to block the user interface (like updating a chart).

To prioritize rendering, use one of these Hooks:

- [`useTransition`](https://react.dev/reference/react/useTransition) lets you mark a state transition as non-blocking and allow other updates to interrupt it.
- [`useDeferredValue`](https://react.dev/reference/react/useDeferredValue) lets you defer updating a non-critical part of the UI and let other parts update first.

---

## Other Hooks[](https://react.dev/reference/react/hooks#other-hooks "Link for Other Hooks")

These Hooks are mostly useful to library authors and aren’t commonly used in the application code.

- [`useDebugValue`](https://react.dev/reference/react/useDebugValue) lets you customize the label React DevTools displays for your custom Hook.
- [`useId`](https://react.dev/reference/react/useId) lets a component associate a unique ID with itself. Typically used with accessibility APIs.
- [`useSyncExternalStore`](https://react.dev/reference/react/useSyncExternalStore) lets a component subscribe to an external store.

- [`useActionState`](https://react.dev/reference/react/useActionState) allows you to manage state of actions.

---



