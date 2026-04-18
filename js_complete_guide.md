# Complete JavaScript Guide for Python Developers
### Learn JS to control your browser from your Python backend

---

> **How to use this file:**
> Read one section. Write the code examples yourself. Run them in browser console. Then move to next section.
> Never copy paste. Always type manually.

---

# PART 1 — JavaScript Basics

---

## Chapter 1 — How JavaScript Runs

Before writing any code, understand where JS actually runs.

Python runs in your terminal. JS runs in two places:
- **Browser** — this is what you care about
- **Node.js** — terminal (you don't need this for your goal)

### How to run JS right now

Open any browser. Press **F12**. Click **Console** tab. Type:
```javascript
console.log("hello")
```
Press Enter. You just ran JavaScript.

This console is your best friend. Use it constantly to test small pieces of code.

### Linking JS to HTML

Create a file called `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>My App</title>
</head>
<body>
    <h1 id="title">Hello</h1>

    <!-- Always put script at bottom of body -->
    <script src="app.js"></script>
</body>
</html>
```

Create `app.js` in same folder:
```javascript
console.log("JS is running")
```

Open `index.html` in browser. Press F12. Console tab shows "JS is running".

Why put script at bottom? Because HTML loads top to bottom. If script is at top, it runs before HTML elements exist and can't find them.

---

## Chapter 2 — Variables

### var, let, const

Python has one way to make a variable. JS has three. Here's the simple rule:

```javascript
// const — use this by default
// value cannot be reassigned
const name = "Aman"
const age = 20

// let — use when you need to reassign
let count = 0
count = 1       // this works
count = 2       // this works

// var — never use this
// it has confusing behavior, old JS only
var x = 5       // avoid completely
```

**Simple rule: always use `const`. Switch to `let` only when you need to change the value.**

```javascript
// Real example
const API_URL = "http://localhost:5000"    // never changes → const
let isLoading = false                       // changes → let
let users = []                             // will be reassigned → let
```

### Data Types

```javascript
// String — text
const name = "Aman"
const city = 'Nashik'           // single quotes also work
const greeting = `Hello ${name}`  // template literal — like Python f-string

// Number — no int/float difference in JS
const age = 20
const price = 99.5
const negative = -10

// Boolean
const isLoggedIn = true
const hasError = false

// null — intentional empty value (you set it)
const data = null

// undefined — variable exists but no value assigned
let result
console.log(result)    // undefined

// Array — like Python list
const fruits = ["apple", "banana", "mango"]

// Object — like Python dict
const user = {
    name: "Aman",
    age: 20,
    isStudent: true
}
```

### Checking types

```javascript
typeof "hello"      // "string"
typeof 42           // "number"
typeof true         // "boolean"
typeof null         // "object"  ← weird JS quirk, null is not an object
typeof undefined    // "undefined"
typeof []           // "object"
typeof {}           // "object"

// Better way to check array
Array.isArray([1,2,3])   // true
Array.isArray("hello")   // false
```

### JS vs Python — differences that will confuse you

```javascript
// 1. Equality — always use === in JS
5 == "5"     // true  ← type coercion, dangerous
5 === "5"    // false ← strict equality, safe
5 !== "5"    // true  ← not equal (strict)

// 2. Truthy and falsy
// These are all falsy in JS (behave like False):
false
0
""           // empty string
null
undefined
NaN

// Everything else is truthy:
"hello"      // truthy
1            // truthy
[]           // truthy — empty array is truthy! different from Python
{}           // truthy — empty object is truthy!

// 3. null vs undefined
let a = null        // you explicitly said "no value"
let b               // JS says "no value assigned yet"

// 4. console.log instead of print
console.log("hello")
console.log("name:", name, "age:", age)
console.log({ name, age })    // logs object nicely
```

---

## Chapter 3 — Strings

```javascript
const name = "Aman"
const city = "Nashik"

// Length
name.length         // 4

// Uppercase / lowercase
name.toUpperCase()  // "AMAN"
name.toLowerCase()  // "aman"

// Check if includes
name.includes("ma")     // true
name.startsWith("Am")   // true
name.endsWith("an")     // true

// Replace
"hello world".replace("world", "JS")   // "hello JS"

// Split — like Python split()
"one,two,three".split(",")    // ["one", "two", "three"]

// Trim — remove spaces
"  hello  ".trim()    // "hello"

// Slice — extract part
"hello".slice(0, 3)   // "hel"
"hello".slice(-2)     // "lo"

// Template literals — most important
const age = 20
const message = `My name is ${name} and I am ${age} years old`
// Can also do expressions inside:
const result = `Two plus two is ${2 + 2}`
const upper = `Name in caps: ${name.toUpperCase()}`

// Multi-line strings with template literals
const html = `
    <div>
        <h1>${name}</h1>
        <p>${city}</p>
    </div>
`
```

---

## Chapter 4 — Numbers and Math

```javascript
// Basic math
10 + 5    // 15
10 - 5    // 5
10 * 5    // 50
10 / 3    // 3.3333...
10 % 3    // 1  (remainder)
2 ** 3    // 8  (power — same as Python)

// Math object
Math.round(4.6)    // 5
Math.floor(4.9)    // 4
Math.ceil(4.1)     // 5
Math.abs(-10)      // 10
Math.max(1,5,3)    // 5
Math.min(1,5,3)    // 1
Math.random()      // random number between 0 and 1

// Random integer between 1 and 10
Math.floor(Math.random() * 10) + 1

// Convert string to number
parseInt("42")       // 42
parseFloat("3.14")   // 3.14
Number("99")         // 99
Number("hello")      // NaN — Not a Number

// Check if NaN
isNaN(Number("hello"))   // true

// Increment / decrement
let x = 5
x++    // x becomes 6
x--    // x becomes 5
x += 10   // x becomes 15
x -= 5    // x becomes 10
x *= 2    // x becomes 20
x /= 4    // x becomes 5
```

---

## Chapter 5 — Arrays

Arrays are extremely important because your Python backend sends JSON arrays constantly.

```javascript
// Create array
const fruits = ["apple", "banana", "mango", "orange"]
const numbers = [1, 2, 3, 4, 5]
const mixed = ["hello", 42, true, null]     // can mix types
const empty = []

// Access elements — 0 indexed like Python
fruits[0]     // "apple"
fruits[2]     // "mango"
fruits[-1]    // undefined ← JS doesn't support negative index like Python
fruits[fruits.length - 1]  // "orange" ← last element in JS

// Length
fruits.length   // 4

// Check if value exists
fruits.includes("banana")   // true
fruits.includes("grape")    // false

// Find index
fruits.indexOf("mango")     // 2
fruits.indexOf("grape")     // -1 (not found)
```

### Adding and removing

```javascript
const arr = [1, 2, 3]

// Add to end
arr.push(4)         // [1, 2, 3, 4]
arr.push(5, 6)      // [1, 2, 3, 4, 5, 6]

// Remove from end
arr.pop()           // removes 6, returns 6

// Add to start
arr.unshift(0)      // [0, 1, 2, 3, 4, 5]

// Remove from start
arr.shift()         // removes 0, returns 0

// Remove by index (splice)
arr.splice(1, 1)    // removes 1 element at index 1
// arr is now [1, 3, 4, 5]

// Splice to insert
arr.splice(1, 0, 99)  // at index 1, remove 0, insert 99
// arr is now [1, 99, 3, 4, 5]
```

### Array methods — the important ones

```javascript
const users = [
    { name: "Aman", age: 20, role: "developer" },
    { name: "Ravi", age: 25, role: "designer" },
    { name: "Priya", age: 22, role: "developer" },
    { name: "Kiran", age: 30, role: "manager" }
]

// forEach — loop through (like Python for loop)
users.forEach(user => {
    console.log(user.name)
})
// Aman, Ravi, Priya, Kiran

// map — transform each item, returns NEW array
const names = users.map(user => user.name)
// ["Aman", "Ravi", "Priya", "Kiran"]

const upperNames = users.map(user => user.name.toUpperCase())
// ["AMAN", "RAVI", "PRIYA", "KIRAN"]

// filter — keep items matching condition, returns NEW array
const developers = users.filter(user => user.role === "developer")
// [{ name: "Aman"... }, { name: "Priya"... }]

const adults = users.filter(user => user.age >= 22)
// [{ name: "Ravi"... }, { name: "Priya"... }, { name: "Kiran"... }]

// find — returns FIRST match (not array, just the item)
const aman = users.find(user => user.name === "Aman")
// { name: "Aman", age: 20, role: "developer" }

// findIndex — returns index of first match
const idx = users.findIndex(user => user.name === "Ravi")
// 1

// some — does at least one match? returns true/false
users.some(user => user.age > 28)    // true (Kiran is 30)
users.some(user => user.age > 50)    // false

// every — do ALL match? returns true/false
users.every(user => user.age > 18)   // true
users.every(user => user.age > 25)   // false

// reduce — combine all into single value
const numbers = [1, 2, 3, 4, 5]
const sum = numbers.reduce((total, num) => total + num, 0)
// 15

// sort — sorts in place (mutates original)
const nums = [3, 1, 4, 1, 5, 9]
nums.sort((a, b) => a - b)    // ascending: [1, 1, 3, 4, 5, 9]
nums.sort((a, b) => b - a)    // descending: [9, 5, 4, 3, 1, 1]

// sort by string property
users.sort((a, b) => a.name.localeCompare(b.name))

// join — array to string (like Python join)
["one", "two", "three"].join(", ")    // "one, two, three"
["one", "two", "three"].join("")      // "onetwothree"

// flat — flatten nested arrays
[1, [2, 3], [4, [5, 6]]].flat()      // [1, 2, 3, 4, [5, 6]]
[1, [2, 3], [4, [5, 6]]].flat(2)     // [1, 2, 3, 4, 5, 6]

// slice — copy portion (like Python slicing, doesn't mutate)
const arr = [1, 2, 3, 4, 5]
arr.slice(1, 3)    // [2, 3]
arr.slice(2)       // [3, 4, 5]
arr.slice(-2)      // [4, 5]  ← negative works here!
```

### Spread operator

```javascript
const a = [1, 2, 3]
const b = [4, 5, 6]

// Combine arrays
const combined = [...a, ...b]    // [1, 2, 3, 4, 5, 6]

// Copy array (new array, not reference)
const copy = [...a]

// Add item without mutating
const newArr = [...a, 4]         // [1, 2, 3, 4]

// Spread in function call
Math.max(...a)    // same as Math.max(1, 2, 3) → 3
```

### Destructuring arrays

```javascript
const fruits = ["apple", "banana", "mango"]

// Old way
const first = fruits[0]
const second = fruits[1]

// Destructuring
const [first, second, third] = fruits
// first = "apple", second = "banana", third = "mango"

// Skip items
const [, , third] = fruits
// third = "mango"

// Rest operator
const [head, ...rest] = fruits
// head = "apple", rest = ["banana", "mango"]

// Swap variables
let x = 1, y = 2
[x, y] = [y, x]
// x = 2, y = 1
```

---

## Chapter 6 — Objects

Objects are how JSON data from your Python backend arrives in JS.

```javascript
// Create object
const user = {
    name: "Aman",
    age: 20,
    city: "Nashik",
    isStudent: true,
    courses: ["Python", "JavaScript"],
    address: {
        street: "MG Road",
        pincode: "422001"
    }
}

// Access — two ways
user.name          // "Aman"
user["name"]       // "Aman" — useful when key is in variable

const key = "age"
user[key]          // 20

// Nested access
user.address.city  // undefined (city not in address)
user.address.street  // "MG Road"
user.courses[0]      // "Python"

// Add property
user.email = "aman@gmail.com"

// Update property
user.age = 21

// Delete property
delete user.city

// Check if property exists
"name" in user     // true
"salary" in user   // false

// Get all keys
Object.keys(user)       // ["name", "age", "isStudent"...]

// Get all values
Object.values(user)     // ["Aman", 20, true...]

// Get key-value pairs
Object.entries(user)    // [["name","Aman"], ["age",20]...]

// Loop through object
Object.entries(user).forEach(([key, value]) => {
    console.log(`${key}: ${value}`)
})
```

### Object destructuring

```javascript
const user = { name: "Aman", age: 20, city: "Nashik", role: "developer" }

// Old way
const name = user.name
const age = user.age

// Destructuring
const { name, age } = user
// name = "Aman", age = 20

// Rename while destructuring
const { name: userName, age: userAge } = user
// userName = "Aman", userAge = 20

// Default values
const { name, salary = 0 } = user
// salary = 0 (since not in object)

// Rest in objects
const { name, age, ...rest } = user
// rest = { city: "Nashik", role: "developer" }

// Nested destructuring
const { address: { street } } = user    // if user had address object
```

### Spread with objects

```javascript
const user = { name: "Aman", age: 20 }

// Copy object
const copy = { ...user }

// Merge objects
const extra = { city: "Nashik", role: "developer" }
const merged = { ...user, ...extra }
// { name: "Aman", age: 20, city: "Nashik", role: "developer" }

// Update a property without mutating
const updated = { ...user, age: 21 }
// { name: "Aman", age: 21 }

// This is how you update state without mutating:
let state = { users: [], loading: false, error: null }
state = { ...state, loading: true }
```

### Shorthand property names

```javascript
const name = "Aman"
const age = 20

// Old way
const user = { name: name, age: age }

// Shorthand — when variable name matches key name
const user = { name, age }
// { name: "Aman", age: 20 }

// Very common in fetch requests:
async function createUser(name, role) {
    await fetch('/api/users', {
        method: 'POST',
        body: JSON.stringify({ name, role })  // shorthand here
    })
}
```

---

## Chapter 7 — Functions

```javascript
// Regular function declaration
function greet(name) {
    return `Hello ${name}`
}

// Function expression
const greet = function(name) {
    return `Hello ${name}`
}

// Arrow function — use this most of the time
const greet = (name) => {
    return `Hello ${name}`
}

// Arrow function — short form (implicit return)
const greet = (name) => `Hello ${name}`

// Single parameter — can drop parentheses
const greet = name => `Hello ${name}`

// No parameters
const sayHello = () => "Hello"

// Multiple parameters
const add = (a, b) => a + b

// Multiple lines — needs {} and explicit return
const calculate = (a, b) => {
    const sum = a + b
    const product = a * b
    return { sum, product }
}
```

### Parameters and arguments

```javascript
// Default parameters
function greet(name = "stranger") {
    return `Hello ${name}`
}
greet()           // "Hello stranger"
greet("Aman")     // "Hello Aman"

// Rest parameters — like *args in Python
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0)
}
sum(1, 2, 3, 4, 5)    // 15

// Destructuring in parameters
function displayUser({ name, age, role = "user" }) {
    console.log(`${name}, ${age}, ${role}`)
}
displayUser({ name: "Aman", age: 20 })
// "Aman, 20, user"

// This is very useful when working with API responses:
const users = [
    { name: "Aman", age: 20, role: "developer" }
]
users.forEach(({ name, role }) => {
    console.log(`${name} is a ${role}`)
})
```

### Higher order functions

Functions that take other functions as arguments.

```javascript
// You've already seen these:
users.map(user => user.name)      // map takes a function
users.filter(user => user.age > 18)  // filter takes a function

// setTimeout — run function after delay
setTimeout(() => {
    console.log("runs after 2 seconds")
}, 2000)

// Your own higher order function
function repeat(fn, times) {
    for (let i = 0; i < times; i++) {
        fn(i)
    }
}

repeat((i) => console.log(`Run ${i}`), 3)
// Run 0
// Run 1
// Run 2
```

---

## Chapter 8 — Scope

Scope means: where can a variable be accessed?

```javascript
// Global scope — accessible everywhere
const globalVar = "I am global"

function myFunction() {
    console.log(globalVar)    // accessible here
}

// Function scope — only inside the function
function myFunction() {
    const localVar = "I am local"
    console.log(localVar)     // works
}
console.log(localVar)         // ERROR: localVar is not defined

// Block scope — only inside {} (with let and const)
if (true) {
    const blockVar = "inside block"
    let blockLet = "also inside"
    var oldVar = "var ignores blocks"    // don't use var
}
console.log(blockVar)     // ERROR
console.log(blockLet)     // ERROR
console.log(oldVar)       // "var ignores blocks" ← why var is dangerous

// Practical example
function loadUsers() {
    const users = []              // only exists in loadUsers

    if (true) {
        const temp = "temp"       // only exists in this block
        users.push("Aman")        // can access parent scope
    }

    return users
}
```

### Scope chain

JS looks for variables starting from innermost scope, moving outward.

```javascript
const x = "global"

function outer() {
    const x = "outer"

    function inner() {
        const x = "inner"
        console.log(x)        // "inner" — found in own scope
    }

    function inner2() {
        console.log(x)        // "outer" — not in inner2, found in outer
    }

    inner()
    inner2()
}

function other() {
    console.log(x)            // "global" — not in other, found in global
}
```

---

## Chapter 9 — Closures

Closures are one of the most important concepts in JS. A closure happens when a function remembers variables from its outer scope even after the outer function has finished running.

```javascript
// Basic closure example
function makeGreeter(greeting) {
    // greeting lives here

    return function(name) {
        // this inner function "closes over" greeting
        return `${greeting} ${name}`
    }
}

const sayHello = makeGreeter("Hello")
const sayHi = makeGreeter("Hi")

sayHello("Aman")    // "Hello Aman"
sayHello("Ravi")    // "Hello Ravi"
sayHi("Priya")      // "Hi Priya"

// makeGreeter has finished running but greeting is still remembered
```

### Why closures matter in practice

```javascript
// Counter — closure maintains private state
function makeCounter(start = 0) {
    let count = start    // this is "private" — can't access from outside

    return {
        increment: () => ++count,
        decrement: () => --count,
        reset: () => { count = start },
        value: () => count
    }
}

const counter = makeCounter(10)
counter.increment()   // 11
counter.increment()   // 12
counter.decrement()   // 11
counter.value()       // 11
counter.reset()
counter.value()       // 10

// count is not accessible directly:
counter.count         // undefined — protected
```

### Closures in event listeners

```javascript
// This is where closures trip people up
const buttons = document.querySelectorAll('.btn')

// Wrong — classic closure bug with var
for (var i = 0; i < buttons.length; i++) {
    buttons[i].addEventListener('click', () => {
        console.log(i)    // always prints the FINAL value of i
    })
}

// Right — let creates new scope each iteration
for (let i = 0; i < buttons.length; i++) {
    buttons[i].addEventListener('click', () => {
        console.log(i)    // prints correct i for each button
    })
}

// Right — use the actual data, not index
const users = ["Aman", "Ravi", "Priya"]
users.forEach((user, index) => {
    buttons[index].addEventListener('click', () => {
        console.log(user)    // closure over user — works perfectly
    })
})
```

### Real world closure — API call with config

```javascript
// Closure to create API caller with base URL baked in
function createApiClient(baseUrl) {
    // baseUrl is captured in closure

    async function get(endpoint) {
        const res = await fetch(`${baseUrl}${endpoint}`)
        return res.json()
    }

    async function post(endpoint, data) {
        const res = await fetch(`${baseUrl}${endpoint}`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(data)
        })
        return res.json()
    }

    return { get, post }
}

const api = createApiClient('http://localhost:5000')

// Now use it without repeating base URL
const users = await api.get('/api/users')
const newUser = await api.post('/api/users', { name: "Aman" })
```

---

## Chapter 10 — The `this` Keyword

`this` is context-dependent. It refers to different things depending on how a function is called.

```javascript
// In global scope
console.log(this)    // window object in browser

// In a regular function — this is the caller
const user = {
    name: "Aman",
    greet: function() {
        console.log(this.name)    // "Aman" — this is user object
    }
}
user.greet()    // "Aman"

// Problem — regular function in callback loses this
const user = {
    name: "Aman",
    greetLater: function() {
        setTimeout(function() {
            console.log(this.name)    // undefined — this is window here!
        }, 1000)
    }
}

// Solution — use arrow function (arrow functions don't have their own this)
const user = {
    name: "Aman",
    greetLater: function() {
        setTimeout(() => {
            console.log(this.name)    // "Aman" — arrow uses outer this
        }, 1000)
    }
}
```

### Simple rule for your use case

For event listeners and callbacks: **always use arrow functions**.

```javascript
// Use arrow functions in event listeners
button.addEventListener('click', () => {
    // this inside here refers to outer scope (probably window)
    // but you don't need this — use your state object instead
    loadUsers()
})

// For object methods, use regular function if you need this
const api = {
    baseUrl: 'http://localhost:5000',
    get: async function(endpoint) {
        const res = await fetch(this.baseUrl + endpoint)  // this works here
        return res.json()
    }
}
```

---

## Chapter 11 — Conditionals and Loops

### if / else

```javascript
const age = 20

if (age >= 18) {
    console.log("adult")
} else if (age >= 13) {
    console.log("teen")
} else {
    console.log("child")
}

// Ternary operator — short if/else
const label = age >= 18 ? "adult" : "minor"

// Nullish coalescing — use default if null/undefined
const name = user.name ?? "Anonymous"

// Optional chaining — safe access to nested properties
const street = user?.address?.street    // undefined if address doesn't exist
// without this: user.address.street would throw ERROR if address is null
```

### Switch

```javascript
const role = "developer"

switch (role) {
    case "developer":
        console.log("writes code")
        break
    case "designer":
        console.log("makes UI")
        break
    case "manager":
        console.log("manages team")
        break
    default:
        console.log("unknown role")
}
```

### Loops

```javascript
// for loop
for (let i = 0; i < 5; i++) {
    console.log(i)    // 0, 1, 2, 3, 4
}

// while loop
let count = 0
while (count < 5) {
    console.log(count)
    count++
}

// for...of — loop through array values (like Python for x in arr)
const fruits = ["apple", "banana", "mango"]
for (const fruit of fruits) {
    console.log(fruit)
}

// for...in — loop through object keys
const user = { name: "Aman", age: 20 }
for (const key in user) {
    console.log(`${key}: ${user[key]}`)
}

// forEach — most common for arrays
fruits.forEach((fruit, index) => {
    console.log(`${index}: ${fruit}`)
})

// break and continue
for (let i = 0; i < 10; i++) {
    if (i === 3) continue    // skip 3
    if (i === 7) break       // stop at 7
    console.log(i)
}
```

---

# PART 2 — DOM Control

---

## Chapter 12 — What is the DOM?

DOM = Document Object Model. It's a tree of all HTML elements that JS can read and change.

When browser loads your HTML:
```html
<body>
    <div id="app">
        <h1>Hello</h1>
        <p>World</p>
    </div>
</body>
```

JS sees it as a tree of objects you can manipulate:
```
document
└── body
    └── div#app
        ├── h1
        └── p
```

Everything you see on the page is a node in this tree. JS can:
- Find any element
- Read its content
- Change its content
- Show/hide it
- Add/remove elements
- Listen for clicks and inputs

---

## Chapter 13 — Selecting Elements

```javascript
// querySelector — select first matching element (like CSS selector)
document.querySelector('#myId')         // by ID
document.querySelector('.myClass')      // by class
document.querySelector('p')            // by tag
document.querySelector('div.card')     // div with class card
document.querySelector('#list .item')  // .item inside #list

// querySelectorAll — select ALL matching elements
const items = document.querySelectorAll('.item')
// returns NodeList (like array but not exactly)

// Convert NodeList to real array
const itemsArray = Array.from(items)
// or
const itemsArray = [...items]

// Now you can use all array methods
items.forEach(item => console.log(item))    // forEach works on NodeList
items.map(...)    // ERROR — map doesn't work on NodeList directly
Array.from(items).map(...)   // works

// getElementById — old but fast
document.getElementById('myId')

// Search within element (not whole document)
const container = document.querySelector('#container')
container.querySelector('.item')     // only searches inside container
container.querySelectorAll('.item')

// Navigate the DOM tree
const el = document.querySelector('.card')
el.parentElement              // parent element
el.children                   // all child elements
el.firstElementChild          // first child
el.lastElementChild           // last child
el.nextElementSibling         // next sibling
el.previousElementSibling     // previous sibling

// Check if element exists before using it
const el = document.querySelector('#maybeExists')
if (el) {
    el.textContent = "found it"
}
```

---

## Chapter 14 — Reading and Changing Elements

```javascript
const title = document.querySelector('#title')

// ── Reading content ──────────────────────────────

title.textContent    // text only, no HTML tags
title.innerHTML      // text with HTML tags
title.innerText      // visible text (respects CSS display:none)

// Reading attributes
const link = document.querySelector('a')
link.href
link.getAttribute('href')
link.getAttribute('data-id')     // custom data attributes

// Reading input values
const input = document.querySelector('#myInput')
input.value          // current value typed by user
input.checked        // for checkbox — true/false

// ── Changing content ──────────────────────────────

title.textContent = "New title"        // safe — no HTML injection possible
title.innerHTML = "<em>New</em> title" // allows HTML — be careful

// Changing attributes
link.href = "https://google.com"
link.setAttribute('href', 'https://google.com')
link.setAttribute('disabled', '')      // add disabled
link.removeAttribute('disabled')       // remove disabled

// ── Changing style ──────────────────────────────

const box = document.querySelector('.box')

box.style.display = 'none'          // hide
box.style.display = 'block'         // show
box.style.display = 'flex'          // flex container
box.style.color = 'red'
box.style.backgroundColor = '#fff'  // camelCase in JS
box.style.fontSize = '16px'
box.style.width = '200px'

// ── Working with classes ──────────────────────────────

box.classList.add('active')              // add class
box.classList.remove('active')           // remove class
box.classList.toggle('active')           // add if missing, remove if present
box.classList.contains('active')         // returns true/false
box.classList.replace('old', 'new')      // replace one class with another

// className — all classes as string (use classList instead)
box.className                            // "box card active"
```

---

## Chapter 15 — Creating and Removing Elements

This is how you render data from your Python backend onto the page.

```javascript
// Create element
const div = document.createElement('div')
const p = document.createElement('p')
const button = document.createElement('button')

// Add content
div.textContent = "Hello"
p.innerHTML = "<strong>Bold text</strong>"
button.textContent = "Click me"

// Add classes
div.classList.add('card')
button.classList.add('btn', 'btn-primary')

// Add attributes
button.setAttribute('data-id', '42')
button.disabled = false

// Append to DOM
document.querySelector('#container').appendChild(div)

// Insert at specific position
const list = document.querySelector('#list')
const newItem = document.createElement('li')
newItem.textContent = "New item"

list.prepend(newItem)           // add at start
list.append(newItem)            // add at end
list.insertBefore(newItem, list.firstChild)  // before specific element

// Remove element
div.remove()                    // remove itself
list.removeChild(newItem)       // parent removes child
```

### Efficient rendering with innerHTML

When displaying data from API, `innerHTML` is faster than creating many elements:

```javascript
const users = [
    { id: 1, name: "Aman", role: "developer" },
    { id: 2, name: "Ravi", role: "designer" },
    { id: 3, name: "Priya", role: "manager" }
]

// Slow way — creating each element manually
const container = document.querySelector('#users')
users.forEach(user => {
    const card = document.createElement('div')
    card.classList.add('card')
    card.textContent = user.name
    container.appendChild(card)
})

// Fast way — build HTML string, set once
const container = document.querySelector('#users')
container.innerHTML = users
    .map(user => `
        <div class="card" data-id="${user.id}">
            <h3>${user.name}</h3>
            <p>${user.role}</p>
            <button class="delete-btn" data-id="${user.id}">Delete</button>
        </div>
    `)
    .join('')

// Even better — with document fragment (for large lists)
const fragment = document.createDocumentFragment()
users.forEach(user => {
    const card = document.createElement('div')
    card.textContent = user.name
    fragment.appendChild(card)
})
document.querySelector('#users').appendChild(fragment)
// Only one DOM update instead of many
```

---

## Chapter 16 — Events

Events are user actions (click, type, scroll) or browser actions (page loaded) that JS can react to.

```javascript
const button = document.querySelector('#myBtn')

// addEventListener — the right way
button.addEventListener('click', () => {
    console.log("clicked!")
})

// Named function — good for removing later
function handleClick() {
    console.log("clicked!")
}
button.addEventListener('click', handleClick)
button.removeEventListener('click', handleClick)    // remove specific listener

// Event object — info about what happened
button.addEventListener('click', (event) => {
    console.log(event.target)         // element that was clicked
    console.log(event.target.id)      // its ID
    console.log(event.target.dataset.id)  // data-id attribute
    console.log(event.clientX)        // mouse X position
    console.log(event.clientY)        // mouse Y position
})
```

### Common events

```javascript
// Click
button.addEventListener('click', handler)

// Input — fires on every keystroke
input.addEventListener('input', (e) => {
    console.log(e.target.value)    // current input value
})

// Change — fires when value changes and loses focus
select.addEventListener('change', (e) => {
    console.log(e.target.value)    // selected option
})

// Submit — form submission
form.addEventListener('submit', (e) => {
    e.preventDefault()             // IMPORTANT: stops page reload
    const data = new FormData(e.target)
    console.log(data.get('username'))
})

// Keydown — keyboard press
document.addEventListener('keydown', (e) => {
    console.log(e.key)             // "Enter", "Escape", "a", etc.
    if (e.key === 'Enter') { ... }
    if (e.key === 'Escape') { ... }
    if (e.ctrlKey && e.key === 's') {    // Ctrl+S
        e.preventDefault()
        saveData()
    }
})

// Focus and blur
input.addEventListener('focus', () => console.log("focused"))
input.addEventListener('blur', () => console.log("unfocused"))

// Page events
document.addEventListener('DOMContentLoaded', () => {
    // runs when HTML is fully loaded
    // good place to initialize your app
    init()
})

window.addEventListener('load', () => {
    // runs when everything (images, etc.) is loaded
})

// Scroll
window.addEventListener('scroll', () => {
    console.log(window.scrollY)    // how far scrolled
})
```

### Event delegation — very important pattern

Instead of adding listeners to every item, add ONE to the parent.

```javascript
// Problem: you have 100 items, adding 100 listeners is slow
// Also: if items are added dynamically, they won't have listeners

// Wrong approach
document.querySelectorAll('.item').forEach(item => {
    item.addEventListener('click', handleClick)    // 100 listeners!
})

// Right approach — event delegation
document.querySelector('#list').addEventListener('click', (e) => {
    // check if the clicked thing is what we want
    if (e.target.classList.contains('item')) {
        handleClick(e.target)
    }

    // for delete buttons inside cards
    if (e.target.classList.contains('delete-btn')) {
        const id = e.target.dataset.id    // get data-id attribute
        deleteUser(id)
    }

    // for any button inside a card
    if (e.target.closest('.card')) {
        const card = e.target.closest('.card')
        const id = card.dataset.id
        // handle click on anything inside card
    }
})

// e.target.closest() — finds nearest ancestor matching selector
// Very useful for event delegation with nested elements
```

### Practical example — render and handle dynamically created buttons

```javascript
const users = [
    { id: 1, name: "Aman" },
    { id: 2, name: "Ravi" }
]

// Render
document.querySelector('#users').innerHTML = users
    .map(u => `
        <div class="user-card" data-id="${u.id}">
            <span>${u.name}</span>
            <button class="edit-btn">Edit</button>
            <button class="delete-btn">Delete</button>
        </div>
    `)
    .join('')

// Handle all events with one listener on parent
document.querySelector('#users').addEventListener('click', (e) => {
    const card = e.target.closest('.user-card')
    if (!card) return                           // clicked outside a card

    const id = Number(card.dataset.id)

    if (e.target.classList.contains('edit-btn')) {
        editUser(id)
    }
    if (e.target.classList.contains('delete-btn')) {
        deleteUser(id)
    }
})
```

---

## Chapter 17 — State Pattern

This is the most important design concept for JS UIs.

**The problem without state:**

```javascript
// Without state — chaos
function showUsers() {
    document.querySelector('#list').innerHTML = "..."
}
function hideUsers() {
    document.querySelector('#list').style.display = 'none'
}
function filterUsers(role) {
    // where is the original list? we don't know
}
// UI gets inconsistent fast
```

**The solution — state object drives everything:**

```javascript
// State — single source of truth
let state = {
    users: [],
    filteredUsers: [],
    loading: false,
    error: null,
    filter: 'all',
    searchQuery: ''
}

// render — UI is always built from state
function render() {
    const { users, filteredUsers, loading, error } = state

    // Loading state
    if (loading) {
        document.querySelector('#content').innerHTML = `
            <div class="spinner">Loading...</div>
        `
        return
    }

    // Error state
    if (error) {
        document.querySelector('#content').innerHTML = `
            <div class="error">
                <p>${error}</p>
                <button onclick="loadUsers()">Retry</button>
            </div>
        `
        return
    }

    // Empty state
    if (filteredUsers.length === 0) {
        document.querySelector('#content').innerHTML = `
            <p>No users found.</p>
        `
        return
    }

    // Normal state
    document.querySelector('#content').innerHTML = filteredUsers
        .map(user => `
            <div class="card" data-id="${user.id}">
                <h3>${user.name}</h3>
                <p>${user.role}</p>
                <button class="delete-btn" data-id="${user.id}">Delete</button>
            </div>
        `)
        .join('')
}

// Update state functions — always call render() after
function setLoading(isLoading) {
    state = { ...state, loading: isLoading }
    render()
}

function setError(message) {
    state = { ...state, error: message, loading: false }
    render()
}

function setUsers(users) {
    state = { ...state, users, filteredUsers: users, loading: false, error: null }
    render()
}

function setFilter(role) {
    state = { ...state, filter: role }
    applyFilters()
}

function setSearch(query) {
    state = { ...state, searchQuery: query }
    applyFilters()
}

// Apply filter + search together
function applyFilters() {
    let result = state.users

    if (state.filter !== 'all') {
        result = result.filter(u => u.role === state.filter)
    }

    if (state.searchQuery) {
        const q = state.searchQuery.toLowerCase()
        result = result.filter(u => u.name.toLowerCase().includes(q))
    }

    state = { ...state, filteredUsers: result }
    render()
}

// Event listeners — update state, let render() handle UI
document.querySelector('#searchInput').addEventListener('input', (e) => {
    setSearch(e.target.value)
})

document.querySelector('#roleFilter').addEventListener('change', (e) => {
    setFilter(e.target.value)
})

// Initialize
async function init() {
    setLoading(true)
    try {
        const res = await fetch('/api/users')
        const users = await res.json()
        setUsers(users)
    } catch (err) {
        setError("Failed to load users. Is your Python server running?")
    }
}

init()
```

---

# PART 3 — Fetch API and Python Integration

---

## Chapter 18 — Promises

Before async/await, JS used Promises. You need to understand them because async/await is built on top.

```javascript
// A Promise is a wrapper around a value that may not exist yet
// It has three states: pending, fulfilled, rejected

// Creating a promise
const promise = new Promise((resolve, reject) => {
    // do async work
    setTimeout(() => {
        const success = true
        if (success) {
            resolve("data is here")     // success
        } else {
            reject("something failed")  // failure
        }
    }, 2000)
})

// Using a promise with .then() and .catch()
promise
    .then(data => console.log(data))     // runs on resolve
    .catch(err => console.log(err))      // runs on reject
    .finally(() => console.log("done"))  // runs always

// fetch() returns a Promise
fetch('/api/users')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(err => console.log(err))

// This is what async/await simplifies
```

---

## Chapter 19 — Async / Await

Async/await makes async code look and feel like synchronous code.

```javascript
// async keyword makes function return a Promise
async function loadData() {
    return "data"    // auto-wrapped in Promise
}

// await keyword pauses until Promise resolves
// can only use await inside async function
async function loadUsers() {
    const response = await fetch('/api/users')    // waits here
    const users = await response.json()           // waits here
    return users
}

// Error handling with try/catch
async function loadUsers() {
    try {
        const response = await fetch('/api/users')

        // Check if request was successful
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`)
        }

        const users = await response.json()
        return users

    } catch (error) {
        console.error("Failed:", error.message)
        throw error    // re-throw if you want caller to handle it
    }
}

