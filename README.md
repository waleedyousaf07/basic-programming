# basic-programming

## Introduction:

JavaScript, DSA, OOP, Databases, and Networking Cheatsheet 🚀📚

My secret weapon for leveling up in Core JavaScript, Data Structures and Algorithms (DSA), Object-Oriented Programming (OOP), Databases, and Networking (loading :p). 

Packed with bite-sized knowledge nuggets and playful explanations. Whether I'm conquering new coding realms or need a speedy refresher before an interview, this is my go-to guide! 🎮⚔️

<br><hr><br>

## Core JS

JavaScript is a lightweight, interpreted, object-oriented language with first-class functions, and is best known as the scripting language for Web pages, but it's used in many non-browser environments as well.

EcmaScript uses `just in time` compiler.

### JS to Machine Code

JS file enters the engine (`V8`). The parser does `lexical analysis (tokennizer)` which breaks the code into tokens to indentify their meaning. These tokens makes `Abstract Syntax Tree` which validates the correct use of language keywords and elements. Later on `ASTs` are used to generate actual machine code.

JS is interpreted by `Ignition` and compiled by JIT compiler i.e. `TurboFan`.

Initially, the ASTs generated in the previous step are given to the interpreter which generates `non-optimized machine code` quickly and the `execution can start with no delay`.

`Profiler watches` the code as it runs and `identifies areas` where `optimizations can be performed`. For example, a ‘for’ loop running 100 times but producing the same result in each iteration.

Using this profiler, `any unoptimized code` is `passed to the compiler` to perform optimizations and generate machine code which `eventually replaces its counterpart` in the previously generated non-optimized code by the interpreter.

As the `profiler and compiler constantly make changes` to the bytecode, the JavaScript execution `performance gradually improves`.

### Interpreter

In interpreter, the source code is read line by line.
It neither links the files nor generates machine code.

- Translates one statement at a time into machine code. 
- Takes very less time to analyze the source code. However, the overall time to execute the process is much slower.
- Does not generate an intermediary code. Hence, an highly efficient in terms of memory. 
- Keeps translating the program continuously till the first error is confronted. If any error is spotted, it stops working and hence debugging becomes easy. 
- Interpreters are used by programming languages like Ruby and Python for example. 

### Compiler

In compiled, the source file typically will be “compiled” to machine code (or byte code) before being executed.
Compiler will first analyze all the code, if something is worng, it thorws an error. If no errors are spotted, it converts into machine code.

- Scans the entire program and translates whole into machine code at once.
- Takes a lot of time to analyze the source code. However, the overall time taken to execute the process is much faster.
- A compiler always generates an intermediary object code. It will need further linking. Hence more memory is needed. 
- A compiler generates the error message only after it scans the complete program and hence debugging is relatively harder while working with a compiler. 
- Compliers are used by programming languages like C and C++ for example.

JS does just in time compilation. There is no clear distinction that JS is a compiled or interpreted language. 

### Transpiler

Transpiler is a type of translator that takes the source code of a program written in a programming language as its input and produces an equivalent source code in the same or a different programming language

### Transpiler vs Compiler

The difference between transpiler and compiler is in the level of abstraction in the output. Generally, a compiler produces machine executable code, whereas transpiler produces another developer artifact

### Treeshaking

Its an `optimization` technique to `remove unused code`. Improves:

- Interpreter execution time
- Downloading time of code onto the browser

A tree shaking utility analyzes your code before running it, to detect code that was never used and remove it prior to execution.

`ASTs` are used and even extra `whitespaces` are removed.

