# JavaScript — Complete Explained Guide
### Every concept explained in plain English. Every line explained.

---

> You know Python. This guide explains JS from scratch, comparing to Python where helpful.
> Every line of code has an explanation. No skipping.

---

# CHAPTER 1 — How JavaScript Works

## Where does JS run?

Python runs in your terminal through the Python interpreter.
JS runs inside your browser — Chrome, Firefox, Edge.

When browser opens a webpage, it downloads:
- HTML — the structure (headings, paragraphs, buttons)
- CSS — the appearance (colors, sizes)
- JavaScript — the behavior (what happens when you click, what data to show)

You do not need Node.js. You do not need to install anything.
The browser already has JS built in.

## How to run JS right now

Open Chrome. Press **F12**. Click **Console** tab.

Type this and press Enter:
```javascript
console.log("hello world")
```

`console.log()` is exactly like Python's `print()`.
You just ran JavaScript in your browser.

## Linking JS to HTML

Create two files in the same folder.

**index.html:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>My App</title>
</head>
<body>

    <h1 id="title">Hello</h1>

    <!-- This line tells browser to load your JS file -->
    <!-- ALWAYS put this at bottom, just before </body> -->
    <script src="app.js"></script>

</body>
</html>
```

**Why at the bottom?**
HTML loads top to bottom. If your script is at the top, it runs before `<h1>` exists.
Then when JS tries to find the `<h1>`, it does not exist yet — error.
Putting script at the bottom means all HTML is already loaded before JS runs.

**app.js:**
```javascript
console.log("JS is running")
```

Open index.html in browser, press F12, look at Console tab.
You will see "JS is running".

---

# CHAPTER 2 — Variables

## Three ways to declare variables

Python has one way: `name = "Aman"`
JS has three. Simple rule:

```javascript
// const — value cannot be reassigned. Use this by default.
const name = "Aman"
const age = 20
const apiUrl = "http://localhost:5000"

// let — value can be reassigned. Use when value needs to change.
let count = 0
count = 1    // works — let allows reassignment
count = 2    // works

// var — old way. Has bugs. Never use.
var x = 5    // pretend this does not exist
```

**Rule: Always start with `const`. If you get an error saying you cannot reassign, switch to `let`. Never use `var`.**

Why `const` exists: it protects important values from accidentally changing.
```javascript
const apiUrl = "http://localhost:5000"
apiUrl = "something else"    // ERROR — this is good protection
```

## Data Types

```javascript
// String — text. Three ways to write:
const name = "Aman"              // double quotes
const city = 'Nashik'            // single quotes — same thing
const greeting = `Hello ${name}` // backtick — special, for inserting variables

// Number — JS has ONE number type for both integers and decimals
// Python has int and float. JS has just number.
const age = 20          // whole number
const price = 99.5      // decimal — no "float" type needed
const negative = -10

// Boolean — true or false
// NOTE: lowercase in JS. Python uses uppercase True/False.
const isLoggedIn = true
const hasError = false

// null — you explicitly set this to mean "no value right now"
const userData = null

// undefined — JS sets this when you declare a variable but give no value
let result                // declared but no value
console.log(result)      // prints: undefined

// Array — same as Python list
const fruits = ["apple", "banana", "mango"]

// Object — same as Python dictionary
const user = {
    name: "Aman",    // key: value pairs
    age: 20,
    isStudent: true
}
```

## The Biggest Difference From Python — Equality

This trips every Python developer in JS. Learn it once, never get confused again.

```javascript
// In Python: == compares values and is generally safe
// In JS: == does "type coercion" — tries to convert types to match

5 == "5"       // TRUE in JS — it converted string "5" to number 5
0 == false     // TRUE in JS — it converted false to 0
"" == false    // TRUE in JS — dangerous!

// === is STRICT equality — checks value AND type, no conversion
// ALWAYS USE === IN JS

5 === "5"      // FALSE — different types (number vs string)
5 === 5        // TRUE — same value, same type
"hi" === "hi"  // TRUE

// !== is strict not equal — ALWAYS USE THIS TOO
5 !== "5"      // TRUE — strictly not equal

// RULE: Always === and !==. Never == and !=.
```

## Truthy and Falsy

In JS, values that behave like `false` in if-statements:
```javascript
// These are all FALSY (like Python's False):
false
0
""           // empty string
null
undefined
NaN          // Not a Number (result of things like 0/0)

// IMPORTANT DIFFERENCE FROM PYTHON:
[]   // empty array — TRUTHY in JS (falsy in Python!)
{}   // empty object — TRUTHY in JS (falsy in Python!)

// Example:
if ([]) {
    console.log("runs!")    // YES, this runs — [] is truthy
}
if ("") {
    console.log("runs!")    // NO, this does not run — "" is falsy
}
```

---

# CHAPTER 3 — Template Literals

Template literals are JS's version of Python f-strings.
Use backtick character ` (key below Escape) instead of quotes.

```javascript
const name = "Aman"
const age = 20

// Old way — messy concatenation with +
const msg = "Hello, my name is " + name + " and I am " + age + " years old."

// Template literal — clean, readable
// Put variable inside ${ }
const msg = `Hello, my name is ${name} and I am ${age} years old.`

// Any expression works inside ${ }
const result = `Two plus three is ${2 + 3}`           // "Two plus three is 5"
const upper = `Uppercase: ${name.toUpperCase()}`      // "Uppercase: AMAN"

// Multi-line — just press Enter inside backticks
const html = `
    <div class="card">
        <h2>${name}</h2>
        <p>Age: ${age}</p>
    </div>
`
// This builds an HTML string with your data inside
// You will use this constantly to show Python data on the page
```

---

# CHAPTER 4 — Strings

A "method" is a function that belongs to a value. You call it with a dot.

```javascript
const name = "Aman Sharma"

// .length — number of characters. Property, not method, so no ()
name.length            // 11
// Why no ()? length is a stored value, not a function. Properties have no ().

// .toUpperCase() and .toLowerCase()
name.toUpperCase()     // "AMAN SHARMA"
name.toLowerCase()     // "aman sharma"
// Original name is not changed. Returns new string.

// .trim() — removes spaces from start and end
"  hello  ".trim()     // "hello"
// Use this always on form input values — users often accidentally add spaces

// .includes() — does the string contain this text?
name.includes("Aman")  // true
name.includes("Ravi")  // false

// .startsWith() / .endsWith()
name.startsWith("Aman")  // true
name.endsWith("rma")     // true

// .replace() — replace first match
"hello world".replace("world", "JS")   // "hello JS"

// .split() — break into array at separator (like Python split())
"apple,banana,mango".split(",")        // ["apple", "banana", "mango"]
"hello".split("")                      // ["h", "e", "l", "l", "o"]

// .slice(start, end) — get part of string
// end index is NOT included
"hello world".slice(0, 5)    // "hello"
"hello world".slice(6)       // "world" — from index 6 to end
"hello world".slice(-5)      // "world" — last 5 characters

// Converting string to number
Number("42")       // 42
Number("3.14")     // 3.14
Number("hello")    // NaN — conversion failed

// Converting number to string
String(42)         // "42"
(42).toString()    // "42"
```

---

# CHAPTER 5 — Arrays

```javascript
// Create
const fruits = ["apple", "banana", "mango", "orange"]
const empty = []

// Access — 0 indexed same as Python
fruits[0]     // "apple"
fruits[3]     // "orange"

// DIFFERENCE FROM PYTHON: negative indexing does NOT work
fruits[-1]    // undefined — not "orange" like Python!

// To get last item in JS:
fruits[fruits.length - 1]    // "orange"
// fruits.length is 4, so fruits[4-1] = fruits[3] = "orange"

// Length
fruits.length    // 4

// Check if value exists
fruits.includes("banana")    // true
fruits.includes("grape")     // false

// Find index (returns -1 if not found)
fruits.indexOf("mango")      // 2
fruits.indexOf("grape")      // -1
```

## Adding and Removing

```javascript
const arr = [1, 2, 3]

// push() — add to end (like Python append())
arr.push(4)       // arr = [1, 2, 3, 4]
arr.push(5, 6)    // arr = [1, 2, 3, 4, 5, 6]

// pop() — remove from end (like Python pop())
arr.pop()         // removes 6, returns 6. arr = [1, 2, 3, 4, 5]

// unshift() — add to start
arr.unshift(0)    // arr = [0, 1, 2, 3, 4, 5]

// shift() — remove from start
arr.shift()       // removes 0. arr = [1, 2, 3, 4, 5]

// filter to remove by value — most common in real apps
const withoutThree = arr.filter(n => n !== 3)
// withoutThree = [1, 2, 4, 5] — arr unchanged
// This is how you remove a deleted task from state
```