// Calling async function
loadUsers()
    .then(users => console.log(users))
    .catch(err => console.log(err))

// OR inside another async function
async function init() {
    const users = await loadUsers()
    console.log(users)
}
```

### Multiple async operations

```javascript
// Sequential — one after another (slower)
async function loadAll() {
    const users = await fetch('/api/users').then(r => r.json())
    const posts = await fetch('/api/posts').then(r => r.json())
    // posts starts AFTER users finishes
}

// Parallel — all at once (faster)
async function loadAll() {
    const [users, posts] = await Promise.all([
        fetch('/api/users').then(r => r.json()),
        fetch('/api/posts').then(r => r.json())
    ])
    // both start at same time
}

// Promise.allSettled — don't fail if one fails
async function loadAll() {
    const results = await Promise.allSettled([
        fetch('/api/users').then(r => r.json()),
        fetch('/api/posts').then(r => r.json())
    ])

    results.forEach(result => {
        if (result.status === 'fulfilled') {
            console.log(result.value)
        } else {
            console.log("failed:", result.reason)
        }
    })
}

// Promise.race — use whichever resolves first
async function withTimeout(promise, ms) {
    const timeout = new Promise((_, reject) =>
        setTimeout(() => reject(new Error("Timeout")), ms)
    )
    return Promise.race([promise, timeout])
}
```

---

## Chapter 20 — fetch() API

```javascript
// Basic GET request
async function getUsers() {
    const response = await fetch('http://localhost:5000/api/users')
    const users = await response.json()
    return users
}

