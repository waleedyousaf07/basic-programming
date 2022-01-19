# basic-programming

## Introduction:

A repo covering basics of programming concepts specifically JS.
<br/><br/>

## Core

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

### HTML 5

- iFrames
- New elements
  - <video controls preload><source src="video.mp4" type="video/ogg; codecs='vorbis, theora'" /></video>
  - <audio autoplay="autoplay" controls="controls"><source src="file.mp3" /></audio>
  - <nav><a href="/html/">HTML</a></nav>
  - <header><img src="company-logo.png" /><nav>...</nav></header>
  - <canvas></canvas>
  - <footer>...</footer>
  - <figure><img src="image/image-1.jpg" alt="About ADMEC" />
      <figcaption><p>This is our institute </p></figcaption>
    </figure>
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

### JS Variable declartors

let, const, var

### Var

Var declarations are globally scoped or function/locally scoped. They can be re-declared and updated. They are hoisted and can be used if declared after getting called.

### Const

Cannot be reinialized. Has a block level scope. Primitive types cannot be updated/re-assigned/re-declared but objects and arrays can. Every const declaration, therefore, must be initialized at the time of declaration.

Const create a variable name binding so that name cannot be re-inialized but the properties can. So its mutable. They cant be hoisted. 

### Let

Can be re initialized. Has a block level scope. It cannot be redeclared withing its scope.

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

### Time and Space Complexity (BigO) (https://github.com/jamiebuilds/itsy-bitsy-data-structures/blob/master/itsy-bitsy-data-structures.js) **-**

### MVC

It is a design pattern. The goal is divide large application into specific sections each having their own purpose.

User requesting a specific page from the server. The server responds to a specific controller. 

Controller: `Handles the entire request` from the client. And will tell the rest of the server what to do with the request. It acts as a middleman b/w model and view. It should not contain much code. 

Model: After receiving the request, the controller asks the model to get the data. Model is `responsible for all of the data logic` of the request. It interacts with the DB and handles all CRUD saving and other data operations. The controller shouldnt interact with the data it should always ask the model. Model doesnt need to do anything on failure or success, controller will handle that.

View: After the model sends the data to controller, then controller sends the data to view to `render` and view is only concerned for displaying the data its feeded with. The view will send the HTML (or so) back to controller which then is served to the user.

Important to note is that `model and view never interact` with each other. Presentation and Logic is completely separate.

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

### OOP

- Class (`class className`)

- Object (`new ClassName(params)`)

- Inheritance (`extends`)

- Polymorphism

  Polymorphism -> `Many-forms`. Can have a same function in parent and a class which is `inherited` and if we `override` in child class(function overriding) then the parent's function has 2 forms.

- Abstraction

  It is hiding the implementation and only showing the functionality or essentials.

  Not allowing the user to access a class's variable or function. Instead, let other local functions of the class calculate and use those methods and properties.

- Encapsulation

  It is wrapping up the data and methods under a single unit.

  Properties and methods are private.

  It is binding of data to functions.

  A mechanism of `restriciting direct access` to some of the object's components. It also bundles methods which operate on that data. Its required for:

  - Security, controlled access
  - Hide implementation and expose behaviour
  - Loose coupling - modify the implementation anytime

  `Getters and setter methods` are used to get those objects/properties. 

- Association

  If two classes in a model need to communicate with each other, there must be a link between them, and that can be represented by an association (connector).

  Aggregation and Composition are subsets of association meaning they are specific cases of association.

- Aggregation

  Aggregation implies a relationship where the child can exist independently of the parent. Example: Class (parent) and Student (child). Delete the Class and the Students still exist.

- Composition 

  Composition implies a relationship where the child cannot exist independent of the parent. Example: House (parent) and Room (child). Rooms don't exist separate to a House.

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

### Closure

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

### Imediately Invoked Functions

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

### Hoisting

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

There are two callback queues, one for macrotasks and one for microtasks (usually for promises) and first micro runs and then macro runs

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

## Data Structures
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

## Algos

## Javascript
- Classes
- Functions
- Inheritence (`extends`)

  Inherits properties/functions from its parent class

- Interfaces (`has`)

  Defines a shape objects/classes can take

- Abstraction
- JS methods
  - forEach
  - map
  - shift

  It removes the first item and returns that first item. It mutates the array
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

- Shallow/Deep Copies

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

- Throttling
  
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

- Debouncing
  
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

- Pure Functions

  When a function calculates its output from using other than its parameters as an input. When its not completly and only dependant on its inputs. 

  A pure function is a function which,

  - Given the same inputs, always returns the same output
  - Has no side-effects (only changes to local scope are allowed. Read operations are okay. Some read operations have side effects like `Math.random()` which generates new number by changing the Math's reading position and other methods which involves reading from an external sensor that involves a "take measurement" command.) 

  A pure function is `Referentially Transparent`. Referential Transparency, roughly, means that you can replace the call to the function with its return value or vice versa at any point in the program, without changing the meaning of the program.

- HOCs

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

- lodash

## ES6

- Arrow funcs
- let, const

## Git/GitHub

## Middlewares

Software that enables one or more kinds of communication or connectivity between two or more applications or application components in a distributed network.

## APIs
- CRUD
- Axios

  Used to make requests to an API endpoint

- REST Arch & RestFul APIs

## Linting
- ESLint

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

## Test Cases
- Unit Tests
  - JEST
  - Enzymes
- Integration Tests

## JWTs

## JSON Server
 - ### <b>Installation:</b>

    To install, go in any project folder or install it globally using `-g` like

        npm install -g json-server

    To run, execute command

        json-server --watch db.json --port 3001

    where `db.json` can have static json

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

## Sockets
- sockets.io
