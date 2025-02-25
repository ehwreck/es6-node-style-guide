# Node.js Style Guide

This is a guide for writing consistent and aesthetically pleasing node.js code.
It is inspired by what is popular within the community, and flavored with some
personal opinions.

There is a .jshintrc which enforces these rules as closely as possible. You can
either use that and adjust it, or use
[this script](https://gist.github.com/kentcdodds/11293570) to make your own.

This guide was created by [Felix Geisendörfer](http://felixge.de/) and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license. You are encouraged to fork this repository and make adjustments
according to your preferences.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## Table of contents

### Formatting
* [2 Spaces for indentation](#2-spaces-for-indentation)
* [Newlines](#newlines)
* [No trailing whitespace](#no-trailing-whitespace)
* [Use Semicolons](#use-semicolons)
* [80 characters per line](#80-characters-per-line)
* [Use single quotes](#use-single-quotes)
* [Opening braces go on the same line](#opening-braces-go-on-the-same-line)
* [Declare one variable per let statement](#declare-one-variable-per-let-statement)

### Naming Conventions
* [Use lowerCamelCase for variables, properties and function names](#use-lowercamelcase-for-variables-properties-and-function-names)
* [Use UpperCamelCase for class names](#use-uppercamelcase-for-class-names)
* [Use UPPERCASE for Constants](#use-uppercase-for-constants)

### Variables
* [Object / Array creation](#object--array-creation)

### Conditionals
* [Use the === operator](#use-the--operator)
* [Use multi-line ternary operator](#use-multi-line-ternary-operator)
* [Use descriptive conditions](#use-descriptive-conditions)

### Functions
* [Write small functions](#write-small-functions)
* [Return early from functions](#return-early-from-functions)
* [Name your closures](#name-your-closures)
* [No nested closures](#no-nested-closures)
* [Method chaining](#method-chaining)

### Comments
* [Use slashes for comments](#use-slashes-for-comments)

### Miscellaneous
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [Requires At Top](#requires-at-top)
* [Getters and setters](#getters-and-setters)
* [Do not extend built-in prototypes](#do-not-extend-built-in-prototypes)

## Formatting

You may want to use [editorconfig.org](http://editorconfig.org/) to enforce the formatting settings in your editor. Use the [Node.js Style Guide .editorconfig file](.editorconfig) to have indentation, newslines and whitespace behavior automatically set to the rules set up below.

### 2 Spaces for indentation

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces - a special kind of hell is awaiting you otherwise.

### Newlines

Use UNIX-style newlines (`\n`), and a newline character as the last character
of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.

### No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

### Use Semicolons

According to [scientific research][hnsemicolons], the usage of semicolons is
be a traditionalist when it comes to abusing error correction mechanisms for
cheap syntactic pleasures.

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

### 80 characters per line

Limit your lines to 80 characters. Yes, screens have gotten much bigger over the
last few years, but your brain has not. Use the additional room for split screen,
your editor supports that, right?

### Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
let foo = 'bar';
```

*Wrong:*

```js
let foo = "bar";
```

### Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log('winning');
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing');
}
```

Also, notice the use of whitespace before and after the condition statement.

### Declare one variable per let statement

Declare one variable per let statement, it makes it easier to re-order the
lines. However, ignore [Crockford][crockfordconvention] when it comes to
declaring variables deeper inside a function, just put the declarations wherever
they make sense.

*Right:*

```js
let keys   = ['foo', 'bar'];
let values = [23, 42];

let object = {};
while (keys.length) {
  let key = keys.pop();
  object[key] = values.pop();
}
```

*Wrong:*

```js
let keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

## Naming Conventions

### Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  They
should also be descriptive. Single character variables and uncommon
abbreviations should generally be avoided.

*Right:*

```js
let adminUser = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
let admin_user = db.query('SELECT * FROM users ...');
```

### Use UpperCamelCase for class names

Class names should be capitalized using `UpperCamelCase`.

*Right:*

```js
const BankAccount = () => {
}
```

*Wrong:*

```js
const bank_Account = () => {
}
```

### Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

*Right:*

```js
let SECOND = 1 * 1000;

const File() => {
}
File.FULL_PERMISSIONS = 0777;
```

*Wrong:*

```js
const SECOND = 1 * 1000;

const File = () => {
}
File.fullPermissions = 0777;
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Variables

### Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
let a = ['hello', 'world'];
let b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
let a = [
  'hello', 'world'
];
let b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Conditionals

### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
let a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Wrong:*

```js
let a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Use multi-line ternary operator

The ternary operator should not be used on a single line. Split it up into multiple lines instead.

*Right:*

```js
let foo = (a === b)
  ? 1
  : 2;
```

*Wrong:*

```js
let foo = (a === b) ? 1 : 2;
```

### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
let isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Export and import

### Exporting from a file
Exporting variables, functions, or classes from a file can be achieved in a couple different ways in ES6.
A couple sceneraios you will encounter are below.

#### Exporting multiple items from a file
```js
// FILE 1
const add = (a, b) => {
  return a + b;
}

const subtract = (a, b) => {
  return a - b;
}

export { add, substract }
```

```js
// FILE 1
export const add = (a, b) => {
  return a + b;
}

export const subtract = (a, b) => {
  return a - b;
}
```

Importing from the examples above is done as below:
```js
// FILE 2
import { add, subtract } from './file1.js'
```

#### Exporting a single item from a file
When exporting a single item from a file it is cleaner to use a default export.
It is not recommended to export default an anonymous function.
```js
// FILE 1
export default function isTall(inches){
  return inches > 72
}
```
```js
function isTall(inches){
  return inchex > 72
}

export default isTall;
```
Importing from the examples above looks like this. Notice this is way cleaner.
```js
// FILE 2
import isTall from './file1.js'
```

#### Exporting for libraries (used on libraries such as ReactJS, etc.)
```js
export const add = (a, b) => {
  return a + b;
}
export const subtract = (a, b) =>{
    return a - b;
}
export const multiply = (a, b) => {
  return a * b;
}
export const divide = (a, b) => {
  return a / b;
}
const Math = {add, subtract, multiply, divide};

export default Math;
```

Importing from the example above looks like this.
```js
// FILE 2
import Math, { add } from './file1.js'

// Using the functions
Math.multiply(1,2);

add.(1,2);
```

## Functions

### Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Return early from functions

as possible.

*Right:*

```js
const isPercentage = (val) => {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*Wrong:*

```js
const isPercentage = (val) => {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
const isPercentage = (val) => {
  let isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### Name your closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', onEnd);

const onEnd = () => {
  console.log('winning');
}
```

*Wrong:*

```js
req.on('end', () => {
  console.log('losing');
});
```

### No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(() => {
  client.connect(afterConnect);
}, 1000);

const afterConnect = () => {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(() => {
  client.connect(() => {
    console.log('losing');
  });
}, 1000);
```


### Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec((err, user) => {
    return true;
  });
```

*Wrong:*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec((err, user) => {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec((err, user) => {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec((err, user) => {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec((err, user) => {
    return true;
  });
```

## Comments

### Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
let matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
const loadUser = (id, cb) => {
  // ...
}

let isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
let matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, () => { ... })
const loadUser = (id, cb) => {
  // ...
}

// Check if the session is valid
let isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Miscellaneous

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

### Requires At Top

Always put requires at top of file to clearly illustrate a file's dependencies. Besides giving an overview for others at a quick glance of dependencies and possible memory impact, it allows one to determine if they need a package.json file should they choose to use the file elsewhere.

### Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
let a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = () => {
  return !this.length;
}

let a = [];
if (a.empty()) {
  console.log('losing');
}
```