// Response object
const response = await fetch('/api/data')
response.ok           // true if status 200-299
response.status       // 200, 404, 500, etc
response.statusText   // "OK", "Not Found", etc
response.headers      // response headers
response.json()       // parse body as JSON (returns Promise)
response.text()       // parse body as text (returns Promise)

// Always check response.ok
async function getUsers() {
    const response = await fetch('/api/users')

    if (!response.ok) {
        if (response.status === 404) throw new Error("Users not found")
        if (response.status === 401) throw new Error("Not authenticated")
        if (response.status === 500) throw new Error("Server error")
        throw new Error(`Error: ${response.status}`)
    }

    return response.json()
}
```

### All request types

```javascript
// GET — fetch data
const users = await fetch('/api/users').then(r => r.json())

// POST — send data
async function createUser(name, role) {
    const response = await fetch('/api/users', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ name, role })
    })

    if (!response.ok) throw new Error('Failed to create user')
    return response.json()    // returns created user
}

// PUT — replace entire resource
async function updateUser(id, data) {
    const response = await fetch(`/api/users/${id}`, {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
    })
    return response.json()
}

// PATCH — update partial resource
async function markDone(taskId) {
    const response = await fetch(`/api/tasks/${taskId}/done`, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ done: true })
    })
    return response.json()
}

