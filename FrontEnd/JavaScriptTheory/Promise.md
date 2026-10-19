# JavaScript Promise — Complete Explanation

A Promise in JavaScript is an object that represents the eventual result of an operation that may complete in the future, either successfully or unsuccessfully.

I'll explain it from zero in easy Hinglish, with examples, output, dry runs, and interview questions.

## 1. Understand Promise with a real-life example

Imagine you order a pizza online. 🍕

- Pending: Your pizza is being prepared.
- Fulfilled: Your pizza has arrived successfully.
- Rejected: Your order failed.

A JavaScript Promise works similarly. It represents a result that may become available later.

### Pending

The operation is still in progress.

Fulfilled

Operation succeeded

resolve()

Rejected

Operation failed

reject()

A Promise has three states:

| State       | Meaning                                  |
| ----------- | ---------------------------------------- |
| `pending`   | Initial state; result is not settled yet |
| `fulfilled` | Operation completed successfully         |
| `rejected`  | Operation failed                         |

Once a Promise is fulfilled or rejected, it is settled and cannot change to another state.

## 2. Why do we need Promises?

Consider this example:

```
console.log("Order placed");

setTimeout(() => {
  console.log("Pizza delivered");
}, 2000);

console.log("Watching TV");
```

Output:

```
Order placed
Watching TV
Pizza delivered
```

The pizza delivery happens later, but JavaScript continues executing other code.

In real applications, we use asynchronous operations for:

- Fetching data from an API.
- Reading files.
- Database operations.
- Timers and other tasks that complete later.

Promises help us represent and handle the results of these operations.

## 3. How to create a Promise

We create a Promise using the `Promise` constructor.

```
const myPromise = new Promise((resolve, reject) => {
  resolve("Success!");
});

console.log(myPromise);
```

The Promise is fulfilled with the value `"Success!"`.

The constructor accepts an executor function, which receives two important functions:

- `resolve(value)` — fulfills the Promise with a value.
- `reject(reason)` — rejects the Promise with a reason.

Important: The executor function runs immediately when the Promise is constructed.

### Example of a successful Promise

```
const myPromise = new Promise((resolve, reject) => {
  resolve("Data received");
});

myPromise.then((result) => {
  console.log(result);
});
```

Output:

```
Data received
```

### Dry run

1. `new Promise()` creates a Promise.
2. The executor runs immediately.
3. `resolve("Data received")` fulfills the Promise.
4. `.then()` handles the fulfilled value.
5. `"Data received"` is printed.

## 4. What are `resolve()` and `reject()`?

### A. `resolve()` — success

```
const promise = new Promise((resolve, reject) => {
  resolve("Login successful");
});

promise.then((result) => {
  console.log(result);
});
```

Output:

```
Login successful
```

`resolve()` fulfills the Promise here, so `.then()` receives the success value.

### B. `reject()` — failure

```
const promise = new Promise((resolve, reject) => {
  reject("Login failed");
});

promise.catch((error) => {
  console.log(error);
});
```

Output:

```
Login failed
```

`reject()` rejects the Promise, and `.catch()` handles the rejection.

Easy Hinglish:

- `resolve()` = kaam successful hua.
- `reject()` = kaam fail hua.
- `.then()` = success value handle karna.
- `.catch()` = error handle karna.

## 5. The three most important Promise methods

### A. `.then()`

Used to handle a fulfilled Promise. It can also handle a rejection if you supply a second callback, but `.catch()` is often clearer for errors.

```
const promise = Promise.resolve(100);

promise.then((result) => {
  console.log(result);
});
```

Output:

```
100
```

### B. `.catch()`

Used to handle a rejected Promise.

```
const promise = Promise.reject("Something went wrong");

promise.catch((error) => {
  console.log(error);
});
```

Output:

```
Something went wrong
```

### C. `.finally()`

Runs when the Promise settles, whether fulfilled or rejected. It is useful for cleanup, such as hiding a loading indicator.

