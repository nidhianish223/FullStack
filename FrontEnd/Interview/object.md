# JavaScript Object and Its Methods — Complete Guide

In JavaScript, an object is a collection of properties stored as key-value pairs. Objects help us store related information and functions together.

I'll explain this in easy Hinglish with examples, outputs, and interview questions so you can understand the concepts and explain them in English during an interview.

## 1. What is an Object in JavaScript?

Example:

```
const student = {
  name: "Nidhi",
  age: 27,
  course: "BCA",

  greet: function () {
    return "Hello!";
  }
};

console.log(student.name);
console.log(student.age);
console.log(student.greet());
```

Output:

```
Nidhi
27
Hello!
```

Easy explanation:

- `student` — object ka naam.
- `name`, `age`, `course` — properties (data).
- `"Nidhi"`, `27`, `"BCA"` — property values.
- `greet()` — method (object ke andar function).

Property = data; Method = function associated with an object.

## 2. How to access object properties

There are two common ways.

### A. Dot notation

```
const person = {
  name: "Rahul",
  age: 25
};

console.log(person.name);
console.log(person.age);
```

Output: `Rahul`, `25`

### B. Bracket notation

```
const person = {
  name: "Rahul",
  age: 25
};

console.log(person["name"]);
console.log(person["age"]);
```

Output: `Rahul`, `25`

Bracket notation is especially useful when the property name is stored in a variable or contains spaces.

```
const person = {
  name: "Rahul",
  "first name": "Rahul Kumar"
};

const key = "name";

console.log(person[key]);
console.log(person["first name"]);
```

Output:

```
Rahul
Rahul Kumar
```

## 3. Adding, updating and deleting properties

```
const user = {
  name: "Nidhi",
  age: 27
};

// Add a property
user.city = "Chennai";

// Update a property
user.age = 28;

// Delete a property
delete user.city;

console.log(user);
```

Output:

```
{ name: "Nidhi", age: 28 }
```

Remember these three operations:

| Operation | Syntax                  |
| --------- | ----------------------- |
| Add       | `user.city = "Chennai"` |
| Update    | `user.age = 28`         |
| Delete    | `delete user.city`      |

## 4. Important JavaScript Object methods

JavaScript provides built-in methods through the `Object` constructor. These are useful for reading, copying, checking and protecting objects.

### 1. `Object.keys()`

Returns an array containing all the object's own property names (keys).

```
const student = {
  name: "Nidhi",
  age: 27,
  course: "BCA"
};

console.log(Object.keys(student));
```

Output:

```
["name", "age", "course"]
```

Easy meaning: Object ke saare keys ki list mil jaati hai.

### 2. `Object.values()`

Returns an array containing the values of an object's own enumerable properties.

```
const student = {
  name: "Nidhi",
  age: 27,
  course: "BCA"
};

console.log(Object.values(student));
```

Output:

```
["Nidhi", 27, "BCA"]
```

Easy meaning: Sirf values ki list milegi.

### 3. `Object.entries()`

Returns an array of key-value pairs. Each pair is represented by a two-element array.

```
const student = {
  name: "Nidhi",
  age: 27
};

console.log(Object.entries(student));
```

Output:

```
[
  ["name", "Nidhi"],
  ["age", 27]
]
```

Easy meaning: Key aur value dono ek saath milte hain.

### Difference between `keys()`, `values()` and `entries()`

| Method                | Returns         | Example result                  |
| --------------------- | --------------- | ------------------------------- |
| `Object.keys(obj)`    | Keys            | `["name", "age"]`               |
| `Object.values(obj)`  | Values          | `["Nidhi", 27]`                 |
| `Object.entries(obj)` | Key-value pairs | `[["name","Nidhi"],["age",27]]` |

### 4. `Object.assign()`

Copies enumerable own properties from one or more source objects into a target object.

```
const first = { name: "Nidhi" };
const second = { age: 27 };

const result = Object.assign({}, first, second);

console.log(result);
```

Output:

```
{ name: "Nidhi", age: 27 }
```

Easy meaning: Multiple objects ki properties ko ek target object mein copy kar sakte hain.

Important: `Object.assign()` is a shallow copy, not a deep copy. Nested objects can still be shared.

### 5. `Object.freeze()`

Prevents adding, deleting or changing the values of an object's own data properties.

```
const user = {
  name: "Nidhi",
  age: 27
};

Object.freeze(user);

user.age = 30;
user.city = "Chennai";
delete user.name;

console.log(user);
```

Output:

```
{ name: "Nidhi", age: 27 }
```

Easy meaning: Object ko freeze karne ke baad uski existing properties ko normally change nahi kar sakte.