## The Important Array Methods

### forEach — loop through array

```javascript
const users = ["Aman", "Ravi", "Priya"]

// Python: for user in users: print(user)
users.forEach(user => {
    // "user" is the name you give each item — choose any name
    // => is the arrow function syntax, like lambda in Python
    console.log(user)
})
// prints: Aman, Ravi, Priya

// With index:
users.forEach((user, index) => {
    // index is automatically the second parameter
    console.log(`${index}: ${user}`)
})
// prints: 0: Aman, 1: Ravi, 2: Priya
```

### map — transform each item, get new array

```javascript
const numbers = [1, 2, 3, 4, 5]

// Python: [x * 2 for x in numbers]
const doubled = numbers.map(n => n * 2)
// doubled = [2, 4, 6, 8, 10]
// numbers is still [1, 2, 3, 4, 5] — map does NOT change original

// Real use — Python API returns user objects, you want just names
const users = [
    { id: 1, name: "Aman", role: "developer" },
    { id: 2, name: "Ravi", role: "designer" }
]

const names = users.map(user => user.name)
// names = ["Aman", "Ravi"]
// For each user object, we return just user.name

// Building HTML strings — this is how you render data on page
const html = users
    .map(user => `<div class="card">${user.name} — ${user.role}</div>`)
    .join('')
// .join('') connects all strings into one string with no separator
// html = '<div class="card">Aman — developer</div><div class="card">Ravi — designer</div>'

document.querySelector('#users').innerHTML = html
// This puts all the cards on the page at once
```

### filter — keep only matching items

```javascript
const users = [
    { name: "Aman", age: 20, role: "developer" },
    { name: "Ravi", age: 25, role: "designer" },
    { name: "Priya", age: 22, role: "developer" },
    { name: "Kiran", age: 30, role: "manager" }
]

// Python: [u for u in users if u['role'] == 'developer']
const developers = users.filter(user => user.role === "developer")
// developers = [Aman's object, Priya's object]
// users is unchanged

// Filter by search query — user types in search box
const query = "a"
const results = users.filter(user =>
    user.name.toLowerCase().includes(query.toLowerCase())
    // toLowerCase on both sides = case-insensitive search
    // includes() = is query anywhere in the name?
)
// results = [Aman, Ravi, Kiran] — all contain letter "a"

// Remove item by ID — when user deletes a task
const taskId = 2
const updatedTasks = tasks.filter(task => task.id !== taskId)
// Returns all tasks EXCEPT the one with id 2
// Original tasks array is unchanged
```

### find — get first match

```javascript
const users = [
    { id: 1, name: "Aman" },
    { id: 2, name: "Ravi" },
    { id: 3, name: "Priya" }
]

// Returns the ITEM ITSELF (not an array, not array of one)
const user = users.find(u => u.id === 2)
// user = { id: 2, name: "Ravi" }

const notFound = users.find(u => u.id === 99)
// notFound = undefined — not an error, just undefined

// Always check if found before using:
const user = users.find(u => u.id === 2)
if (user) {
    console.log(user.name)    // safe — only runs if user was found
}
```

### sort — sort the array

```javascript
const nums = [10, 1, 21, 2]

// Default sort converts to strings first — WRONG for numbers!
nums.sort()    // [1, 10, 2, 21] — sorted as strings, wrong!

// Always use comparison function for numbers:
nums.sort((a, b) => a - b)    // [1, 2, 10, 21] — ascending, correct
nums.sort((a, b) => b - a)    // [21, 10, 2, 1] — descending

// How does the comparison function work?
// If (a - b) is negative: a comes before b
// If (a - b) is positive: b comes before a
// If 0: same, keep order

// Sort objects by name:
users.sort((a, b) => a.name.localeCompare(b.name))
// localeCompare works like a - b but for strings
// Returns negative/positive/0 — exactly what sort needs
```

## Spread Operator `...`

```javascript
const a = [1, 2, 3]
const b = [4, 5, 6]

// Combine arrays — ... "unpacks" each array
const combined = [...a, ...b]    // [1, 2, 3, 4, 5, 6]

// Copy array — new array, no shared reference
const copy = [...a]    // [1, 2, 3]
copy.push(4)           // a is still [1, 2, 3]

// Add item without changing original
const withFour = [...a, 4]    // [1, 2, 3, 4]
// a is still [1, 2, 3]

// This is important for state updates:
state = { ...state, tasks: [...state.tasks, newTask] }
// Adds newTask to end without mutating original state
```

## Array Destructuring

```javascript
const fruits = ["apple", "banana", "mango"]

// Old way
const first = fruits[0]
const second = fruits[1]

// Destructuring — extracts values into named variables
const [first, second, third] = fruits
// first = "apple", second = "banana", third = "mango"

// Skip items with empty comma
const [, , third] = fruits
// third = "mango" (first two skipped)

// Rest — collect remaining into array
const [head, ...rest] = fruits
// head = "apple"
// rest = ["banana", "mango"]
```

---

# CHAPTER 6 — Objects

Objects are THE most important thing when working with APIs.
Your Python backend sends JSON. JSON is objects and arrays.

```javascript
const user = {
    name: "Aman",                   // string value
    age: 20,                        // number value
    isStudent: true,                // boolean value
    courses: ["Python", "JS"],      // array value
    address: {                      // nested object value
        street: "MG Road",
        pincode: "422001"
    }
}

// Two ways to access values:
user.name           // "Aman" — dot notation, most common
user["name"]        // "Aman" — bracket notation

// When to use bracket notation?
// When the key is stored in a variable:
const field = "age"
user[field]         // 20 — looks up user["age"]
// user.field would look for a key literally called "field" — wrong

// Nested access:
user.address.street    // "MG Road"
user.courses[0]        // "Python"
user.courses[1]        // "JS"

// Add new property:
user.email = "aman@gmail.com"

// Update property:
user.age = 21

// Delete property:
delete user.city

// Check if property exists:
"name" in user      // true
"salary" in user    // false
```

## Object Methods

```javascript
const user = { name: "Aman", age: 20, city: "Nashik" }

// Get all keys as array
Object.keys(user)      // ["name", "age", "city"]

// Get all values as array
Object.values(user)    // ["Aman", 20, "Nashik"]

// Get key-value pairs
Object.entries(user)   // [["name","Aman"], ["age",20], ["city","Nashik"]]

// Loop through object:
Object.entries(user).forEach(([key, value]) => {
    // [key, value] destructures each ["name", "Aman"] pair
    // into separate variables key and value
    console.log(`${key}: ${value}`)
})
// prints:
// name: Aman
// age: 20
// city: Nashik
```

## Object Destructuring

```javascript
const user = { name: "Aman", age: 20, city: "Nashik", role: "developer" }

// Old way
const name = user.name
const age = user.age

// Destructuring — creates variables matching key names automatically
const { name, age, role } = user
// name = "Aman", age = 20, role = "developer"

// Rename while destructuring:
const { name: userName, age: userAge } = user
// userName = "Aman" (the key is name, we renamed the variable to userName)
// userAge = 20

// Default values if key doesn't exist:
const { name, salary = 0 } = user
// salary = 0 — user has no salary key, so default is used

// Destructuring in function parameters:
// Instead of:
function showUser(user) {
    console.log(user.name, user.age)
}

// You can destructure directly in parameter:
function showUser({ name, age }) {
    // name and age extracted automatically from passed object
    console.log(name, age)
}

showUser({ name: "Aman", age: 20 })    // works perfectly
// Very useful with API data — your Python data arrives as objects
```

## Spread With Objects

```javascript
const user = { name: "Aman", age: 20 }
const location = { city: "Nashik", country: "India" }

// Merge two objects
const fullProfile = { ...user, ...location }
// fullProfile = { name: "Aman", age: 20, city: "Nashik", country: "India" }
// ... spreads all properties of each object into the new object

// Copy object (no shared reference)
const copy = { ...user }

// Update one property without changing original:
const updated = { ...user, age: 21 }
// updated = { name: "Aman", age: 21 }
// user is still { name: "Aman", age: 20 }

// THIS IS THE KEY STATE UPDATE PATTERN:
let state = { users: [], loading: false, error: null }

// Update loading while keeping everything else:
state = { ...state, loading: true }
// state = { users: [], loading: true, error: null }
// Spread keeps users and error, then loading: true overrides loading

// Update multiple fields:
state = { ...state, loading: false, error: "something failed" }
// state = { users: [], loading: false, error: "something failed" }
```

## Shorthand Property Names

