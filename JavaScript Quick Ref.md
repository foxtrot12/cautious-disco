
### Variables

- **Definition**: Named storage.
- Variables are dynamically typed.
- Data has types but a variable is not bound to a particular type.

### Example
```javascript 
let x = 10; // number
x = "hello"; // string
```

## Closures

- **Definition**: Combination of a function bundled together with references to its surrounding state.

### Example
```javascript
function makeCounter() {     
    let count = 0;     
    return function() {         
        count++;         
        return count;     
    }; 
} 

let counter = makeCounter(); 
console.log(counter()); // 1
console.log(counter()); // 2
```

## `use strict`

- **Purpose**: Ensures no changes to legacy code before ES5; this is used to make those changes. Post-ES5, they are off by default.
- Classes and modules of modern JS enable this by default.

### Example
```javascript
"use strict"; 
x = 3.14; // This will cause an error because x is not declared
```

## `var`
- **Old declaration** for variables, not used in modern scripts.
- No block scope, only function or global scope.
- Tolerates redeclarations.
- Can be declared after usage.

### Example
```javascript
function example() {
    console.log(x); // undefined
    var x = 5;
    console.log(x); // 5
}
```

## Hoisting

- **Definition**: Declaring all variables at the top of the script or function since block scope doesn’t apply.
- **Behavior**: JavaScript moves all variable declarations to the top.
    - `let`/`const` to block top
    - `var` to function or script top
- Declarations can be hoisted, not initialization.

### Example

```javascript
console.log(hoistedVar); // undefined 
var hoistedVar = "This is hoisted";  
console.log(hoistedLet); // ReferenceError: Cannot access 'hoistedLet' before initialization 
let hoistedLet = "This is not hoisted";
```

## Nullish Coalescing (`??`)

- Treats `null` and `undefined` the same way.
- `res = a ?? b` is equivalent to `res = (a !== null && a !== undefined) ? a : b`
- Newest addition; older browsers need polyfills.

### Example
```javascript
let name; 
let defaultName = "Default"; 
console.log(name ?? defaultName); // "Default"
```

## Logical OR (`||`)

- Returns the first truthy value.
- `null`/`undefined`/`false`/`0`/`""` are falsy values.
- Only deals with `null` and `undefined`.

### Example
```javascript
let name = ""; 
let defaultName = "Default"; 
console.log(name || defaultName); // "Default"
```

## `break`

- Used to break out of a loop.

### Example
```javascript
for (let i = 0; i < 10; i++) {     
    if (i === 5) {         
        break;     
    }     
    console.log(i); 
}
```

## Function Expression

- `x = function() {}`

### Example
```javascript
let sayHi = function() {     
    console.log("Hi"); 
}; 
sayHi(); // Hi
```

## Functions

- A function is a value just like a variable, no matter how it is declared.

### Example
```javascript
function greet() {     
    console.log("Hello!"); 
}  
let greetFunction = greet; 
greetFunction(); // Hello!
```

## Arrow Functions
- **Definition**: Dynamically create functions like function expressions.
- **Syntax**: `const afunc = (x) => x;`

### Example
```javascript
const afunc = (x) => x;
console.log(afunc(5)); // 5
```
- Better for situations where the function is executed somewhere else (e.g., `forEach` or `setTimeout`).
- Have no `this`. `this` is accessed from outside the function where it is declared.
- Cannot be used as constructors because they don’t have `this` and cannot use `new`.

### Example
```javascript
let group = {
    title: "Some Group",
    students: ["Student1", "Student2"],

    showList() {
        this.students.forEach(
            student => console.log(this.title + ": " + student)
        );
    }
};

group.showList(); // Some Group: Student1, Some Group: Student2
```

- Arrow functions cannot be used with `constructors` as they don’t have `this` and cannot use `new`.

### Bind vs Arrow Function
- **Bind**: Creates a new bound version with the given `this`.
- **Arrow Function**: Has no `this` to begin with.

### Example
```javascript
function Person() {
    this.age = 0;

    setInterval(() => {
        this.age++; // |this| properly refers to the person object
    }, 1000);
}

let p = new Person();
```

