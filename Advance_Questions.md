# Advance Level React and JavaScript Interview Questions

This document contains advanced interview questions suitable for React and JavaScript developers.

## React Questions

1. **Explain the reconciliation process in React.**
   ***Answer:*** The reconciliation process is how React determines what changes need to be applied to the real DOM. It diffs the previous virtual DOM tree against the new one, identifies differences (using element types and keys for lists), and updates only the changed parts, minimizing costly DOM operations.
2. **How does React's Fiber architecture work? Why was it introduced?**
3. **What are hooks and how do they differ from class-based components?**
4. **Describe useRef and how it can be used to access DOM elements.**
5. **What is the difference between controlled and uncontrolled components?**
6. **How do you implement code splitting and lazy loading in a React application?**
7. **Explain context API and when it's appropriate to use versus state management libraries like Redux.**
8. **Describe the purpose of React.memo, useMemo, and useCallback and when to use each.**
9. **What are higher-order components (HOCs) and render props? Provide examples.**
10. **How would you optimize a React application's performance?**
11. **Explain server-side rendering (SSR) in React and its benefits/challenges.**
12. **How do you manage side effects in a React application?**
13. **Discuss the use of error boundaries in React.**
14. **Explain Suspense and concurrent features in React 18+.**
15. **Describe how to build a custom hook and share logic between components.**

## JavaScript Questions

1. **Explain the event loop and how asynchronous JavaScript works.**
2. **Describe prototypes and inheritance in JavaScript.**
3. **What are closures and how are they used?**
4. **Explain the difference between var, let, and const.**
5. **What is hoisting and how does it affect variable/function declarations?**
6. **Describe the module systems available in JavaScript (CommonJS, ES Modules, etc.).**
7. **Explain the difference between call, apply, and bind.**
8. **What are promises and how do async/await work under the hood?**
9. **Discuss event delegation and its benefits.**
10. **How do you handle errors in asynchronous code?**
11. **What are generators and iterators?**
12. **Explain the concept of debouncing and throttling.**
13. **Describe memory leaks in JavaScript and how to prevent them.**
14. **What are Map and Set, and how do they differ from Object and Array?**
15. **Explain the spread/rest operators and destructuring assignment.**
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