```javascript
const name = "Aman"
const age = 20

// Old way — repeating yourself
const user = { name: name, age: age }

// Shorthand — when variable name equals key name
const user = { name, age }
// JS sees: the key should be "name", and the value should be the variable "name"
// Same as { name: name, age: age }

// Common when sending data to Python:
async function createUser(name, role) {
    await fetch('/api/users', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ name, role })    // shorthand for { name: name, role: role }
    })
}
```

---

# CHAPTER 7 — Functions

```javascript
// Way 1: Function declaration — can be called before it's defined
function greet(name) {
    return `Hello ${name}`
}
greet("Aman")    // "Hello Aman"

// Way 2: Arrow function — most modern, use this most of the time
const greet = (name) => {
    return `Hello ${name}`
}

// Arrow function short form — when body is ONE expression, skip {} and return
const greet = (name) => `Hello ${name}`
// The expression is automatically returned

// Single parameter — can skip parentheses
const greet = name => `Hello ${name}`

// No parameters — must have empty ()
const sayHello = () => "Hello everyone"

// Multiple parameters
const add = (a, b) => a + b

// Multiple lines — needs {} and explicit return
const calculate = (a, b) => {
    const sum = a + b
    const product = a * b
    return { sum, product }
}
```

## Default Parameters

```javascript
// If argument not provided, use default value
function greet(name = "stranger") {
    return `Hello ${name}`
}

greet()          // "Hello stranger" — used default
greet("Aman")    // "Hello Aman" — used provided value
```

## Rest Parameters

```javascript
// Collects all arguments into an array — like Python *args
function sum(...numbers) {
    // numbers is an array of everything passed
    return numbers.reduce((total, n) => total + n, 0)
}

sum(1, 2, 3)         // 6
sum(1, 2, 3, 4, 5)   // 15
```

## Functions as Values

In JS, functions are values. You can store them in variables, pass them as arguments.

```javascript
// Storing function in variable
const sayHi = () => "Hi!"
const myFn = sayHi    // myFn holds the same function
myFn()                // "Hi!"

// Passing function to another function — this is how forEach, map, filter work
// setTimeout runs a function after a delay
setTimeout(() => {
    // This arrow function is passed as first argument to setTimeout
    console.log("2 seconds later")
}, 2000)    // 2000 milliseconds = 2 seconds
// setTimeout will call that function after 2 seconds
```

---

# CHAPTER 8 — Scope

Scope = where can I access a variable?

```javascript
// Global scope — outside all functions, accessible everywhere
const apiUrl = "http://localhost:5000"

function loadUsers() {
    console.log(apiUrl)    // can access global variable
}

// Function scope — only inside the function
function loadUsers() {
    const users = []    // only exists inside loadUsers
}
console.log(users)    // ERROR — users doesn't exist here

// Block scope — only inside { } with let or const
if (true) {
    const blockVar = "inside block"
    console.log(blockVar)    // works
}
console.log(blockVar)        // ERROR — outside the block

// var ignores block scope — another reason never to use it
if (true) {
    var leaked = "I escape blocks!"
}
console.log(leaked)    // "I escape blocks!" — var leaked out!
```

## Scope Chain

When JS looks for a variable, it starts at the current scope.
If not found, looks at the outer scope. Then outer's outer. All the way to global.

```javascript
const level1 = "global"

function outer() {
    const level2 = "outer function"

    function inner() {
        const level3 = "inner function"

        // inner can see ALL three:
        console.log(level1)    // "global" — found by going up to global
        console.log(level2)    // "outer function" — found by going up to outer
        console.log(level3)    // "inner function" — found in own scope
    }

    // outer can only see level1 and level2:
    console.log(level3)    // ERROR — level3 only exists in inner, below outer
}
```

---

# CHAPTER 9 — Closures

A closure happens when an inner function remembers variables from its outer function,
even after the outer function has finished executing.

In Python: when a function finishes, its variables disappear.
In JS: inner functions keep a reference to outer function's variables. They stay alive.

```javascript
// When makeCounter() runs and returns, you might think count is gone.
// But the returned inner function still has a reference to count.
// Count stays alive as long as the returned function exists.

function makeCounter() {
    let count = 0    // count lives in makeCounter's scope

    return function() {
        count = count + 1    // inner function accesses count from outer scope
        return count
    }
}

const counter = makeCounter()
// makeCounter has finished. But count lives on because inner function references it.

counter()    // 1
counter()    // 2
counter()    // 3

// count cannot be accessed directly:
counter.count    // undefined — it's private!
```

## Why Closures Matter — Real Example

```javascript
// Create API caller with base URL baked in through closure
function createApiCaller(baseUrl) {
    // baseUrl is in createApiCaller's scope

    // These inner functions close over baseUrl
    // Even after createApiCaller finishes, they remember baseUrl

    async function get(endpoint) {
        // baseUrl comes from outer scope via closure
        const res = await fetch(baseUrl + endpoint)
        return res.json()
    }

    async function post(endpoint, data) {
        const res = await fetch(baseUrl + endpoint, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(data)
        })
        return res.json()
    }

    return { get, post }
}

const api = createApiCaller('http://localhost:5000')
// createApiCaller is done running. But get and post remember baseUrl.

const users = await api.get('/api/users')
// Internally: fetch('http://localhost:5000/api/users')

const newUser = await api.post('/api/users', { name: 'Aman' })
// Internally: fetch('http://localhost:5000/api/users') with POST
```

## The Classic Closure Bug

```javascript
// Adding click listeners in a loop — tricky

// WRONG — using var
for (var i = 0; i < 3; i++) {
    buttons[i].addEventListener('click', () => {
        console.log(i)    // always prints 3! not 0, 1, 2
    })
}
// Why? var doesn't create a new scope each loop iteration.
// All three functions share THE SAME i.
// By click time, loop is done and i = 3.

// CORRECT — use let (creates new scope each iteration)
for (let i = 0; i < 3; i++) {
    buttons[i].addEventListener('click', () => {
        console.log(i)    // correctly prints 0, 1, or 2
    })
}
// Why? let creates a new i for each iteration. Each function has its own i.

// BEST — use forEach with the actual data
const items = ["apple", "banana", "mango"]
items.forEach((item, index) => {
    buttons[index].addEventListener('click', () => {
        console.log(item)    // correctly prints the fruit name
    })
})
```

---

# CHAPTER 10 — The `this` Keyword

`this` refers to the "context" — the object that called the function.
For your use case, follow one simple rule and you'll be fine.

```javascript
// In an object method, this = the object
const user = {
    name: "Aman",
    greet: function() {
        // this is the user object here
        console.log(`Hello, I am ${this.name}`)
    }
}
user.greet()    // "Hello, I am Aman"

// PROBLEM: regular function in callback loses this
const user = {
    name: "Aman",
    greetLater: function() {
        setTimeout(function() {
            // Here, this is NOT user. It's the global window object.
            // setTimeout called this function without user as context.
            console.log(this.name)    // undefined
        }, 1000)
    }
}

// SOLUTION: arrow functions inherit this from surrounding scope
const user = {
    name: "Aman",
    greetLater: function() {
        setTimeout(() => {
            // Arrow function has no own this
            // It uses this from greetLater — which is user
            console.log(this.name)    // "Aman"
        }, 1000)
    }
}

// YOUR PRACTICAL RULE:
// Always use arrow functions for event listeners and callbacks.
// You will almost never need to worry about this.

button.addEventListener('click', () => {
    // Arrow function — no this issues
    // Just call your functions directly
    loadUsers()
})
```

---

# CHAPTER 11 — Conditionals and Loops

```javascript
// if / else if / else — same as Python, but with () and {}
const age = 20

if (age >= 18) {
    console.log("adult")
} else if (age >= 13) {
    console.log("teenager")
} else {
    console.log("child")
}

// Ternary — short if/else for single values
// condition ? valueIfTrue : valueIfFalse
const label = age >= 18 ? "adult" : "minor"
const btnText = state.loading ? "Loading..." : "Submit"

// Optional chaining ?. — safe access to possibly null/undefined
const user = null
user.name      // TypeError: Cannot read 'name' of null — CRASH!
user?.name     // undefined — safe

const user = { address: null }
user.address.street    // CRASH — address is null
user?.address?.street  // undefined — safe

// Nullish coalescing ?? — use default if null or undefined
const name = user.name ?? "Anonymous"
// If user.name is null or undefined: use "Anonymous"
// If user.name is 0 or "": still use those values

// for loop
for (let i = 0; i < 5; i++) {
    // let i = 0 — start
    // i < 5 — continue while true
    // i++ — increment after each run
    console.log(i)    // 0, 1, 2, 3, 4
}

// for...of — loop through array values (like Python "for x in arr:")
const fruits = ["apple", "banana", "mango"]
for (const fruit of fruits) {
    console.log(fruit)
}

// for...in — loop through object keys
const user = { name: "Aman", age: 20 }
for (const key in user) {
    console.log(key, user[key])
}
// name Aman
// age 20

// while
let count = 0
while (count < 5) {
    console.log(count)
    count++    // MUST increment or infinite loop
}
```