// DELETE — remove resource
async function deleteUser(id) {
    const response = await fetch(`/api/users/${id}`, {
        method: 'DELETE'
    })

    if (!response.ok) throw new Error('Failed to delete')
    // DELETE usually returns 204 No Content or { message: "deleted" }
}

// Send with auth token (from localStorage)
async function getSecureData() {
    const token = localStorage.getItem('token')

    const response = await fetch('/api/secure-data', {
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${token}`
        }
    })
    return response.json()
}
```

---

## Chapter 21 — Complete Error Handling

Error handling is not optional. Your UI must handle every possible failure.

```javascript
// Full error handling pattern
async function loadUsers() {
    // 1. Set loading state
    state = { ...state, loading: true, error: null }
    render()

    try {
        // 2. Make request
        const response = await fetch('/api/users')

        // 3. Check HTTP status
        if (!response.ok) {
            const errorBody = await response.json().catch(() => ({}))
            throw new Error(errorBody.message || `Server error ${response.status}`)
        }

        // 4. Parse response
        const users = await response.json()

        // 5. Update state on success
        state = { ...state, users, loading: false }

    } catch (error) {
        // 6. Handle different error types
        if (error.name === 'TypeError' && error.message.includes('fetch')) {
            // Network error — Python server not running
            state = { ...state, error: "Cannot connect to server. Is Python running?", loading: false }
        } else if (error.name === 'AbortError') {
            // Request was cancelled — don't show error
            return
        } else {
            state = { ...state, error: error.message, loading: false }
        }
    } finally {
        // 7. Always runs — even if error
        render()
    }
}

// Retry logic
async function loadWithRetry(url, maxRetries = 3) {
    for (let attempt = 1; attempt <= maxRetries; attempt++) {
        try {
            const response = await fetch(url)
            if (!response.ok) throw new Error(`HTTP ${response.status}`)
            return await response.json()
        } catch (error) {
            if (attempt === maxRetries) throw error
            // Wait before retrying (exponential backoff)
            await new Promise(r => setTimeout(r, attempt * 1000))
        }
    }
}
```

---

## Chapter 22 — Loading States

Loading states make your UI feel professional. Without them, the page looks broken.

```javascript
// Complete loading state management
let state = {
    data: [],
    loading: false,
    error: null
}

function render() {
    const container = document.querySelector('#content')
    const loadBtn = document.querySelector('#loadBtn')

    // Update button state
    if (loadBtn) {
        loadBtn.disabled = state.loading
        loadBtn.textContent = state.loading ? "Loading..." : "Load Data"
    }

    // Render based on state
    if (state.loading) {
        container.innerHTML = `
            <div class="loading">
                <div class="spinner"></div>
                <p>Fetching data from server...</p>
            </div>
        `
        return
    }

    if (state.error) {
        container.innerHTML = `
            <div class="error-box">
                <p>❌ ${state.error}</p>
                <button onclick="loadData()">Try Again</button>
            </div>
        `
        return
    }

    if (state.data.length === 0) {
        container.innerHTML = `<p>No data found.</p>`
        return
    }

    container.innerHTML = state.data
        .map(item => `<div class="item">${item.name}</div>`)
        .join('')
}
```

---

## Chapter 23 — Form Handling

```javascript
// HTML form (do not use <form action="..."> — handle in JS)
/*
<form id="addUserForm">
    <input type="text" id="nameInput" placeholder="Name" required>
    <input type="text" id="roleInput" placeholder="Role" required>
    <button type="submit">Add User</button>
    <p id="formError" style="color:red"></p>
</form>
*/

const form = document.querySelector('#addUserForm')

form.addEventListener('submit', async (e) => {
    e.preventDefault()    // ALWAYS — stops page reload

    // Get values
    const name = document.querySelector('#nameInput').value.trim()
    const role = document.querySelector('#roleInput').value.trim()

    // Validate
    const errorEl = document.querySelector('#formError')
    errorEl.textContent = ''

    if (!name) {
        errorEl.textContent = "Name is required"
        return
    }
    if (!role) {
        errorEl.textContent = "Role is required"
        return
    }
    if (name.length < 2) {
        errorEl.textContent = "Name too short"
        return
    }

    // Disable form while submitting
    const submitBtn = form.querySelector('button[type="submit"]')
    submitBtn.disabled = true
    submitBtn.textContent = "Adding..."

    try {
        const response = await fetch('/api/users', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ name, role })
        })

        if (!response.ok) throw new Error('Failed to add user')

        const newUser = await response.json()

        // Add to state and re-render
        state.users.push(newUser)
        render()

        // Reset form
        form.reset()
        document.querySelector('#nameInput').focus()    // put cursor back in input

    } catch (err) {
        errorEl.textContent = err.message
    } finally {
        submitBtn.disabled = false
        submitBtn.textContent = "Add User"
    }
})

// Get all form values at once using FormData
form.addEventListener('submit', (e) => {
    e.preventDefault()
    const formData = new FormData(e.target)
    const data = Object.fromEntries(formData)
    // data = { name: "Aman", role: "developer" }
    console.log(data)
})
```

---

## Chapter 24 — AbortController

Cancel fetch requests that are no longer needed.

```javascript
// Without AbortController — problem scenario:
// User types fast in search box
// "a" → fetch starts
// "am" → another fetch starts
// "ama" → another fetch starts
// All three might complete in random order
// Last letter typed might not show last result

// With AbortController — cancel old requests
let searchController = null

async function search(query) {
    // Cancel previous request if it's still running
    if (searchController) {
        searchController.abort()
    }

    // Create new controller for this request
    searchController = new AbortController()

    try {
        const response = await fetch(`/api/search?q=${query}`, {
            signal: searchController.signal    // attach to request
        })
        const data = await response.json()
        displayResults(data)

    } catch (error) {
        if (error.name === 'AbortError') {
            // Request was cancelled — this is fine, ignore it
            return
        }
        showError(error.message)
    }
}

// Combined with debounce
function debounce(fn, delay) {
    let timer
    return (...args) => {
        clearTimeout(timer)
        timer = setTimeout(() => fn(...args), delay)
    }
}

const debouncedSearch = debounce(search, 300)

document.querySelector('#searchInput').addEventListener('input', (e) => {
    debouncedSearch(e.target.value)
})
```

---

# PART 4 — Advanced Concepts

---

## Chapter 25 — The Event Loop (How JS is actually async)

JS runs in a single thread. Only one thing runs at a time. But it handles async without blocking. How?

```javascript
console.log("1 — start")

setTimeout(() => {
    console.log("3 — setTimeout 0ms")
}, 0)

Promise.resolve().then(() => {
    console.log("2 — Promise")
})

console.log("4 — end")

// Output:
// 1 — start
// 4 — end
// 2 — Promise         ← microtask queue runs before macrotask
// 3 — setTimeout 0ms  ← macrotask queue
```

**The queues:**
- **Call stack** — currently executing code
- **Microtask queue** — Promises, `queueMicrotask()` — runs BEFORE next macrotask
- **Macrotask queue** — `setTimeout`, `setInterval`, I/O events — runs AFTER microtasks

**Practical impact:**
```javascript
async function example() {
    console.log("A")

    await fetch('/api/data')    // pauses here, releases control

    console.log("B")            // runs after fetch resolves (in microtask)
}

example()
console.log("C")    // runs BEFORE B because await released control

// Output: A, C, B
```

---

## Chapter 26 — Closures in Depth

```javascript
// Module pattern — closure for encapsulation
const UserStore = (() => {
    let users = []           // private
    let nextId = 1           // private

    function add(name, role) {
        const user = { id: nextId++, name, role }
        users.push(user)
        return user
    }

    function remove(id) {
        users = users.filter(u => u.id !== id)
    }

    function getAll() {
        return [...users]    // return copy, not reference
    }

    function find(id) {
        return users.find(u => u.id === id)
    }

    return { add, remove, getAll, find }   // public API
})()

UserStore.add("Aman", "developer")
UserStore.add("Ravi", "designer")
UserStore.getAll()          // [{ id:1, ...}, { id:2, ...}]
UserStore.users             // undefined — private!

// Memoization — cache function results
function memoize(fn) {
    const cache = {}

    return function(...args) {
        const key = JSON.stringify(args)
        if (key in cache) {
            return cache[key]    // return cached result
        }
        cache[key] = fn(...args)
        return cache[key]
    }
}

const expensiveCalc = memoize((n) => {
    // imagine this is slow
    return n * n
})

expensiveCalc(5)    // calculates: 25
expensiveCalc(5)    // returns cached: 25 (instant)
expensiveCalc(6)    // calculates: 36
```

---

## Chapter 27 — Debounce and Throttle

**Debounce:** Wait until user stops doing something, then run once.

```javascript
function debounce(fn, delay) {
    let timer

    return function(...args) {
        clearTimeout(timer)               // cancel previous timer
        timer = setTimeout(() => {
            fn(...args)                   // run after delay
        }, delay)
    }
}

// Search: only fetch after user stops typing for 300ms
const searchInput = document.querySelector('#search')
const debouncedSearch = debounce(async (query) => {
    const results = await fetch(`/api/search?q=${query}`).then(r => r.json())
    displayResults(results)
}, 300)

searchInput.addEventListener('input', (e) => {
    debouncedSearch(e.target.value)
})
```

**Throttle:** Run at most once per time period.

```javascript
function throttle(fn, limit) {
    let lastRun = 0

    return function(...args) {
        const now = Date.now()
        if (now - lastRun >= limit) {
            lastRun = now
            fn(...args)
        }
    }
}

// Scroll handler: run at most every 100ms
const throttledScroll = throttle(() => {
    console.log("scroll position:", window.scrollY)
}, 100)

window.addEventListener('scroll', throttledScroll)
```

---

## Chapter 28 — MutationObserver

Watch the DOM for changes.

```javascript
// Watch for any changes in #container
const observer = new MutationObserver((mutations) => {
    mutations.forEach(mutation => {
        if (mutation.type === 'childList') {
            console.log("Children added/removed")
            mutation.addedNodes.forEach(node => console.log("Added:", node))
            mutation.removedNodes.forEach(node => console.log("Removed:", node))
        }
        if (mutation.type === 'attributes') {
            console.log("Attribute changed:", mutation.attributeName)
        }
    })
})

observer.observe(document.querySelector('#container'), {
    childList: true,       // watch add/remove children
    attributes: true,      // watch attribute changes
    subtree: true          // watch all descendants too
})

// Stop watching
observer.disconnect()

// Real use: auto-scroll to bottom when messages added
const chatBox = document.querySelector('#chat')
const chatObserver = new MutationObserver(() => {
    chatBox.scrollTop = chatBox.scrollHeight    // scroll to bottom
})
chatObserver.observe(chatBox, { childList: true })
```

---

## Chapter 29 — IntersectionObserver

Detect when elements enter/exit the viewport.

```javascript
// Lazy load — only load image when it's visible
const imageObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            const img = entry.target
            img.src = img.dataset.src    // load actual image
            imageObserver.unobserve(img) // stop watching once loaded
        }
    })
}, {
    threshold: 0.1    // trigger when 10% visible
})

document.querySelectorAll('img[data-src]').forEach(img => {
    imageObserver.observe(img)
})

// Infinite scroll — load more when bottom is reached
const sentinel = document.querySelector('#bottom-sentinel')
const loadMoreObserver = new IntersectionObserver(async (entries) => {
    if (entries[0].isIntersecting && !state.loading) {
        await loadMoreUsers()    // load next page
    }
})
loadMoreObserver.observe(sentinel)
```

---

## Chapter 30 — ES Modules

Split your code into organized files.

```javascript
// utils.js
export const API_URL = 'http://localhost:5000'

export function formatDate(dateStr) {
    return new Date(dateStr).toLocaleDateString('en-IN')
}

export async function apiFetch(endpoint, options = {}) {
    const response = await fetch(`${API_URL}${endpoint}`, {
        headers: {
            'Content-Type': 'application/json',
            ...options.headers
        },
        ...options
    })
    if (!response.ok) throw new Error(`API error: ${response.status}`)
    return response.json()
}

// Default export (only one per file)
export default function createStore(initialState) {
    let state = initialState
    // ...
}
```

```javascript
// state.js
export let state = {
    users: [],
    loading: false,
    error: null
}

export function setState(updates) {
    state = { ...state, ...updates }
}
```

```javascript
// main.js
import { API_URL, formatDate, apiFetch } from './utils.js'
import createStore from './utils.js'    // default import
import { state, setState } from './state.js'

async function loadUsers() {
    setState({ loading: true })
    const users = await apiFetch('/api/users')
    setState({ users, loading: false })
}
```

```html
<!-- index.html — add type="module" -->
<script type="module" src="main.js"></script>
```

---

## Chapter 31 — localStorage

Persist data across page reloads.

```javascript
// Save
localStorage.setItem('key', 'value')
localStorage.setItem('user', JSON.stringify({ name: 'Aman', role: 'dev' }))

// Get
const value = localStorage.getItem('key')
const user = JSON.parse(localStorage.getItem('user'))

// Delete
localStorage.removeItem('key')

// Clear everything
localStorage.clear()

// Check if exists
if (localStorage.getItem('token')) {
    // user is logged in
}

// Practical: auth token flow
async function login(username, password) {
    const response = await fetch('/api/login', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ username, password })
    })

    if (!response.ok) throw new Error('Login failed')

    const { token, user } = await response.json()
    localStorage.setItem('token', token)
    localStorage.setItem('currentUser', JSON.stringify(user))

    // Redirect or update UI
    showDashboard(user)
}

function logout() {
    localStorage.removeItem('token')
    localStorage.removeItem('currentUser')
    showLoginForm()
}

function isLoggedIn() {
    return !!localStorage.getItem('token')
}

// Send token with every request
async function authFetch(endpoint, options = {}) {
    const token = localStorage.getItem('token')
    return fetch(`http://localhost:5000${endpoint}`, {
        ...options,
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${token}`,
            ...options.headers
        }
    })
}
```

---

## Chapter 32 — WebSockets (Realtime)

For realtime data from your Python backend (live notifications, chat, live updates).

```python
# Python — app.py with flask-socketio
# pip install flask-socketio

from flask import Flask
from flask_socketio import SocketIO, emit

app = Flask(__name__)
socketio = SocketIO(app, cors_allowed_origins="*")

@socketio.on('connect')
def on_connect():
    print("Client connected")
    emit('welcome', { 'message': 'Connected to server' })

@socketio.on('send_message')
def on_message(data):
    # Broadcast to all connected clients
    emit('new_message', data, broadcast=True)

@socketio.on('disconnect')
def on_disconnect():
    print("Client disconnected")

if __name__ == '__main__':
    socketio.run(app, debug=True)
```

```javascript
// JS — with socket.io client
// Include in HTML: <script src="https://cdn.socket.io/4.6.0/socket.io.min.js"></script>

const socket = io('http://localhost:5000')

// Connection events
socket.on('connect', () => {
    console.log('Connected! ID:', socket.id)
})

socket.on('disconnect', () => {
    console.log('Disconnected')
})

// Listen for events from server
socket.on('welcome', (data) => {
    console.log(data.message)
})

socket.on('new_message', (data) => {
    appendMessage(data)
})

// Send events to server
function sendMessage(text) {
    socket.emit('send_message', {
        text,
        sender: 'Aman',
        time: new Date().toISOString()
    })
}

// Chat form
document.querySelector('#chatForm').addEventListener('submit', (e) => {
    e.preventDefault()
    const input = document.querySelector('#messageInput')
    sendMessage(input.value)
    input.value = ''
})

function appendMessage(data) {
    const div = document.createElement('div')
    div.textContent = `${data.sender}: ${data.text}`
    document.querySelector('#messages').appendChild(div)
}
```

---

## Chapter 33 — setInterval and setTimeout

```javascript
// setTimeout — run once after delay
const timerId = setTimeout(() => {
    console.log("runs after 3 seconds")
}, 3000)

// Cancel it
clearTimeout(timerId)

// setInterval — run repeatedly
const intervalId = setInterval(() => {
    console.log("runs every 2 seconds")
}, 2000)

// Cancel it
clearInterval(intervalId)

// Auto-refresh data every 30 seconds
let refreshInterval = null

function startAutoRefresh() {
    refreshInterval = setInterval(async () => {
        await loadUsers()    // re-fetch from Python
    }, 30000)
}

function stopAutoRefresh() {
    clearInterval(refreshInterval)
}

// Start on page load, stop when user navigates away
startAutoRefresh()
window.addEventListener('beforeunload', stopAutoRefresh)

// Countdown timer
function startCountdown(seconds) {
    let remaining = seconds

    const interval = setInterval(() => {
        remaining--
        document.querySelector('#timer').textContent = remaining

        if (remaining <= 0) {
            clearInterval(interval)
            document.querySelector('#timer').textContent = "Time's up!"
        }
    }, 1000)
}
```

---

# PART 5 — Browser DevTools

---

## Chapter 34 — Using DevTools Effectively

Open with **F12** or **Ctrl+Shift+I**.

### Console tab

```javascript
// Different log levels
console.log("normal message")
console.warn("warning — shows in yellow")
console.error("error — shows in red")
console.info("info message")

// Log objects nicely
console.log({ name: "Aman", users: [...state.users] })
console.table(users)    // displays array of objects as table

// Group related logs
console.group("API Call")
console.log("URL:", url)
console.log("Response:", data)
console.groupEnd()

// Time something
console.time("fetch users")
await loadUsers()
console.timeEnd("fetch users")    // prints: "fetch users: 245ms"

// Count how many times something runs
console.count("render")    // render: 1
console.count("render")    // render: 2
console.count("render")    // render: 3
console.countReset("render")
```

### Network tab

This is how you debug API calls.

1. Open Network tab
2. Reload page or trigger a fetch
3. Click on any request to see:
   - **Headers** — request method, URL, status code
   - **Payload** — what you sent (POST body)
   - **Response** — what server returned
   - **Timing** — how long it took

**Common things to check:**
- Status 200 → success
- Status 404 → wrong URL
- Status 500 → Python server error (check Python terminal)
- Status 0 or network error → Python server not running
- CORS error → add flask-cors to Python

### Sources tab — Debugging

Set breakpoints to pause execution and inspect values.

1. Open Sources tab
2. Find your JS file
3. Click line number to set breakpoint
4. Trigger the code
5. Execution pauses, hover variables to see values
6. Use Step Over (F10), Step Into (F11), Continue (F8)

Or use `debugger` statement in code:
```javascript
async function loadUsers() {
    const response = await fetch('/api/users')
    debugger    // pauses here in devtools
    const users = await response.json()
    return users
}
```

---

# PART 6 — Complete Projects

---

## Project 1 — Hello World (Stage 1)

**Goal:** Fetch data from Python, show on page.

**Python (app.py):**
```python
from flask import Flask, jsonify
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

@app.route('/api/hello')
def hello():
    return jsonify({
        "message": "Hello from Python!",
        "name": "Aman",
        "version": "1.0"
    })

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

Install: `pip install flask flask-cors`
Run: `python app.py`

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello World</title>
</head>
<body>
    <h1 id="message">Loading...</h1>
    <p id="name"></p>
    <p id="error" style="color: red; display: none;"></p>

    <script src="app.js"></script>
</body>
</html>
```

**app.js:**
```javascript
async function init() {
    try {
        const response = await fetch('http://localhost:5000/api/hello')

        if (!response.ok) throw new Error(`Server error: ${response.status}`)

        const data = await response.json()

        document.getElementById('message').textContent = data.message
        document.getElementById('name').textContent = `Name: ${data.name}`

    } catch (error) {
        document.getElementById('message').textContent = 'Failed to load'
        document.getElementById('error').style.display = 'block'
        document.getElementById('error').textContent = error.message
    }
}

init()
```

---

## Project 2 — User List Manager (Stage 2)

**Goal:** Fetch users, render as cards, filter and search.

**Python (app.py):**
```python
from flask import Flask, jsonify, request
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

users = [
    { "id": 1, "name": "Aman Sharma", "role": "developer", "age": 20 },
    { "id": 2, "name": "Ravi Kumar", "role": "designer", "age": 25 },
    { "id": 3, "name": "Priya Singh", "role": "developer", "age": 22 },
    { "id": 4, "name": "Kiran Patil", "role": "manager", "age": 30 },
    { "id": 5, "name": "Deepa Nair", "role": "designer", "age": 27 }
]

@app.route('/api/users')
def get_users():
    return jsonify(users)

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>User List</title>
</head>
<body>
    <h1>Users</h1>

    <input type="text" id="searchInput" placeholder="Search by name...">

    <select id="roleFilter">
        <option value="all">All roles</option>
        <option value="developer">Developer</option>
        <option value="designer">Designer</option>
        <option value="manager">Manager</option>
    </select>

    <p id="count"></p>
    <div id="userList"></div>
    <p id="error" style="color:red"></p>

    <script src="app.js"></script>
</body>
</html>
```

**app.js:**
```javascript
let state = {
    users: [],
    filteredUsers: [],
    loading: false,
    error: null,
    searchQuery: '',
    roleFilter: 'all'
}

function render() {
    const listEl = document.querySelector('#userList')
    const countEl = document.querySelector('#count')
    const errorEl = document.querySelector('#error')

    errorEl.textContent = ''

    if (state.loading) {
        listEl.innerHTML = '<p>Loading users...</p>'
        return
    }

    if (state.error) {
        errorEl.textContent = state.error
        listEl.innerHTML = ''
        return
    }

    countEl.textContent = `Showing ${state.filteredUsers.length} of ${state.users.length} users`

    if (state.filteredUsers.length === 0) {
        listEl.innerHTML = '<p>No users match your search.</p>'
        return
    }

    listEl.innerHTML = state.filteredUsers.map(user => `
        <div style="border:1px solid #ccc; padding:10px; margin:10px 0;">
            <strong>${user.name}</strong>
            <span>${user.role}</span>
            <span>Age: ${user.age}</span>
        </div>
    `).join('')
}

function applyFilters() {
    let result = state.users

    if (state.roleFilter !== 'all') {
        result = result.filter(u => u.role === state.roleFilter)
    }

    if (state.searchQuery) {
        const q = state.searchQuery.toLowerCase()
        result = result.filter(u => u.name.toLowerCase().includes(q))
    }

    state = { ...state, filteredUsers: result }
    render()
}

async function loadUsers() {
    state = { ...state, loading: true, error: null }
    render()

    try {
        const response = await fetch('http://localhost:5000/api/users')
        if (!response.ok) throw new Error(`Server error: ${response.status}`)

        const users = await response.json()
        state = { ...state, users, filteredUsers: users, loading: false }
        render()
    } catch (error) {
        state = { ...state, error: error.message, loading: false }
        render()
    }
}

// Events
document.querySelector('#searchInput').addEventListener('input', (e) => {
    state = { ...state, searchQuery: e.target.value }
    applyFilters()
})

document.querySelector('#roleFilter').addEventListener('change', (e) => {
    state = { ...state, roleFilter: e.target.value }
    applyFilters()
})

// Start
loadUsers()
```

---

## Project 3 — Task Manager (Main Project — Stage 3)

**Goal:** Full CRUD. This is your most important project.

**Python (app.py):**
```python
from flask import Flask, jsonify, request
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

tasks = []
next_id = 1

@app.route('/api/tasks', methods=['GET'])
def get_tasks():
    return jsonify(tasks)

@app.route('/api/tasks', methods=['POST'])
def create_task():
    global next_id
    data = request.get_json()

    if not data or not data.get('title'):
        return jsonify({ "error": "Title is required" }), 400

    task = {
        "id": next_id,
        "title": data['title'],
        "done": False,
        "priority": data.get('priority', 'medium')
    }
    tasks.append(task)
    next_id += 1
    return jsonify(task), 201

@app.route('/api/tasks/<int:task_id>', methods=['DELETE'])
def delete_task(task_id):
    global tasks
    original_length = len(tasks)
    tasks = [t for t in tasks if t['id'] != task_id]

    if len(tasks) == original_length:
        return jsonify({ "error": "Task not found" }), 404

    return jsonify({ "message": "Task deleted" })

@app.route('/api/tasks/<int:task_id>/toggle', methods=['PATCH'])
def toggle_task(task_id):
    for task in tasks:
        if task['id'] == task_id:
            task['done'] = not task['done']
            return jsonify(task)

    return jsonify({ "error": "Task not found" }), 404

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Task Manager</title>
</head>
<body>
    <h1>Task Manager</h1>

    <form id="taskForm">
        <input type="text" id="titleInput" placeholder="Task title..." required>
        <select id="prioritySelect">
            <option value="low">Low</option>
            <option value="medium" selected>Medium</option>
            <option value="high">High</option>
        </select>
        <button type="submit" id="submitBtn">Add Task</button>
        <p id="formError" style="color:red"></p>
    </form>

    <p id="stats"></p>
    <div id="taskList"></div>

    <script src="app.js"></script>
</body>
</html>
```

**app.js:**
```javascript
const API = 'http://localhost:5000'

let state = {
    tasks: [],
    loading: false,
    error: null,
    submitting: false
}

function render() {
    const listEl = document.querySelector('#taskList')
    const statsEl = document.querySelector('#stats')
    const submitBtn = document.querySelector('#submitBtn')

    // Stats
    const total = state.tasks.length
    const done = state.tasks.filter(t => t.done).length
    statsEl.textContent = `${done} of ${total} tasks completed`

    // Submit button state
    submitBtn.disabled = state.submitting
    submitBtn.textContent = state.submitting ? 'Adding...' : 'Add Task'

    // Loading
    if (state.loading) {
        listEl.innerHTML = '<p>Loading tasks...</p>'
        return
    }

    // Error
    if (state.error) {
        listEl.innerHTML = `
            <p style="color:red">${state.error}</p>
            <button onclick="loadTasks()">Retry</button>
        `
        return
    }

    // Empty
    if (state.tasks.length === 0) {
        listEl.innerHTML = '<p>No tasks yet. Add one above!</p>'
        return
    }

    // Render tasks
    listEl.innerHTML = state.tasks.map(task => `
        <div style="
            display:flex;
            align-items:center;
            gap:10px;
            padding:10px;
            margin:5px 0;
            border:1px solid #ccc;
            text-decoration:${task.done ? 'line-through' : 'none'};
            opacity:${task.done ? '0.6' : '1'};
        " data-id="${task.id}">
            <input
                type="checkbox"
                class="toggle-checkbox"
                data-id="${task.id}"
                ${task.done ? 'checked' : ''}
            >
            <span>${task.title}</span>
            <span>[${task.priority}]</span>
            <button class="delete-btn" data-id="${task.id}" style="margin-left:auto">Delete</button>
        </div>
    `).join('')
}

async function loadTasks() {
    state = { ...state, loading: true, error: null }
    render()

    try {
        const res = await fetch(`${API}/api/tasks`)
        if (!res.ok) throw new Error(`Server error: ${res.status}`)
        const tasks = await res.json()
        state = { ...state, tasks, loading: false }
    } catch (err) {
        state = { ...state, error: err.message, loading: false }
    }

    render()
}

async function deleteTask(id) {
    try {
        const res = await fetch(`${API}/api/tasks/${id}`, { method: 'DELETE' })
        if (!res.ok) throw new Error('Failed to delete task')
        state = { ...state, tasks: state.tasks.filter(t => t.id !== id) }
        render()
    } catch (err) {
        alert(err.message)
    }
}

async function toggleTask(id) {
    try {
        const res = await fetch(`${API}/api/tasks/${id}/toggle`, { method: 'PATCH' })
        if (!res.ok) throw new Error('Failed to update task')
        const updatedTask = await res.json()
        state = {
            ...state,
            tasks: state.tasks.map(t => t.id === id ? updatedTask : t)
        }
        render()
    } catch (err) {
        alert(err.message)
    }
}

// Form submit
document.querySelector('#taskForm').addEventListener('submit', async (e) => {
    e.preventDefault()

    const title = document.querySelector('#titleInput').value.trim()
    const priority = document.querySelector('#prioritySelect').value
    const errorEl = document.querySelector('#formError')

    errorEl.textContent = ''

    if (!title) {
        errorEl.textContent = 'Title is required'
        return
    }

    state = { ...state, submitting: true }
    render()

    try {
        const res = await fetch(`${API}/api/tasks`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ title, priority })
        })

        if (!res.ok) {
            const err = await res.json()
            throw new Error(err.error || 'Failed to add task')
        }

        const newTask = await res.json()
        state = {
            ...state,
            tasks: [...state.tasks, newTask],
            submitting: false
        }
        render()
        e.target.reset()
        document.querySelector('#titleInput').focus()

    } catch (err) {
        errorEl.textContent = err.message
        state = { ...state, submitting: false }
        render()
    }
})

// Event delegation for delete and toggle
document.querySelector('#taskList').addEventListener('click', (e) => {
    if (e.target.classList.contains('delete-btn')) {
        const id = Number(e.target.dataset.id)
        deleteTask(id)
    }
    if (e.target.classList.contains('toggle-checkbox')) {
        const id = Number(e.target.dataset.id)
        toggleTask(id)
    }
})

// Initialize
loadTasks()
```

---

## Project 4 — Mini Dashboard (Stage 4)

**Goal:** Multi-section app with auth, auto-refresh, search.

**Python (app.py):**
```python
from flask import Flask, jsonify, request
from flask_cors import CORS
import time

app = Flask(__name__)
CORS(app)

users = [
    { "id": 1, "name": "Aman", "role": "developer", "active": True },
    { "id": 2, "name": "Ravi", "role": "designer", "active": True },
    { "id": 3, "name": "Priya", "role": "manager", "active": False }
]

tasks = [
    { "id": 1, "title": "Build dashboard", "done": True },
    { "id": 2, "title": "Write tests", "done": False },
    { "id": 3, "title": "Deploy to server", "done": False }
]

@app.route('/api/users')
def get_users():
    return jsonify(users)

@app.route('/api/tasks')
def get_tasks():
    return jsonify(tasks)

@app.route('/api/stats')
def get_stats():
    return jsonify({
        "total_users": len(users),
        "active_users": len([u for u in users if u['active']]),
        "total_tasks": len(tasks),
        "done_tasks": len([t for t in tasks if t['done']]),
        "server_time": time.strftime("%H:%M:%S")
    })

@app.route('/api/login', methods=['POST'])
def login():
    data = request.get_json()
    if data.get('username') == 'admin' and data.get('password') == 'admin':
        return jsonify({ "token": "fake-jwt-token-123", "username": "admin" })
    return jsonify({ "error": "Invalid credentials" }), 401

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dashboard</title>
</head>
<body>
    <!-- Login form -->
    <div id="loginSection">
        <h2>Login</h2>
        <input type="text" id="usernameInput" placeholder="admin">
        <input type="password" id="passwordInput" placeholder="admin">
        <button id="loginBtn">Login</button>
        <p id="loginError" style="color:red"></p>
    </div>

    <!-- Dashboard -->
    <div id="dashboardSection" style="display:none">
        <p>Welcome, <span id="welcomeUser"></span></p>
        <button id="logoutBtn">Logout</button>
        <input type="text" id="globalSearch" placeholder="Search...">

        <!-- Sidebar -->
        <button class="nav-btn" data-section="stats">Stats</button>
        <button class="nav-btn" data-section="users">Users</button>
        <button class="nav-btn" data-section="tasks">Tasks</button>

        <!-- Content area -->
        <div id="dashContent"></div>
    </div>

    <script src="app.js"></script>
</body>
</html>
```

**app.js:**
```javascript
const API = 'http://localhost:5000'

let state = {
    currentSection: 'stats',
    data: { stats: null, users: [], tasks: [] },
    loaded: { stats: false, users: false, tasks: false },
    loading: false,
    error: null,
    searchQuery: ''
}

let refreshInterval = null

// ── Auth ──────────────────────────────────────────

function getToken() {
    return localStorage.getItem('token')
}

async function login() {
    const username = document.querySelector('#usernameInput').value.trim()
    const password = document.querySelector('#passwordInput').value.trim()
    const errorEl = document.querySelector('#loginError')
    const loginBtn = document.querySelector('#loginBtn')

    errorEl.textContent = ''
    loginBtn.disabled = true
    loginBtn.textContent = 'Logging in...'

    try {
        const res = await fetch(`${API}/api/login`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ username, password })
        })

        if (!res.ok) throw new Error('Invalid credentials')

        const { token, username: user } = await res.json()
        localStorage.setItem('token', token)
        localStorage.setItem('username', user)

        showDashboard()
    } catch (err) {
        errorEl.textContent = err.message
    } finally {
        loginBtn.disabled = false
        loginBtn.textContent = 'Login'
    }
}

function logout() {
    localStorage.removeItem('token')
    localStorage.removeItem('username')
    clearInterval(refreshInterval)
    document.querySelector('#dashboardSection').style.display = 'none'
    document.querySelector('#loginSection').style.display = 'block'
}

function showDashboard() {
    document.querySelector('#loginSection').style.display = 'none'
    document.querySelector('#dashboardSection').style.display = 'block'
    document.querySelector('#welcomeUser').textContent = localStorage.getItem('username')

    loadSection('stats')
    startAutoRefresh()
}

// ── API helpers ──────────────────────────────────────────

async function authFetch(endpoint) {
    const res = await fetch(`${API}${endpoint}`, {
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${getToken()}`
        }
    })
    if (!res.ok) throw new Error(`Error ${res.status}`)
    return res.json()
}

