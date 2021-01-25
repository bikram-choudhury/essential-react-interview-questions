# Essential React interview questions
---
It's a book about React and JavaScript interview question. We hope that it will help all javascript developers to prepare for a technical job interview.


1 . [HTML5](#html5)

2 . [CSS](#css)

3 . [JavaScript](#javascript)

4 . [React](#react)

## HTML5

---

### 1. Request Lifecycle

- Browser translate the hostname to get the ip address with the help of DNS server.
- Browser will open the TCP connections to the ip address.
- Then send a HTTP request with the given method (i.e: GET req).
- When Server software will get the HTTP request, then it will process the request and generate the response.
- Once browser recieves the response, TCP connection will get closed.
- Then browser parses the HTML from the response.
- A DOM tree is built out of the parsed HTML and new requests are made to the server for each new resources i.e: images, stylesheets, JS files.
- Stylesheets are parsed and renders each resources.
- JavaScript files are parsed and executed.

### 2. Semantic HTML

- A semantic HTML clearly describes its meaning to both browser and the developer.
- These are also useful for SEO

### 3. Canvas

- It is a container that is used to draw graphics on the fly with scripting.

```javascript
const canvasEl = document.getElementById('element');
const context = canvasEl.getContext('2d');

context.fillStyle = 'red';
context.fillRect(x-axis position, y-axis position, width, height);

context.strokeStyle = 'green';
context.beginPath();
// context.moveTo(x-axis position, y-axis position);
context.moveTo(270, 50);
context.lineTo(370, 50);
context.lineTo(370, 100);
context.closePath();
context.stroke();
```

### 4. Responsive approach for images

```html
<!-- with sizes -->
<img
  srcset="elva-fairy-480w.jpg 480w, elva-fairy-800w.jpg 800w"
  sizes="(max-width: 600px) 480px,800px"
  src="elva-fairy-800w.jpg"
  alt="Elva dressed as a fairy"
/>
<!-- without sizes -->
<img
  srcset="elva-fairy-320w.jpg, elva-fairy-480w.jpg 1.5x, elva-fairy-640w.jpg 2x"
  src="elva-fairy-640w.jpg"
  alt="Elva dressed as a fairy"
/>
<!-- Art direction -->
<picture>
  <source media="(min-width:650px)" srcset="img_pink_flowers.jpg" />
  <source media="(min-width:465px)" srcset="img_white_flower.jpg" />
  <img src="img_orange_flowers.jpg" alt="Flowers" style="width:auto;" />
</picture>
```

### 5. Fallback in HTML5

```html
<video autoplay>
  <source
    src="/resources/video/product-hero.mp4.mp4"
    type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'
  />
  <source
    src="/resources/video/product-hero.webmhd.webm"
    type='video/webm; codecs="vp8, vorbis"'
  />
  <img
    src="/images/product/product-parent-hero.jpg"
    title="Your browser does not support the <video> tag"
  />
</video>

<progress max="100" value="20">
  <div class="progress-bar">
    <span style="width: 20%;">Progress: 20%</span>
  </div>
</progress>
```

### 6. Web Worker

- A web worker is a JavaScript running in the background, without affecting the performance of the page.

```javascript
var w;

function startWorker() {
  if (typeof Worker !== "undefined") {
    if (typeof w == "undefined") {
      w = new Worker("demo-worker.js");
    }
    w.onmessage = function (event) {
      document.getElementById("result").innerHTML = event.data;
    };
  } else {
    document.getElementById("result").innerHTML =
      "Sorry! No Web Worker support.";
  }
}
function stopWorker() {
  w.terminate();
  w = undefined;
}
startWorker();
```

```javascript
// demo-worker.js
var i = 0;
function timeCount() {
  ++i;
  postMessage(i);
  setTimeout("timeCount()", 500);
}
timeCount();
```

### 7. GeoLocation

- Get user's geo location on user's approval.

```javascript
function getLocation() {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition((position) => {
      console.log(position.coords.latitude, position.coords.longitude);
    }, showError);
  } else {
    return "Geolocation is not supported by this browser.";
  }
}

function watchLocation() {
  if (navigator.geolocation) {
    navigator.geolocation.watchPosition((position) => {
      console.log(position.coords.latitude, position.coords.longitude);
    }, showError);
    // navigator.geolocation.clearWatch();
  } else {
    return "Geolocation is not supported by this browser.";
  }
}

function showError(error) {
  switch (error.code) {
    case error.PERMISSION_DENIED:
      return "User denied the request for Geolocation.";
      break;
    case error.POSITION_UNAVAILABLE:
      return "Location information is not available";
      break;
    case error.TIMEOUT:
      return "The request to get user location timed out.";
      break;
    case error.UNKNOWN_ERROR:
      return "An unknown error occurred.";
      break;
  }
}
```

### 8. SEO compatible markups

- We should use semantic tags
- Special HTML tags should be used while developing semantic links between different documents.
- The most important content of the page must be placed in the beginning of the page
- HTML5 tags helps to make indexing fast and reliable because HTML5 tags are well known by the BOTs.

## CSS

---

### 1. Shorthand properties in css

- **margin**, **padding**, **border-width**, **border-radius**: top right bottom left
- **background**: color image repeat position
- **font**: style weight size/line-height family
- **border**: width style color

### 2. PreProcessors of CSS

- SCSS, LESS, Stylus

### 3. Specificity

- inline id class tag

### 4. Cascade

- Apply the last style

### 5. Layout styling approach

- **Flexbox Model:** One-dimensional layout method for laying out items in rows or columns. Items flex to fill additional space and shrink to fit into smaller spaces.

## Javascript

---

### 1. How JavaScript Works ?

#### Answer

- JS is synchronous single threaded programming language
- JS enginee run the code in the execution context
  - #### Execution context
    - memory / variable Environment - All variables will initialized with undefined in key:value pair
    - code/Thread of excution
- While running the programe for each function block a new execution context will get create and get pushed into the call stack. Once the programe completes it will popout from stack give the control to global execution context.

### 2. What is JavaScript enginee and how it works ?

### 3. What is Scope of a function ?

#### Answer

- Scope is defined as (local memory space + parent's lexical environment)

### 4. What is Block ?

#### Answer

- Block is defined as a compound statement or group of statements and it is annotade with {}.
- #### Why is compound statement required ?
  - It is used where JS requires multiple statements as a single statement.

### 5. What is Closure ?

#### Answer

- It's a function that bind with or along with it's lexical scope
- Usages:
  - Module design pattern
  - Currying
  - Functions like once
  - memoize
  - maintaining state in async world
  - setTimeout
  - Iterators

### 6. What is callbacks ?

#### Answer

- All First class citizens/functions those are passed as arguments to another function is called callbacks.
- Because of callbacks we can achieve async tasks

### 7. What can go into theses microtask queues ?

#### Answer

- Promises & MutationObservers (keeps on checking weather there is any mutation in the DOM tree or not, if there is any mutation in DOM tree then it can run some callbacks)

### 8. What is Currying ?

#### Answer

- Currying in JS is an advanced technique of working with functions and transforms those.
- It can be achieved in 2 ways.
  ```javascript
  <!-- code with bind -->
  function sum(a, b) {
    console.log(a + b);
  }
  const sumBy2 = sum.bind(null, 2);
  sumBy2(3);
  ```
  ```javascript
  <!-- code with closure -->
  function sum(a) {
    return function(b) {
        console.log(a + b);
    }
  }
  const sumBy2 = sum(2);
  sumBy2(3);
  ```

### 9. Write a polyfill for bind method.

#### Answer

```javascript
Function.prototype.myBind = function (context, ...args) {
  const _this = this;
  return function (...params) {
    _this.apply(context, args.concat(params));
  };
};
```

### 10. What is debouncing ?

#### Answer

- It is generally used for performance optimization or limit the rate of function calls
- On triggered it will execute the provided function after a specific delay.

```javascript
let count = 0;
const debounce = (fn, delay) => {
  let timer;
  return () => {
    const context = this,
      args = arguments;
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(context, args);
    }, delay);
  };
};
const onKeyUp = (event) => {
  console.log(
    `Do API call or do something with value = ${element.value}`,
    ++dCount
  );
};
const handleKeyUp = debounce(onKeyUp, 300);
```

### 11. What is throtlling ?

#### Answer

- It is generally used for performance optimization or limit the rate of function calls
- On triggered it will execute the provided function on immidiate basis and later the function will execute for a interval of time.

```javascript
let count = 0;
const throtlling = (fn, delay) => {
  let flag = true;
  return () => {
    const context = this,
      args = arguments;
    if (flag) {
      fn.apply(context, args);
      flag = false;
      setTimeout(() => {
        flag = true;
      }, delay);
    }
  };
};
const onClick = (event) => {
  console.log(`Do some API call`, ++tCount);
};
const handleClick = throttle(onClick, 300);
```

### 12. What is async & defer attributes in script tag ?

##### Answer from [YouTube](https://youtu.be/IrHmpdORLu8)

#### Answer

- These are the boolean attributes used along with script tag to load external scripts efficiantly into our web page.
- There are 2 parts in webpage loading
  1. HTML parsing
  2. Loading of the scripts
     - Fetching the script from server + executing the script in the browser line by line
- **async**: Fetch script files in parallel with HTML parsing -> pause HTML parsing + script executed -> complete HTML parsing
- **defer**: Fetch script files in parallel with HTML parsing -> complete HTML parsing -> Execute the script

### 13. What is Event bubbling & Event capturing ?

#### Answer

- **Bubbling**: bubble up the event
- **Capture**: tricklle down the event
- **addEventListener** has 3rd argument as useCapture.
  - If (useCapture == true) capture event (or) event excution starts from parent down to child
  - if (useCapture == false) bubbling event (or) event excution starts from child upto parent

### 14. What is Event Delegation ?

#### Answer

- It is a technique to handle the events in a better way. It is possible only because of Event Bubbling.
- In this we should attach an event at parent instead of child. If we add event listner at child then multiple handlers will be hanging out there, but if we will add the handler at parent then only one handler will be available instead of all.

### 15. What is Prototype ?

### 16. What is Starvation in callback queue ?

## React

---

### 1. What is ReactJs ?

#### Answer

- It is an open source client side JavaScript library which is used for building user interfaces especially for SPA.
- This is developed & maintained by Facebook on 2013.

### 2. Advantages ?

#### Answer

- With the help of **Virtual DOM**, it provides High performance w.r.t DOM manipulation / updation.
- Easy to integrate with 3rd party libraries i.e: Meteor, Node
- Can be used at both **client** & **server** side.
- Easy to write UI testcases.
- High Readability.

### 3. Disadvantages ?

#### Answer

- Not a full scale framework. i.e: It's just a view
- Library is quite large. If we includes redux library, then it is very huge.
- Uses inline JSX for templating.
- Difficult to learn for nvoice programmers.

### 4. What is JSX ?

#### Answer

- JavaScript XML / JavaScript Extension.
- It is the combination of JavaScript & HTML.
- It is very Robust & boost up JS performance.

### 5. What is Virtual DOM ? And Explain it's working

#### Answer

- It is a light weight JavaScript object which is a copy of Real DOM.
- It works in 3 simple steps. i.e:
  1. When any updation occurs in the client, then the entire UI is re-render in Virtual DOM.
  2. Then the difference between Previous DOM & Virtual DOM is calculated.
  3. Once the calculation are done, the Real DOM will be updated with only the things that have changed.

### 6. Virtual DOM vs Real DOM ?

| **Virtual DOM**                      | **Real DOM**                              |
| ------------------------------------ | ----------------------------------------- |
| Updates faster                       | Update slow                               |
| Can't update HTML directly           | Can update HTML directly                  |
| Updates if JSX element renders       | Creates a new DOM, if any element updates |
| DOM manipulation is not an expensive | DOM manipulation is very expensive        |
| No Memory wastage                    | High memory wastage                       |

### 7. React vs Angular ?

| **Cases**    | **React**                                       | **Angular**                                                                          |
| ------------ | ----------------------------------------------- | ------------------------------------------------------------------------------------ |
| Architecture | View                                            | MVC                                                                                  |
| DOM          | Virtual DOM                                     | Real DOM                                                                             |
| Data binding | One way (Data passes only from parent to child) | Two way (Both @Input & @Output / Data passes from parent to child & child to parent) |
| Debugging    | Compile time                                    | Run time                                                                             |
| Rendering    | CSR & SSR                                       | CSR                                                                                  |
| Author       | Facebook                                        | Google                                                                               |

### 8. what is render() ?

#### Answer

- It is a pure function.
- Every component shoul have this method, that returns a single React element which is the representation of native DOM component.

### 9. what is props ?

#### Answer

- Short form of properties
- These are immutable / Read-Only / Pure
- Always passed down from parent to child
- Use to render the dynamic data

### 10. what is state ?

#### Answer

- Basis of the components.
- Immutable, but can be update using this.setState()
- Using state, dynamic & interactive elements can be created.

### 11. What is strict mode ?

#### Answer

- It is an usefull component for highlighting potential problems by doing some additional checks in an application.
- Like `<Fragment>`, `<StrictMode>` is also doesn't render any element in the DOM.
- Additional checks:
  1. Indentifies Unsafe component life-cycles
  2. Warns about deprecated functionalites like: String Refs, findDOMNode
  3. Detects unexpected side-effects

### 12. What is Atomic Design Pattern in React ?

#### Answer

- Atoms -> Molecules -> Organisms -> Templates -> Pages
- Atoms: Basic building blocks like: Input, Buttons, form labels etc.
- Molecules: Grouping atoms together, such as combining a button, input and form label to build functionality.
- Organisms: Grouping Molecules together to create an interfaces.
- Templates: Grouping Organisms together to create a sections of a Page.
- Pages: Grouping templates together create a Page.

### 13. Caching / Offline loading in React

### 14. Server Side Rendering

#### Answer from [YouTube](https://www.youtube.com/watch?v=82tZAPMHfT4)

#### What ?

- It is a process of taking a client side JS framework and rendering to static HTML, CSS & JS on the server.

#### Why ?

- Renders the website faster and also provides benefits in SEO

#### Why do we need SSR ?
- Some type of websites need complex features that rely heavily on JS. These kind of websites use JS frameworks like Angular, React, Preact, vueJS. But there is a kind of inherent problem when it comes to these frameworks. They tie up your rendering code in JS and on poor network this can be a problem for your first render. 
- So we can solve this problems with server side rendering. Because in SSR we can generate HTML on the server and send that down to browser. So the user will see the HTML version of your app immediately as the JS app boots up in the background.

#### What are the problems of SSR ?
- There is time & effort associated with server to generate these documents. 
- So if it takes a while to generate these documents then it will not give you fast page load. To solve this problem we can cache our content at the server side using CDN, so for the next user server will not generate the documents again but sends the documents from cache.

#### How browser renders a page ?
- Browser recieves index.html. Then it download it's corresponding css files. When browser recieves all it's css files then it starts rendering. Then it doenload JS files for excution.

#### How SSR works in react ?
- React is a really great fit for SSR because of it's Virtual DOM concepts. And Virtual DOM is like the DOM in the browser but in a virtual way. That means it can go anywhere like: on the server. 
- Which means we can take our own react app and creates a virtual version of it on the server and then render it out to a string, which is just a HTML, send that down to browser. And browser will render that pretty fast.
- Then it will creates a virtual version of the app on the client side and check if the client's virtual DOM is same as the server's HTML string. If it is same then it will not rerender.