---

# CHAPTER 12 — What is the DOM?

DOM = Document Object Model.

When browser loads HTML, it builds a tree of objects in memory.
Each HTML element becomes a JS object you can read and change.

Your HTML:
```html
<body>
  <div id="app">
    <h1>Hello</h1>
    <button>Click</button>
  </div>
</body>
```

Becomes this tree:
```
document
  body
    div#app
      h1
      button
```

JS can find any element, read its content, change it, show/hide it, listen for clicks.
The `document` object is your entry point to everything.

---

# CHAPTER 13 — Selecting Elements

Before changing anything, you need to find it.

```javascript
// querySelector — find FIRST matching element using CSS selector syntax
document.querySelector('#myId')         // find by id (# prefix)
document.querySelector('.myClass')      // find by class (. prefix)
document.querySelector('p')             // find by tag name
document.querySelector('button.delete-btn')  // button with that class
document.querySelector('#list .item')   // .item inside #list

// Returns the element object, or null if not found

// ALWAYS check if element exists before using it:
const el = document.querySelector('#mightNotExist')
if (el) {
    el.textContent = "found!"    // only runs if element exists
}

// querySelectorAll — find ALL matching elements
const allItems = document.querySelectorAll('.item')
// Returns NodeList — like array but not exactly

// NodeList has forEach but not map/filter/reduce
allItems.forEach(item => console.log(item))    // works
// allItems.map(...)    // ERROR

// Convert to real array to use all array methods:
const arr = Array.from(allItems)
const arr = [...allItems]    // spread into array

// Search within specific element (not whole document)
const container = document.querySelector('#container')
const items = container.querySelectorAll('.item')
// Only finds .item elements INSIDE container
```

---

# CHAPTER 14 — Reading and Changing Elements

```javascript
const title = document.querySelector('#title')
// title is now a JS object representing the h1 element

// ── Reading content ──────────────────────────────────────────────

title.textContent    // text only, no HTML tags
title.innerHTML      // text with HTML tags included

// For an element like: <h1>Hello <strong>World</strong></h1>
title.textContent    // "Hello World" — just the text
title.innerHTML      // "Hello <strong>World</strong>"

// ── Changing content ──────────────────────────────────────────────

// textContent — SAFE. Whatever you set shows as literal text.
title.textContent = "New Title"

// innerHTML — allows HTML. Parses and renders tags.
title.innerHTML = "<strong>Bold</strong> Title"
// Warning: never put user-typed text in innerHTML — security risk

// ── Show and Hide ──────────────────────────────────────────────

const box = document.querySelector('#box')

box.style.display = 'none'     // hides completely, takes no space
box.style.display = 'block'    // shows as block element
box.style.display = 'flex'     // shows as flexbox

// ── Changing style ──────────────────────────────────────────────

// CSS property names become camelCase in JS
// "background-color" in CSS → "backgroundColor" in JS
// "font-size" in CSS → "fontSize" in JS

box.style.color = 'red'
box.style.backgroundColor = '#fff'
box.style.fontSize = '18px'
box.style.width = '200px'

// ── Classes ──────────────────────────────────────────────

// Adding/removing classes is better than direct style changes
// Because you can define the style in CSS and just toggle the class

box.classList.add('active')            // add class
box.classList.remove('active')         // remove class
box.classList.toggle('active')         // add if missing, remove if present
box.classList.contains('active')       // true or false

// ── Attributes ──────────────────────────────────────────────

const link = document.querySelector('a')
link.href                             // read href
link.getAttribute('href')             // same, works for custom attributes too
link.setAttribute('href', '/new')     // set attribute
link.removeAttribute('disabled')      // remove attribute

// data- attributes — storing data in HTML elements
// HTML: <button data-id="42" data-role="admin">Click</button>
const btn = document.querySelector('button')
btn.dataset.id      // "42" — note: always a string
btn.dataset.role    // "admin"

// Reading input value
const input = document.querySelector('#nameInput')
input.value         // whatever user has typed right now
input.checked       // true/false for checkbox
```

---

# CHAPTER 15 — Creating Elements and Rendering Data

When Python sends data, you need to create HTML and put it on the page.

```javascript
// Creating elements
const div = document.createElement('div')      // <div></div>
const p = document.createElement('p')
const button = document.createElement('button')

// After creating, the element does NOT appear yet — you must append it

// Set it up:
div.textContent = "Hello World"
div.classList.add('card')
div.setAttribute('data-id', '42')

// Add to page (appears now):
const container = document.querySelector('#container')
container.appendChild(div)    // adds as LAST child of container

// Removing:
div.remove()    // removes element from page

// ── innerHTML approach — much better for rendering lists ──────────────────────────────────────────────

// When you have data from Python, build HTML string and set it all at once:
const users = [
    { id: 1, name: "Aman", role: "developer" },
    { id: 2, name: "Ravi", role: "designer" }
]

const container = document.querySelector('#users')

// Build one HTML string:
container.innerHTML = users
    .map(user => `
        <div class="card" data-id="${user.id}">
            <h3>${user.name}</h3>
            <p>${user.role}</p>
            <button class="delete-btn" data-id="${user.id}">Delete</button>
        </div>
    `)
    .join('')
// .map() creates array of HTML strings, one per user
// .join('') connects them all into one big string
// innerHTML sets entire content at once — fast

// This REPLACES everything inside #users with the new cards
// If you want to ADD to existing content: container.innerHTML += ...
```

---

# CHAPTER 16 — Events

Events are things that happen: click, type, form submit, key press.
You "listen" for events and run code when they happen.

```javascript
const button = document.querySelector('#myBtn')

// addEventListener(eventName, functionToRun)
button.addEventListener('click', () => {
    console.log("Button clicked!")
})
// Every time user clicks the button, that console.log runs

// The function gets an event object with details:
button.addEventListener('click', (event) => {
    console.log(event.target)              // the element clicked
    console.log(event.target.id)           // its id
    console.log(event.target.textContent)  // its text
    console.log(event.target.dataset.id)   // its data-id attribute
    console.log(event.clientX, event.clientY) // mouse position
})

// ── Common events ──────────────────────────────────────────────

// click — user clicks element
button.addEventListener('click', () => doSomething())

// input — fires on EVERY keystroke while typing
const searchInput = document.querySelector('#search')
searchInput.addEventListener('input', (event) => {
    const query = event.target.value    // text typed so far
    filterUsers(query)                  // filter in real time
})

// change — fires when select/checkbox changes
const roleSelect = document.querySelector('#role')
roleSelect.addEventListener('change', (event) => {
    const selected = event.target.value    // selected option value
    filterByRole(selected)
})

// submit — fires when form submits
const form = document.querySelector('#myForm')
form.addEventListener('submit', (event) => {
    // CRITICAL: call preventDefault() or page will reload!
    event.preventDefault()
    // Now handle the form yourself
    const name = document.querySelector('#name').value
    createUser(name)
})

// keydown — fires when key is pressed
document.addEventListener('keydown', (event) => {
    console.log(event.key)             // "Enter", "Escape", "a", etc
    if (event.key === 'Escape') closeModal()
    if (event.ctrlKey && event.key === 's') {
        event.preventDefault()
        saveData()
    }
})

// DOMContentLoaded — fires when HTML is fully parsed — use for initialization
document.addEventListener('DOMContentLoaded', () => {
    initApp()    // safe to run because all HTML elements exist now
})
```

## Event Delegation — One Listener for Many Elements

The problem: if you add click listener to every item in a list, you have many listeners.
Also, items added later (from API) won't have listeners.

The solution: ONE listener on the parent. Check what was clicked inside the handler.

```javascript
// You render users dynamically:
container.innerHTML = users.map(u => `
    <div class="user-card" data-id="${u.id}">
        <span>${u.name}</span>
        <button class="edit-btn">Edit</button>
        <button class="delete-btn">Delete</button>
    </div>
