Exam mein Call(), Apply() and Bind() in JavaScript ka answer is format mein likho. Ye answer definition, syntax, example aur difference ke saath hai.

# Call(), Apply() and Bind() in JavaScript

## 1. Introduction

In JavaScript, `call()`, `apply()` and `bind()` are predefined methods that are used to control the value of the `this` keyword inside a function. They allow us to use a function with a specific object.

## 2. Call() Method

Definition: The `call()` method calls a function immediately and allows us to set the value of `this`. Arguments are passed individually.

Syntax:

```
functionName.call(object, arg1, arg2);
```

Example:

```
const person = {
    name: "Nidhi"
};

function greet(city) {
    console.log(this.name + " lives in " + city);
}

greet.call(person, "Chennai");
```

Output:

```
Nidhi lives in Chennai
```

Explanation: The `call()` method sets `this` to the `person` object and executes the function immediately.

## 3. Apply() Method

Definition: The `apply()` method calls a function immediately and sets the value of `this`. Arguments are passed as an array.

Syntax:

```
functionName.apply(object, [arg1, arg2]);
```

Example:

```
const person = {
    name: "Nidhi"
};

function greet(city) {
    console.log(this.name + " lives in " + city);
}

greet.apply(person, ["Chennai"]);
```

Output:

```
Nidhi lives in Chennai
```

Explanation: The `apply()` method works like `call()`, but it accepts arguments in an array.

## 4. Bind() Method

Definition: The `bind()` method creates and returns a new function with a specified `this` value. The new function can be executed later.

Syntax:

```
const newFunction = functionName.bind(object, arg1, arg2);
```

Example:

```
const person = {
    name: "Nidhi"
};

function greet(city) {
    console.log(this.name + " lives in " + city);
}

const newGreet = greet.bind(person, "Chennai");

newGreet();
```

Output:

```
Nidhi lives in Chennai
```

Explanation: The `bind()` method creates a new function without executing it immediately. The function executes when `newGreet()` is called.

## 5. Difference between Call(), Apply() and Bind()

| Basis        | `call()`                                | `apply()`                             | `bind()`                                  |
| ------------ | --------------------------------------- | ------------------------------------- | ----------------------------------------- |
| Execution    | Immediately                             | Immediately                           | Later, when called                        |
| Arguments    | Passed individually                     | Passed as an array                    | Passed individually                       |
| Return value | Function's result                       | Function's result                     | A new function                            |
| Main purpose | Call a function with a specified `this` | Call a function using array arguments | Create a function with a specified `this` |

## 6. Conclusion

The `call()`, `apply()` and `bind()` methods are useful for controlling the `this` keyword in JavaScript. The main difference is that `call()` and `apply()` execute a function immediately, whereas `bind()` returns a new function that can be executed later.

Exam tip: For a 5-mark question, write the introduction, definitions, syntax and one example of each method. For a 10-mark question, also include the comparison table and conclusion.