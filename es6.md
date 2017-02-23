**ES2015 (ES6)**

**Arrows**

They share the this of surrounding code

() =&gt; { }

**Classes**

Supports inheritance, super calls, instance and static methods and constructors.

class Cat extends Animal {

}

**Enhanced Object Literals**

Can use shorthand

var obj = {

    \_\_proto\_\_: protoObj,

    singleAttr,

    methodName() {

        return super.methodName();

    }

}

**Template strings**

`This is a template

string.`

`Template string with a ${variable} included`

**Deconstructing**

// list matching

var [a, ,b] = [1,2,3];

a === 1;

b === 3;

// object matching

var { op: a, lhs: { op: b }, rhs: c }

       = getASTNode()

// object matching shorthand

// binds `op`, `lhs` and `rhs` in scope

var {op, lhs, rhs} = getASTNode()

// Can be used in parameter position

function g({name: x}) {

  console.log(x);

}

g({name: 5})

// Fail-soft destructuring

var [a] = [];

a === undefined;

// Fail-soft destructuring with defaults

var [a = 1] = [];

a === 1;

// Destructuring + defaults arguments

function r({x, y, w = 10, h = 10}) {

  return x + y + w + h;

}

r({x:1, y:2}) === 23

**Default, Rest and Spread**

// default

function f(x, y=12) {

// unknown number of values

// y is an array

function f(x, ...y) {

// Pass each elem of array as argument

f(...[1,2,3]) == 6

**Let + Const**

let is the new var, and const can only be defined and set once. Cannot be used before it is assigned.

let x = &quot;string&quot;;

cont y = 45;

**Iterators + For..Of**

The for...of loop has been added, to loop through iterable objects (arrays, map. Set, string, typed array, etc)

for (var n of fibonacci) {

    console.log(n);

}

**Generators**

Creates a generator function, which returns a Generator object.

Calling a generator function does not execute its body immediately. When the iterators next() method is called, the functions body is executed until the first yield expression.

function\* findAnimal(args) {

     ....

}

**Unicode**

Full Unicode support.

**Modules**

Runtime behaviour is defined by the host-defined default loader.

export function() {

    ....

}

import {member} from &quot;lib/math&quot;;

**Map + Set + WeakMap + WeakSet**

Efficient data structures for common algorithms. WeakMaps provides leak-free object-key&#39;d side tables.

// sets

var s = new Set();

s.add(&quot;hello&quot;).add(&quot;goodbye&quot;).add(&quot;hello&quot;);

s.has(&quot;hello&quot;) === true;

// maps

var m = new Map();

m.set(&quot;hello&quot;, 42);

m.get(&quot;hello&quot;);

var ws = new WeakSet();

ws.add({ data: 42 });

// Because the added object has no other references, it will not be held in the set

// Weak maps

var wm = new WeakMap();

wm.set(s, { extra: 42 });

**Math + Number + String + Object APIs (limited babel support)**

Number.EPSILON

Number.isInteger(Infinity) // false

Number.isNaN(&quot;NaN&quot;) // false

Math.acosh(3) // 1.762747174039086

Math.hypot(3, 4) // 5

Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

&quot;abcde&quot;.includes(&quot;cd&quot;) // true

&quot;abc&quot;.repeat(3) // &quot;abcabcabc&quot;

Array.from(document.querySelectorAll(&quot;\*&quot;)) // Returns a real Array

Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior

[0, 0, 0].fill(7, 1) // [0,7,7]

[1,2,3].findIndex(x =&gt; x == 2) // 1

[&quot;a&quot;, &quot;b&quot;, &quot;c&quot;].entries() // iterator [0, &quot;a&quot;], [1,&quot;b&quot;], [2,&quot;c&quot;]

[&quot;a&quot;, &quot;b&quot;, &quot;c&quot;].keys() // iterator 0, 1, 2

[&quot;a&quot;, &quot;b&quot;, &quot;c&quot;].values() // iterator &quot;a&quot;, &quot;b&quot;, &quot;c&quot;

Object.assign(Point, { origin: new Point(0,0) })

**Promises**

A library for asynchronous programming. A value that may be available in the future.

**Reflect API**



**Limited support in Babel**

**Module Loaders**



**Proxies**



**Symbols**



**Subclassable Built-ins **

Can extend classes such as Array, Date, Elements.

**Binary and Octal Literals**