`).join('')

// WRONG: add listener to every button
// These work for CURRENT buttons, but not for future ones
container.querySelectorAll('.delete-btn').forEach(btn => {
    btn.addEventListener('click', () => deleteUser(btn.dataset.id))
})

// RIGHT: ONE listener on container catches ALL clicks inside
container.addEventListener('click', (event) => {
    // event.target = exact element clicked (could be button, span, etc)

    if (event.target.classList.contains('delete-btn')) {
        // A delete button was clicked
        // Find the parent card to get the user id
        const card = event.target.closest('.user-card')
        // .closest() walks UP the DOM tree to find nearest ancestor matching selector
        const userId = card.dataset.id
        deleteUser(userId)
    }

    if (event.target.classList.contains('edit-btn')) {
        const card = event.target.closest('.user-card')
        const userId = card.dataset.id
        editUser(userId)
    }
})
// This ONE listener handles ALL current and future user cards
```

---

# CHAPTER 17 — State Pattern

This is the most important design pattern for UI code.

## The Problem Without State

```javascript
// Without state — chaos when things get complex
function showLoading() {
    document.querySelector('#list').innerHTML = '<p>Loading...</p>'
}

function filterUsers(role) {
    // WHERE IS THE ORIGINAL DATA? We replaced it with innerHTML!
    // We have no idea what the full list was anymore.
}
```

## The Solution — State Object

All data in one object. UI always built from that data.
Change data → call render() → UI updates.

```javascript
// ── 1. Define state — all data lives here ──────────────────────────────────────────────
let state = {
    users: [],           // full list from Python API
    filteredUsers: [],   // what's currently displayed
    loading: false,      // are we fetching data?
    error: null,         // error message or null
    searchQuery: '',     // current search input value
    filter: 'all'        // current role filter selection
}

// ── 2. render() — builds UI from state, called every time state changes ──────────────────────────────────────────────
function render() {
    const container = document.querySelector('#userList')
    const loadBtn = document.querySelector('#loadBtn')

    // Update button
    loadBtn.disabled = state.loading
    // If loading is true: button is disabled (can't click)
    // If loading is false: button is enabled
    loadBtn.textContent = state.loading ? "Loading..." : "Load Users"

    // Loading state — show spinner, stop here
    if (state.loading) {
        container.innerHTML = `<div>Loading...</div>`
        return    // return stops render here, rest doesn't run
    }

    // Error state — show error message and retry button, stop here
    if (state.error) {
        container.innerHTML = `
            <p style="color:red">${state.error}</p>
            <button onclick="loadUsers()">Try Again</button>
        `
        return
    }

    // Empty state — no results
    if (state.filteredUsers.length === 0) {
        container.innerHTML = `<p>No users match your search.</p>`
        return
    }

    // Normal state — render the list
    container.innerHTML = state.filteredUsers
        .map(user => `
            <div class="card" data-id="${user.id}">
                <h3>${user.name}</h3>
                <p>${user.role}</p>
                <button class="delete-btn" data-id="${user.id}">Delete</button>
            </div>
        `)
        .join('')
}

// ── 3. State update functions — always update state then call render() ──────────────────────────────────────────────

// Never update DOM directly. Always go through state.

async function loadUsers() {
    // Update state to show loading
    state = { ...state, loading: true, error: null }
    // { ...state } keeps everything, then loading: true overrides loading
    render()    // render now shows loading spinner

    try {
        const response = await fetch('http://localhost:5000/api/users')
        const users = await response.json()

        // Update state with data
        state = {
            ...state,             // keep searchQuery and filter etc
            users: users,         // store full list
            filteredUsers: users, // initially show all
            loading: false        // done loading
        }
    } catch (error) {
        state = {
            ...state,
            loading: false,
            error: error.message
        }
    }

    render()    // render again with new state
}

function setSearch(query) {
    state = { ...state, searchQuery: query }
    applyFilters()    // recalculate filteredUsers
}

function setFilter(role) {
    state = { ...state, filter: role }
    applyFilters()
}

function applyFilters() {
    let result = state.users    // start with full list

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

// ── 4. Events — update state, let render handle UI ──────────────────────────────────────────────

document.querySelector('#loadBtn').addEventListener('click', loadUsers)

document.querySelector('#searchInput').addEventListener('input', (e) => {
    setSearch(e.target.value)
})

document.querySelector('#roleFilter').addEventListener('change', (e) => {
    setFilter(e.target.value)
})

// ── 5. Start ──────────────────────────────────────────────
loadUsers()
```

---

# CHAPTER 18 — Promises and async/await

## Why Async Exists

JS runs in ONE thread. If it fetched data synchronously, the page freezes while waiting.
Async lets JS start a task, do other things while waiting, then handle the result.

## Promises

A Promise is an object representing a value that will arrive in the future.

```javascript
// fetch() returns a Promise immediately
// The actual data isn't ready yet
const promise = fetch('http://localhost:5000/api/users')

// Three states:
// pending — waiting for server to respond
// fulfilled — server responded, data ready
// rejected — something went wrong

// Handle with .then() and .catch():
promise
    .then(response => {
        // response is the HTTP response, not the data yet!
        return response.json()    // parse JSON, returns another Promise
    })
    .then(data => {
        // NOW data is your actual array/object from Python
        console.log(data)
    })
    .catch(error => {
        // Runs if anything goes wrong (network error, server error)
        console.log("Error:", error.message)
    })
    .finally(() => {
        // Runs ALWAYS — success or failure
        hideSpinner()
    })
```

## async/await — Cleaner Syntax

```javascript
// async keyword makes function return a Promise
// Inside it, you can use await to pause until a Promise resolves

async function loadUsers() {
    // await PAUSES this function here until fetch completes
    // Other code can still run while we wait — page does NOT freeze
    const response = await fetch('http://localhost:5000/api/users')
    // response is HTTP response object

    // response.json() also returns a Promise — await it
    const users = await response.json()
    // users is now your actual array

    return users
}

// Calling an async function:
loadUsers()    // starts running, does not wait

// OR inside another async function:
async function init() {
    const users = await loadUsers()    // waits for loadUsers to finish
    render(users)
}
```

**Golden rule: `await` can only be used inside `async` functions.**

---

# CHAPTER 19 — fetch() — All HTTP Methods

## GET — Fetch Data From Python

```javascript
async function getUsers() {
    // fetch() with just a URL = GET request (default)
    const response = await fetch('http://localhost:5000/api/users')

    // response object properties:
    response.ok          // true if status 200-299
    response.status      // 200, 404, 500 (number)
    response.statusText  // "OK", "Not Found"

    // Always check if request succeeded:
    if (!response.ok) {
        // throw creates Error and jumps to catch block
        throw new Error(`Request failed: ${response.status}`)
    }

    // response.json() reads body and parses JSON — returns Promise
    const users = await response.json()
    return users    // your array/object from Python
}
```

## POST — Send Data To Python

```javascript
async function createUser(name, role) {
    const response = await fetch('http://localhost:5000/api/users', {
        // Second argument to fetch is the options object

        method: 'POST',
        // Tell server how to interpret the body
        headers: {
            'Content-Type': 'application/json'
            // Without this, Flask doesn't know you're sending JSON
        },
        // body is what you're sending
        // JSON.stringify converts JS object to JSON string
        // { name: "Aman", role: "dev" } → '{"name":"Aman","role":"dev"}'
        body: JSON.stringify({ name, role })
    })

    if (!response.ok) {
        const err = await response.json().catch(() => ({}))
        // .catch(() => ({})) — if JSON parsing fails, use empty object
        throw new Error(err.message || `Error: ${response.status}`)
    }

    return response.json()    // the created object from Python (with its id)
}

// Using it:
try {
    const newUser = await createUser("Aman", "developer")
    // Add to state without refetching everything:
    state = { ...state, users: [...state.users, newUser] }
    render()
} catch (error) {
    state = { ...state, error: error.message }
    render()
}
```

## DELETE — Remove Data

