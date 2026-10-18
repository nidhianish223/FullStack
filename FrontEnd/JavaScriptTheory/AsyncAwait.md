# Async and Await in JavaScript — Complete Explanation

`async` and `await` are important JavaScript concepts used in asynchronous programming. They make asynchronous code easier to write and understand.

I'll explain from basics in easy Hinglish, with code, output, dry runs, interview answers, and practice questions.

## 1. First, understand synchronous vs asynchronous JavaScript

### A. Synchronous code

Synchronous means code executes one statement at a time, in order.

```
console.log("First");
console.log("Second");
console.log("Third");
```

Output:

```
First
Second
Third
```

JavaScript executes the first statement, then the second, then the third.

### B. Asynchronous code

Asynchronous programming allows JavaScript to handle operations that complete later, such as fetching data from a server or waiting for a timer.

```
console.log("First");

setTimeout(() => {
  console.log("Second");
}, 2000);

console.log("Third");
```

Output:

```
First
Third
Second
```

Why? The timer completes later, so JavaScript continues executing the remaining synchronous code first.

Here, `2000` means 2000 milliseconds, or 2 seconds.

## 2. What is a Promise?

Before learning `async/await`, you should understand a Promise.

A Promise is an object representing the eventual success or failure of an asynchronous operation.

A Promise has three states:

| State     | Meaning                          |
| --------- | -------------------------------- |
| Pending   | Operation is not finished yet    |
| Fulfilled | Operation completed successfully |
| Rejected  | Operation failed                 |

Example:

```
const promise = new Promise((resolve, reject) => {
  resolve("Data received");
});

promise.then((result) => {
  console.log(result);
});
```

Output:

```
Data received
```

Easy Hinglish:

- `resolve()` — operation successful hua.
- `reject()` — operation fail hua.
- `.then()` — successful result handle karta hai.
- `.catch()` — error handle karta hai.

## 3. What is `async` in JavaScript?

The `async` keyword is used before a function to make it an async function. An async function always returns a Promise.

Example:

```
async function greet() {
  return "Hello Nidhi";
}

console.log(greet());
```

Output will be a Promise, conceptually like:

```
Promise { "Hello Nidhi" }
```

To get the value from that Promise, you can use `.then()`:

```
greet().then((result) => {
  console.log(result);
});
```

Output:

```
Hello Nidhi
```

Notice that even though we returned a normal string, the async function wrapped it in a fulfilled Promise.

### Important rule

```
async function test() {
  return 10;
}
```

This behaves like returning a Promise fulfilled with `10`, rather than returning the number directly.

## 4. What is `await` in JavaScript?

The `await` keyword is used inside an async function to wait for a Promise to settle and then obtain its fulfilled value.

In simple words, `await` ka matlab hai: Promise ka result aane tak is async function ke next step ko pause karo.

Example:

```
function getData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Data received");
    }, 2000);
  });
}

async function showData() {
  const result = await getData();
  console.log(result);
}

showData();
```

Output after approximately 2 seconds:

```
Data received
```

### Dry run — step by step

1

`showData()` starts

JavaScript enters the async function.

2

`await getData()`

The Promise is pending. The async function pauses at this line.

3

The timer finishes

After about 2 seconds, `resolve("Data received")` fulfills the Promise.

4

The function resumes

`result` gets the string `"Data received"`, which is printed.

Important interview point: `await` pauses the async function, not the entire JavaScript program. Other code can continue running.

## 5. Why do we need `async/await`?

Consider this Promise-based code:

```
function getUser() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Nidhi");
    }, 1000);
  });
}

getUser().then((name) => {
  console.log(name);
});
```

Using `async/await`, we can write:

```
async function displayUser() {
  const name = await getUser();
  console.log(name);
}

displayUser();
```

Both print:

```
Nidhi
```

The advantage is that `async/await` makes asynchronous code look more like ordinary, sequential code. It can also make error handling easier with `try...catch`.

## 6. Difference between `async` and `await`

| `async`                                        | `await`                                              |
| ---------------------------------------------- | ---------------------------------------------------- |
| Declares an async function                     | Waits for a Promise's result                         |
| Makes the function return a Promise            | Pauses that async function until the Promise settles |
| Written before `function` or an arrow function | Usually used inside an async function                |
| Example: `async function test()`               | Example: `const x = await getData()`                 |

## 7. Error handling with `try...catch`

Sometimes an asynchronous operation fails. For example, a server request might fail or a Promise might reject.

We can handle this using `try...catch`.

