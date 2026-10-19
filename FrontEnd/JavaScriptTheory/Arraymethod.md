# Array Methods in JavaScript — Detailed Notes

## 1. What is an Array in JavaScript?

An array is a special variable used to store multiple values in a single variable. Arrays can store strings, numbers, objects, and other data types.

Example:

```
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits);
console.log(fruits[0]);
```

Output:

```
["Apple", "Mango", "Banana"]
Apple
```

Explanation:

- `fruits` is an array.
- Array indexing starts from `0`.
- `fruits[0]` returns `"Apple"`.
- `fruits[1]` returns `"Mango"`.

## 2. What are Array Methods?

Array methods are built-in JavaScript functions used to perform operations on arrays, such as adding elements, removing elements, searching, sorting, and transforming data.

For example, instead of manually adding an item to an array, we can use the `push()` method.

```
const numbers = [10, 20, 30];

numbers.push(40);

console.log(numbers);
```

Output:

```
[10, 20, 30, 40]
```

## 3. Important Array Methods

JavaScript has many array methods. For learning and interviews, understand them in these categories:

## 4. Adding and Removing Array Elements

### A. `push()`

The `push()` method adds one or more elements to the end of an array.

```
const arr = [10, 20, 30];

arr.push(40);

console.log(arr);
```

Output: `[10, 20, 30, 40]`

### B. `pop()`

The `pop()` method removes the last element from an array and returns that element.

```
const arr = [10, 20, 30];

const result = arr.pop();

console.log(result);
console.log(arr);
```

Output:

```
30
[10, 20]
```

### C. `unshift()`

The `unshift()` method adds one or more elements to the beginning of an array.

```
const arr = [20, 30];

arr.unshift(10);

console.log(arr);
```

Output: `[10, 20, 30]`

### D. `shift()`

The `shift()` method removes the first element from an array and returns it.

```
const arr = [10, 20, 30];

const result = arr.shift();

console.log(result);
console.log(arr);
```

Output:

```
10
[20, 30]
```

### Comparison

| Method      | Operation          | Position  |
| ----------- | ------------------ | --------- |
| `push()`    | Adds element(s)    | End       |
| `pop()`     | Removes an element | End       |
| `unshift()` | Adds element(s)    | Beginning |
| `shift()`   | Removes an element | Beginning |

Easy trick: `push` and `pop` work at the end; `shift` and `unshift` work at the beginning.

## 5. `slice()` Method

The `slice()` method extracts a portion of an array and returns it as a new array. It does not change the original array.

Syntax:

```
array.slice(start, end);
```

- `start`: Index from which extraction begins.
- `end`: Index where extraction stops, but this index is not included.

Example:

```
const arr = [10, 20, 30, 40, 50];

const result = arr.slice(1, 4);

console.log(result);
console.log(arr);
```

Output:

```
[20, 30, 40]
[10, 20, 30, 40, 50]
```

Dry run:

- Index 1 contains `20`.
- Index 2 contains `30`.
- Index 3 contains `40`.
- Index 4 is excluded.

Therefore, the result is `[20, 30, 40]`.

## 6. `splice()` Method

The `splice()` method can add, remove, or replace elements in an array. Unlike `slice()`, it modifies the original array.

Syntax:

```
array.splice(start, deleteCount, item1, item2);
```

Example 1: Removing elements

```
const arr = [10, 20, 30, 40];

arr.splice(1, 2);

console.log(arr);
```

Output:

```
[10, 40]
```

Explanation: Starting at index `1`, it removes two elements: `20` and `30`.

Example 2: Adding elements

```
const arr = [10, 30, 40];

arr.splice(1, 0, 20);

console.log(arr);
```

Output: `[10, 20, 30, 40]`

Explanation: Start at index `1`, delete zero elements, and insert `20`.

Example 3: Replacing elements

```
const arr = [10, 20, 30];

arr.splice(1, 1, 99);

console.log(arr);
```

Output: `[10, 99, 30]`

Explanation: It removes `20` and inserts `99` at index `1`.

### Difference between `slice()` and `splice()`

| `slice()`                           | `splice()`                                  |
| ----------------------------------- | ------------------------------------------- |
| Extracts a portion of an array.     | Adds, removes, or replaces elements.        |
| Does not modify the original array. | Modifies the original array.                |
| Returns the extracted elements.     | Returns the removed elements.               |
| Syntax: `slice(start, end)`         | Syntax: `splice(start, deleteCount, items)` |

## 7. `concat()` Method

The `concat()` method combines two or more arrays and returns a new array.

```
const a = [1, 2];
const b = [3, 4];

const result = a.concat(b);

console.log(result);
```

Output: `[1, 2, 3, 4]`

The original arrays remain unchanged.

## 8. `indexOf()` and `includes()`

### A. `indexOf()`

Returns the index of the first matching element. If the element is not found, it returns `-1`.