// ── Section loading ──────────────────────────────────────────

async function loadSection(section) {
    state = { ...state, currentSection: section, loading: true, error: null }
    renderSection()

    // Only fetch if not loaded yet (lazy loading)
    if (!state.loaded[section]) {
        try {
            const data = await authFetch(`/api/${section}`)
            state = {
                ...state,
                data: { ...state.data, [section]: data },
                loaded: { ...state.loaded, [section]: true },
                loading: false
            }
        } catch (err) {
            state = { ...state, error: err.message, loading: false }
        }
    } else {
        state = { ...state, loading: false }
    }

    renderSection()
}

async function refreshCurrentSection() {
    const section = state.currentSection
    try {
        const data = await authFetch(`/api/${section}`)
        state = {
            ...state,
            data: { ...state.data, [section]: data }
        }
        renderSection()
    } catch (err) {
        console.error("Auto-refresh failed:", err.message)
    }
}

function startAutoRefresh() {
    refreshInterval = setInterval(refreshCurrentSection, 30000)
}

// ── Search and filter ──────────────────────────────────────────

function debounce(fn, delay) {
    let timer
    return (...args) => {
        clearTimeout(timer)
        timer = setTimeout(() => fn(...args), delay)
    }
}

const applySearch = debounce((query) => {
    state = { ...state, searchQuery: query }
    renderSection()
}, 300)