## Transpilers
- **Definition**: Transpile new JS code to old for older browsers.

### Example
```javascript
let height = height ?? 100;
// Transpiled to:
let height = (height !== null && height !== undefined) ? height : 100;
```

## Polyfills
- **Definition**: Adds or contains new functions that are not present in older browsers.
- Acts as built-in functions.

### Example
```javascript
if (!String.prototype.includes) {
    String.prototype.includes = function(search, start) {
        'use strict';
        if (typeof start !== 'number') {
            start = 0;
        }
        if (start + search.length > this.length) {
            return false;
        } else {
            return this.indexOf(search, start) !== -1;
        }
    };
}
```


## Objects
- Stored as a keyed collection of data.
- Computed properties can be used.

### Example
```javascript
let fruit = "apple";
let bag = {
  [fruit]: 5
};
console.log(bag.apple); // 5
```

## "in" Operator
- Used to find if a key is in an object.

### Example
```javascript
let bag = { apple: 5 };
console.log("apple" in bag); // true
console.log("orange" in bag); // false
```

## Object References and Copying
- Objects are stored and copied by reference, whereas primitives are by value.

### Example
```javascript
let message = "Hello";
let phrase = message;

let user = { name: "Alice" };
let admin = user;
admin.name = "Bob";

console.log(user.name); // Bob
```

## Comparison by Reference
- Objects are only equal if they reference the same object.

### Example
```javascript
let a = { name: "Alice" };
let b = a;
console.log(a === b); // true

let c = { name: "Alice" };
let d = { name: "Alice" };
console.log(c === d); // false
```

## Const Objects
- Const objects can be modified.

### Example
```javascript
const person = { name: "Alice" };
person.name = "Bob"; // Allowed
console.log(person.name); // Bob
```

## Structured Clone
- Clones nested objects.
- Supports circular references but does not support function properties.

### Example
```javascript
let clone = structuredClone(user);
```


## For...in Loop
- Used to loop over properties of an object.

### Example
```javascript
let bag = { apple: 5, orange: 10 };
for (let key in bag) {
    console.log(key); // apple, orange
    console.log(bag[key]); // 5, 10
}
```

## Object Property Order
- Integer properties are sorted, others appear in the order of creation.

### Example
```javascript
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "1": "USA"
};
for (let code in codes) {
    console.log(code); // 1, 41, 49
}

```

# Garbage Collection

## Reachability
- **Readable** values are those that are accessible or usable; they are stored in the memory.

- Any object that is unreachable is removed by garbage collection processes.

```javascript
let user = { name: "Chris" };
user = null;
// Reference to name is lost
// name is garbage collected
```

```javascript
let user = { name: "Ram" };
let admin = user;
user = null;
// Reference to name is still present in admin, hence it will not be removed from memory.
```

### Enhanced Explanation

- In the first example, when `user` is assigned `null`, the reference to the object containing `{ name: "Chris" }` is lost, making it unreachable. The garbage collector will then remove this object from memory.

- In the second example, the object `{ name: "Ram" }` is still referenced by the variable `admin` even after `user` is assigned `null`. Hence, the object will not be garbage collected because it is still reachable through `admin`.

# `this` in JavaScript

- `this` is used by methods to access information stored in the object.

```javascript
let eg = {
    name: "Lakshman",
    displayName() {
        console.log(this.name);
    }
};
```

- `this` is not bound. It is computed at runtime if not declared or initialized.

```javascript
let eg1 = { name: "Person1" };
let eg2 = { name: "Person2" };

function displayName() {
    console.log(this.name);
}

eg1.displayName = displayName;
eg2.displayName = displayName;

console.log(eg1.displayName()); // Person1
console.log(eg2.displayName()); // Person2
```

## Consequences of Unbound `this`

In JavaScript, the value of `this` is determined by how a function is called, not where it is defined. When `this` is unbound, it can lead to unexpected behavior, especially in the following scenarios:

1. **Global Context:** If a function using `this` is called without any context (e.g., not as a method of an object), `this` will refer to the global object (`window` in browsers, `global` in Node.js). This can lead to accidental modification of global variables.

    ```javascript
    function showName() {
        console.log(this.name);
    }
    
    global.name = "Global Name";
    showName(); // Outputs: "Global Name"
    ```

