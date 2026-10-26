# Currying Function in JavaScript — Short Notes

## 1. Definition

Currying is a technique in JavaScript in which a function that takes multiple arguments is converted into a sequence of functions, each taking one argument at a time.

## 2. Example

```
function add(a) {
    return function(b) {
        return function(c) {
            return a + b + c;
        };
    };
}

console.log(add(2)(3)(4)); // 9
```

Output:

```
9
```

## 3. Explanation

- `add(2)` takes the first argument `a = 2`.
- `(3)` takes the second argument `b = 3`.
- `(4)` takes the third argument `c = 4`.
- Finally, the function returns `2 + 3 + 4 = 9`.

## 4. Advantages of Currying

1. Code Reusability: Functions can be reused with fixed arguments.
2. Function Composition: Helps combine smaller functions.
3. Partial Application: Some arguments can be fixed in advance.
4. Better Modularity: Breaks complex functions into smaller functions.

## 5. Arrow Function Example

```
const add = a => b => c => a + b + c;

console.log(add(2)(3)(4)); // 9
```

Conclusion: Currying converts a function with multiple arguments into a sequence of functions that take one argument at a time. It is useful for code reusability and functional programming.