```
async function getData() {
  try {
    const result = await Promise.reject("Something went wrong");
    console.log(result);
  } catch (error) {
    console.log(error);
  }
}

getData();
```

Output:

```
Something went wrong
```

How it works:

- `try` contains the code that might fail.
- If the awaited Promise rejects, control moves to `catch`.
- `error` contains the rejection reason in this example.

If you don't handle a rejection inside the function, the async function's returned Promise will reject. The caller should handle it appropriately.

## 8. Real-life example: Fetching API data

Suppose we want to get user data from a server.

```
async function getUser() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/users/1"
    );

    if (!response.ok) {
      throw new Error("Failed to fetch user");
    }

    const data = await response.json();

    console.log(data);
    console.log(data.name);
  } catch (error) {
    console.log("Error:", error.message);
  }
}

getUser();
```

This example uses a public test API.

Dry run:

1. `fetch()` sends an HTTP request and returns a Promise.
2. The first `await` waits for the response.
3. `response.ok` checks whether the HTTP status is in the successful range.
4. `response.json()` returns another Promise that reads and parses the response body.
5. The second `await` waits for the parsed data.
6. `data.name` accesses the user's name.
7. If a network error, parsing error, or explicitly thrown error occurs, `catch` handles it.

Interview tip: `fetch()` does not automatically reject for HTTP errors such as `404 Not Found`. Check `response.ok` or `response.status`.

## 9. Sequential execution using `await`

When you use `await` one after another, the operations generally run sequentially.

```
function task1() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Task 1 completed"), 1000);
  });
}

function task2() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Task 2 completed"), 1000);
  });
}

async function runTasks() {
  const a = await task1();
  console.log(a);

  const b = await task2();
  console.log(b);
}

runTasks();
```

Output:

```
Task 1 completed
Task 2 completed
```

Total time is approximately 2 seconds because `task2()` starts after `task1()` finishes.

## 10. Parallel execution using `Promise.all()`

If two independent tasks can run together, `Promise.all()` can save time.

```
async function runTasks() {
  const results = await Promise.all([
    task1(),
    task2()
  ]);

  console.log(results);
}

runTasks();
```

Output:

```
["Task 1 completed", "Task 2 completed"]
```

Total time is approximately 1 second because both timers start together.

| Sequential `await`                                  | `Promise.all()`                      |
| --------------------------------------------------- | ------------------------------------ |
| Runs dependent steps one after another              | Waits for multiple Promises together |
| Can take longer for independent tasks               | Often faster for independent tasks   |
| Useful when the next task needs the previous result | Useful when tasks are independent    |

Remember: `Promise.all()` rejects if any input Promise rejects, unless you handle the error or use a different approach such as `Promise.allSettled()`.

## 11. Common mistakes in async/await

### Mistake 1: Forgetting `await`

```
async function test() {
  const result = Promise.resolve(10);
  console.log(result);
}

test();
```

The output is a Promise object, not the number `10`.

Correct code:

```
async function test() {
  const result = await Promise.resolve(10);
  console.log(result);
}

test();
```

Output:

```
10
```

### Mistake 2: Thinking `await` blocks everything

```
async function test() {
  console.log("A");
  await Promise.resolve();
  console.log("B");
}

test();
console.log("C");
```

Output:

```
A
C
B
```

Why? After reaching `await`, the async function pauses. JavaScript continues with `console.log("C")` before resuming the function.

### Mistake 3: Assuming `await` automatically handles errors

`await` does not make a rejected Promise successful. Use `try...catch` or handle the returned Promise with `.catch()`.

## 12. How to write async/await in an interview

You can use this answer directly:

Definition of Async/Await in JavaScript

Async and await are features of JavaScript used to handle asynchronous operations. The `async` keyword declares a function that always returns a Promise. The `await` keyword pauses the execution of the async function until the awaited Promise settles. If the Promise is fulfilled, await returns its value; if it is rejected, await throws the rejection reason.

Async/await makes asynchronous code easier to read and maintain. Errors can be handled using `try...catch`. It is commonly used with API requests, database operations and other asynchronous tasks.

## 13. Interview practice — predict the output

Question 1: What will be the output?

```
async function test() {
  console.log("A");

  await Promise.resolve();

  console.log("B");
}

test();
console.log("C");
```

A. A, B, C

B. A, C, B

C. C, A, B

D. A, B only

Check my answer

Learn these four concepts together for interviews: Promise, async, await, and try...catch. Once these are clear, API calls and asynchronous JavaScript questions become much easier.