```
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.indexOf("Mango"));
console.log(fruits.indexOf("Grapes"));
```

Output:

```
1
-1
```

### B. `includes()`

Checks whether an array contains a particular value. It returns `true` or `false`.

```
const numbers = [10, 20, 30];

console.log(numbers.includes(20));
console.log(numbers.includes(50));
```

Output:

```
true
false
```

## 9. `find()` and `findIndex()`

### A. `find()`

Returns the first element that satisfies a condition. If no element matches, it returns `undefined`.

```
const numbers = [5, 12, 18, 25];

const result = numbers.find(n => n > 15);

console.log(result);
```

Output: `18`

Explanation: `5` and `12` do not satisfy the condition. `18` is the first number greater than `15`, so it is returned.

### B. `findIndex()`

Returns the index of the first element that satisfies a condition. If no element matches, it returns `-1`.

```
const numbers = [5, 12, 18, 25];

const result = numbers.findIndex(n => n > 15);

console.log(result);
```

Output: `2`

Because `18` is at index `2`.

## 10. `forEach()` Method

The `forEach()` method executes a callback function for each element of an array. It is generally used to perform an action for every element.

```
const numbers = [10, 20, 30];

numbers.forEach(n => {
    console.log(n);
});
```

Output:

```
10
20
30
```

Important: `forEach()` returns `undefined`; it does not create a new array of callback results.

## 11. `map()` Method

The `map()` method applies a function to every array element and returns a new array containing the results.

```
const numbers = [1, 2, 3, 4];

const result = numbers.map(n => n * 2);

console.log(result);
```

Output: `[2, 4, 6, 8]`

Dry run:

| Input | Operation | Output |
| ----- | --------- | ------ |
| 1     | 1 × 2     | 2      |
| 2     | 2 × 2     | 4      |
| 3     | 3 × 2     | 6      |
| 4     | 4 × 2     | 8      |

Original array: `[1, 2, 3, 4]`

New array: `[2, 4, 6, 8]`

## 12. `filter()` Method

The `filter()` method creates a new array containing only the elements that satisfy a given condition.

```
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers.filter(n => n % 2 === 0);

console.log(result);
```

Output: `[2, 4, 6]`

Explanation: The condition `n % 2 === 0` checks whether a number is even. Only the even numbers are included in the result.

## 13. `reduce()` Method

The `reduce()` method processes array elements to produce a single accumulated result, such as a sum or product.

Syntax:

```
array.reduce((accumulator, currentValue) => {
    return accumulator + currentValue;
}, initialValue);
```

- `accumulator`: Stores the accumulated result.
- `currentValue`: The current array element.
- `initialValue`: The starting value of the accumulator.

Example:

```
const numbers = [10, 20, 30, 40];

const result = numbers.reduce((acc, curr) => {
    return acc + curr;
}, 0);

console.log(result);
```

Output: `100`

Dry run:

| Step    | Accumulator (`acc`) | Current value (`curr`) | New accumulator |
| ------- | ------------------- | ---------------------- | --------------- |
| Initial | 0                   | —                      | 0               |
| 1       | 0                   | 10                     | 10              |
| 2       | 10                  | 20                     | 30              |
| 3       | 30                  | 30                     | 60              |
| 4       | 60                  | 40                     | 100             |

Final result: `100`.

### Difference between `map()`, `filter()`, `reduce()` and `forEach()`

| Method      | Purpose                             | Return value                                |
| ----------- | ----------------------------------- | ------------------------------------------- |
| `map()`     | Transforms each element             | New array                                   |
| `filter()`  | Selects matching elements           | New array                                   |
| `reduce()`  | Accumulates values                  | Single result, or another accumulated value |
| `forEach()` | Performs an action for each element | `undefined`                                 |

Remember this simple rule:

- `map()` = change values.
- `filter()` = select values.
- `reduce()` = combine values.
- `forEach()` = perform an action.

## 14. `sort()` Method

The `sort()` method sorts the elements of an array. By default, it sorts elements as strings in ascending order and modifies the original array.

Example:

```
const numbers = [40, 10, 30, 20];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output: `[10, 20, 30, 40]`

Explanation: `a - b` sorts numbers in ascending order.

For descending order:

```
const numbers = [40, 10, 30, 20];

numbers.sort((a, b) => b - a);

console.log(numbers);
```

Output: `[40, 30, 20, 10]`

Important: Without a comparison function, numeric arrays may be sorted incorrectly for numerical purposes.

```
[1, 10, 2].sort();
```

Output: `[1, 10, 2]`

This happens because the default sorting compares string representations.

## 15. `reverse()` Method

The `reverse()` method reverses the order of elements in an array. It modifies the original array.

```
const numbers = [10, 20, 30, 40];

numbers.reverse();

console.log(numbers);
```

Output: `[40, 30, 20, 10]`

## 16. `join()` Method

The `join()` method converts the elements of an array into a string, using a specified separator.

```
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.join(", "));
```

Output:

```
Apple, Mango, Banana
```

Another example:

```
const numbers = [1, 2, 3];