2. **Strict Mode:** In strict mode, `this` will be `undefined` when a function is called without an explicit context, leading to errors if the code assumes `this` is always an object.

    ```javascript
    'use strict';
    
    function showName() {
        console.log(this.name);
    }
    
    showName(); // TypeError: Cannot read property 'name' of undefined
    ```

3. **Event Handlers:** In event handlers, `this` usually refers to the element that received the event, which can be different from the object the method was originally bound to.

    ```javascript
    let obj = {
        name: "Object Name",
        showName() {
            console.log(this.name);
        }
    };
    
    document.querySelector("button").addEventListener("click", obj.showName);
    // 'this' in showName refers to the button element, not obj
    ```

4. **Arrow Functions:** Arrow functions do not have their own `this` context. They inherit `this` from the parent scope at the time they are defined. This can be both advantageous and a source of bugs if not understood properly.

    ```javascript
    let obj = {
        name: "Object Name",
        showName: () => {
            console.log(this.name);
        }
    };
    
    obj.showName(); // 'this' is undefined in arrow function, will not output "Object Name"
    ```

Understanding the binding of `this` is crucial for writing correct and predictable JavaScript code. When in doubt, it's often helpful to use explicit binding methods like `.call()`, `.apply()`, or `.bind()`.

# Constructor / `new` Operator

```javascript
function User(name) {
    console.log(new.target); // [Function: User]
    this.name = name;
    this.isAdmin = false;
}

let user = new User("Krishan");
```

- `new.target` in function to check if the function is called via `new`.

## Symbol Type

- Represents a unique identifier.

```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2); // false
```

- Guaranteed to be unique.
- Primitive unique value.
- Allows to create hidden properties in objects.

### Explanation

1. **Constructor Function and `new` Operator**:
    - A constructor function is a special type of function that is used to create instances of an object. The `new` operator is used to call a constructor function and create a new instance.
    - `new.target` is a property that lets you detect whether a function or constructor was called using the `new` operator. If a function is called using `new`, `new.target` will be a reference to the constructor or function; otherwise, it will be `undefined`.

2. **Symbol Type**:
    - Symbols are a new primitive type introduced in ECMAScript 6 (ES6). Each symbol value returned from `Symbol()` is unique. Symbols are often used to add unique property keys to an object that won't collide with keys any other code might add to the object.
    - Symbols can be used to create "hidden" properties of an object that are not traversed in `for...in` loops or `Object.keys()` method.


# Global Symbol Registry

- No other part of the code can accidentally access hidden properties.

```javascript
let user = { name: "Ram" };
let id = Symbol("id");

user[id] = 1;
console.log(user.id); // undefined
console.log(user[id]); // 1
```

## Global Symbols

- **Global Symbol Registry**: A global symbol registry exists where symbols can be created and accessed later.

```javascript
let key = Symbol.for("key");
```

- If `key` exists in the global registry, it is returned; else, a new one is created and then returned.

- Global symbols are present application-wide.

```javascript
let id1 = Symbol.for("id");
console.log(Symbol.keyFor(id1)); // "id"
```

- `Symbol.keyFor()` returns the key of the symbol. This only works for the global registry.

### Explanation

1. **Symbols and Hidden Properties**:
    - Symbols allow creating unique identifiers for object properties, ensuring that no other part of the code can accidentally access these hidden properties. This is particularly useful for adding private properties to objects.

2. **Global Symbol Registry**:
    - The global symbol registry is a global environment where you can create and access symbols using `Symbol.for()`. If a symbol with the given key already exists, it returns that symbol; otherwise, it creates a new symbol with the given key.
    - `Symbol.keyFor()` can be used to retrieve the key for a global symbol, which helps in identifying the symbol in the global registry.


# Object to Primitive Conversion

- In case of logical operations (`+`, `-`, `?`, etc.), objects are automatically converted to primitives.

```javascript
let obj1 = { valueOf() { return 3; } };
let obj2 = { valueOf() { return 2; } };

console.log(obj1 + obj2); // 5
```

- JavaScript does not allow customizing how operators work on objects directly.

