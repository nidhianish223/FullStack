# Closure in JavaScript — Short Notes

## 1. Definition

A Closure in JavaScript is created when an inner function remembers and can access variables from its outer function, even after the outer function has finished executing.

## 2. Example

```
function outer() {
    let count = 0;

    function inner() {
        count++;
        console.log(count);
    }

    return inner;
}

const result = outer();

result(); // 1
result(); // 2
result(); // 3
```

## 3. Explanation

- `outer()` creates a variable `count`.
- `inner()` accesses and modifies the `count` variable.
- `return inner` returns the inner function.
- Even after `outer()` finishes, `inner()` remembers the `count` variable.

This behavior is called a Closure.

## 4. Advantages of Closure

1. Data Privacy: Variables can be kept private.
2. State Management: Maintains values between function calls.
3. Function Factory: Helps create functions with different behaviors.
4. Encapsulation: Keeps related data and functions together.

## 5. Real-Life Example

```
function bankAccount() {
    let balance = 1000;

    return function() {
        console.log(balance);
    };
}

const account = bankAccount();
account(); // 1000
```

Here, `balance` cannot be accessed directly from outside the function, but the returned function can access it.

Conclusion: A closure allows an inner function to remember and access variables from its outer lexical scope, even after the outer function has completed execution.