```javascript
async function deleteUser(id) {
    // Template literal builds URL: '/api/users/1' or '/api/users/2'
    const response = await fetch(`http://localhost:5000/api/users/${id}`, {
        method: 'DELETE'
        // Usually no body for DELETE
    })

    if (!response.ok) throw new Error(`Failed to delete: ${response.status}`)

    // Remove from local state too — filter out the deleted item
    state = {
        ...state,
        users: state.users.filter(u => u.id !== Number(id))
        // Keep all users EXCEPT the one with matching id
        // Number(id) converts string to number in case id came from dataset
    }
    render()
}
```

## PATCH — Update Partial Data

```javascript
async function markTaskDone(taskId) {
    const response = await fetch(`http://localhost:5000/api/tasks/${taskId}/done`, {
        method: 'PATCH',    // PATCH updates part of resource. PUT replaces all.
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ done: true })    // only the field we want to update
    })

    if (!response.ok) throw new Error('Failed to update')

    const updatedTask = await response.json()    // Python returns updated task

    // Update that specific task in state:
    state = {
        ...state,
        tasks: state.tasks.map(task =>
            task.id === taskId ? updatedTask : task
            // If this task's id matches: replace with updatedTask
            // Otherwise: keep the original task
        )
    }
    render()
}
```

---

# CHAPTER 20 — Error Handling

Never skip this. Your Python server will go down. Network will fail. Always handle errors.

```javascript
async function loadUsers() {
    state = { ...state, loading: true, error: null }
    render()

    try {
        // try: attempt this code
        const response = await fetch('/api/users')

        // response.ok = false for 4xx and 5xx errors
        if (!response.ok) {
            throw new Error(`Server error: ${response.status}`)
            // throw stops execution and jumps to catch
        }

        const users = await response.json()
        state = { ...state, users, loading: false }

    } catch (error) {
        // catch: runs if anything throws inside try

        // Identify type of error:
        if (error.name === 'TypeError') {
            // Network error — usually means server is not running
            state = { ...state, error: "Cannot reach server. Is Python running?", loading: false }
        } else if (error.name === 'AbortError') {
            // Request was cancelled — ignore it
            return
        } else {
            // Other errors — server returned error, JSON parse failed, etc
            state = { ...state, error: error.message, loading: false }
        }

    } finally {
        // finally: runs ALWAYS — whether try succeeded or catch ran
        // Perfect for cleanup like hiding spinner
        render()
    }
}
```

---

# CHAPTER 21 — Form Handling

```javascript
// HTML:
// <form id="createForm">
//   <input id="nameInput" type="text">
//   <input id="emailInput" type="email">
//   <button type="submit">Create</button>
//   <p id="formError"></p>
// </form>

const form = document.querySelector('#createForm')

form.addEventListener('submit', async (event) => {
    // MUST call first. Without this, browser reloads page.
    // The default form behavior is to reload and send data in URL.
    // We don't want that — we handle it ourselves.
    event.preventDefault()

    // Get values — .trim() removes leading/trailing spaces
    // Users often accidentally type spaces, trim removes them
    const name = document.querySelector('#nameInput').value.trim()
    const email = document.querySelector('#emailInput').value.trim()

    const errorEl = document.querySelector('#formError')
    errorEl.textContent = ''    // clear any previous error message

    // Validate before sending to Python
    if (!name) {
        errorEl.textContent = 'Name is required'
        return    // stop — don't send to Python
    }
    if (name.length < 2) {
        errorEl.textContent = 'Name must be at least 2 characters'
        return
    }
    if (!email || !email.includes('@')) {
        errorEl.textContent = 'Valid email is required'
        return
    }

    // Disable submit button while sending
    // Prevents user from clicking submit twice
    const submitBtn = form.querySelector('button[type="submit"]')
    submitBtn.disabled = true
    submitBtn.textContent = 'Creating...'

    try {
        const response = await fetch('/api/users', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ name, email })
        })

        if (!response.ok) {
            const errorData = await response.json().catch(() => ({}))
            throw new Error(errorData.message || 'Failed to create')
        }

        const newUser = await response.json()

        // Add to state
        state = { ...state, users: [...state.users, newUser] }
        render()

        // Clear form so user can enter next item easily
        form.reset()
        document.querySelector('#nameInput').focus()    // cursor back in name field

    } catch (error) {
        errorEl.textContent = error.message

    } finally {
        // Always re-enable button — whether success or failure
        submitBtn.disabled = false
        submitBtn.textContent = 'Create'
    }
})
```

---

# CHAPTER 22 — AbortController

When user types in search and triggers multiple requests, cancel the old ones.

```javascript
let currentRequest = null    // tracks current search request

async function search(query) {
    // If there's an ongoing request, cancel it
    if (currentRequest) {
        currentRequest.abort()
        // This tells the browser: stop this fetch, we don't need it anymore
    }

    // Create new controller for this request
    currentRequest = new AbortController()
    // currentRequest.signal is an object that communicates the cancel signal to fetch

    try {
        const response = await fetch(`/api/search?q=${query}`, {
            signal: currentRequest.signal    // link signal to this fetch
        })
        // If abort() is called on currentRequest while awaiting, fetch throws AbortError

        const results = await response.json()
        state = { ...state, filteredUsers: results }
        render()

    } catch (error) {
        if (error.name === 'AbortError') {
            return    // request was cancelled — this is expected, ignore
        }
        state = { ...state, error: error.message }
        render()
    }
}
```

---

# CHAPTER 23 — Debounce

Wait until user stops typing, then run function once.
Without this: typing "aman" fires 4 API calls. With this: fires 1.

```javascript
function debounce(functionToRun, delay) {
    // timer holds reference to the pending setTimeout
    let timer

    // Returns a wrapper function
    return function(...args) {
        // Cancel the previous pending call (if any)
        // If user types again before delay is up, this cancels it and restarts
        clearTimeout(timer)

        // Schedule the actual function call after the delay
        timer = setTimeout(() => {
            functionToRun(...args)    // call original function with its arguments
        }, delay)
    }
}

// Create debounced search with 300ms delay
const debouncedSearch = debounce(search, 300)

document.querySelector('#search').addEventListener('input', (e) => {
    debouncedSearch(e.target.value)
    // If user types "a", then 50ms later "m", then 50ms later "a", then "n":
    // Each new keystroke cancels the previous timer and starts fresh
    // Only after user stops typing for 300ms does search() actually run
    // Result: ONE API call for "aman" instead of four
})
```

---

# CHAPTER 24 — localStorage

Saves data that persists even after page close or browser restart.
Perfect for auth tokens, user preferences.

```javascript
// Save — both key and value must be strings
localStorage.setItem('token', 'abc123')

// Save objects — convert to JSON string first
const user = { name: "Aman", role: "dev" }
localStorage.setItem('currentUser', JSON.stringify(user))
// JSON.stringify converts: { name: "Aman" } → '{"name":"Aman"}'

// Read
const token = localStorage.getItem('token')    // "abc123" or null if not saved

// Read object — convert back from JSON string
const userString = localStorage.getItem('currentUser')
// JSON.parse converts: '{"name":"Aman"}' → { name: "Aman" }
const user = userString ? JSON.parse(userString) : null
// Check for null first — JSON.parse(null) throws error

// Delete
localStorage.removeItem('token')

// ── Login flow ──────────────────────────────────────────────

async function login(username, password) {
    const response = await fetch('/api/login', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ username, password })
    })

    if (!response.ok) throw new Error('Invalid credentials')

    const data = await response.json()
    // data = { token: "abc123", user: { name: "Aman" } }

    // Store token — future requests will include this
    localStorage.setItem('token', data.token)
    localStorage.setItem('currentUser', JSON.stringify(data.user))

    showDashboard()
}

function logout() {
    localStorage.removeItem('token')
    localStorage.removeItem('currentUser')
    showLoginForm()
}