## Boolean Context

- In a boolean context, all objects are `true`; there is no conversion to other values.

## Numeric Conversion

- Numeric conversion happens when mathematical operations are performed.

```javascript
let date1 = new Date("2024-07-01");
let date2 = new Date("2024-07-10");

console.log(date2 - date1); // 777600000 (milliseconds difference)
```

## String Conversion

- String conversion usually happens when an object is output using `console.log(obj)` or when used as an object key.

```javascript
let obj = {
    toString() {
        return "This is an object";
    }
};

console.log(String(obj)); // "This is an object"
console.log(obj + ""); // "This is an object"
```

## Customizing Object to Primitive Conversion

- String and numeric conversions can be implemented using special object methods.

### Using `Symbol.toPrimitive`

- `Symbol.toPrimitive` is a property that allows objects to define their own conversion behavior.

```javascript
let user = {
    name: "Brahma",
    savings: 1000,
    [Symbol.toPrimitive](hint) {
        if (hint === "string") {
            return this.name;
        }
        return this.savings;
    }
};

console.log(`User: ${user}`); // "User: Brahma"
console.log(+user); // 1000
console.log(user + 500); // 1500
```

### Explanation

1. **Logical Operations**:
    - Objects are auto-converted to primitives during logical operations like addition or subtraction. This conversion uses internal methods to obtain primitive values.

2. **Boolean Context**:
    - All objects are considered `true` in a boolean context, irrespective of their content or value.

3. **Numeric Conversion**:
    - When mathematical operations are performed, objects are converted to numbers. For instance, subtracting dates converts them to their respective time values.

4. **String Conversion**:
    - Objects are often converted to strings when they are used in contexts that expect a string, like `console.log` or string concatenation. This is typically handled by the `toString` method or `Symbol.toPrimitive`.

5. **Custom Object Conversion**:
    - You can customize how objects are converted to primitives by defining methods like `valueOf`, `toString`, or using the `Symbol.toPrimitive` symbol. This provides fine-grained control over the conversion process.

# Methods of Primitives

- JavaScript allows working with primitives as objects.
- JavaScript also has built-in functions.
- Object wrappers are used to provide these methods and are later destroyed.

```javascript
let str = "abc"; // str is a primitive

console.log(str.toUpperCase()); // "ABC"
// Object wrapper is created, value is computed, and then the object wrapper is destroyed.
```

## Numbers

- Numbers can be written with underscores for readability. For example: `100_000_000` is allowed and ignored by JavaScript.

### Method Calls on Numbers

- Using two dots to call a method on a number:

```javascript
let num = 39.97;
console.log(num.toString()); // "39.97"
```

### Imprecise Calculations

- If a number overflows 64-bit, the number becomes `Infinity`.

```javascript
console.log(1e500); // Infinity
```

- Imprecision in floating-point calculations:

```javascript
console.log(0.1 + 0.2 === 0.3); // false
console.log(0.1 + 0.2); // 0.30000000000000004
```

### Explanation

1. **Methods of Primitives**:
    - JavaScript allows primitives (like strings and numbers) to use methods. When a method is called on a primitive, JavaScript internally wraps the primitive in an object. For example, calling `toUpperCase` on a string temporarily converts it to a `String` object, performs the method, and then converts it back to a primitive.
    - This is why you can call methods directly on string and number literals, even though they are not objects.

2. **Underscore in Numbers**:
    - JavaScript supports the use of underscores (`_`) in numeric literals to improve readability, particularly for large numbers. These underscores are ignored by the JavaScript engine.
    
3. **Calling Methods on Numbers**:
    - When using methods on number literals directly, you need to be careful with the syntax. For instance, `39.97.toString()` is valid, but `39.toString()` can be problematic due to the dot being interpreted as a decimal point. Using two dots, like `39..toString()`, solves this issue by clearly separating the number and method call.

4. **Imprecise Calculations**:
    - Floating-point arithmetic in JavaScript (and most programming languages) can lead to imprecise results due to the way numbers are represented in binary form. This is evident in calculations like `0.1 + 0.2`, which results in `0.30000000000000004` instead of `0.3`.
    - When numbers exceed the limit of 64-bit representation, they are considered `Infinity` in JavaScript.