```
Promise.resolve("Success")
  .then((result) => {
    console.log(result);
  })
  .finally(() => {
    console.log("Operation finished");
  });
```

Output:

```
Success
Operation finished
```

### Difference between `then()`, `catch()` and `finally()`

| Method       | Purpose                                                              |
| ------------ | -------------------------------------------------------------------- |
| `.then()`    | Handle fulfillment; can also handle rejection with a second callback |
| `.catch()`   | Handle rejection                                                     |
| `.finally()` | Run cleanup after settlement                                         |

Important: `.finally()` normally passes through the original result or rejection unless its callback throws an error or returns a rejected Promise.

## 6. Promise with `setTimeout()` — important example

```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Task completed");
  }, 2000);
});

promise.then((result) => {
  console.log(result);
});

console.log("Hello");
```

Output:

```
Hello
Task completed
```

The second message appears after approximately two seconds.

### Dry run

1

Promise created

The executor starts immediately and schedules the timer.

2

`console.log("Hello")`

JavaScript does not wait for the timer, so `Hello` prints first.

3

Timer finishes

After approximately two seconds, `resolve()` fulfills the Promise.

4

`.then()` executes

The callback runs as a microtask and prints `Task completed`.

## 7. What is Promise chaining?

Promise chaining means using multiple `.then()` calls to perform steps one after another, passing results from one step to the next.

```
Promise.resolve(5)
  .then((num) => {
    console.log(num);
    return num * 2;
  })
  .then((result) => {
    console.log(result);
    return result + 5;
  })
  .then((finalResult) => {
    console.log(finalResult);
  });
```

Output:

```
5
10
15
```

### Dry run

1. The first `.then()` receives `5`.
2. It returns `5 * 2`, which is `10`.
3. The next `.then()` receives `10` and returns `15`.
4. The final `.then()` receives and prints `15`.

Important interview point: Each `.then()` returns a new Promise. If you return a normal value, the next Promise fulfills with that value. If you return another Promise, the chain waits for it to settle.

## 8. Error handling in Promise chaining

```
Promise.reject("Network error")
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log("Finished");
  });
```

Output:

```
Network error
Finished
```

Because the original Promise is rejected, the success callback is skipped and the error goes to `.catch()`.

If a `.then()` callback throws an error, the Promise returned by that `.then()` becomes rejected, and a later `.catch()` can handle it.

Example:

```
Promise.resolve(10)
  .then((value) => {
    throw new Error("Invalid value");
  })
  .catch((error) => {
    console.log(error.message);
  });
```

Output:

```
Invalid value
```

## 9. Four important static Promise methods

These are frequently asked in JavaScript interviews.

### A. `Promise.all()`

Waits for all input Promises to fulfill. If any input Promise rejects, the returned Promise rejects.

```
const p1 = Promise.resolve(10);
const p2 = Promise.resolve(20);
const p3 = Promise.resolve(30);

Promise.all([p1, p2, p3]).then((results) => {
  console.log(results);
});
```

Output:

```
[10, 20, 30]
```

Use it when all results are needed.

### B. `Promise.allSettled()`

Waits for all input Promises to settle, whether fulfilled or rejected.

```
const p1 = Promise.resolve("Success");
const p2 = Promise.reject("Failed");

Promise.allSettled([p1, p2]).then((results) => {
  console.log(results);
});
```

Output, simplified:

```
[
  { status: "fulfilled", value: "Success" },
  { status: "rejected", reason: "Failed" }
]
```

Use it when you need the outcome of every operation.

### C. `Promise.race()`

Settles with the outcome of the first input Promise to settle. The first outcome may be fulfillment or rejection.

```
const p1 = new Promise((resolve) => {
  setTimeout(() => resolve("First"), 1000);
});

const p2 = new Promise((resolve) => {
  setTimeout(() => resolve("Second"), 2000);
});

Promise.race([p1, p2]).then((result) => {
  console.log(result);
});
```

