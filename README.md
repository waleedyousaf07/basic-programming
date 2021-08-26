# basic-programming

## Introduction:

A repo covering basics of programming concepts.
<br/><br/>

## Core

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

### Polymorphism

### Const

Const create a variable name binding so that name cannot be re-inialized but the properties can. So its mutable.

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

### Binding

### Asynchronous

### Synchronous

### Async await

### Closure

When an inner function has access to outer function's variables along with its own and global variables.

They are functions with preserved data.

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

### Hoisting

### Memory 

### Heap

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

### Class & Prototypal Inheritance

### Promise

### Anonymous Functions

They are the functions which dont have a name.

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
    one is the `current` of this iteration, where and second parameter of reduce
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
  
  Delaying function execution. Like search after 500ms

- Debouncing
  
  Prevent the event trigger from being fired too often

- Pure Functions

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

## APIs
- CRUD
- Axios
- REST Arch & RestFul APIs

## Linting
- ESLint

## CSS/SASS
- CSS
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
