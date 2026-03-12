# Advance Level React and JavaScript Interview Questions

This document contains advanced interview questions suitable for React and JavaScript developers.

## React Questions

1. **Explain the reconciliation process in React.**
   ***Answer:*** The reconciliation process is how React determines what changes need to be applied to the real DOM. It diffs the previous virtual DOM tree against the new one, identifies differences (using element types and keys for lists), and updates only the changed parts, minimizing costly DOM operations.
2. **How does React's Fiber architecture work? Why was it introduced?**

   ***Answer:*** React Fiber re‑architected the reconciliation algorithm into a linked tree of "fibers", each representing a component and its state. Work is broken into small units that can be scheduled, paused, or aborted, enabling interruptible rendering and prioritization. Fiber was introduced to support features like time‑slicing, suspense, and asynchronous rendering, improving responsiveness for complex UIs.
3. **What are hooks and how do they differ from class-based components?**

   ***Answer:*** Hooks are functions such as `useState` and `useEffect` that let you use React state and lifecycle features inside functional components. They eliminate the need for class syntax, avoid `this` binding, and allow logic to be reused across components by creating custom hooks. Hooks lead to simpler, more composable code compared to class‑based components.
4. **Describe useRef and how it can be used to access DOM elements.**

   ***Answer:*** `useRef` returns a mutable ref object whose `.current` property persists across renders. You can attach it to a JSX element via the `ref` prop to hold a reference to a DOM node (`const inputRef = useRef(); <input ref={inputRef} />`). It’s also handy for storing mutable values that don’t trigger re‑renders.
5. **What is the difference between controlled and uncontrolled components?**

   ***Answer:*** Controlled components have their value driven by React state (`value={state}`) and update via `onChange`, giving React full control over the input. Uncontrolled components let the DOM maintain the value, accessed with a ref and `defaultValue` (`<input defaultValue="..." ref={ref} />`). Controlled inputs are easier to validate and synchronize, while uncontrolled ones can reduce boilerplate for simple forms.
6. **How do you implement code splitting and lazy loading in a React application?**

   ***Answer:*** Use dynamic `import()` expressions with `React.lazy()` and wrap the lazy component in `<Suspense fallback={...}>`. For route‑based splitting, frameworks like React Router support lazy components per route. Bundlers such as Webpack automatically create separate chunks for each dynamic import.
7. **Explain context API and when it's appropriate to use versus state management libraries like Redux.**

   ***Answer:*** The Context API (`React.createContext` + `Provider`) lets you pass data deeply through the tree without prop drilling (e.g. theme, locale, auth). It works well for modest amounts of global or cross‑cutting state. For complex state with middleware, debugging tools, or large apps, a dedicated library like Redux or MobX may be more appropriate.
8. **Describe the purpose of React.memo, useMemo, and useCallback and when to use each.**

   ***Answer:*** `React.memo` memoizes a component to skip re‑rendering when props are shallowly equal. `useMemo` caches the result of an expensive computation between renders. `useCallback` memoizes a function reference to prevent child components from receiving new props unnecessarily. Use them as focused performance optimizations when you identify costly renders or stable dependencies.
9. **What are higher-order components (HOCs) and render props? Provide examples.**

   ***Answer:*** A higher‑order component is a function that takes a component and returns an enhanced one, for example `withRouter(Component)` or `withAuth(Component)`. Render props involve passing a function as a child that returns JSX, like `<DataLoader>{data => <Display data={data}/>}</DataLoader>`. Both patterns were used for logic reuse before hooks became mainstream.
10. **How would you optimize a React application's performance?**

   ***Answer:*** Optimize by memoizing components and values, splitting code, lazy loading, virtualizing long lists, reducing unnecessary re‑renders, avoiding inline functions/objects in JSX, and profiling with React DevTools. Keep component trees shallow, batch state updates, and move expensive computations outside render.
11. **Explain server-side rendering (SSR) in React and its benefits/challenges.**

   ***Answer:*** SSR generates HTML on the server by rendering React components, sending a fully formed page to the client. Benefits include faster first‑paint, improved SEO, and a better perceived load time. Challenges include hydration complexity, data fetching on both server and client, extra server resources, and avoiding browser‑only APIs during render.
12. **How do you manage side effects in a React application?**

   ***Answer:*** Use the `useEffect` hook (or lifecycle methods in classes) to run side effects like network requests, subscriptions, or manual DOM updates. Return a cleanup function to avoid leaks. For complex side‑effect logic or caching, consider libraries such as React Query, Redux‑Saga, or custom hooks.