Important: `Object.freeze()` is shallow. Nested objects can still be modified unless they are frozen separately.

### 6. `Object.seal()`

Prevents adding or deleting properties, but existing writable properties can still be updated.

```
const user = {
  name: "Nidhi",
  age: 27
};

Object.seal(user);

user.age = 30;
user.city = "Chennai";
delete user.name;

console.log(user);
```

Output:

```
{ name: "Nidhi", age: 30 }
```

Easy meaning: Property add/delete nahi kar sakte, lekin existing value update kar sakte hain.

### 7. `Object.preventExtensions()`

Prevents adding new properties to an object. Existing properties may still be updated or deleted, subject to their property descriptors.

```
const user = {
  name: "Nidhi",
  age: 27
};

Object.preventExtensions(user);

user.age = 30;
user.city = "Chennai";

console.log(user);
```

Output:

```
{ name: "Nidhi", age: 30 }
```

Easy meaning: Nayi property add nahi kar sakte, lekin existing properties ko normally update kar sakte hain.

### Difference between protection methods

| Method                       | Add | Delete | Update existing writable property |
| ---------------------------- | --- | ------ | --------------------------------- |
| `Object.preventExtensions()` | ❌   | ✅      | ✅                                 |
| `Object.seal()`              | ❌   | ❌      | ✅                                 |
| `Object.freeze()`            | ❌   | ❌      | ❌                                 |

### 8. `Object.isFrozen()`, `Object.isSealed()` and `Object.isExtensible()`

These methods check an object's protection status.

```
const a = { x: 10 };
const b = { x: 10 };
const c = { x: 10 };

Object.freeze(a);
Object.seal(b);
Object.preventExtensions(c);

console.log(Object.isFrozen(a));    // true
console.log(Object.isSealed(b));    // true
console.log(Object.isExtensible(c)); // false
```

- `Object.isFrozen(obj)` checks whether the object is frozen.
- `Object.isSealed(obj)` checks whether the object is sealed.
- `Object.isExtensible(obj)` checks whether new properties can be added.

Note that a sealed object can also be frozen if all its properties are non-writable, so these statuses are not mutually exclusive.

### 9. `Object.hasOwn()`

Checks whether a property belongs directly to an object, rather than being inherited from its prototype.

```
const student = {
  name: "Nidhi",
  age: 27
};

console.log(Object.hasOwn(student, "name"));
console.log(Object.hasOwn(student, "city"));
```

Output:

```
true
false
```

Easy meaning: Object ke andar directly woh property present hai ya nahi, ye check karta hai.

### 10. `Object.create()`

Creates a new object using the specified prototype object.

```
const person = {
  greet() {
    return "Hello!";
  }
};

const student = Object.create(person);

student.name = "Nidhi";

console.log(student.name);
console.log(student.greet());
```

Output:

```
Nidhi
Hello!
```

Here, `student` inherits the `greet()` method from `person`.

Easy meaning: Ek object ko doosre object ki properties aur methods inherit karne ke liye use kar sakte hain.

### 11. `Object.defineProperty()`

Defines a property on an object and lets you configure its behavior.

```
const user = {};

Object.defineProperty(user, "name", {
  value: "Nidhi",
  writable: false,
  enumerable: true,
  configurable: false
});

console.log(user.name);
```

Output:

```
Nidhi
```

Meaning of the options:

| Option         | Meaning                                                                    |
| -------------- | -------------------------------------------------------------------------- |
| `value`        | Property ki value                                                          |
| `writable`     | Value update kar sakte hain ya nahi                                        |
| `enumerable`   | Property normal enumeration mein appear hogi ya nahi                       |
| `configurable` | Property delete kar sakte hain ya descriptor change kar sakte hain ya nahi |

Here, `writable: false` means the `name` value cannot be changed through normal assignment.

### 12. `Object.fromEntries()`

Converts key-value pairs into an object. It is often used with the output of `Object.entries()`.

```
const entries = [
  ["name", "Nidhi"],
  ["age", 27]
];

const user = Object.fromEntries(entries);

console.log(user);
```

Output:

```
{ name: "Nidhi", age: 27 }
```

Easy meaning: Key-value pairs ki list ko object mein convert kar deta hai.

### 13. `Object.is()`

Compares two values to determine whether they are the same according to JavaScript's `Object.is()` rules.

```
console.log(Object.is(10, 10));
console.log(Object.is(10, 20));
console.log(Object.is(NaN, NaN));
```

Output:

```
true
false
true
```

One important difference from `===`:

```
console.log(NaN === NaN);       // false
console.log(Object.is(NaN, NaN)); // true
```