# Strings

- Strings can access characters.

```javascript
let str = "abc";
console.log(str[0]); // "a"
console.log(str.at(0)); // "a"
```

- Strings are immutable.

```javascript
let str = "hi";
str[0] = "b"; // Error: Strings are immutable
console.log(str[0]); // "h"
```

## String Comparison

- Comparison is in alphabetical order.

```javascript
console.log("a" > "Z"); // true
// Lowercase is always greater than uppercase
```

- Diacritical marks are out of order.

```javascript
console.log("Ö" < "xyz"); // true
// "Ö" is treated differently than 'o' due to the diacritical mark
```

## `localeCompare`

- Use `localeCompare` for more accurate string comparison.

```javascript
let str1 = "hello";
let str2 = "hello";

console.log(str1.localeCompare(str2)); // 0 if equivalent
```

### Explanation

1. **Character Access**:
    - You can access individual characters in a string using bracket notation `str[0]` or the `at` method `str.at(0)`. Both return the character at the specified position.

2. **Immutability**:
    - Strings in JavaScript are immutable, meaning once a string is created, it cannot be altered. Any operations that seem to modify a string will instead create a new string. For instance, trying to change a character in a string using bracket notation will not work and will result in an error or be ignored.

3. **String Comparison**:
    - Strings are compared based on their Unicode values. This means that lowercase letters (`"a"`) are greater than uppercase letters (`"Z"`), as Unicode values for lowercase letters are higher.
    - Diacritical marks (accents, umlauts, etc.) affect the order of comparison. For example, `"Ö"` (O with umlaut) is compared differently than `"o"` or `"O"`.

4. **`localeCompare`**:
    - The `localeCompare` method is used for comparing strings in a more localized context, considering language-specific rules. It returns `0` if the strings are equivalent, a negative number if the reference string is sorted before the compared string, and a positive number if it is sorted after.

# Array Methods

- Negative indexes are allowed.

```javascript
let arr = [1, 2, 3];
arr.splice(-1, 0, 4, 5);
console.log(arr); // [1, 2, 4, 5, 3]
```

## Symbol.isConcatSpreadable

- If present in an array-like object, it is treated as an array by `concat`, and its elements are added.

```javascript
let arr = [1, 2];
let arrayLike = {
    0: 'x',
    1: 'y',
    length: 2,
    [Symbol.isConcatSpreadable]: true
};

console.log(arr.concat(arrayLike)); // [1, 2, 'x', 'y']
```

## `includes` and `indexOf`

- `includes` handles `NaN` correctly, whereas `indexOf` does not.

```javascript
let arr = [NaN];
console.log(arr.includes(NaN)); // true
console.log(arr.indexOf(NaN)); // -1
```

## `find`

- Useful in arrays of objects. Looks for the first element that makes the function return `true`.

```javascript
let arr = [{ id: 1, name: 'Sajid' }, { id: 2, name: 'Raj' }];
let user = arr.find(item => item.id === 1);
console.log(user); // { id: 1, name: 'Sajid' }
console.log(user.name); // 'Sajid'
```

### Additional Find Methods

- `findIndex`: Returns the index of the first element that satisfies the condition.

```javascript
let index = arr.findIndex(item => item.id === 1);
console.log(index); // 0
```

- `findLastIndex`: Returns the index of the last element that satisfies the condition.

```javascript
let lastIndex = arr.findLastIndex(item => item.id === 1);
console.log(lastIndex); // 0
```

## `filter`

- Returns an array of all elements that make the function return `true`.

```javascript
let users = [
    { id: 1, name: 'Sajid' },
    { id: 2, name: 'Raj' },
    { id: 3, name: 'John' }
];
let filteredUsers = users.filter(user => user.id < 3);
console.log(filteredUsers); // [{ id: 1, name: 'Sajid' }, { id: 2, name: 'Raj' }]
```

## Transform Array

### `map`

- Calls a function for each element and returns an array of results.

```javascript
let names = ['Krishan', 'Raj', 'Bram'];
let nameLengths = names.map(item => item.length);
console.log(nameLengths); // [7, 3, 4]
```