// Send token with every request:
async function authFetch(endpoint, options = {}) {
    const token = localStorage.getItem('token')
    return fetch(`http://localhost:5000${endpoint}`, {
        ...options,
        headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${token}`,
            // Bearer is standard prefix for JWT tokens
            ...options.headers
        }
    })
}
```

---

# CHAPTER 25 — setInterval and Auto-Refresh

```javascript
// setInterval — run code repeatedly at fixed intervals
const intervalId = setInterval(() => {
    console.log("runs every 2 seconds")
}, 2000)    // 2000ms = 2 seconds

// Stop it
clearInterval(intervalId)

// setTimeout — run code ONCE after delay
const timerId = setTimeout(() => {
    console.log("runs after 3 seconds, just once")
}, 3000)

// Cancel if needed
clearTimeout(timerId)

// ── Auto-refresh data from Python ──────────────────────────────────────────────

let refreshTimer = null

function startAutoRefresh() {
    // Fetch fresh data every 30 seconds
    refreshTimer = setInterval(async () => {
        try {
            const response = await fetch('/api/data')
            const data = await response.json()
            state = { ...state, data }
            render()
        } catch (error) {
            // Silently fail — don't show error for auto-refresh
            // User can see stale data, that's okay
            console.error("Auto-refresh failed:", error.message)
        }
    }, 30000)    // 30000ms = 30 seconds
}

function stopAutoRefresh() {
    clearInterval(refreshTimer)
}

// Start when user logs in, stop when they log out:
startAutoRefresh()
window.addEventListener('beforeunload', stopAutoRefresh)
```

---

# CHAPTER 26 — ES Modules

Split code into multiple files that import from each other.

```javascript
// ── utils.js ──────────────────────────────────────────────

// export makes this available to other files
export const API_BASE = 'http://localhost:5000'

export function formatDate(dateString) {
    // Convert "2024-01-15" to "15 Jan 2024"
    return new Date(dateString).toLocaleDateString('en-IN', {
        day: '2-digit', month: 'short', year: 'numeric'
    })
}

// A reusable fetch wrapper — all API calls go through this
// This way error handling is consistent everywhere
export async function apiFetch(endpoint, options = {}) {
    const token = localStorage.getItem('token')

    const response = await fetch(`${API_BASE}${endpoint}`, {
        ...options,    // spread any options passed in (method, body etc)
        headers: {
            'Content-Type': 'application/json',
            // Add auth token if logged in
            ...(token ? { 'Authorization': `Bearer ${token}` } : {}),
            // Allow caller to add or override headers
            ...options.headers
        }
    })

    if (!response.ok) throw new Error(`API error: ${response.status}`)
    return response.json()
}
```

```javascript
// ── main.js ──────────────────────────────────────────────

// import pulls in exports from other files
// { } curly braces for named exports
import { API_BASE, formatDate, apiFetch } from './utils.js'

async function loadUsers() {
    // Uses apiFetch from utils.js — no need to repeat URL or auth header logic
    const users = await apiFetch('/api/users')
    state = { ...state, users }
    render()
}
```

```html
<!-- index.html — type="module" enables ES modules -->
<script type="module" src="main.js"></script>
```

---

# CHAPTER 27 — DevTools

Press **F12** to open. These three tabs are your main tools.

## Console Tab

```javascript
// Different log levels for different situations:
console.log("regular info")       // gray
console.warn("potential issue")   // yellow
console.error("something broke")  // red

// Log object — click to expand in console
console.log(user)
console.log("User:", user, "State:", state)

// Display array as table — great for API response data
console.table(users)
// Shows: | index | name | age | role |

// Group related logs:
console.group("API Call to /users")
console.log("Sending request...")
console.log("Response:", data)
console.groupEnd()

// Time something:
console.time("render time")
render()
console.timeEnd("render time")    // "render time: 5ms"
```

## Network Tab

Open Network tab, then trigger your fetch request.
Click the request to see:

- **Status**: 200=ok, 404=not found, 500=server error, (failed)=no connection
- **Payload**: what you sent in POST body — verify it's correct
- **Response**: what Python returned — is it the right data?

Common problems and solutions:
```
(failed) red        → Python server not running. python app.py
500 error           → Error in Python code. Check Python terminal.
404 Not Found       → Wrong URL. Check fetch URL matches Flask route.
400 Bad Request     → Wrong data format. Check what you're sending.
CORS error          → Add flask-cors. pip install flask-cors, then CORS(app).
```

## Sources Tab — Debugging

1. Find your JS file in left panel
2. Click a line number → blue dot (breakpoint)
3. Trigger the code (click button, reload page)
4. Code pauses at that line
5. Hover any variable to see its current value
6. F10 = next line, F8 = continue

Or add in code:
```javascript
async function loadUsers() {
    debugger    // pauses HERE when devtools is open
    const response = await fetch('/api/users')
    // Can now inspect response, check its value before continuing
}
```

---

# COMPLETE PROJECTS

---

## Project 1 — Hello World

**What you learn:** Basic Python → JSON → JS → DOM connection.

**app.py:**
```python
from flask import Flask, jsonify
from flask_cors import CORS

# Create Flask app
app = Flask(__name__)

# CORS allows browser at one address to call server at different address/port
# Without this, browser blocks the request (security policy)
CORS(app)

@app.route('/api/hello')
def hello():
    # jsonify converts Python dict to proper JSON response
    return jsonify({
        "message": "Hello from Python!",
        "name": "Aman"
    })

# debug=True: auto-reloads when you save the file
app.run(debug=True, port=5000)
```

```bash
pip install flask flask-cors
python app.py
```

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
    <p id="error" style="color:red; display:none;"></p>

    <script src="app.js"></script>
</body>
</html>
```

**app.js:**
```javascript
async function init() {
    // Get references to elements
    const messageEl = document.getElementById('message')
    const nameEl = document.getElementById('name')
    const errorEl = document.getElementById('error')

    try {
        // Fetch from Python backend
        const response = await fetch('http://localhost:5000/api/hello')

        // response.ok = true for 200-299. false for 4xx and 5xx.
        if (!response.ok) {
            throw new Error(`Server error: ${response.status}`)
        }

        // Parse JSON body
        const data = await response.json()
        // data = { message: "Hello from Python!", name: "Aman" }

        // Put data on page
        messageEl.textContent = data.message
        nameEl.textContent = `Name: ${data.name}`

    } catch (error) {
        // Show error
        messageEl.textContent = 'Failed to load'
        errorEl.style.display = 'block'
        errorEl.textContent = error.message
    }
}

init()
```

---

## Project 2 — User List With Search and Filter

**What you learn:** Load from API, render list, filter and search in JS without extra API calls.

**app.py:**
```python
from flask import Flask, jsonify
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

users = [
    { "id": 1, "name": "Aman Sharma", "role": "developer", "age": 20 },
    { "id": 2, "name": "Ravi Kumar", "role": "designer", "age": 25 },
    { "id": 3, "name": "Priya Singh", "role": "developer", "age": 22 },
    { "id": 4, "name": "Kiran Patil", "role": "manager", "age": 30 }
]

@app.route('/api/users')
def get_users():
    return jsonify(users)

app.run(debug=True, port=5000)
```

**index.html:**
```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Users</title></head>
<body>
    <h1>Users</h1>
    <input type="text" id="searchInput" placeholder="Search by name...">
    <select id="roleFilter">
        <option value="all">All Roles</option>
        <option value="developer">Developer</option>
        <option value="designer">Designer</option>
        <option value="manager">Manager</option>
    </select>
    <p id="count"></p>
    <div id="userList"></div>
    <p id="error" style="color:red;"></p>
    <script src="app.js"></script>
</body>
</html>
```

**app.js:**
```javascript
// State — all data lives here
let state = {
    users: [],
    filteredUsers: [],
    loading: false,
    error: null,
    searchQuery: '',
    roleFilter: 'all'
}

// render — builds entire UI from current state
function render() {
    const listEl = document.querySelector('#userList')
    const countEl = document.querySelector('#count')
    const errorEl = document.querySelector('#error')

    errorEl.textContent = ''

    if (state.loading) {
        listEl.innerHTML = '<p>Loading...</p>'
        countEl.textContent = ''
        return
    }

    if (state.error) {
        errorEl.textContent = state.error
        listEl.innerHTML = ''
        return
    }

    countEl.textContent =
        `Showing ${state.filteredUsers.length} of ${state.users.length} users`

    if (state.filteredUsers.length === 0) {
        listEl.innerHTML = '<p>No users match.</p>'
        return
    }

    // map each user to HTML string, join into one string, set as innerHTML
    listEl.innerHTML = state.filteredUsers
        .map(user => `
            <div style="border:1px solid #ccc;padding:12px;margin:8px 0;border-radius:6px;">
                <strong>${user.name}</strong>
                <span style="color:#666;margin-left:10px;">${user.role}</span>
                <span style="color:#999;margin-left:10px;">Age: ${user.age}</span>
            </div>
        `)
        .join('')
}

// Recalculate filteredUsers from full list applying both filters
function applyFilters() {
    let result = state.users    // start with full list

    // Apply role filter
    if (state.roleFilter !== 'all') {
        result = result.filter(user => user.role === state.roleFilter)
    }

    // Apply search — case insensitive
    if (state.searchQuery) {
        const q = state.searchQuery.toLowerCase()
        result = result.filter(user =>
            user.name.toLowerCase().includes(q)
        )
    }

    state = { ...state, filteredUsers: result }
    render()
}

// Fetch users from Python
async function loadUsers() {
    state = { ...state, loading: true, error: null }
    render()

    try {
        const response = await fetch('http://localhost:5000/api/users')
        if (!response.ok) throw new Error(`Server error: ${response.status}`)

        const users = await response.json()
        state = { ...state, users, filteredUsers: users, loading: false }

    } catch (error) {
        state = {
            ...state,
            loading: false,
            error: `Load failed: ${error.message}. Is Python running?`
        }
    }

    render()
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

## Project 3 — Task Manager (Main Project)

**What you learn:** Full CRUD. Loading states. Error handling. Form validation. Event delegation.
**This single project covers everything in Stages 1, 2, and 3.**

**app.py:**
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
    data = request.get_json()    # reads JSON body sent from JS

    if not data or not data.get('title'):
        return jsonify({ "error": "Title is required" }), 400
        # 400 = Bad Request

    task = {
        "id": next_id,
        "title": data['title'],
        "done": False,
        "priority": data.get('priority', 'medium')    # default 'medium'
    }

    tasks.append(task)
    next_id += 1

    return jsonify(task), 201    # 201 = Created

@app.route('/api/tasks/<int:task_id>', methods=['DELETE'])
def delete_task(task_id):
    global tasks
    original = len(tasks)
    tasks = [t for t in tasks if t['id'] != task_id]

    if len(tasks) == original:
        return jsonify({ "error": "Not found" }), 404

    return jsonify({ "message": "Deleted" })

@app.route('/api/tasks/<int:task_id>/toggle', methods=['PATCH'])
def toggle_task(task_id):
    for task in tasks:
        if task['id'] == task_id:
            task['done'] = not task['done']    # flip True/False
            return jsonify(task)

    return jsonify({ "error": "Not found" }), 404

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
        <p id="formError" style="color:red;margin:0;"></p>
    </form>

    <p id="stats"></p>
    <div id="taskList"></div>

    <script src="app.js"></script>
</body>
</html>
```

**app.js — fully commented:**
```javascript
const API = 'http://localhost:5000'

// All app state lives here
let state = {
    tasks: [],
    loading: false,
    error: null,
    submitting: false    // true while POST request is in progress
}

function render() {
    const listEl = document.querySelector('#taskList')
    const statsEl = document.querySelector('#stats')
    const submitBtn = document.querySelector('#submitBtn')

    // Update submit button based on submitting state
    submitBtn.disabled = state.submitting
    // If submitting: disabled (grey out), text shows "Adding..."
    // If not submitting: enabled, text shows "Add Task"
    submitBtn.textContent = state.submitting ? 'Adding...' : 'Add Task'

    // Show task completion stats
    const total = state.tasks.length
    const done = state.tasks.filter(t => t.done).length
    statsEl.textContent = `${done} of ${total} tasks done`

    // Loading — show spinner
    if (state.loading) {
        listEl.innerHTML = '<p>Loading tasks...</p>'
        return
    }

    // Error — show message with retry button
    if (state.error) {
        listEl.innerHTML = `
            <p style="color:red;">${state.error}</p>
            <button onclick="loadTasks()">Try Again</button>
        `
        return
    }

    // Empty — no tasks yet
    if (state.tasks.length === 0) {
        listEl.innerHTML = '<p>No tasks yet. Add one above!</p>'
        return
    }

    // Render task list
    listEl.innerHTML = state.tasks
        .map(task => `
            <div
                data-id="${task.id}"
                style="
                    display:flex;
                    align-items:center;
                    gap:12px;
                    padding:12px;
                    margin:6px 0;
                    border:1px solid #ddd;
                    border-radius:6px;
                    text-decoration:${task.done ? 'line-through' : 'none'};
                    opacity:${task.done ? '0.6' : '1'};
                "
            >
                <input
                    type="checkbox"
                    class="toggle-check"
                    data-id="${task.id}"
                    ${task.done ? 'checked' : ''}
                >
                <span style="flex:1;">${task.title}</span>
                <span style="color:#999;font-size:0.85em;">[${task.priority}]</span>
                <button class="delete-btn" data-id="${task.id}">Delete</button>
            </div>
        `)
        .join('')
}

// Load all tasks from Python
async function loadTasks() {
    state = { ...state, loading: true, error: null }
    render()

    try {
        const response = await fetch(`${API}/api/tasks`)
        if (!response.ok) throw new Error(`Server error: ${response.status}`)

        const tasks = await response.json()
        state = { ...state, tasks, loading: false }

    } catch (error) {
        state = {
            ...state,
            loading: false,
            error: `Could not load: ${error.message}`
        }
    }

    render()
}

// Delete a task
async function deleteTask(id) {
    const numId = Number(id)    // dataset gives string, convert to number

    try {
        const response = await fetch(`${API}/api/tasks/${numId}`, {
            method: 'DELETE'
        })

        if (!response.ok) throw new Error('Delete failed')

        // Remove from state — keep all tasks EXCEPT the deleted one
        state = {
            ...state,
            tasks: state.tasks.filter(t => t.id !== numId)
        }
        render()

    } catch (error) {
        alert(`Delete failed: ${error.message}`)
    }
}

// Toggle task done/not-done
async function toggleTask(id) {
    const numId = Number(id)

    try {
        const response = await fetch(`${API}/api/tasks/${numId}/toggle`, {
            method: 'PATCH'
        })

        if (!response.ok) throw new Error('Toggle failed')

        const updatedTask = await response.json()
        // Python returned the task with flipped done value

        // Update that task in state — replace matching task, keep others
        state = {
            ...state,
            tasks: state.tasks.map(task =>
                task.id === numId ? updatedTask : task
            )
        }
        render()

    } catch (error) {
        alert(`Update failed: ${error.message}`)
    }
}

// Add new task — form submit handler
document.querySelector('#taskForm').addEventListener('submit', async (event) => {
    event.preventDefault()    // stop page reload

    const titleInput = document.querySelector('#titleInput')
    const prioritySelect = document.querySelector('#prioritySelect')
    const errorEl = document.querySelector('#formError')

    const title = titleInput.value.trim()
    const priority = prioritySelect.value

    errorEl.textContent = ''    // clear old error

    // Validate
    if (!title) {
        errorEl.textContent = 'Task title is required'
        return
    }
    if (title.length < 3) {
        errorEl.textContent = 'Title must be at least 3 characters'
        return
    }

    // Set submitting state — render() will disable button and show "Adding..."
    state = { ...state, submitting: true }
    render()

    try {
        const response = await fetch(`${API}/api/tasks`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ title, priority })
        })

        if (!response.ok) {
            const errData = await response.json().catch(() => ({}))
            throw new Error(errData.error || 'Failed to create task')
        }

        const newTask = await response.json()
        // Python returned the new task with its id, done:false, etc

        // Add new task to state array
        state = {
            ...state,
            tasks: [...state.tasks, newTask],    // existing tasks + new task at end
            submitting: false
        }
        render()

        // Clear form for next entry
        titleInput.value = ''
        prioritySelect.value = 'medium'
        titleInput.focus()    // cursor back in title field

    } catch (error) {
        errorEl.textContent = error.message
        state = { ...state, submitting: false }
        render()
    }
})

// ONE event listener on task list for all clicks inside it
document.querySelector('#taskList').addEventListener('click', (event) => {
    // event.target = exact element that was clicked

    if (event.target.classList.contains('delete-btn')) {
        // Delete button was clicked
        const id = event.target.dataset.id    // data-id attribute value
        deleteTask(id)
    }

    if (event.target.classList.contains('toggle-check')) {
        // Checkbox was clicked
        const id = event.target.dataset.id
        toggleTask(id)
    }
})

// Start the app
loadTasks()
```

---

# QUICK REFERENCE

## Array methods

```javascript
arr.map(fn)       // transform each item, returns new array
arr.filter(fn)    // keep matching items, returns new array
arr.find(fn)      // first matching item, returns item (not array)
arr.forEach(fn)   // loop through, returns nothing
arr.some(fn)      // any match? returns boolean
arr.every(fn)     // all match? returns boolean
arr.sort((a,b) => a-b)         // ascending numbers
arr.sort((a,b) => a.name.localeCompare(b.name))  // by string property
arr.includes(val)   // contains value? boolean
arr.indexOf(val)    // index of value (-1 if not found)
```

## State update pattern

```javascript
// Always use spread to not mutate state
state = { ...state, loading: true }
render()

// Never do:
state.loading = true    // mutates state — causes bugs
render()
```

## fetch pattern

```javascript
async function apiCall() {
    state = { ...state, loading: true }
    render()
    try {
        const res = await fetch('/endpoint', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(data)
        })
        if (!res.ok) throw new Error(`Error: ${res.status}`)
        const result = await res.json()
        state = { ...state, result, loading: false }
    } catch (err) {
        state = { ...state, error: err.message, loading: false }
    } finally {
        render()
    }
}
```

## DOM operations

```javascript
document.querySelector('#id')           // find by id
document.querySelectorAll('.class')     // find all by class

el.textContent = "text"                 // set text (safe)
el.innerHTML = "<b>html</b>"            // set html
el.style.display = 'none'              // hide
el.classList.toggle('active')          // toggle class
el.dataset.id                          // read data-id attribute
input.value                            // input current value

el.addEventListener('click', fn)
form.addEventListener('submit', e => { e.preventDefault() })
```

---

*Read one chapter. Close file. Write the code from memory. Open browser and test. Then next chapter.*