### 14. `Object.getPrototypeOf()`

Returns the prototype of an object.

```
const user = {
  name: "Nidhi"
};

console.log(Object.getPrototypeOf(user) === Object.prototype);
```

Output:

```
true
```

Easy meaning: Check karta hai ki object ka prototype kya hai.

### 15. `Object.setPrototypeOf()`

Sets the prototype of an existing object.

```
const animal = {
  eat() {
    return "Eating";
  }
};

const dog = {};

Object.setPrototypeOf(dog, animal);

console.log(dog.eat());
```

Output:

```
Eating
```

Use this carefully. For normal inheritance, setting the prototype when creating the object is generally preferable to changing it later.

## 5. Common object-related methods: `hasOwnProperty()`, `toString()` and `valueOf()`

These methods are commonly encountered through an object's prototype.

```
const user = {
  name: "Nidhi"
};

console.log(user.hasOwnProperty("name")); // true
console.log(user.toString());             // [object Object]
console.log(user.valueOf() === user);     // true
```

- `hasOwnProperty()` checks for an object's own property. For safer checking on arbitrary objects, prefer `Object.hasOwn()`.
- `toString()` converts an object to a string representation.
- `valueOf()` returns the object's primitive value when applicable; for an ordinary object, it usually returns the object itself.

## 6. Loop through an object

### Using `for...in`

```
const student = {
  name: "Nidhi",
  age: 27,
  course: "BCA"
};

for (let key in student) {
  console.log(key, student[key]);
}
```

Output:

```
name Nidhi
age 27
course BCA
```

`for...in` iterates over enumerable string keys, including inherited ones. If you only want an object's own keys, use `Object.keys()` or check `Object.hasOwn()`.

### Using `Object.entries()` with `for...of`

```
const student = {
  name: "Nidhi",
  age: 27
};

for (const [key, value] of Object.entries(student)) {
  console.log(key, value);
}
```

Output:

```
name Nidhi
age 27
```

This is convenient when you need both the key and value.

## 7. Object destructuring

Destructuring extracts properties into variables.

```
const student = {
  name: "Nidhi",
  age: 27
};

const { name, age } = student;

console.log(name);
console.log(age);
```

Output:

```
Nidhi
27
```

## 8. The `this` keyword inside an object method

The `this` keyword generally refers to the object used to call a regular method.

```
const student = {
  name: "Nidhi",

  greet() {
    return "Hello " + this.name;
  }
};

console.log(student.greet());
```

Output:

```
Hello Nidhi
```

Here, `this.name` refers to `student.name`.

Be careful: arrow functions do not create their own `this`, so an arrow function should not be used as an object method when you expect `this` to refer to that object.

## 9. Quick revision for JavaScript interviews

| Method                       | Main purpose                                                            |
| ---------------------------- | ----------------------------------------------------------------------- |
| `Object.keys()`              | Get property keys                                                       |
| `Object.values()`            | Get property values                                                     |
| `Object.entries()`           | Get key-value pairs                                                     |
| `Object.assign()`            | Copy properties into a target                                           |
| `Object.freeze()`            | Prevent changes to existing data properties and prevent adding/deleting |
| `Object.seal()`              | Prevent adding/deleting properties                                      |
| `Object.preventExtensions()` | Prevent adding properties                                               |
| `Object.hasOwn()`            | Check an own property                                                   |
| `Object.create()`            | Create an object with a specified prototype                             |
| `Object.defineProperty()`    | Define/configure a property                                             |
| `Object.fromEntries()`       | Convert entries into an object                                          |
| `Object.is()`                | Compare two values                                                      |
| `Object.getPrototypeOf()`    | Get an object's prototype                                               |
| `Object.setPrototypeOf()`    | Set an object's prototype                                               |
| `Object.isFrozen()`          | Check frozen status                                                     |
| `Object.isSealed()`          | Check sealed status                                                     |
| `Object.isExtensible()`      | Check whether properties can be added                                   |

## 10. Practice question

What will be the output?

```
const obj = {
  a: 10,
  b: 20
};

console.log(Object.keys(obj));
console.log(Object.values(obj));
console.log(Object.entries(obj));
```

A. All three return only the values `10, 20`.

B. Keys return `["a","b"]`, values return `[10,20]`, and entries return `[["a",10],["b",20]]`.

C. All three return the original object.

D. The code produces an error.

Check my answer

My suggestion: Learn `keys()`, `values()`, `entries()`, `assign()`, `freeze()`, `seal()`, `hasOwn()` and `create()` first. These are useful foundations for JavaScript coding and interviews.