Output:

```
First
```

### D. `Promise.any()`

Fulfills with the first fulfilled input Promise. It ignores earlier rejections while waiting for a fulfillment. If all inputs reject, it rejects with an `AggregateError`.

```
const p1 = Promise.reject("Error 1");

const p2 = new Promise((resolve) => {
  setTimeout(() => resolve("Success 2"), 1000);
});

Promise.any([p1, p2]).then((result) => {
  console.log(result);
});
```

Output after approximately one second:

```
Success 2
```

### Comparison of all four methods

| Method                 | What it waits for                     | Result                                     |
| ---------------------- | ------------------------------------- | ------------------------------------------ |
| `Promise.all()`        | All fulfill, or one rejects           | Array of values, or rejection              |
| `Promise.allSettled()` | Every Promise settles                 | Array of outcomes                          |
| `Promise.race()`       | First Promise settles                 | First outcome                              |
| `Promise.any()`        | First Promise fulfills, or all reject | First fulfilled value, or `AggregateError` |

## 10. Difference between Promise and `async/await`

`async/await` is built on top of Promises. It provides another way to write asynchronous code.

Promise using `.then()`:

```
function getData() {
  return Promise.resolve("Data received");
}

getData().then((result) => {
  console.log(result);
});
```

Same example using `async/await`:

```
async function showData() {
  const result = await getData();
  console.log(result);
}

showData();
```

Both print:

```
Data received
```

| Promise with `.then()`                       | `async/await`                                      |
| -------------------------------------------- | -------------------------------------------------- |
| Uses `.then()` and `.catch()`                | Uses `await` and often `try...catch`               |
| Can chain asynchronous steps                 | Often easier to read for sequential steps          |
| Returns a Promise from `.then()`             | An async function always returns a Promise         |
| Useful for composing asynchronous operations | Useful for writing readable asynchronous functions |

## 11. Common Promise mistakes

### Mistake 1: Forgetting to return a value

```
Promise.resolve(5)
  .then((num) => {
    num * 2;
  })
  .then((result) => {
    console.log(result);
  });
```

Output:

```
undefined
```

Why? The first callback doesn't return anything.

Correct code:

```
Promise.resolve(5)
  .then((num) => {
    return num * 2;
  })
  .then((result) => {
    console.log(result);
  });
```

Output:

```
10
```

### Mistake 2: Thinking `resolve()` immediately executes `.then()`

```
console.log("A");

Promise.resolve().then(() => {
  console.log("B");
});

console.log("C");
```

Output:

```
A
C
B
```

Why? Promise callbacks such as `.then()` are scheduled as microtasks. They run after the current synchronous code completes.

### Mistake 3: Thinking `Promise.all()` makes every task succeed

`Promise.all()` rejects if any input Promise rejects. It does not automatically convert failures into successful results.

Use `Promise.allSettled()` if you need to collect both successes and failures.

## 12. JavaScript interview answer

You can write this definition in an interview:

What is a Promise in JavaScript?

A Promise is a JavaScript object that represents the eventual completion or failure of an asynchronous operation. It has three states: pending, fulfilled and rejected. The `resolve()` function fulfills a Promise, while `reject()` rejects it. The `.then()` method handles fulfillment, `.catch()` handles rejection, and `.finally()` executes after the Promise settles. Promises help manage asynchronous operations such as API requests and allow asynchronous tasks to be chained together.

## 13. Practice question — predict the output

Question 1: Promise chaining

```
Promise.resolve(10)
  .then((num) => {
    return num + 5;
  })
  .then((result) => {
    console.log(result);
  });
```

What will be the output?

A. `10`

B. `15`

C. `5`

D. `undefined`

Check my answer

My recommendation: Learn Promise states, `then()`, `catch()`, chaining, and `Promise.all()` first. Then practice `Promise.race()` and `Promise.any()`—they are particularly useful for JavaScript interviews.