### `sort`

- Sorts an array in place and also returns the sorted array. Items are sorted as strings by default.

```javascript
let arr = [1, 2, 15];
arr.sort();
console.log(arr); // [1, 15, 2]

// Custom compare function
arr.sort((a, b) => a - b);
console.log(arr); // [1, 2, 15]
```

### `reverse`

- Reverses the order of elements in an array.

```javascript
let arr = [1, 2, 3];
arr.reverse();
console.log(arr); // [3, 2, 1]
```

# `split` Method

- The `split` method splits a string into an array of substrings, and returns the new array.

```javascript
let names = "Ram, Lakshman, Hanuman";
let nameArray = names.split(", ");
console.log(nameArray); // ["Ram", "Lakshman", "Hanuman"]
```

- You can limit the number of splits by providing a second parameter.

```javascript
let limitedNames = names.split(", ", 2);
console.log(limitedNames); // ["Ram", "Lakshman"]
```

- `split` can also be used with other characters.

```javascript
let str = "string";
let charArray = str.split("");
console.log(charArray); // ["s", "t", "r", "i", "n", "g"]
```

# `join` Method

- The `join` method joins all elements of an array into a string.

```javascript
let joinedNames = nameArray.join(", ");
console.log(joinedNames); // "Ram, Lakshman, Hanuman"
```

### Explanation

1. **`split` Method**:
    - The `split` method is used to divide a string into an array of substrings based on a specified delimiter. The original string remains unchanged.
    - The method takes two arguments: the delimiter (a string or regular expression) and an optional limit on the number of splits.
    - Example: Splitting a comma-separated string into an array of names.

2. **`join` Method**:
    - The `join` method is used to join all elements of an array into a single string. The elements are separated by a specified delimiter.
    - This method is particularly useful for creating a string from an array of substrings.
    - Example: Joining an array of names into a single comma-separated string.

# `reduce` and `reduceRight` Methods

- Used to calculate a single value based on the array.

```javascript
let arr = [1, 2, 3, 4];

let result = arr.reduce((accumulator, item) => accumulator + item, 0);
console.log(result); // 10
```

- The function is applied to all array elements one after another and carries its result to the next call.

### Parameters

1. **accumulator**: Result of the previous function call, equals the initial value the first time if provided.
2. **item**: Current array element.
3. **index**: Position of the current element.
4. **array**: The array being iterated.

```javascript
let value = arr.reduce((accumulator, item, index, array) => {
    // Logic here
}, initialValue);
```

## `thisArg` Parameter

- An optional parameter accepted by all array methods (other than `sort`) that becomes `this` for the function.

```javascript
let army = {
    minAge: 18,
    maxAge: 27,
    canJoin(user) {
        return user.age >= this.minAge && user.age < this.maxAge;
    }
};

let users = [
    { age: 16 },
    { age: 20 },
    { age: 23 }
];

let soldiers = users.filter(army.canJoin, army);
console.log(soldiers); // [{ age: 20 }, { age: 23 }]
```

### Explanation

1. **`reduce` and `reduceRight`**:
    - These methods iterate through an array and apply a function to each element to produce a single accumulated result. The `reduceRight` method operates similarly but from right to left.
    - The callback function used with `reduce` receives four parameters: `accumulator`, `item`, `index`, and `array`. The `accumulator` is the result of the previous callback invocation, and the `item` is the current element being processed.

2. **`thisArg` Parameter**:
    - Array methods such as `filter`, `map`, `forEach`, etc., accept an optional `thisArg` parameter. This parameter is used as `this` within the callback function. If not provided, `this` is `undefined` in strict mode or the global object in non-strict mode.
    - This is useful for passing the context (`this` value) into the callback function, ensuring it has access to the required properties and methods.


Based on your notes, here is a cleaned-up and formatted version of the JavaScript concepts you wrote down, with examples added where needed:

## Iterables

- **Generalization of arrays**: Allows for any object to be used in a `for...of` loop.
- **Symbol.iterator**: An object must implement this method to be iterable.