13. **Discuss the use of error boundaries in React.**

   ***Answer:*** Error boundaries are class components that implement `componentDidCatch` and `getDerivedStateFromError` to catch rendering errors in their descendant tree and display a fallback UI. They prevent an entire app from crashing due to uncaught exceptions. They do not catch errors in event handlers, asynchronous code, or during server-side rendering.
14. **Explain Suspense and concurrent features in React 18+.**

   ***Answer:*** Suspense lets components “wait” for asynchronous resources by throwing a promise; you supply a fallback UI while the resource is pending. Concurrent features (like `startTransition`, `useDeferredValue`, and automatic batching) allow React to interrupt and prioritize renders, making UIs more responsive. Together they enable smoother loading states and transitions in React 18+.
15. **Describe how to build a custom hook and share logic between components.**

   ***Answer:*** A custom hook is a function prefixed with `use` that may call other hooks to encapsulate reusable stateful logic. For example:

```js
function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  useEffect(() => {
    const handler = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handler);
    return () => window.removeEventListener('resize', handler);
  }, []);
  return width;
}
```

Then you can call `const width = useWindowWidth();` in multiple components to share behavior.

## JavaScript Questions

1. **Explain the event loop and how asynchronous JavaScript works.**

   ***Answer:*** JavaScript runs on a single thread with an event loop that handles a call stack, a microtask queue (Promises, `queueMicrotask`), and a macrotask queue (timers, I/O, UI events). Synchronous code executes immediately on the stack; asynchronous callbacks are queued and executed when the stack is empty, with microtasks drained before macrotasks.
2. **Describe prototypes and inheritance in JavaScript.**

   ***Answer:*** Every object has an internal `[[Prototype]]` link to another object; property lookups walk this prototype chain. Functions have a `prototype` property used when creating objects with `new`. Inheritance is achieved by setting one object's prototype to another (e.g., `Child.prototype = Object.create(Parent.prototype)`), allowing shared methods.
3. **What are closures and how are they used?**

   ***Answer:*** A closure is a function that retains access to variables from its lexical scope even after the outer function has returned. They are used for data privacy (module pattern), factory functions, callbacks, and maintaining state across async operations.
4. **Explain the difference between var, let, and const.**

   ***Answer:*** `var` is function‑scoped and hoisted (initialized as `undefined`), whereas `let` and `const` are block‑scoped and reside in the Temporal Dead Zone until declaration executes. `const` cannot be reassigned but does not make objects immutable. `let` allows reassignment but still respects block scope.
5. **What is hoisting and how does it affect variable/function declarations?**

   ***Answer:*** Hoisting is JavaScript’s behavior of moving declarations to the top of their scope during compilation. Function declarations are hoisted with their definition, allowing calls before the code appears. Variables declared with `var` are hoisted and initialized to `undefined`; `let`/`const` are hoisted but not initialized, creating a Temporal Dead Zone until the declaration line.
6. **Describe the module systems available in JavaScript (CommonJS, ES Modules, etc.).**

   ***Answer:*** CommonJS (`require/exports`) is used in Node.js and loads modules synchronously. AMD and UMD were earlier browser patterns. ES Modules (`import/export`) are the standardized syntax supported in browsers and Node; they are statically analyzable and support tree shaking. Bundlers handle interop between systems.
7. **Explain the difference between call, apply, and bind.**

   ***Answer:*** `.call(thisArg, arg1, arg2...)` invokes a function with an explicit `this` and individual arguments. `.apply(thisArg, argsArray)` is similar but takes arguments as an array. `.bind(thisArg, ...args)` returns a new function permanently bound to the given `this` and optionally preset arguments.
8. **What are promises and how do async/await work under the hood?**

   ***Answer:*** A promise represents an eventual value or error and has `then`/`catch` handlers queued as microtasks when resolved/rejected. `async` functions return promises; `await` pauses execution in that function until the awaited promise settles, effectively syntactic sugar over chaining `then` callbacks. Under the hood, `await` transforms the code into a generator-like state machine that handles promise resolution.
9. **Discuss event delegation and its benefits.**

   ***Answer:*** Event delegation leverages event bubbling by attaching a single listener to a parent element and handling events for its children via `event.target`. Benefits include fewer listeners, dynamic elements working without reattaching handlers, and reduced memory usage.