// ── Rendering ──────────────────────────────────────────

function renderSection() {
    const el = document.querySelector('#dashContent')
    const { currentSection, loading, error, data, searchQuery } = state

    if (loading) { el.innerHTML = '<p>Loading...</p>'; return }
    if (error) { el.innerHTML = `<p style="color:red">${error}</p>`; return }

    if (currentSection === 'stats') {
        const s = data.stats
        if (!s) return
        el.innerHTML = `
            <h2>Stats</h2>
            <p>Total users: ${s.total_users}</p>
            <p>Active users: ${s.active_users}</p>
            <p>Total tasks: ${s.total_tasks}</p>
            <p>Done tasks: ${s.done_tasks}</p>
            <p>Server time: ${s.server_time}</p>
        `
    }

    if (currentSection === 'users') {
        let users = data.users
        if (searchQuery) {
            const q = searchQuery.toLowerCase()
            users = users.filter(u => u.name.toLowerCase().includes(q))
        }
        el.innerHTML = `
            <h2>Users (${users.length})</h2>
            ${users.map(u => `
                <div>
                    <strong>${u.name}</strong>
                    ${u.role}
                    ${u.active ? '✓ Active' : '✗ Inactive'}
                </div>
            `).join('')}
        `
    }

    if (currentSection === 'tasks') {
        let tasks = data.tasks
        if (searchQuery) {
            const q = searchQuery.toLowerCase()
            tasks = tasks.filter(t => t.title.toLowerCase().includes(q))
        }
        el.innerHTML = `
            <h2>Tasks (${tasks.length})</h2>
            ${tasks.map(t => `
                <div style="text-decoration:${t.done ? 'line-through' : 'none'}">
                    ${t.done ? '✓' : '○'} ${t.title}
                </div>
            `).join('')}
        `
    }
}