console.log(numbers.join("-"));
```

Output: `1-2-3`

## 17. `some()` and `every()` Methods

### A. `some()`

Returns `true` if at least one element satisfies the condition.

```
const numbers = [1, 3, 5, 8];

console.log(numbers.some(n => n % 2 === 0));
```

Output: `true`

Explanation: At least one number, `8`, is even.

### B. `every()`

Returns `true` only if all elements satisfy the condition.

```
const numbers = [2, 4, 6, 8];

console.log(numbers.every(n => n % 2 === 0));
```

Output: `true`

If even one element fails the condition, `every()` returns `false`.

| `some()`                         | `every()`                 |
| -------------------------------- | ------------------------- |
| At least one element must match. | Every element must match. |
| Returns a Boolean.               | Returns a Boolean.        |

## 18. `flat()` Method

The `flat()` method creates a new array by flattening nested arrays to a specified depth. Its default depth is `1`.

```
const numbers = [1, 2, [3, 4], [5, 6]];

console.log(numbers.flat());
```

Output:

```
[1, 2, 3, 4, 5, 6]
```

For deeper nested arrays:

```
const arr = [1, [2, [3, 4]]];

console.log(arr.flat(2));
```

Output: `[1, 2, 3, 4]`

## 19. Which Array Methods Modify the Original Array?

This is an important interview topic.

| Modifies the original array | Does not modify the original array |
| --------------------------- | ---------------------------------- |
| `push()`                    | `slice()`                          |
| `pop()`                     | `concat()`                         |
| `shift()`                   | `map()`                            |
| `unshift()`                 | `filter()`                         |
| `splice()`                  | `reduce()`                         |
| `sort()`                    | `find()`                           |
| `reverse()`                 | `includes()`                       |
|                             | `findIndex()`                      |
|                             | `some()`                           |
|                             | `every()`                          |
|                             | `flat()`                           |

Note: Methods such as `forEach()` do not inherently modify the original array, but their callback can modify it. Also, `sort()` and `reverse()` modify the original array; `toSorted()` and `toReversed()` provide non-mutating alternatives in modern JavaScript.

## 20. Quick Revision Notes

Use this table to revise the most important methods before an exam or interview.

| Method        | Use                                        |
| ------------- | ------------------------------------------ |
| `push()`      | Add elements at the end                    |
| `pop()`       | Remove the last element                    |
| `shift()`     | Remove the first element                   |
| `unshift()`   | Add elements at the beginning              |
| `slice()`     | Extract a portion                          |
| `splice()`    | Add, remove or replace elements            |
| `concat()`    | Combine arrays                             |
| `indexOf()`   | Find the index of a value                  |
| `includes()`  | Check whether a value exists               |
| `find()`      | Return the first matching element          |
| `findIndex()` | Return the index of the first match        |
| `forEach()`   | Execute a function for every element       |
| `map()`       | Transform elements                         |
| `filter()`    | Select matching elements                   |
| `reduce()`    | Accumulate values                          |
| `sort()`      | Sort elements                              |
| `reverse()`   | Reverse element order                      |
| `join()`      | Convert array elements into a string       |
| `some()`      | Check whether at least one element matches |
| `every()`     | Check whether all elements match           |
| `flat()`      | Flatten nested arrays                      |

## 21. How to Write in an Exam

Question: Explain array methods in JavaScript with examples.

Answer:

JavaScript provides several built-in array methods to manipulate and process arrays. These methods help programmers add, remove, search, sort and transform array elements.

The important array methods are:

1. `push()` — adds elements at the end of an array.
2. `pop()` — removes the last element.
3. `shift()` — removes the first element.
4. `unshift()` — adds elements at the beginning.
5. `slice()` — extracts a portion without modifying the original array.
6. `splice()` — adds, removes or replaces elements.
7. `map()` — transforms every element and returns a new array.
8. `filter()` — returns elements that satisfy a condition.
9. `reduce()` — combines elements into an accumulated result.
10. `forEach()` — executes a callback for each element.

Example:

```
const numbers = [1, 2, 3, 4];

console.log(numbers.map(n => n * 2));
console.log(numbers.filter(n => n > 2));
```

Output:

```
[2, 4, 6, 8]
[3, 4]
```

Conclusion: Array methods make JavaScript programming easier, shorter and more efficient by providing built-in operations for working with collections of data.

## Practice question

What will be the output of the following code?

```
const arr = [10, 20, 30, 40];

console.log(arr.slice(1, 3));
console.log(arr);
```

A. `[20, 30]` and `[10, 20, 30, 40]`

B. `[20, 30, 40]` and `[10, 20, 30, 40]`

C. `[20, 30]` and `[10, 40]`

D. `[10, 20, 30]` and `[10, 20, 30, 40]`

Check answer