Tools like `webpack` automatically performs `treeshaking` but to ensure, in your `webpack.config.js` or `vue.config.js` (if you're using Vue CLI), ensure that the mode is set to "production". This enables various optimizations, including tree shaking.

Vue 3 supports component-level tree shaking. This means that if you're using the Composition API and splitting your components into smaller functions, unused code from those functions can be eliminated during the build process.

Make use of ES6 import and export statements. This helps tree shaking identify which parts of your code are used and which are not. Tree shaking is most effective when you're using modular code and only importing what you need. If you import entire libraries or large chunks of code, tree shaking might not work as effectively.

For minification, the `productionSourceMap` option disables source maps in the production build, which is often recommended to reduce the size of the build artifacts.

### Isomorphic JS

Same JS will/can run on a Client or Browser just as it works on the server. The code should be such or have cases that both the browser and server can understand and read

### Sprites

They are used to load alot of images in a web page together by making single(maybe few) http requests resulting in less time to load the page

### JS Variable declartors

let, const, var

### Var

Var declarations are globally scoped or function/locally scoped. They can be re-declared and updated. They are hoisted and can be used if declared after getting called.

### Const

Cannot be reinialized. Has a block level scope. Primitive types cannot be updated/re-assigned/re-declared but objects and arrays can. Every const declaration, therefore, must be initialized at the time of declaration.

Const create a variable name binding so that name cannot be re-inialized but the properties can. So its mutable. They are hoisted differently than `var`. 

### Let

Can be re initialized. Has a block level scope. It cannot be redeclared withing its scope. They are hoisted differently than `var`

### Var, Let, Const Scopes

    var a = 5;
    const b = 10;
    let c = 15;

    function foo() {
      a = 51;
      const b = 101;
      let c = 151;
      console.log('inside foo: ', a, b, c);
    }

    console.log('Before foo: ', a, b, c); // 5 10 15
    foo(); // 51 101 151
    console.log('After foo: ', a, b, c); // 51 10 15

Following is only true for `var`

    for (var i = 0; i < 5; i++) {
      console.log('i is: ', i);
    };

    const bool = true;
    if (bool) {
      let blockLevelVar = 'Heyy';
    }

    console.log('i outside is: ', i, blockLevelVar); // i outside is: 5 Heyy

### Primitive Types

They are simple and atomic. They are stored as values in memory.

- number
- string
- boolean
- undefined
- null
- symbol

    They are introduced in ECMAScript 2015. Once you create a symbol, its value is kept `private and for internal use`. All that remains after the creation is the `symbol reference`.

        const mySymbol = Symbol();

    Every time you invoke Symbol() we get a new and unique symbol, guaranteed to be different from all other symbols

        Symbol() === Symbol() //false

    You can pass a parameter to Symbol(), and that is used as the symbol description, useful just for debugging purposes

        console.log(Symbol()) //Symbol()
        console.log(Symbol('Some Test')) //Symbol(Some Test)
    
    Symbols are often used to identify object properties

        const NAME = Symbol()
        const person = {
          [NAME]: 'Ema'
        }

        person[NAME] //'Ema'

        const RUN = Symbol()
        person[RUN] = () => 'Ema is running'
        console.log(person[RUN]()) //'Ema is running'

    Symbols are `not enumerated`, which means that they do `not get included in a for..of or for..in loop` ran upon an object.

    Symbols are `not` part of the `Object.keys()` or `Object.getOwnPropertyNames()` result.

    You can access all the symbols assigned to an object using the `Object.getOwnPropertySymbols()` method.


### Referenced Types

They are not simple atomic values but are objects made up of multiple properties. They are stored as a reference in memory.

- objects
- arrays
- functions

### Functional Programming (FP)

A process of creating software through `pure functions`, `avoiding shared state`, `mutable data` and `side effects`.

It is declarative. 

- Pure functions [see details in Pure Function's section]
- Function composition (Combining 2 functions. Using the result of one function in another function and so on...)
- Avoid shared state
- Avoid mutating state
- Avoid side effects (any state change that is observed outside the called function other than its return value. The include: Modifying external var/prop, logging to console, writing to screen, writing to file, writing to network, triggering external process, calling any other function with side effects)

### Imperitive vs Declarative

In imperative style, we'll have to tell the framework step by step what needs to be done

    const doubleMap = numbers => {
      const doubled = [];
      for (let i = 0; i < numbers.length; i++) {
        doubled.push(numbers[i] * 2);
      }
      return doubled;
    };

    console.log(doubleMap([2, 3, 4])); // [4, 6, 8]

In a declarative style, we'll just ask the framework what needs to be done and that framework should know how and what to do.

    onst doubleMap = numbers => numbers.map(n => n * 2);

    console.log(doubleMap([2, 3, 4])); // [4, 6, 8]

### Mutable/Imutable

  In immuatability, we create and assign it again, the reference is also changed. In mutability, the reference remains the same, only value changes.

  The first approach is to mutate the data by directly changing the data’s values. The second approach is to replace the data with a new copy which has the desired changes.

  Detecting change in mutable component requires comparing it with the previous copies of itself. In immutablity, the new object can be compared with the object which it is referenced by.

  JS provides a method called `freeze` which then doesnt allow the `1st level` properties to update. So only the primitive properties are frozen. Will have to iterate over each nested one in order to completly freeze it.

  We can use `Object.assign` or `spread` to avoid mutation.

### DOM

    const btn = document.querySelector('button');
    btn.addEventListener('click', () => {
      alert('Clicked!');

      let pElem = document.createElement('p');
      pElem.textContent = 'This is a newly-added paragraph.';
      document.body.appendChild(pElem);
    });

### Component vs Element (React)

An element is a basis object that describe DOM node and its properties. Cant apply any methods on it.

A component is a function or class which takes props and can have state and returns an element.

### Controlled vs Uncontrolled Components (React)

A Controlled Component is one that takes its `current value through props` and `notifies changes through callbacks` like onChange. A `parent component "controls"` it by handling the callback and managing its own state and passing the new values as props to the controlled component. You could also call this a `"dumb component"`. 

    <input type="text" value={value} onChange={handleChange} />

A Uncontrolled Component is one that `stores its own state internally`, and you `query the DOM` using a `ref` to find its current value when you need it. This is a bit more like traditional HTML.

    <input type="text" defaultValue="foo" ref={inputRef} />
    // Use `inputRef.current.value` to read the current value of <input>

### Asynchronous

Some actions may take time like fetching data from api, video streaming etc. To overcome these, we use `async callbacks` or `promises` which keeps the task in the background and continue main program execution and responds/notifies when the task is completed. Now as JS is `single threaded`, the async operations which are in-progress in the background are pushed in an `event queue` which runs after the `main thread` has finished processing. The queued operations finish asap and return their result to js environment. 

### Synchronous

While each operation is being processed, rendering is blocked.

### Promise **-**

The promise is an object representing the completion or failure of the async operation. They are essentially a returned object to which you attach callback functions, rather than having to pass callbacks into a function. 

Advantages of promise over conventional callbacks:
- Can `chain multiple async operations` together using `multiple .then()` operations, passing the result of one into the next one as an input.
- Promise callbacks are always called in the `strict order` they are placed in the `event queue`.
- `Error handling` is much `better` — all errors are handled by a `single .catch()` block at the end of the block.
- Promises `avoid inversion of control`, unlike old-style callbacks, which lose full control of how the function will be executed when passing a callback to a third-party library.

      const myPromise = () => {
        return new Promise((resolve, reject) => {
          let error = false;
          setTimeout(() => {
            if (!error) {
              resolve(/* some nested logic */);    	
            }
            else {
              reject('Something went wrong');
            }
          }, 2000);
        }) 
      }	

      doSomething()
      .then(result => doSomethingElse(result))
      .then(newResult => doThirdThing(newResult))
      .then(finalResult => {
        console.log(`Got the final result: ${finalResult}`);
      })
      .catch(failureCallback);

  Important: `Always return results`, otherwise callbacks won't catch the result of a previous promise
  
We can define a promise like:

      let myPromise = new Promise(resolve, reject) => {
      	let myFlag = false;
	if (myFlag) {
	  resolve('Had success');	
	} else {
	  reject('Had a failure');
	}
      };
      
      myPromise
        .then((message) => console.log(message))
	.catch((error) =>  console.log(error))
      
      doSomething()
      .then(result => doSomethingElse(result))
      .then(newResult => doThirdThing(newResult))
      .then(finalResult => {
        console.log(`Got the final result: ${finalResult}`);
      })
      .catch(failureCallback);
      
      Promise.all([myPromise1, myPromise2, myPromise3]).then((messages) => console.log(messages);
      // it waits until all are resolved and returns all the results in an array
      
      Promise.race([myPromise1, myPromise2, myPromise3]).then((message) => console.log(message);
      // it returns the first resolved promise's result

### Async await

    const myPromise = () => {
      return new Promise((resolve, reject) => {
        let error = false;
        setTimeout(() => {
          if (!error) {
            resolve();    	
          }
          else {
            reject('Something went wrong');
          }
        }, 2000);
      }) 
    }

    const myAsyncFunction = async () => {
      await myPromise();
      console.log('In async - promise ran')
    }

    /* async function myAsyncFunction() {
      await myPromise();
      console.log('In async - promise ran')
    } */

    myAsyncFunction();

### Blob

It is a `file-like object` of immutable raw data which can be `read as text or binary data`. Blobs can represent data that isn't necessarily in a JavaScript-native format.

    const obj = {hello: 'world'};
    const blob = new Blob([JSON.stringify(obj, null, 2)], {type : 'application/json'});

One way to read content from a Blob is to use a FileReader. Another way to read content from a Blob is to use a Response.

### Binding

It is when we explicitly(by default its windows, objects' own etc) assign this to a value.

Binding an object to function: 

    let player = {
      name: 'Neymar',
      club: 'PSG',
    };

    function printPlayerName() {
      console.log(this.name);
    }

    let playerNameFunc = printPlayerName.bind(player);

    playerNameFunc();

Binding doesnt work with arrow function.

### Class & Prototypal Inheritance

Its like one object trying to access properties and methods of other objects.

Each primitive or referenced type will have access to certain properties like an array can use `forEach` `length` `push` etc. Thats given by prototype. Every time js attaches an hidden obj `__proto__` (or `prototype`) which has all these functions and properties.

The __proto__ also has its own __proto__ property which is `Array.prototype`, that has its own __proto__ which is `Object.prototype` and it has its own __proto__ which is null. This is called prototype chain. This was for array (same for function). For objects, the first __proto__ will be an `Object prototype` so the next one would be null.

This supports the notion that everything in js is an object.

---------------OR----------

Every object by default has a property `prototype`. By default, its empty. We can add properties and methods to it. When we create objects from this function like instance of a class, that object will inherit these preoperties and methods from the parent.

JS has no literal `class` implementation. ES6 has class keyword but it prototype and gives constructor.

Every function is a constructor in JS.

We create an object from the func/class, then is created from a master object and all have the properties and they look up the prototype chain. 

### Threads

A thread is basically a `single process` that a program can use to complete tasks. Each thread can only do a `single task at once`. Each task `will run sequentially`; a task has to complete before the next one can be started.

Many computers now have `multiple cores`, so can do multiple things at once. Programming `languages that can support multiple threads` can use multiple cores to complete `multiple tasks simultaneously`.

`JS is single threaded`. Means everything runs on the main thread. Although, now `Web workers` allow you to send some of the js processing off to a `separate thread`, called a `worker` so that you `can run multiple js chunks` simultaneously. You'd generally use a worker to run `expensive processes off the main thread` so that user interaction is `not blocked`. The worker thread can perform tasks `without interfering with the user interface`.


### Web Workers

When `executing scripts` in an HTML page, the page becomes `unresponsive` until the script is finished.

A web worker is a JavaScript that `runs in the background`, independently of other scripts, `without affecting the performance` of the page. You can `continue to do whatever` you want: clicking, selecting things, etc., while the `web worker runs in the background`.

A worker is an object created using a `constructor (e.g. Worker())` that runs a named JavaScript file — this file contains the code that will run in the worker thread; workers run in `another global context` that is different from the current window. Thus, using the `window shortcut` to get the current global scope (instead of self) within a Worker will `return an error`.

The worker `context` is represented by a `DedicatedWorkerGlobalScope object` in the case of `dedicated workers (standard workers that are utilized by a single script; shared workers use SharedWorkerGlobalScope)`. A dedicated worker is only accessible from the script that `first spawned` it, whereas `shared workers` can be accessed from `multiple scripts`.

You can run whatever code you like inside the worker thread, with some exceptions. For example, you `can't directly manipulate the DOM` from inside a worker, or use some default methods and `properties of the window`  or the `parent`. But you can use a large number of items available under window, including WebSockets, and data storage mechanisms like IndexedDB.

Data is sent between workers and the main thread via a system of messages — both sides send their messages using the postMessage() method, and respond to messages via the onmessage event handler (the message is contained within the Message event's data attribute.) The data is copied rather than shared.

If you need to immediately terminate a running worker from the main thread, you can do so by calling the worker's terminate method.

    var myWorker = new Worker('worker.js');
    myWorker.terminate();

Problem:
- Not able to access the DOM — you can't get a worker to directly do anything to update the UI.

### Anonymous Functions

They are the functions which dont have a name.

### Closure ***

When an inner function has access to (its lexical scope) outer function's variables along with its own and global variables. And even ifs accessed later on, it would have reference to those properties and methods.

They are functions with preserved data.

It also helps in data encapsulation (and functional currying)

    function counter() {
      var count = 10;

      return () => count++; 
    }

    // nobody can directly change counter, they'll have to use this method

    counter()();

Also, will help create new copies w/o worrying about the previous counter state

    const counter1 = counter();
    counter1(); // 11
    counter1(); // 12

    const counter2 = counter();
    counter2(); // 11

In JS, the inner functions will have access to its outer vars but anything outside wont have access to the vars defined inside because JS uses `lexical scoping` i.e. a closure is a function that captures variables from its lexical scope.

    var passed = 3;

    var add = () => {
      var inner = 2;
      return passed + inner;
    };

    console.log(add());

We could've passed the global var 3 as a param but we didnt and now the above example is the simplest form of closure cuz it is using variables from the outside. We can verify by logging the func add to console and see in `function scope` where it has a Closure with a key `passed` and value `3`.

A detailed example would be a function inside a function.

    var add = (passed) => {
      var _add = (inner) => { // inner in context to `add`
        return passed + inner;
      };

      return _add;
    };

    console.log(add(3)); // returns the func `_add`

    var addThree = new add(3);
    var addFour = new add(4);

    console.log(addThree(1)); // returns 4;

Here, within this `add` function, we have a function `_add` which returns a value but the `add` returns a function i.e. `_add`

Every function has a set of variables that it can access. So all the references to these vars are stored in a stack.

A closure has three `scope chains`.

- Has access to its own scope. Vars defined inside it
- Has access to the vars of outer function
- Has access to the global variables

Disadvantages:
- Memory extensive (sometimes garbage is not collected)
- Can lead to memory leak

### Constructor Function

    function Counter() {
      var count = 0;

      this.increment = function () {
        count++;
      }
      this.decrement = function () {
        count--;
      }
    }

    var counter1 = new Counter();
    counter1.increment()

### Async, Defer

While a page can have HTML and scripts, assume some of the HTML is getting parsed, and before ending a script is encountered. Script is ran in 2 parts, first its `fetched` and then its `executed`. So, until these the HTML parsing is blocked. 

We can use `async` attribute which fetches the script while loading the HTML and when it gets loaded, HTML pasring stops and script gets executed. After its execution, HTML parsing continues.
Async doesnt gurantee order of execution of multiple scripts and dependat scripts can break but defere does.

`Defer` is somewhat same but instead of executing the script right after fething, it `waits for HTML` to completely parsed and then executes.

### Curring

It is when a function `doesnt take all of its arguments` upfront. It `gets one argument` and then it `returns another function` which we'll call with the second argument and so on until all the arguments are provided. The function at the end of the chain will return the value.

Simple version of a function

    let dragon = (name, size, element) => name + ' is a' + size + ' that breathes ' + element;

    console.log(dragon('duffy', 'tiny', 'fire'));


Currying version

    let dragon = (name) => (size) => (element) => name + ' is a' + size + ' that breathes ' + element;

        console.log(dragon('duffy')('tiny')('fire'));
        // OR
        const duffy = dragon('duffy');
        const tinyDuffy = duffy('tiny');

        console.log(tinyDuffy('fire'));

We made the function curriable but if we already have functions which are not curriable, then we can use libraries like lodash which provides methods to make them curriable.

### Functional Chaining

We can call another method on the result of one method. Its a way to call a sequence of methods in `OOP`. Each of the function call would be returning the reference to `this` and hence can call another method against that object.

    new Array(1, 2, 3, 4)
      .filter(x => x % 2 === 0)
      .reduce((mem, x) => mem + x)


### Functional Composition
We can call another method on the result of one method. Its a way to call a sequence of methods in `Functional Programming`. f(g(x)). This functionality of calling the first function and passing its result directly to a second function can be extracted to avoid code repetition.

    const isEven = x => x % 2 === 0;
    const filterOutOdd = collection => collection.filter(isEven);

    const add = (x, y) => x + y;
    const sum = collection => collection.reduce(add);

    const sumEven = collection => sum(filterOutOdd(collection));

    sumEven([1, 2, 3, 4]);

    // Using compose
    const compose = (fn1, fn2) => inputObject => fn1(fn2(inputObject));

    const isEven = x => x % 2 === 0
    const filterOutOdd = collection => collection.filter(isEven)

    const add = (x, y) => x + y
    const sum = collection => collection.reduce(add)

    const sumEven = collection => compose(sum, filterOutOdd)(collection)

    sumEven([1, 2, 3, 4])

Which functions to compose:

- unary — ones that accept just one argument,
- small — to achieve more reusability,
- pure — this is especially important when composing complex functionality, as function impurity is “contagious”,
- curried, and accepting data as the last argument — to make expressions more concise.

### Imediately Invoked Functions Expressions (IIFE)

Mostly used to create blocks and can have variables with scope rather than global.

    // Block level code
    {
      (function() {
        var v = 'var';
        let l = 'let';
      })()
    }
    
### call, apply and bind methods

In JS, every function has a `call` method in which we can pass the reference of the callee (the params can be the 2nd parameter (and go on)) like another function can borrow it. 

    const obj = {
      firstName: 'Cristiano',
      lastName: 'Ronaldo',
      printFullName: (skill, age) => {
        console.log(this.firstName + ' ' + this.lastName + ' skilled in ' + skill);
      }
    };

    const obj2 = {
      firstName: 'Neymar',
      lastName: 'JR',
    };

    obj.printFullName.call(obj2, 'speed', 33);
    
`apply` is same as call but sends an array of params as second parameter
    
    obj.printFullName.apply(obj2, ['speed', 29]);

`bind` is also almost same to call but instead of directly calling, it returns a method which we can call later

    const bindedMethod = obj.printFullName.apply(obj2, ['speed', 29]);
    bindedMethod();

### Memoization

A technique where we `store the result` of a function for later usage. If in future, we call that method with the same input, it wouldnt do complex and long computations and will return the same `cached result`. It should be applied to pure functions.

Can use `Ramda` which has other features as well. `nano-memoize` is another

### Event Bubbling

Click events execute from the element clicked and then will go all the way to the parent.

`e.stopPropagation()` can be used to avoid bubbling and will stop execution of the elements further up the order. 

### Event Capturing

First the parent element executes and goes all the way to the child. 

By default event bubbling occurs but we can choose to use event capturing by:

    var elem = document.querySelector('#my-element');
    elem.addEventListener('click', () => console.log('Element clicked'), true); // 3rd arg is useCapture

### Hoisting ***

The default behavior of moving all the declarations at the top of the scope before code execution. A function or a variable can be used before declaration.

In terms of variables and constants, keyword var is hoisted and let and const does not allow hoisting.

    a = 5;
    console.log(a); // 5
    var a;

However, initializations are not hoisted.

    console.log(a); // undefined
    var a = 5;

The above program behaves as

    var a;
    console.log(a); // undefined
    a = 5;

For `functions`, if used as an expression, an error occurs because only declarations are hoisted.

    greet(); // gives reference error

    let greet = function() {
        console.log('Hi, there.');
    }
  
But it can be fixed by

    greet(); // Hi, there.

    function greet() {
        console.log('Hi, there.');
    }

### Heap

Whenever you `define a variable, constant, object, etc` in your javascript program, you need some `place to store` it. This place is nothing but the `memory heap`.

When the statement var a = 10 is encountered, a location in the memory is assigned to store the value of a.

The memory available is limited and complex programs may have a number of variable and nested objects. This makes it essential to make wise use of the available memory.

Unlike languages like C, where we need to explicitly allocate and free memory, JS provides the feature of `automatic garbage collection`. Once the `object/variable is out of context` and will not be of use anymore, it’s `memory is reclaimed and returned to the free memory pool`.

### Mark and Sweep algorithm

Mark the objects as reachable/unreachable and sweep the unreachable ones.

### Memory Leaks

Memory leaks are `parts of memory` that the `application needed` and used `in the past` and it is `not needed anymore` but its `storage is yet not returned` to the memory pool. `Global variables` are common examples which are kept even if they arent being used. Also, if we create `Event Listeners` and not remove them after going out of context.

### Web APIs

The things which browsers provide out of the box which V8 doesnt orivudes. Like `DOM, ajax (XMLHTTPRequest), setTimeout`. They are other threads but we cant use them as normal threads.

### Call Stack

As JS is a single threaded language, it has one call stack, can do one thing at a time(so we need asynchronous to get around).

Callstack records where in the program we are. We call a function, we push it on the top of the stack, when that function returns, it gets popped from the top. 

If we go in an infinite loop or many function calls pushed in the stack, the stack overflows giving error `Maximum call stack size exceeded`.

### Event Loops

Although JS is `single threaded`, but that means it can do one thing only at the `runtime` but browser is more than runtime. When an async task starts, it comes to `call stack`, initiates and then goes to web apis and gets removed from the call stack. Then in `web apis` it keeps on processing as a background task in thread. 

When it gets completed, it `comes to task queue`, and then to the `event loop`. Now the event loop's job is to see if there is anything in the call stack or like its empty, it looks at the  `task queue` and if there is anything, it pushes to the stack.

The reason we need event loop is that we cant simply push back the queued task directly on the stack cuz then it'll disturb the normal flow of things happening.

There are two callback queues, one for macrotasks/Task Queue and one for microtasks/Job Queue (usually for promises and other priority items) and first micro runs and then macro runs

### Render Queue

Render runs after every around 16ms. Render only runs if the callstack is empty. So debounce can be used on heavy event based process like on scroll if something is happening. 

### Stack vs Heap based Memory

Because the data is added and removed in a `LIFO` manner, `stack-based memory` allocation is `very simple` and typically `much faster` than `heap-based` memory allocation (also known as `dynamic memory allocation`) typically allocated via `malloc` (memory allocation).

The major difference between Stack memory and heap memory is that the stack is used to store the order of method execution and local variables while the heap memory stores the objects and it uses dynamic memory allocation and deallocation.

`Stack is a linear` data structure whereas `Heap is a hierarchical` data structure.

Stack variables can't be `resized` whereas Heap variables can be resized. Stack memory is allocated in a `contiguous block` (consective) whereas Heap memory is allocated in any random order.

### Lexical Scoping (Static Scoping)

Lexical scoping is a convention used with many programming languages that sets the scope (range of functionality) of a variable so that it may only be called (referenced) from within the block of code in which it is defined. The scope is determined when the code is compiled.

In this scoping a variable always `refers to its top level` environment.

    const global = 20;

    function foo() {
      return 10;
    }

    function bar() {
      const global = 10;
      return foo();
    }

    console.log(bar()); // returns 20 cuz lexical scope  is looking at the top level declaration.

        var global = 20;

        function foo() {
          return global;
        }

        function bar() {
          var global = 10;
          return foo();
        }

        console.log(bar()); // returns 20 cuz lexical scope  is looking at the top level declaration.

  In static scoping the compiler first searches in the `current block`, then in `global variables`, then in successively `smaller scopes`.

### Dynamic Scope

With dynamic scope, a global identifier refers to the identifier associated with the most recent environment. This means that each identifier has a `global stack` of bindings and the occurrence of an identifier is searched in the `most recent binding`.

    const global = 20;

    function foo() {
      return 10;
    }

    function bar() {
      const global = 10;
      return foo();
    }

    console.log(bar()); // returns 10 cuz dynamic scope is looking at the latest executed function's scope.

In simpler terms, in dynamic scoping the compiler first searches the `current block` and then successively all the `calling functions`.

### Lexical vs Dynamic Scope

Lexical scoping refers to when the location of a function's definition determines which variables you have access to. On the other hand, dynamic scoping uses the location of the function's invocation to determine which variables are available.

In most programming languages `static scoping is dominant`. This is simply because in static scoping it’s `easy to reason about and understand` just by looking at code. We can see what variables are in the scope just by `looking at the text` in the editor.

Dynamic scoping does `not care how the code is written`, but instead `how it executes`. Each time a new function is executed, a new scope is `pushed onto the stack`.

### Local Storage vs Session Storage vs Cookies

Cookies: 
  - 4kb
  - HTML 4/5
  - expires on demand
  - stores on browser/server
  - sent with request

Local:
  - 10mb
  - HTML 5
  - expires never
  - stores on browser
  - not  sent with request

Session:
  - 5mb
  - HTML 5
  - expires on tab kill
  - stores on browser
  - not sent with request

### CORS

While in SOP (same origin policy), browser never allows to share the resources from different origins.

The requesting website must have same origin means `protocol` e.g. https, `domain` e.g. my-site.com and `port` 4000

It works like when request from one origin is made, a `preflight` OPTIONS call request is made before that to ensure the validity of request. If valid, the requestee will set additional headers which will let the client/browser know its safe and then the actual call is made. The requestee will set the headers like `Access-Control-Allow-Origin: *` where * means any domain can access. Additinally some other headers will help retrict methods like GET, POST, DELETE

### JS methods
  - forEach
  - map
  - shift: It removes the first item and returns that first item. It mutates the array
  - unshift
  - slice

    The slice() method returns a shallow copy of a portion of an 
    array into a new array object selected from start to end (end not 
    included) where start and end represent the index of items in 
    that array. The original array will not be modified. The params are

    `slice(start, end)`

    where start (not required) is index at which to start extraction and if its undefined, start is 0th index. End (not required) used to extract upto but not including that index.

    A negative index can be used, indicating an offset from the end of the sequence. slice(2,-1) extracts the third element through the second-to-last element in the sequence.

    If end is omitted, slice extracts through the end of the sequence (arr.length)

    Returns a new array containing the extracted elements.

  - splice

    Mutates the array by removing or replacing and/or adding the 
    new elements. The params are 

    `splice(start, deleteCount, item1, item2, itemN)`

    where start is the index (required param) to start from, deleteCount (not required) is the number
    of items to be deleted from that index (can be 0 or in minus) and 
    item/item...(not required) are the items to be added after that start index. 
    Slice returns the array of removed elements 

      
  - reduce
    
    Takes 2 arguments, the first one is a callback method, which further takes
    two arguments where first one is the `total` or `accumalator` and second 
    one is the `current` of this iteration, and second parameter of reduce
    is the initial value of accumalator. It returns a single value

        const myReducedArray = myArray.reduce((total, item) => total + (item.num1 + item.num2), 0) 

### Shallow / Deep Copies

  In a shallow copy, a new object is created that has an exact copy 
  of the values in the original object. If any of the fields of the 
  object are references to other objects, just the reference 
  addresses are copied i.e., only the memory address is copied.

      var employeeDetailsOriginal = { name: 'Max', age: 25, profession: 'Software Engineer' };

      var employeeDetailsDuplicate = employeeDetailsOriginal; //Shallow copy!

      employeeDetailsDuplicate.name = 'NameChanged'; // Also changes name of employeeDetailsOriginal

  A deep copy copies all fields, and makes copies of dynamically 
  allocated memory pointed to by the fields. A deep copy occurs when 
  an object is copied along with the objects to which it refers

      var employeeDetailsDuplicate = { 
        name: employeeDetailsOriginal.name,
        age: employeeDetailsOriginal.age,
        profession: employeeDetailsOriginal.profession
      }; // Deep copy, now the original object's values' persists
  
  Better ways to copy objects deeply are

      var objectIsNew = JSON.parse(JSON.stringify(objectIsOld));

### Type Coercion

  Type coercion is the automatic or implicit conversion of values from one data type to another. For example, converting a string value to an equivalent number value

      let a = 12;
      let b = "12"

      if (a == b) {
        console.log('Both are equal');
      } else {
        console.log('Both are not equal');
      }
      // Output: 'Both are equal'

      let c = a + b
      console.log(c); // output: '1212'

  To avoid this inconsistent behaviour, we can use '===' to also check the type while comparing and explicitly converting the variable to number while adding

### Throttling
  
  Delaying function execution. Like search after 500ms. It will wait until the delay/timeout.

      const throttle = (func, limit) => {
      let flag = true;
      return (...args) => { // `...args` will capture all the params as we dont know how many they can be
        if (flag) {
          func.apply(this, args);
          flag = false;

          setTimeout(() => {
            timer = undefined;
          }, limit);
        }
      };
    };

    const throttledSearchRecords = throttle(searchRecords(), 1000);

### Debouncing
  
  Prevent the event trigger from being fired too often. It waits for certain time (delay/timeout) that is the difference between the events. Means if the trigger difference of two events is greater than the delay, only then make a call.

      const debounce = (func, timeout) => {
        let timer;
        return (...args) => { // `...args` will capture all the params as we dont know how many they can be
          if (!timer) {
            func.apply(this, args);
          }
          clearTimeout(timer);
          timer = setTimeout(() => {
            timer = undefined;
          }, timeout);
        };
      };

      const debouncedSearchRecords = debounce(searchRecords(), 1000);

### Temporal Dead Zone

Variables declared with let and const are not hoisted and they dont have a default value of undefined. That is the Temporal Dead Zone where variabled are un reachable. They exist in temporal dead zone from start until we initialize them.

### Pure Functions

  When a function calculates its output from using other than its parameters as an input. When its not completly and only dependant on its inputs. 

  A pure function is a function which,

  - Given the same inputs, always returns the same output
  - Has no side-effects (only changes to local scope are allowed. Read operations are okay. Some read operations have side effects like `Math.random()` which generates new number by changing the Math's reading position and other methods which involves reading from an external sensor that involves a "take measurement" command.) 

  A pure function is `Referentially Transparent`. Referential Transparency, roughly, means that you can replace the call to the function with its return value or vice versa at any point in the program, without changing the meaning of the program.

### Higher Order Functions

  Its a function that either takes a function as a parameter or returns a function

   - Function accepting a function

          document.addEventListener("click", () => myFunction());
  - Function returning a function

          const createMultiplier = (multiplier) => {
            return (x) => {
              return x * multiplier
            }
          };

          // OR

          const createMultiplier = (multiplier) => (x) => x * multiplier;

          let doubleMe = createMultiplier(2);
          let tripleMe = createMultiplier(3);
      In JS, functions are considered as first class citizens like numbers, 
      strings and we can assign a variable or a const a function. We can pass
      them as a param and can return them from functions
  - Popular HOCs
      
      - forEach()
      - map()
      - filter()
      - reduce()
      - sort()

### ES6 Features

- let and const Keywords
- Arrow Functions
- Multi-line Strings
- Default Parameters
- Template Literals
- Spread/Rest operators
- Destructuring Assignment
- Enhanced Object Literals
- Promises
- Classes
- Modules

<br><hr><br>

## HTML

### Semantic HTML

Semantic HTML refers to the practice of using HTML elements according to their intended meaning and purpose, rather than just for visual styling or layout. 

It provides context and meaning to the content of a web page, making it more accessible, understandable, and maintainable. Semantic HTML helps search engines, assistive technologies, and developers to better understand the structure and content of a web page.

- The `<header>` element represents the introductory content at the top of a section or page. It often contains branding, navigation, or other header-related content.
- The `<nav>` element represents a section of the page that contains navigation links.
- The `<main>` element represents the main content of a document. It should be unique to the document and not repeated across a set of documents such as site navigation.
- The `<article>` element represents a self-contained composition that could be distributed and reused independently. It could be a blog post, a news article, a forum post, etc.
- The `<section>` element represents a thematic grouping of content. It helps to organize and structure the content of the page.
- The `<aside>` element represents content that is tangentially related to the content around it. It's often used for sidebars, pull quotes, advertising, or similar content.
- The `<footer>` element represents the footer of a section or the whole page. It typically contains information about the author, copyright, contact details, or links to related documents.


### HTML 5

- iFrames
- New elements
  - `<video controls preload><source src="video.mp4" type="video/ogg; codecs='vorbis, theora'" /></video>`
  - `<audio autoplay="autoplay" controls="controls"><source src="file.mp3" /></audio>`
  - `<nav><a href="/html/">HTML</a></nav>`
  - `<header><img src="company-logo.png" /><nav>...</nav></header>`
  - `<canvas></canvas>`
  - `<footer>...</footer>`
  - ```
    <figure><img src="image/image-1.jpg" alt="About ADMEC" />
      <figcaption><p>This is our institute </p></figcaption>
    </figure>
    ```
- New types of inputs i.e. email, month, number, range, search, tel, color, week, url, time, date, datetime-local etc. ContentEditable, Progress, section, main(1 page can only have 1 main, also, navs, headers, footers are not allowed)
- Placeholders
- Required attribute
- Preload Videos
- Regex
- Accessibility (validations in forms)
- Inline elements/Dynamic Page Support
    - mark – It highlights the content that is marked in some or the other way.
    - time – This helps in adding current time as well as date to the webpage.
    - meter – It helps in indicating that how much space in the storage disk is still there.
    - progress bar – It helps in knowing the progress of the task that has been assigned for its completion.
- nonce (we usually use nonce attribute inside script and style tag. This nonce tag basically generates a random number which is for one time use only. So, it is regenerated each time the page refreshes. It is great features as it can be used to increase the security of the content of the page. This helps in stating and providing the authority to the webpage to specify a particular script or style.)

<br><hr><br>

## CSS/SASS
- CSS
  - Selectors
    - \# = id
    - . = class
    - .name1.name2 = Selects all elements with both name1 and name2 set within its class attribute
    - .name1 .name2 = Selects all elements with name2 that is a descendant of an element with name1
    - \* = Selects all elements
    - p = Selects all \<p> elements
    - p.intro = Selects all \<p> elements with class="intro"
    - div, p = Selects all \<div> elements and all \<p> elements
    - div p =	Selects all \<p> elements inside \<div> elements
    - div > p =	Selects all \<p> elements where the parent is a \<div> element
    - div + p =	Selects the first \<p> element that is placed immediately after \<div> elements
    - p ~ ul =	Selects every \<ul> element that is preceded by a \<p> element
    - \[target] =	Selects all elements with a target attribute
    - \[target=_blank] =	Selects all elements with target="_blank"
    - \[title~=flower] =	Selects all elements with a title attribute containing the word "flower"

    - a:active = Selects the active link
    - p::after =	Insert something after the content of each \<p> element
    - input:checked =	Selects every checked \<input> element

  - Pseudo classes
- SASS

  Sass is a preprocessor scripting language that is interpreted or compiled into Cascading Style Sheets.
  Its an extension to CSS. It allows us to use variables, functions
  conditions. Its written in ruby.
  
  - Using variables:

        $myFavColor: #323232;

        .myClass {
          color: $myFavColor;
        }

  - Nested Styles:

        #myRootWrapper {
          width: 100%;

          .myClass {
            color: $myFavColor;
          }

          ul {
            background: $myFavColor;
          }
        }

    this is equal to following in CSS

        #myRootWrapper {
          width: 100%;
        } 

        #myRootWrapper .myClass {
          color: $myFavColor;
        }

        #myRootWrapper ul {
          background: $myFavColor;
        }
  
  - mixin

    Mixins are basically a reusable chunk of css/sass which we can
    inject in different elements. They allow us to write reusable
    styles. We can pass variables as well to intanciate them at run 
    time like

        @mixin important-text {
          color: red;
          font-size: 25px;
          font-weight: bold;
          border: 1px solid blue;
        }
        
        .danger {
          @include important-text;
          background-color: green;
        }

    Simple mixins:

          @mixin myMixin {
            width: 100%;
            color: $myFavColor;

            .myClass {
              padding: 8px;
            }

            // `title` class inside span
            span.title {
              font-weight: bold;
            }
          }

    Now using this mixin

        #myRootWrapper {
          @include myMixin
        }

  - importing other external SASS

    We can create separate files for vars, mixins and separate styles
    files. Import order matters

        @import "./myVars";
    
    And thats it, now we can use mixins and vars from other styles

  - Pseudo classes

        #myRootWrapper {
          width: 100%;

          &:hover {
            background: #323232;
          }
        }
        
  - Math Operators

    Can use, addition, subtraction, multiplication, division

        li {
          width: (14px * 2);
        }

        div {
          width: (100% / 6);
        }

  - Mixin functions

        @mixin myMixin($cols, $mgns) {
          float: right;
          margins: $mgns;
          width: ((100% - (($cols - 1) * $mgns)) / $cols); 
          &:nth-child(${cols}n) {
            margin-right: 0;
          }
        }

        .myClass {
          @include myMixin(4, 2%);
        }

  - Colour Functions

    SASS provides tons of functions for us to use, can [visit this link](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa2xtQU1qTFJrWnFaZmtDUC0wR3ZVZnZITjM1QXxBQ3Jtc0trRDNhZS1yX3JBa2M4bDBsaFcwUUVoelBoOW9laXVCdjhCUnNxU0wzWml2VDNjb2VDQ2pQSGx4TnNUenNwWWhlY1FFeWxka0dxcXJkZUVvRDk4ZVlSbDFTS0xBb09WTTN2RUxieklZeXpVdF9Rc0JYTQ&q=http%3A%2F%2Fsass-lang.com%2Fdocumentation%2FSass%2FScript%2FFunctions.html) 
    for details

        .myClass {
          background: lighten($myFavColor, 5); // 2nd param defines the intensity

          &:hover {
            color: complement($myFavColur);
          }
        }

  - Content Keyword

    It search and puts the style where it finds the context keyword

        @mixin mediaQuery($arg) {
          @media screen and (max-width: $arg) {
             @content; // children when mixin called will get here
          }
        }

        li {
          @includes mediaQuery(600px) {
            width: 100%
          }
        }

  - If statements

        @mixin mediaQuery($arg...) { // when number of args is not specified
          @if length($args) == 1 {
            @media screen and (max-width: nth($arg, 1)) {
             @content; // children when mixin called will get here
            }
          }
          @if length($args) == 2 {
            @media screen and (max-width: nth($arg, 1)) and (min-width: nth($arg, 2)) {
             @content; // children when mixin called will get here
            }
          }
        }

        li {
          @includes mediaQuery(600px, 100px) {
            width: 100%
          }
        }


- Media queries

  It uses the @media rule to include a block of CSS properties only if a certain condition is true

      /* For mobile phones: */
      [class*="col-"] {
        width: 100%;
      }

      @media only screen and (min-width: 600px) {
        /* For tablets: */
        .col-s-1 {width: 8.33%;}
        .col-s-2 {width: 16.66%;}
        .col-s-3 {width: 25%;}
        .col-s-4 {width: 33.33%;}
        .col-s-5 {width: 41.66%;}
        .col-s-6 {width: 50%;}
        .col-s-7 {width: 58.33%;}
        .col-s-8 {width: 66.66%;}
        .col-s-9 {width: 75%;}
        .col-s-10 {width: 83.33%;}
        .col-s-11 {width: 91.66%;}
        .col-s-12 {width: 100%;}
      }

      @media only screen and (min-width: 768px) {
        /* For desktop: */
        .col-1 {width: 8.33%;}
        .col-2 {width: 16.66%;}
        .col-3 {width: 25%;}
        .col-4 {width: 33.33%;}
        .col-5 {width: 41.66%;}
        .col-6 {width: 50%;}
        .col-7 {width: 58.33%;}
        .col-8 {width: 66.66%;}
        .col-9 {width: 75%;}
        .col-10 {width: 83.33%;}
        .col-11 {width: 91.66%;}
        .col-12 {width: 100%;}
      } 

<br><hr><br>

## Git/GitHub

- installation
  - Install git from git scm
- Clone dir/Git Repos
- Setup in webstorm
- Adding an existing project to GitHub
  - in ur project main file, run
    - git init
  - add and commit all files in project by
    - git add .
    - git commit -m "adds all files" 
  - change base branch from master to main (optional - need change cuz git creates `main` branch)
    - git branch -m main
  - now connect to remote repo by
    - git remote add origin https://github.com/WaleedYousaf/ttt.git // link of repo
  - now just push on ur branch
    - git push origin main
- Cloning a project in my webstorm myapp project
- Cloning Margalla/Pulpo
- Git commands
  - Mock commands:
    - git commit --amend --reset-author // resetting author
    - git remote add origin https://github.com/ waleedyousaf07/football_roster  [To ]
      OR git clone ssh://git@github.com/[username]/[repository-name].git
    - git push -u origin master
    - git checkout -b my_branch [created new my_branch and swithced to mybranch]
    - //Make changes in the code
    - git add . [for add all files in current dir] OR git add -A [maybe for all in current dir and its siblings] OR git add filename.js OR $ git add my-file.ts another-file.js new_file.rb  [for adding multiple files concurrently] OR git add folder/subfolder/* 
    - Custom Add: git add src/actions/* src/components/AddPlayerView.js
    - git rm --cached my-file.ts  [to remove myfile.ts from staged basket/area] OR git reset another-file.js [works as opposite of add] OR git reset HEAD .eslintrc
    - git commit -m "my_msg_for the changes" OR git commit -m "my_msg_for the changes" --no-verify [for bypassing .eslint]
    - git push origin my_branch   OR git push -u origin master [with -u, next time we only needs to call git push]
  - Getting & Creating Projects
    - Init
      - command: git init
      - Initialize a local Git repository
      - Getting & Creating Projects
    - Clone
      - git clone ssh://git@github.com/[username]/[repository-name].git
      - git clone /path/to/repository 	//local server
      - git clone username@host:/path/to/repository
      - Create a local copy of a remote repository
      - Getting & Creating Projects
  - Merging my branch with others
    - git add mybranch
    - git commit -m "mybranch msg"
    - git checkout dosriBranch
    - git pull
    - git checkout mybranch
    - git merge dosriBranch
    - [Resolve conflicts]
    - git add mybranch
    - git commit -m "my msg"
  - Restoring / Reverting file from another branch
    - git checkout FROM_BRANCH_NAME path/to/file	
  - Basic Snapshotting
    - status
      - command: git-status
      - Show the working tree status
      - Check status
    - add
      - command: git add [file-name.txt]
      - Add a file to the staging area
    - add
      - command: git add -A
      - Add all new and changed files to the staging area
    - commit
      - git commit -m "[commit message]"
      - Commit changes
    - remove
      - git rm -r [file-name.txt]
      - Remove a file (or folder)
  - Branching & Merging
    - add/remove files to untracked
      - git update-index --assume-unchanged
      - git update-index --no-assume-unchanged path/to/file
    - replace a file with another branch
      - git checkout origin/master [filename]
    - branch
      - git branch 	
      - List branches (the asterisk denotes the current branch)
    - branch 
      - git branch -a
      - List all branches (local and remote)
    - branch
      - git branch [branch name]
      - Create a new branch
    - branch
      - git branch -d [branch name]
      - Delete a branch
    - push
      - git push origin --delete [branch name]
      - Delete a remote branch
    - checkout
      - git checkout -b [branch name]
      - Create a new branch and switch to it
    - checkout
      - git checkout -b [branch name] origin/[branch name]
      - Clone a remote branch and switch to it
    - checkout
      - git checkout [branch name]
      - Switch to a branch
    - checkout
      - git checkout - 
      - Switch to the branch last checked out
    - checkout
      - git checkout -- [file-name.txt] 	
      - Discard changes to a file
    - merge
      - git merge [branch name] 
      - Merge a branch into the active branch
    - merge
      - git merge [source branch] [target branch]
      - Merge a branch into a target branch
    - stash
      - git stash 
      - Stash changes in a dirty working directory
    - stash
      - git stash apply stash@{0}
    - stash
      - git stash clear
      - Remove all stashed entries 
  - Sharing & Updating Projects
    - push
      - git push origin [branch name]
      - Push a branch to your remote repository
    - push
      - git push -u origin [branch name]
      - Push changes to remote repository (and remember the branch)
    - push
      - git push 	
      - Push changes to remote repository (remembered branch)
    - push
      - git push origin --delete [branch name] 	
      - Delete a remote branch
    - pull
      - git pull 	
      - Update local repository to the newest commit
    - pull
      - git pull origin [branch name] 
      - Pull changes from remote repository
    - remote
      - git remote add origin ssh://git@github.com/[username]/[repository-name].git 	
      - Add a remote repository
    - remote
      - git remote set-url origin ssh://git@github.com/[username]/[repository-name].git 	
      - Set a repository's origin branch to SSH
  - Inspection & Comparison
    - log
      - git log 	
      - View changes
    - log
      - git log --summary 	
      - View changes (detailed)
    - diff
      - git diff [source branch] [target branch] 	
      - Preview changes before merging
    - revert commit
      - git reset --hard HEAD~1
      - reset to a specific commit	
        - git reset --hard \<commit-hash>
        - git push -f origin \<curr-branch>
    - revert merge
      - git merge --abort

<br><hr><br>

## Docker

- installation
  - [follow official digital ocean link]

- for running docker
  - for local BE, in docker-compose.yml, comment out app and ngnix and add following at the end of web
    - same indentation
      ports:
        - 8081:8081 
  - in directory with docker.yml file, run command:
    - sudo docker compose up -d
  - for viewing logs
    - sudo docker logs -f web
  - check if containers are up
    - sudo docker ps
    - docker ps -a [maybe with all details like id]
  - restart web worker, maybe after changes like restarting npm start
    - sudo docker-compose up -d --f worker
  - check web logs
    - docker logs -f web
    - docker logs -f worker
    - docker logs -f [id of container, can be seen by docker ps command]
    - sudo docker-compose logs -f web worker [maybe for multiple logs in single command]
- for instance on digital ocean
  - check and add ssh key by
    - ssh keygen
    - cat ~/.ssh/id-rsa.pub
  - ask the person to add your public ssh key to instance
  - setup DO instance
    - ssh root@[instance_ip]
    - ls {check if has already any project}
    - git clone [https.. my proj]
    - cd [proj dir]
    - git checkout [my branch to test]
    - {make changes to docker-compose.yml}
      - {comment out app and ngnix}
      - {add in web, after entry point as a sibling}
        ports:
          - 8081:8081 
      - {in image worker -> environment, update SL_USERNAME and API_KEY from SL creds trello}
      - {in image worker -> environment, update WEB_HOOK_BASE_URL to http://[instance_ip]:8081/...}
      - {in worker -> environment, update WEB_HOOK_BASE_URL to http://[instance_ip]:8081/...}
      - {now add the docker-compose.yml changes to instance} nano docker-compose.yml {to show that file}
      - {now clear that file} > docker-compose.yml
      - {now update with the previous changes} nano docker-compose.yml
- FE image on dockerhub:
  - [server/index.js mein https://migrate-db.wanclouds.net address daal dyna url mein]
  - cd doosra-Frontend > sudo docker build -t wancloudsinc/doosra-vpc-frontend:db-mig-demo . 
  - [jb build ojaey image phr]
  - sudo docker push wancloudsinc/doosra-vpc-frontend:db-mig-demo 
  - [jb push ojaey then]
  - sudo docker-compose up -d --force-recreate app [in vpcBackend dir]
- stop and up containers in detach mode:
  - cd doosra-vpc-be>sudo docker-compose stop
  - [Then]
  - sudo docker-compose -d --force-recreate
- for db container (up)
  - mongo [pulpo]
    - sudo docker exec -it mongo sh
    - \# mongo margalladb -u admin -p --authenticationDatabase margalladb
    - [password is password]
    - show collections [shows all tables]
    - db.dropDatabase() [drop whole db]
    - db.users.drop() [drop users' table]

  - mysql [vpc]
    - sudo docker exec -it webdb bash
    - mysql -uwebuser -padmin123
    - use doosradb
- steps to get in remote instances:
  - Pass ssh key to the admin
    - cd ~/.ssh
    - cat id_rsa.pub
  - get into instance
    - ssh root@192.168.1.1

  - add ssh key in remote instance
    - cd .ssh
    - nano authourized_key
  - access db
    - sudo docker exec -it webdb bash
    - select * from user;
- For updating the FE (docker):
  - ssh to 169.59.10.17
  - cd to proj
  - pull latest branch
  - then build `sudo docker build -t wancloudsinc/doosra-vpc-frontend:waleed_test .`
  - then push to docker `docker push wancloudsinc/doosra-vpc-frontend:waleed_test`
  - then in doosra-vpc-be -> update file `doosdocker-compose` update image with my image name i.e. `waleed_test` in app section
  - then `docker-compose up -d --f app`

<br><hr><br>

## Middlewares

Software that enables one or more kinds of communication or connectivity between two or more applications or application components in a distributed network.

- Redux Thunk

Its between action and reducers like for redux logger, while making an action, it also logs that action to the console before setting the state in reducer

<br><hr><br>

## APIs
- CRUD
- Axios

  Used to make requests to an API endpoint

- REST Arch & RestFul APIs

<br><hr><br>

## MVC

It is a design pattern. The goal is divide large application into specific sections each having their own purpose.

User requesting a specific page from the server. The server responds to a specific controller. 

Controller: `Handles the entire request` from the client. And will tell the rest of the server what to do with the request. It acts as a middleman b/w model and view. It should not contain much code. 

Model: After receiving the request, the controller asks the model to get the data. Model is `responsible for all of the data logic` of the request. It interacts with the DB and handles all CRUD saving and other data operations. The controller shouldnt interact with the data it should always ask the model. Model doesnt need to do anything on failure or success, controller will handle that.

View: After the model sends the data to controller, then controller sends the data to view to `render` and view is only concerned for displaying the data its feeded with. The view will send the HTML (or so) back to controller which then is served to the user.

Important to note is that `model and view never interact` with each other. Presentation and Logic is completely separate.

<br><hr><br>

## Linting
- ESLint

<br><hr><br>

## Test Cases
- Unit Tests
  - JEST
  - Enzymes
- Integration Tests

<br><hr><br>

## JWTs

<br><hr><br>

## JSON Server
 - ### <b>Installation:</b>

    To install, go in any project folder or install it globally using `-g` like

        npm install -g json-server

    To run, execute command

        json-server --watch db.json --port 3001

    where `db.json` can have static json

<br><hr><br>

## Express Server
- ### <b>Installation</b>
    Can install in any empty directory. Just cd into a folder and create a new dir, we'll create `pes-app`
		  
        mkdir pes-app
			  
    cd to `pes-app` and execute

		npm init --yes
    
    This will create `pcakage.json` in this folder i.e. `pes-app`. Then, create server.js file in root dir of `pes-app`.
    We can install (optional) `nodemon` to terminate and restart the server i.e. server.js after each change. We can execute command:
		
        npm i -g nodemon
    
    After installing, we can start it by executing:

		nodemon server.js
			  
    For setting environment var PORT and using in server.js, execute:

        set PORT=3006
			  
    Use server.js for HTTP requests i.e. GET, POST. For validation use joi library

<br><hr><br>

## Sockets
- sockets.io

<br><hr><br>

## OOP

### Class (`class className`)

### Object (`new ClassName(params)`)

### Interfaces (`has`)

Defines a shape objects/classes can take

### Polymorphism

Polymorphism -> `Many-forms`. Can have a same function in parent and a class which is `inherited` and if we `override` in child class(function overriding) then the parent's function has 2 forms.

### Abstraction

It is hiding the implementation and only showing the functionality or essentials.

Not allowing the user to access a class's variable or function. Instead, let other local functions of the class calculate and use those methods and properties.

### Encapsulation

It is wrapping up the data and methods under a single unit.

Properties and methods are private.

It is binding of data to functions.

A mechanism of `restriciting direct access` to some of the object's components. It also bundles methods which operate on that data. Its required for:

- Security, controlled access
- Hide implementation and expose behaviour
- Loose coupling - modify the implementation anytime

`Getters and setter methods` are used to get those objects/properties. 

### Inheritance (`extends`)

Inherits properties/functions from its parent class

### Association

If two classes in a model need to communicate with each other, there must be a link between them, and that can be represented by an association (connector).

Aggregation and Composition are subsets of association meaning they are specific cases of association.

### Aggregation

Aggregation implies a relationship where the child can exist independently of the parent. Example: Class (parent) and Student (child). Delete the Class and the Students still exist.

### Composition 

Composition implies a relationship where the child cannot exist independent of the parent. Example: House (parent) and Room (child). Rooms don't exist separate to a House.

<br><hr><br>

## Networking **-**

<br><hr><br>

## Databases **-**

<br><hr><br>

## DSA

### Data Structures
- Stack

  It follows the LIFO. In js, array can be used cuz it supports stack. Example can be `git stash`
  functions like 
    
    - push() -> adds one item at the top
    - pop() -> removes the top value and returns the removed item
    - peek() -> returns the last element but doesnt remove it
    - size() -> shows the length of stack/array

    Palindrome number is if spelled backward, it remains the same

        let myStack = [];
        let word = "racecar";
        let reversed = "";

        // pushing letters in stack
        for (i = 0; i < word.length; i++) {
          myStack.push(word[i]);
        }

        // popping the letters back in a reversed string
        for (i = 0; i < myStack.length; i++) {
          reversed += myStack.pop();
        }
- Queue

  Its kind of an array follows FIFO.

  - print -> prints or logs collectio
  - enqueue -> push an item
  - dequeue -> pop an item but the first one so uses `shift`
  - front -> return the item at the front (0th index)  w/o removing it
  - size -> returns length
  - isEmpty -> returns true if no items

- Priority Queue

  Along with enqueuing an item, we can send a priority, if no priority is passed, it behaves like normal queue

      var pq = new PriorityQueue();
      pq.enqueue(['ronaldo', 5]);
      pq.enqueue(['neymar', 3]);
      pq.enqueue(['bale', 3]);

- Set

   Its kind of an array except no duplicate items and the values
   are not in any particular order. Basic set method provided by ES6
   doesnt include all the methods of set, we may need to implement
   part of it ourself if needed. The methods are

   - has -> returns true false if element is present in set
   - values -> return the collection/array
   - add -> only adds if element isnt already added - uses `has` to check - returns true and false if added
   - remove -> checks if collection has that element and then using its index, removes it by splicing the collection like `coll.splice(indexOfItemToRemove, 1);` and returns true false
   - size -> returns length of collection. For ES6 set, size is not a method but a property so no need to do `mySet.size()` just use `mySet.size`
   - union -> returns union of 2 sets. No duplicate entries
   - intersection -> returns intersection i.e. only common entries
   - difference -> subtracts entries from 1st collection which are in second
   - subset -> if the first set is completly contained within another set. Uses `every` 

- Linked list

  A data structure where elements are stored in a node. The node contains 2 key pieces of information, the element itself and the reference to the next node.

  Some advantages and disadvantages over arrays are
    
    Array/LinkedList

    - Fixed size/dynamic size (although JS hides this in array)
    - Inefficient insertions-deletions/efficient insertions-deletions
    - Random access(effiecient indexing)/no random access
    - Memory wastage/no memory wastage cuz dynamic size
    - Sequential access is faster (elements in contagious mem locations)/sequential access is slower

  Every linked list has a `head`  pointer and a size. Last node points to null

- Circular queue
- Trie

  A datastructure many functional programmings support which `deep freeze` all the properties of the object. 

- Binary Search Tree

  Tree structure has the entries which are `nodes`. The top one is `root`. Have `parent children siblings`. The node which doesnt have any children are `leafNodes`

  In a binary tree however, each node can only have 2 children/branches. They are ordered. Each left sub-tree
  is less than or equal to parent node and each right sub-tree is greater than or equal to the parent node.

  When they use binary search, an average operation can skip about half of the tree so each look-up, insertion 
  or deletion takes time proportional to the logrithm of the number of items stored in a tree. Can use recursion to implement BST. 

  - Height

  Height is the distance from the root to any leaf node. Level of nesting represents the height. The root has a 
  height 0, and so on. Different paths in a same tree can have different heights. 
  
  Each tree will have a minimum and a maximum height. If the tree is balanced, these values will differ at most by 1.

  Searching through a balanced tree is much more efficient

  - Traversal
    
    Ways to travers a tree

      - in-order -> begin at the left most node and end at the right most node. Like left, then parent, then parent's left child, then parent, then parent's right child if any and so on. Go in order left, root, right
      - pre-order -> we explore the root nodes before the leaves. First root node, then traverse left side's first root, then its root, and go in order root, left, right 
      - post-order -> explores the leaf nodes before the roots. So left most leaf, then its right left most leaf, then its right leaf then root and finish one side/branch of the tree.
      - level-order -> is also called breath first search. It explores all the nodes on one level of the tree before moving on to the next level. For each level from top to bottom, follow left to right. 

- Hash Tables

  A hash table is used to implement associative arrays of mapping of key value pairs. Its a common way to implement mao data structure or objects. Widely used cuz of efficiency. 
  
  The average time to lookup is not tied to the number of elements stored in the table.
  
  The avg time complexity in big `O` notation is O(1) for search, insert or delete (worst is O(n))

  It works by taking a key input and then runs it through the hash function which maps strings to numbers and 
  usually numbers corresponds to indexes in an array. All the keys should map to different numbers, cant have same keys/numbers. If two words get hashed to same number, its called collision

### Important Algorithms **-**

- Searching
  - Linear Search
  - Binary Search
  - Depth First Search
  - Breadth First Search
- Sorting
  - Insertions Sort
  - Heap Sort
  - Selection Sort
  - Merge Sort
  - Quick Sort
  - Counting Sort
  - Bubble Sort
  - Shell Sort
  - Timsort
  - Bucket Sort
  - Radix Sort
- Graphs
  - Dijkstra's Algo
  - Bellman Ford Algo
  - Floyd Warshall Algo
  - Topological Sort Algo
  - Flood Fill algo
  - Lee Algo
  - Kruskal's Algo
- Arrays
  - Floyd's Cycle Detection Algo
  - KMP Algo
  - Kadane's Algo
  - Quick Select Algo
  - Boyer - More Majority Vote Algo
- Basics
  - Huffman Coding Compression Algo
  - Euclid's Algo
  - Union Find Algo

### DSA Techniques/Usage **-**

- Use this for that
  - If input array is sorted
    - Binary Search
    - Two pointers
  - If asked for all permutations/subsets
    - Backtracking
  - If given a tree or graph
    - DFS
    - BFS
  - If given a linked list
    - Two pointers
  - If recursion is not allowed
    - Stack
  - If must solve in-place
    - Swap corresponding values
    - Store one or more different values in the same pointer
  - If asked for max/min subarray/subset/options
    - Dynamic Programming
  - If asked for top/least K items
    - Heap
  - If asked for common strings
    - Map
    - Trie
  - Misc
    - Map/Set for O(1) time & O(n) space
    - Sort input for O(nLogn) time & O(1) space 

### DSA YT Channels

- Coding Simplified
  - Array
  - DP
  - Linked List
  - Trees
- Lead Coding by FRAZ
  - Bit Manipulation
  - Maths
  - Linked List
  - Hashing
  - Binary Search
- take U forward
  - Graph
  - Recursion
  - Tree
  - Tries
  - DP
- Aditya Verma
  - Binary Search
  - Recursion
  - DP
  - Stack
  - Heap
- Code NCode
  - Number Theroy
  - Graph
  - DSU
  - String
  - Segment Tree

### Time and Space Complexity (BigO) **-**

Ref: https://github.com/jamiebuilds/itsy-bitsy-data-structures/blob/master/itsy-bitsy-data-structures.js

    / =========================================================================== \
      == - BIG-O NOTATION ------------------------------------------------------ ==
      = ========================================================================= =
      =           a           b                                 d                 =
      =           a         b    O(N^2)                      d                    =
      =     O(N!) a        b                O(N log N)    d                    c  =
      =           a      b                            d                 c         =
      =          a      b                          d             c        O(N)    =
      =          a    b                         d         c                       =
      =          a  b                       d      c                              =
      =         a  b                     d  c                                     =
      =         ab                   c                          O(1)              =
      =  e    e    e    e    ec   d    e    e    e    e    e     e    e    e      =
      =      ba        c      d                                                   =
      =    ba   c        d                       f    f    f    f    f    f    f  =
      == cadf    f d    f    f    f    f    f       O(log N)                     ==
    \ =========================================================================== /

Some common BigO's

    =
    =     Name           Notation     How you feel when they show up at your party
    =     ------------------------------------------------------------------------
    =     Constant       O(1)         AWESOME!!
    =     Logarithmic    O(log N)     GREAT!
    =     Linear         O(N)         OKAY.
    =     Linearithmic   O(N log N)   UGH...
    =     Polynomial     O(N ^ 2)     SHITTY
    =     Exponential    O(2 ^ N)     HORRIBLE
    =     Factorial      O(N!)        WTF
    =

What these would equal given the (N) number of items

    =
    =                N = 5            10             20             30
    =     -----------------------------------------------------------------------
    =     O(1)           1            1              1              1
    =     O(log N)       2.3219...    3.3219...      4.3219...      4.9068...
    =     O(N)           5            10             20             30
    =     O(N log N)     11.609...    33.219...      84.638...      147.204...
    =     O(N ^ 2)       25           100            400            900
    =     O(2 ^ N)       32           1024           1,048,576      1,073,741,824
    =     O(N!)          120          3,628,800      2,432,902,0... 265,252,859,812,191,058,636,308,480,000,000
    =

 It is important to note that data structures may be good at one action but
 bad at another.
 
    =
    =                            Accessing    Searching    Inserting    Deleting
    =    -------------------------------------------------------------------------
    =                  Array     O(1)         O(N)         O(N)         O(N)
    =            Linked List     O(N)         O(N)         O(1)         O(1)
    =     Binary Search Tree     O(log N)     O(log N)     O(log N)     O(log N)
    =

### DSA Questions **-**

Helper link (https://dynalist.io/d/wMhagOjScrKMaPtSti0tiJZk)

- Arrays
  - Pair Sum
    - Question
      - Given an array of integers and a target sum
      - Return pairs in the array which on addition, matches the target sum
    - Uses
      - Two pointers approach
        - Sort the array
        - Keep two pointers `startIndex` & `endIndex` one at start and one at end
        - Run a while loop which will run until `startIndex` is less than `endIndex`
        - Sum both the values at start and end index
        - If the sum is 0, those values are the pair
        - If the sum is less than required sum, increment startIndex
        - If the sum is greater than the required sum, decrement endIndex 
      - Hashmaps
        - Loop through the array
        - On every iteration, check if the number we are on, if adding this in the number (can get by  `currentNum - sum` and extract the value against this key in hashmap) which we have already seen (this will be maintained in the hashmap) is equal to the sum, then its a pair and can return OR push it in a results array
        - If the number doesnt match, store that number (as key) along with its index (as value) in the hashmap 
    - Example
      - Two pointers approach (Complexity: O(n))
        
    	    const nums = [1, 2, 3, 4, 6, 7];
            const goal = 6;
          
            function twoSum(nums, goal) {
              let result = [];
              let start = 0;
              let end = nums.length - 1;

              while (start <= end) {
                const curr = nums[start] + nums[end];

                if (curr > goal) {
                  end -= 1;
                } else if (curr < goal) {
                  start += 1;
                } else {
                  end -= 1;
                  start += 1;
              result.push([start, end]);
                }
              }

              return result;
            }

    	    console.log(twoSum(nums, goal));
        
      - Hasmaps (Complexity: O(n))

            const twoSum = function(nums, target) {
              const hash = {}; // Stores seen numbers: {seenNumber: indexItOccurred}
              for (let i = 0; i < nums.length; i++) { // loop through all numbers
                const n = nums[i]; // grab the current number `n`.
                if (hash[target - n] !== undefined) { // check if the number we need to add to `n` to reach our target has been seen:
                  return [hash[target - n], i]; // grab the index of the seen number, and the index of the current number
                }
                hash[n] = i; // update our hash to include the. number we just saw along with its index.
              }
              return []; // If no numbers add up to equal the `target`, we can return an empty array
            }

            console.log(twoSum([1, 2, 3], 5)); // [1, 2]

  - Overlapping Intervals
    - Question
      - Given a 2D array where each array/set/tuple is a pair of intervals
      - Merge the overlapping intervals
    - Uses
      - Sorting
        - Sort the array by checking every 1st index of the nested arrays
        - Maintain a results array and the last item/nested array
        - Loop through the main array
        - if the value on the first index of current is greater than the value on the last's 1st index, OR we dont have a last, set the last as current and then push the last in the result
        - Else update the 1st index of last by setting 1st index of the current to 1st index of the last
    - Example (Complexity O(nLogn) -> O(logn) for sort and O(n) for merging)

          function merge(ranges) {
            var result = [], last;

            ranges.forEach(function (r) {
              if (!last || r[0] > last[1])
                result.push(last = r);
              else if (r[1] > last[1])
                last[1] = r[1];
            });

            return result;
          }

          r = [[10, 20], [19, 40], [40, 60], [70, 80]];
          console.log(merge(r)); // [[10,60], [70,80]]

  - Sort 0 1 2
    - Question
      - Sort an array of 0's, 1's and 2's
      - Space complexity should be constant O(1) and time sequential O(n)
    - Uses
      - Dutch National Flag Algorithm
        - Keep 3 indexes, low=0, mid=0 and high=arr.length -1
        - Loop until mid <= high
        - while in loop, if arr[mid] equals 0, increment low and mid and then swap the values at low and mid
        - If arr[mid] equals 2, decrement high and then swap values at mid and high
        - If arr[mid] equals 1, increment mid 
    - Example
      - Dutch National Flag Algorithm (Complexity time: O(n) and space O(1))

            let swap = (arr, first, second) => {
              [arr[first], arr[second]] = [arr[second], arr[first]];
            }

            //Solution
            let dutchNatFlag = (arr) => {
              let low = 0;
              let mid = 0;
              let high = arr.length - 1;

              //To sort in ascending order
              while (mid <= high) {
                if (arr[mid] === 0) { 
                  swap(arr, low++, mid++);
                } else if (arr[mid] === 2) {
                  swap(arr, mid, high--);
                } else if (arr[mid] === 1) {
                  mid++;
                }
              }

              return arr;
            }

            let arr = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1]
            console.log(dutchNatFlag(arr)) // [0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2]

  - Search in rotated sorted array
    - Question
      - Search the number in a rotated sorted array
      - Time complexity should be O(log n)
    - Uses
      - Binary Search (Modified)
        - First find the pivot of the rotated array (i.e. index of greatest number whose next is smaller than it)
          - Create a function findPivot which takes the arr, low (0 initially), high (arr.length - 1 initially)
          - Check for base cases, If low is greater than high, return -1 as no pivot and array is not rotated
          - If high equals low, return low
          - Then find mid by adding low and high and then dividing by 2 and flooring it
          - Now check if value in arr at mid is greater than value in arr at mid + 1, then return mid, the pivot
          - If value in arr at mid is less than value in arr at mid - 1, then return mid - 1, the pivot
          - If value in arr at low is greater than or equal to value in arr at mid, then return recurred findPivot(arr, low, mid - 1)
          - Else, return recurred findPivot(arr, mid + 1, high)
        - Implement a mehtod which will do binarySearch
          - Create a function which will take the arr in which to find, low index, high index and item to search
          - If low is greater than high, return -1, i.e. not found
          - Find mid by adding low and high then divide by 2
          - If key equals value in arr at mid, then return mid (as we have to return index)
          - If key is greater than value in arr at mid, then return recurred binarySearch(arr, mid + 1, high, keyToSearch)
          - Else return recurred binarySearch(arr, low, mid - 1, keyToSearch)
        - If pivot is -1, means array is not rotated so call binary search with binarySearch(arr, 0, arr.length - 1, keyToSearch)
        - If pivot found, first check if value in arr at pivot is the value to search, if yes, simpy return pivot w/o binarySearch
        - If value in arr at 0 is less than equal to key, return binarySearch(arr, 0, pivot -1, keyToSearch)
        - Else return binarySearch(arr, pivot + 1, arr.length - 1, keyToSearch)
    - Example

          function binarySearch(arr, low, high, key){
            if (high < low)
              return -1;

            let mid = Math.floor((low + high) / 2);
            if (key == arr[mid])
              return mid;

            if (key > arr[mid])
              return binarySearch(arr, (mid + 1), high, key);

            return binarySearch(arr, low, (mid - 1), key);
          }

          function findPivot(arr, low, high){
            if (high < low)
              return -1;
            if (high == low)
              return low;

            let mid = Math.floor((low + high) / 2);
            if (mid < high && arr[mid] > arr[mid + 1])
              return mid;

            if (mid > low && arr[mid] < arr[mid - 1])
              return (mid - 1);

            if (arr[low] >= arr[mid])
              return findPivot(arr, low, mid - 1);

            return findPivot(arr, mid + 1, high);
          }
          
          function pivotedBinarySearch(arr, n, key){
            let pivot = findPivot(arr, 0, n - 1);

            if (pivot == -1)
              return binarySearch(arr, 0, n - 1, key);

            if (arr[pivot] == key)
              return pivot;

            if (arr[0] <= key)
              return binarySearch(arr, 0, pivot - 1, key);

            return binarySearch(arr, pivot + 1, n - 1, key);
          }


          let arr = [5, 6, 7, 8, 9, 10, 1, 2, 3];
          let keyToFind = 3
          console.log(pivotedBinarySearch(arr, arr.length, keyToFind))

  - Smallest sub array with K distinct elements
    - Question
      - Find find range in array with k distinct elements
    - Uses
      - Sliding Window Algorithm
    - Example (Complexity time: O(n) and space O(k))

          function minRange(arr,n,k) {
            // Initially left and right side is -1 and -1,
            // number of distinct elements are zero and
            // range is n.
            let l = 0, r = n;

            // Initialize right side
            let j = -1;

            let hm = new Map();

            for (let i = 0; i < n; i++) {
              while (j < n) {
                // Increment right side.
                j++;

                // If number of distinct elements less
                // than k.
                if (j < n && hm.size < k) {
                  if (hm.has(arr[j]))
                    hm.set(arr[j],
                          hm.get(arr[j]) + 1);
                  else
                    hm.set(arr[j],1);
                }
                // If distinct elements are equal to k
                // and length is less than previous length.
                if (hm.size == k && ((r - l) >= (j - i))) {
                  l = i;
                  r = j;
                  break;
                }
              }

              // If number of distinct elements less
              // than k, then break.
              if (hm.size < k)
                break;

              // If distinct elements equals to k then
              // try to increment left side.
              while (hm.size == k) {
                if (hm.has(arr[i]) && hm.get(arr[i]) == 1)
                  hm.delete(arr[i]);
                else
                  if (hm.has(arr[i]))
                    hm.set(arr[i],hm.get(arr[i]) - 1);

                // Increment left side.
                i++;

                // It is same as explained in above loop.
                if (hm.size == k && (r - l) >= (j - i)) {
                  l = i;
                  r = j;
                }
              }
              if (hm.has(arr[i]) && hm.get(arr[i]) == 1)
                hm.delete(arr[i]);
              else
                if(hm.has(arr[i]))
                  hm.set(arr[i],hm.get(arr[i]) - 1);
            }

            if (l == 0 && r == n)
              console.log("Invalid k");
            else
              console.log(l + " " + r);
          }
              
              
          // Driver code
          let arr=[1, 1, 2, 2, 3, 3, 4, 5];
          let k = 3;
          minRange(arr, arr.length, k);

- Multi-dimensional arrays
  - Search In Row Wise And Column Wise Sorted Matrix
    - Uses
      - Binary Search
    - Question
    - Example
  - Inplace Rotate Matrix By 90 degree
    - Uses
      - Adhoc Problem
    - Question
    - Example
  - Matrix Median
    - Uses
      - Binary Search
    - Question
    - Example

- Strings
  - Longest Substring Without Repeating Characters
    - Question
      - Given a string, find length of longest sub string w/o a repeating character
    - Uses
      - Sliding Window
        - Maintain a current_string which would be the substring w/o repeating chars
        - Loop through the str length
        - On each iteration, check if current char is in the current_string, if yes, slice the current_string to only contain the characters untile the first repeated ones + 1 index
        - Then append the current char to the current_string and update the lengthOfSubstr to the max of previous lengthOfSubstr and current_string.length 
      - Hashmap
        - Maintain a hashmap which contains the visited chars of string as keys and their indexes as their values
        - Also maintain an index start used to determine already visited chars
        - Also maintain a lengthOfLongestSubstr
        - Iterate over the string
        - On each iteration, check if the the current char of string is a key in hashmap, if yes, update the start with the currentString value + 1
        - Then, update the hasmap's key i.e. the currentString char and its value as current index
        - Also update the lengthOfLongestSubstr by taking max of lengthOfLongestSubstr and (i - start + 1)
    - Example
      - Sliding Window (Time O(n^2 cuz substring is a loop))

            function lengthOfLongestSubstring(string) {
              var lengthOfSubstr = 0, current_string = "", i, char, pos;

              for (i = 0; i < string.length; i++) {
                char = string.charAt(i);
                pos = current_string.indexOf(char);
                if (pos !== -1) {
                  // cut "dv" to "v" when you see another "d"
                  current_string = current_string.substr(pos + 1);
                }
                current_string += char;
                lengthOfSubstr = Math.max(lengthOfSubstr, current_string.length);
              }
              return lengthOfSubstr;
            }

            console.log(lengthOfLongestSubstring("dvdf")); // 3

      - Hashmap (Time O(n), Space O(1))

            function lengthOfLongestSubstring(str) {
              if (!str.length || typeof str !== 'string') return 0;

              if (str.length == 1) return 1;
              let hashTable = {};
              let longestSubstringLength = 0;
              let start = 0;
              for (let i = 0; i < str.length; i++) {
                console.log('hashTable: ', hashTable)
                console.log('hashTable[str[i]]: ', hashTable[str[i]])
                if (hashTable[str[i]] && hashTable[str[i]] >= start) {
                  start = hashTable[str[i]] + 1;
                }
                hashTable[str[i]] = i;
                longestSubstringLength = Math.max(longestSubstringLength, (i - start + 1))
              }
              return longestSubstringLength;
            }

            console.log(lengthOfLongestSubstring("dvdf"));

  - Anagram Difference
    - Question
      - Given 2 strings of equal lengths, required to return the minimum number of manipulations required to make the strings anagram, meaning the strings will have same characters and the sequence can differ
    - Uses
      - Hashmap
        - Initialize a total count of manipulations
        - Initialize a charMap with the all the characters of english alphabets as keys and 0 as their value
        - Loop through the first string and at each iteration, set the charMap's key i.e. current string char and increase its value by one
        - Loop through the second string and at each iteration, set the charMap's key i.e. current string char and decrease the value by one
        - With that, the map would have 0's against the characters that match and some number against chars which dont match in both arrays
        - Finally loop through the map's keys and count the values against each key (take absolute while counting to ignore '-' which basically shows count of second array)
        - Return count/2 as we have sum of counts in both strings and we need manipulation on one
    - Example
        - Hashmap (Time Complexity O(n), Auxilary O(1))
            
              function countManipulations(s1, s2) {
                let count = 0;

                let charArr = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];
                let charMap = {};
                
                for (var i of charArr) {
                  charMap[i] = 0
                }
                  
                for (let i = 0; i < s1.length; i++) {
                  charMap[s1[i]] = charMap[s1[i]] + 1
                }

                for (let i = 0; i < s2.length; i++) {
                  charMap[s2[i]] = charMap[s2[i]] - 1
                }
                
                for (let i in charMap) {
                  if (charMap[i] !== 0) {
                    count += Math.abs(charMap[i]);
                  }
                }
                
                return count / 2;
              }

              console.log(countManipulations('except', 'accept'))

  - Shortest substring with all characters
    - Question
      - Find the smallest window in a string containing all characters of another string
    - Uses
      - Two Pointers and Sliding Window
        - Initialize a map with all characters/alphabets or an array with all character codes
        - Initialize 2 pointers i and j and start incrementing j and on each iteration, if the value on j is not in the map, increase it and increase the count variable, dont increase the count var if value already exists
        - If the count is 0, iterate now using i until the count is zero
        - While iterating, keep track of start index of the result window and update it if already seen the character
    - Example 
      - Sliding Window (Time Complexity: O(n), Auxiliary Complexity: O(1))

            function minWindow(s,t) {
              let m = new Array(256);
              for (let i = 0; i < 256; i++) {
                m[i] = 0;
              }
              
              // Length of ans
              let ans = Number.MAX_VALUE;

              // Starting index of ans
              let start = 0;
              let count = 0;

              // Creating map
              for (let i = 0; i < t.length; i++) {
                if (m[t[i].charCodeAt(0)] == 0) {
                  count++;       
                }

                m[t[i].charCodeAt(0)]++;
              }

              // References of Window
              let i = 0;
              let j = 0;

              // Traversing the window
              while (j < s.length) {

                // Calculations
                m[s[j].charCodeAt(0)]--;

                if (m[s[j].charCodeAt(0)] == 0) {
                  count--;       
                }

                // Condition matching
                if (count == 0) {
                  while (count == 0) {

                    // Sorting ans
                    if (ans > j - i + 1) {
                      ans = Math.min(ans, j - i + 1);
                      start = i;
                    }

                    // Sliding I
                    // Calculation for removing I
                    m[s[i].charCodeAt(0)]++;

                    if (m[s[i].charCodeAt(0)] > 0) {
                      count++;
                    }

                    i++;
                  }
                }
                j++;
              }
              if (ans != Number.MAX_VALUE) {
                return (s).join("").substring(start, (start + ans));
              }
              else {
                return "-1";   
              }
            }

            console.log(minWindow('adobecodebanc'.split(''), 'abc'.split(''))) // "banc"

  - Minimum operations to make strings equal
    - Uses
      - Hashmap
    - Question
    - Example

- Recursion & Backtracking
  - Print Permutations Of String
    - Question
      - You are given an input string 'S'. Your task is to find and return all possible permutations of the input string
    - Uses
      - Recursion & Backtracking
        - Iterate over the string
        - At each iteration, extract the currentChar at i and the remainingString without that currentChar
        - Now join the currentChar with each permutation of the remaingString which is extracted by calling the method recursively and push each in a results array
    - Example
      - Recursion & Backtracking (TC -> O(n!))
        
            function permut(string) {
              if (string.length < 2) return string; // This is our break condition

              var permutations = []; // This array will hold our permutations
              for (var i = 0; i < string.length; i++) {
                var char = string[i];

                // Cause we don't want any duplicates:
                if (string.indexOf(char) != i) // if char was used already
                  continue; // skip it this time

                var remainingString = string.slice(0, i) + string.slice(i + 1, string.length); //Note: you can concat Strings via '+' in JS

                for (var subPermutation of permut(remainingString)) {
                  permutations.push(char + subPermutation)    
                }
              }
              return permutations;
            }

            console.log(permut('bad')) // ["bad", "bda", "abd", "adb", "dba", "dab"]

  - Return Subsets Sum to K
    - Uses
      - Sorting
    - Question
    - Example
  - Sudoku
    - Uses
      - 2d array backtracking
    - Question
    - Example
  - Replace ‘O’ with ‘X’
    - Uses
      - 2d array backtracking
    - Question
    - Example
  - Reach Destination
    - Uses
    - Question
    - Example

- Linked List
  - Merge Two Sorted Linked List
    - Uses
    - Question
    - Example
  - Detect And Remove Loop
    - Uses
    - Question
    - Example
  - Reverse List In K Groups
    - Uses
    - Question
    - Example
  - Intersection Of Two Linked List
    - Uses
    - Question
    - Example
  - Sum Between Zeros
    - Uses
    - Question
    - Example

- Stacks & Queues
  - Implement Stack Using Linked List
    - Uses
    - Question
    - Example
  - Next Greater Element
    - Uses
    - Question
    - Example
  - Implement Queue Using Stack
    - Uses
    - Question
    - Example
  - LRU Cache Implementation
    - Uses
    - Question
    - Example
  - Evaluation Of Post Fix Expression
    - Uses
    - Question
    - Example

- Binary Trees
  - Binary Tree From Parent Array
    - Uses
    - Question
    - Example
  - Maximum Sum Path From Root To Leaf
    - Uses
    - Question
    - Example
  - Print Node At Distance K From Given node
    - Uses
    - Question
    - Example
  - Maximum Width In Binary Tree
    - Uses
      - Hashmap
    - Question
    - Example
  - Time To Burn Tree
    - Uses
    - Question
    - Example

- BST
  - Delete In BST
    - Uses
    - Question
    - Example
  - Sorted Linked List To Balanced BST
    - Uses
    - Question
    - Example
  - Kth Smallest Element In BST
    - Uses
    - Question
    - Example
  - Binary Tree To BST
    - Uses
    - Question
    - Example
  - Pair Sum in BST
    - Uses
    - Question
    - Example

- Priority Queues & Heaps
  - Running Median
    - Uses
    - Question
    - Example
  - Convert Min Heap To Max Heap
    - Uses
    - Question
    - Example
  - Kth Largest Element In Unsorted Array
    - Uses
    - Question
    - Example
  - K Most Frequent Words
    - Uses
    - Question
    - Example
  - Last Stone Weight
    - Uses
    - Question
    - Example

- Graphs
  - Is Graph A Tree?
    - Uses
    - Question
    - Example
  - M Coloring Problem
    - Uses
    - Question
    - Example
  - Snake And Ladder
    - Uses
    - Question
    - Example
  - Shortest Path In Unweighted Graph
    - Uses
    - Question
    - Example
  - Smallest sub array with K distinct elements
    - Uses
    - Question
    - Example
  - Alien Dictionary 
    - Uses
    - Question
    - Example

- Dynamic Programming
  - Edit Distance
    - Uses
    - Question
    - Example
  - Rod Cutting Problem
    - Uses
    - Question
    - Example
  - Longest Palindromic Substring
    - Uses
    - Question
    - Example
  - Knapsack
    - Uses
    - Question
    - Example
  - Palindrome Partioning
    - Uses
    - Question
    - Example

- Misc
  - Implement Hashmap
    - Uses
    - Question
    - Example
  - Implement Trie
    - Uses
    - Question
    - Example
  - Implement Deque
    - Uses
    - Question
    - Example
  - Excel sheet cell references
    - Question
      - Write a program or function that generates and prints Excel sheet cell references in the format A1, B1, C1, ..., Z1, AA1, AB1, AC1, ..., ZZ1, AAA1, AAB1, AAC1, and so on. Given a positive integer 'n', your program should generate and print the first 'n' cell references of an Excel sheet.
    - Uses
      - Base conversion
        - Run a for loop on the count given in question
        - On each iteration, get the cell number from method `generateExcelCellReferences` by passing current iteration (+1 if loop starting from 0) and print it
        - In `generateExcelCellReferences`, initialize a string `letters` containing all 26 english alphabets
        - Also initialize an empty array `result` which would keep the cell reference letters which we can join to make a string before returning cell ref
        - Now run a loop until the `n` (index parameter passed) is greater than 0
        - In loop iteration, get `remainder` by taking modulus of `n-1` (minus 1 cuz we want to find alphabet by index in `letters` string and index start at 0) to 26 i.e. our base in this base-26 problem
        - now update the `result` array by getting the alphabet by using `remainder` as index on `letters` and adding it as first element of `result` array
        - Now update the `n` for next iteration, by dividing `n-1` by 26 and flooring it
        - Finally outside the loop, return the `result` array by joining it to make it a string and adding `'1'` to it because it would be the row ref (we are dealing in only one row) 
    - Example

          function generateExcelCellReferences(n) {
            const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            const result = [];

            while (n > 0) {
              let remainder = (n - 1) % 26; // Get the remainder after dividing by 26
              result.unshift(letters[remainder]); // Add the letter to the front of the result array
              n = Math.floor((n - 1) / 26); // Update n for the next iteration
            }

            return result.join('') + '1'; // Combine the letters and add '1' to form the cell reference
          }

          function printExcelCellReferences(count) {
            for (let i = 1; i <= count; i++) {
              const cellReference = generateExcelCellReferences(i);
              console.log(cellReference);
            }
          }

          const n = 10;
          printExcelCellReferences(n);