### Example
```javascript
let range = {
    from: 1,
    to: 5
};

range[Symbol.iterator] = function() {
    return {
        current: this.from,
        last: this.to,
        next() {
            if (this.current <= this.last) {
                return { done: false, value: this.current++ };
            } else {
                return { done: true };
            }
        }
    };
};

for (let num of range) {
    console.log(num); // 1, 2, 3, 4, 5
}
```

## Map & Set

### Map

- **Keys can be of any type**: string, number, object, etc.
- **NaN can be used as a key**: Uses SameValueZero algorithm, so `NaN` is equal to `NaN`.
- **Chaining**: `map.set()` returns itself, allowing for chaining.
  
#### Methods
- `map.keys()`: Returns an array of keys.
- `map.values()`: Returns an array of values.
- `map.entries()`: Returns an array of all key/value pairs (default iterator for `for...of`).

### Example
```javascript
let map = new Map();
map.set('1', 'val1').set('2', 'val2');

for (let [key, value] of map) {
    console.log(`${key}: ${value}`);
}
```

### Set

- **Set of values**: Only unique values, no duplicates.
- **Repeated calls**: `set.add()` with the same value will not do anything.
- **For...of can be used**: To iterate over the set.

#### Methods
- `set.keys()` and `set.values()`: Return the same values since there are no keys.
- `set.entries()`: Returns an iterable of `[value, value]`.

### Example
```javascript
let set = new Set([1, 2, 3, 3, 4]);
set.add(5);

for (let value of set) {
    console.log(value); // 1, 2, 3, 4, 5
}
```

## Object.fromEntries

- **Purpose**: Create an object from an array of key-value pairs (entries).
- Useful to convert a `Map` back to an `Object`.

### Example
```javascript
let map = new Map([
    ['key1', 'value1'],
    ['key2', 'value2']
]);

let obj = Object.fromEntries(map.entries());
console.log(obj); // { key1: 'value1', key2: 'value2' }
```

Here is a formatted explanation of the concepts from your notes, including WeakMap, WeakSet, destructuring assignment, and JSON handling:

## WeakMap and WeakSet

### WeakMap

- **Doesn't prevent garbage collection**: Keys are objects and can be garbage collected if no other reference exists.
- **All keys must be objects**, not primitives.

### Example
```javascript
let john = { name: "John" };
let weakMap = new WeakMap();
weakMap.set(john, "...");

john = null; // The object can be garbage collected.
```

### Use Cases
- Caching or keeping track of metadata for objects without preventing their garbage collection.

### WeakSet

- **Analogous to Set**: Only stores objects.
- **Objects exist in the set as long as there are references elsewhere**.
- **Does not support `.size` or `.keys`** methods.

### Example
```javascript
let obj1 = { name: "John" };
let obj2 = { name: "Doe" };

let weakSet = new WeakSet();
weakSet.add(obj1);
weakSet.add(obj2);

obj1 = null; // obj1 is eligible for garbage collection.
```

### Use Cases
- Tracking object presence while allowing them to be garbage collected.

### Note
- Both `WeakMap` and `WeakSet` are **not iterable**.

## Destructuring Assignment

- **Extract values** from arrays or properties from objects into distinct variables.

### Example
#### Object Destructuring
```javascript
let person = { name: "Ram", age: 27, faith: "Hindu" };
let { age, name } = person;

console.log(name); // "Ram"
console.log(age);  // 27
```

#### Array Destructuring
```javascript
let arr = [1, 2, 3];
let [a, , c] = arr; // Skipping the second element

console.log(a); // 1
console.log(c); // 3
```

## JSON Handling

- **Data-only format**: Excludes functions, symbolic keys/values, and properties with `undefined` values.

### Circular References
- **Not allowed**: Cannot be stringified into JSON.

### JSON.stringify()

- Converts a JavaScript object into a JSON string.
- Syntax: `JSON.stringify(value, replacer, space)`

### Example
```javascript
let obj = {
    name: "John",
    age: 30,
    greet: function() { console.log("Hello!"); },
    [Symbol('id')]: 123
};

let jsonString = JSON.stringify(obj, null, 2);

console.log(jsonString);
// Output:
// {
//   "name": "John",
//   "age": 30
// }
```