// ── Event listeners ──────────────────────────────────────────

document.querySelector('#loginBtn').addEventListener('click', login)

document.querySelectorAll('.nav-btn').forEach(btn => {
    btn.addEventListener('click', () => loadSection(btn.dataset.section))
})

document.querySelector('#logoutBtn').addEventListener('click', logout)

document.querySelector('#globalSearch').addEventListener('input', (e) => {
    applySearch(e.target.value)
})

// ── Initialize ──────────────────────────────────────────

if (getToken()) {
    showDashboard()
} else {
    document.querySelector('#loginSection').style.display = 'block'
}
```

---

# Quick Reference

## Array methods cheatsheet

| Method | What it does | Returns |
|---|---|---|
| `.map(fn)` | Transform each item | New array |
| `.filter(fn)` | Keep matching items | New array |
| `.find(fn)` | First matching item | Item or undefined |
| `.findIndex(fn)` | Index of first match | Number |
| `.forEach(fn)` | Loop through | undefined |
| `.some(fn)` | Any match? | Boolean |
| `.every(fn)` | All match? | Boolean |
| `.reduce(fn, init)` | Combine to one value | Anything |
| `.includes(val)` | Contains value? | Boolean |
| `.indexOf(val)` | Index of value | Number |
| `.push(val)` | Add to end | New length |
| `.pop()` | Remove from end | Removed item |
| `.slice(start, end)` | Copy portion | New array |
| `.splice(i, n)` | Remove n from index i | Removed items |
| `.sort(fn)` | Sort in place | Mutated array |
| `.join(sep)` | Array to string | String |
| `.flat(depth)` | Flatten nested | New array |

## fetch() cheatsheet

```javascript
// GET
const data = await fetch('/api/resource').then(r => r.json())

// POST
const res = await fetch('/api/resource', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
})

// DELETE
await fetch(`/api/resource/${id}`, { method: 'DELETE' })

// With auth token
const res = await fetch('/api/secure', {
    headers: { 'Authorization': `Bearer ${localStorage.getItem('token')}` }
})
```

## State pattern cheatsheet

```javascript
// 1. Define state
let state = { data: [], loading: false, error: null }

// 2. render() always builds from state
function render() { /* build UI from state */ }

// 3. Only update state, then call render()
state = { ...state, loading: true }
render()

// 4. Never update DOM directly — go through state
```

## Common DOM operations

```javascript
// Select
document.querySelector('#id')
document.querySelectorAll('.class')

// Read
el.textContent
el.value            // for inputs
el.dataset.id       // data-id attribute

// Write
el.textContent = "text"
el.innerHTML = "<b>html</b>"
el.style.display = 'none'
el.classList.toggle('active')

// Create
const div = document.createElement('div')
parent.appendChild(div)
parent.innerHTML = template    // faster for lists

// Events
el.addEventListener('click', handler)
form.addEventListener('submit', e => { e.preventDefault(); ... })
```

---

*End of guide. Now close this file and write code.*