10. **How do you handle errors in asynchronous code?**

   ***Answer:*** Use `.catch()` on promises or try/catch inside `async` functions around `await` expressions. For callbacks, follow the Node style (`err` first) and check for errors. In browsers, attach `window.onunhandledrejection` and `window.onerror` for global handling.
11. **What are generators and iterators?**

   ***Answer:*** An iterator is an object with a `next()` method returning `{value, done}`. A generator function (`function*`) returns a generator, which is both iterable and iterator; `yield` pauses execution and returns a value. Generators are useful for lazy sequences and implementing async flows.
12. **Explain the concept of debouncing and throttling.**

   ***Answer:*** Debouncing delays execution until a pause in events (useful for search input). Throttling limits how often a function can run over time (useful for scroll/resize handlers). Both help improve performance by reducing event frequency.
13. **Describe memory leaks in JavaScript and how to prevent them.**

   ***Answer:*** Memory leaks occur when references to unused objects persist (e.g., forgotten timers, detached DOM nodes, global variables). Prevent leaks by nulling references, removing event listeners, clearing intervals/timeouts, and avoiding large closures.
14. **What are Map and Set, and how do they differ from Object and Array?**

   ***Answer:*** `Map` is an ordered key/value store that accepts any value as a key and preserves insertion order. `Set` is a collection of unique values. Unlike plain objects, maps don't coerce keys to strings and have size property; unlike arrays, sets aren't indexed and maps aren't number‑indexed. They offer better performance for certain operations.
15. **Explain the spread/rest operators and destructuring assignment.**

   ***Answer:*** The spread operator (`...`) expands iterable elements in arrays or object properties (`[...arr]`, `{...obj}`). In function parameters, the rest operator collects remaining arguments into an array (`function foo(...args)`). Destructuring lets you unpack values from arrays or objects into variables (`const {a,b} = obj; const [x,y] = arr;`).
16. **Event Loop**
    You have this code:
    ```js
    console.log("A");

    setTimeout(() => console.log("B"), 0);

    Promise.resolve()
    .then(() => console.log("C"))
    .then(() => {
        setTimeout(() => console.log("D"), 0);
    });

    console.log("E");
    ```
    Tell me:
    a. What is the exact output order?

    ***Answer:*** A | E | C | B | D
    
    b. WHY — step-by-step at event loop + microtask/macrotask level

    ***Answer:*** JavaScript executes in this order: (1) All synchronous code first (A, E print). (2) After the call stack is empty, all microtasks execute (Promise.then() callbacks execute—C prints). (3) During the second .then(), a setTimeout is encountered and pushed to the macrotask queue. (4) After all microtasks complete, macrotasks execute in FIFO order (B prints, then D prints).
    
    c. Where do .then() callbacks go?

    ***Answer:*** Microtask queue
    
    d. When does the second setTimeout get scheduled?
    
    ***Answer:*** The second setTimeout gets scheduled during the second .then() callback execution (which is part of the microtask phase). It's queued in the macrotask queue after the first setTimeout, so it executes after B completes.
    
    e. How could this knowledge impact real UI performance in React apps?

    ***Answer:*** React batches state updates using microtasks. Understanding the event loop helps you predict when renders occur—state updates queued in the same microtask phase batch together and trigger one render. Knowing that microtasks have priority over macrotasks (like setTimeout) means certain race conditions can be avoided. Also, accessing refs immediately reflects changes, but state updates are asynchronous, which is crucial for optimization strategies like useCallback and useMemo dependencies.

17. **Closures + Memory**
    
    You have this code
    ```js
    function createCounter() {
        let count = 0;
        return function() {
            count++;
            return count;
        };
    }

    const counter = createCounter();
    ```
    Tell me

    a. Where is `count` stored in memory?
    ***Answer:*** `count` is stored in the closure scope (the lexical environment of `createCounter`). It persists in memory as long as the returned function exists and maintains a reference to it.

    b. Why is it not garbage collected?
    ***Answer:*** The inner function holds a reference to `count` through its closure. As long as the `counter` function exists and isn't dereferenced, JavaScript's garbage collector cannot reclaim the `count` variable because it's still reachable from live code.

    c. How can closures cause memory leaks in large frontend apps?
    ***Answer:*** Closures can leak memory when they unintentionally capture large objects or DOM references. For example, if a callback captures an entire component state object but only uses one property, the entire object stays in memory. In event listeners or timers that aren't cleaned up, closures keep referencing older component instances, preventing garbage collection and accumulating memory over time.

    d. Give a real React example where this becomes a production issue.
    ***Answer:*** In a modal component with a `setInterval` inside `useEffect`, if you don't clean up the interval, the closure continues to capture the component's state. Each re-render creates a new closure capturing new state, but old closures are never released, leading to stale-closure bugs and memory leaks. Example:
    ```js
    useEffect(() => {
        const interval = setInterval(() => {
            console.log(data); // captures data in closure
        }, 1000);
        // Missing: return () => clearInterval(interval);
    }, [data]); // missing dependency also causes issues
    ```
    The interval holds old references to `data`, and without cleanup, multiple intervals stack up.

18. **`var` vs `let` vs `const` Explain in terms of: Memory model, Temporal Dead Zone**

    ***Answer:*** All three declarations create bindings, not raw memory blocks; the runtime allocates storage when the scope is entered. `var` bindings are hoisted and initialized to `undefined` at the start of their function scope, so you can read them before the line of declaration (hoisting). `let` and `const` are also hoisted but remain uninitialized in the **Temporal Dead Zone (TDZ)** until the execution reaches their declaration, causing a ReferenceError if accessed earlier. `let` allows reassignment within its block scope, while `const` forbids reassigning the binding.

    a. Real production bug that can happen because of `var`

    ***Answer:*** Because `var` is function‑scoped, a loop index leaks outside the loop and may collide with other code. In long‑running scripts or modules this can cause unexpected state or memory retention:
    ```js
    for (var i = 0; i < 3; i++) {
        // ...
    }
    // `i` still exists here with value 3, possibly overwriting another variable
    ```
    A more subtle production issue is accidentally overwriting a variable in an outer scope or keeping a reference alive longer than intended, leading to memory leaks.

    b. Why `const` does NOT make objects immutable

    ***Answer:*** `const` prevents reassignment of the binding, but the object it references remains mutable. Properties can be added, changed, or deleted. To make an object immutable you must use helpers like `Object.freeze()` (shallow) or libraries for deep immutability.

19. What will this log and why?
    ```js
    const obj = {
        name: "Bikram",
        greet() {
            console.log(this.name);
        }
    };

    const greetFn = obj.greet;
    greetFn();
    ```
    ***Answer:*** `undefined` — calling `greetFn` as a standalone function means `this` is not bound to `obj` (it becomes the global object in sloppy mode, so `this.name` is undefined).

    How would this behave differently in:

    a. Browser (non‑strict)
    ***Answer:*** still logs `undefined` for the same reason (global `this` has no `name` property).

    b. Strict mode

    ***Answer:*** `this` will be `undefined`; accessing `this.name` throws a **TypeError** (`Cannot read property 'name' of undefined`).

    c. Arrow‑function version

    ***Answer:*** The arrow version would not use `obj` as `this` at all — arrow functions grab `this` lexically from their surrounding scope. For example,
    ```js
    const obj = {
      name: 'Bikram',
      greet: () => console.log(this.name)
    };
    obj.greet();
    ```
    here `this` refers to whatever `this` was when the object literal was evaluated (usually the global object or `undefined` in a module), so it will not reliably log `'Bikram'`. In short, arrow functions don’t bind `this` to the object.

20. **Shallow vs Deep Copy**
    ```js
    const a = { user: { name: "Sam" } };
    const b = { ...a };
    b.user.name = "Alex";
    ```
    a. Why did this happen?

    ***Answer:*** The object spread (`{ ...a }`) creates a *shallow copy* of `a`. The top‑level property `user` is copied by reference, so both `a.user` and `b.user` point to the same nested object. Modifying `b.user.name` thus mutates the original.

    b. How would you deep copy safely in a React app?

    ***Answer:*** Use a utility that recursively clones all nested values, e.g. `lodash`’s `cloneDeep`, `structuredClone()` in modern environments, or write a custom recursive function. In React, avoid mutating props/state directly; create new objects when updating nested data or use immutable libraries (Immer) so updates produce deep copies automatically.

    c. Why is `JSON.parse(JSON.stringify())` dangerous?

    ***Answer:*** That approach only works for JSON‑serializable data. It drops functions, `undefined`, `Symbol`s, and prototype information, and may fail on circular references, leading to errors or data loss. It’s brittle and unsuitable when objects contain Date, Map/Set, or custom classes.