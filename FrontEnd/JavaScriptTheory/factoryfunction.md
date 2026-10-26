# Factory Function in JavaScript — Short Notes

## Definition

A Factory Function is a normal JavaScript function that creates and returns an object. It is used to create multiple objects with similar properties and methods without using the `new` keyword.

## Example

```
function createUser(name, age) {
    return {
        name: name,
        age: age,
        greet() {
            console.log("Hello " + name);
        }
    };
}

const user1 = createUser("Rahul", 22);
const user2 = createUser("Aman", 25);

console.log(user1.name); // Rahul
console.log(user2.name); // Aman
```

## Advantages

1. Code Reusability: The same function can create multiple objects.
2. Less Code Duplication: No need to write the same object structure repeatedly.
3. Easy to Maintain: Objects can be created using a common structure.
4. No `new` Keyword: Objects can be created by simply calling the function.

## Factory Function vs Constructor Function

| Factory Function              | Constructor Function           |
| ----------------------------- | ------------------------------ |
| Uses a normal function call.  | Usually called with `new`.     |
| Returns an object explicitly. | Uses `this` to set properties. |
| Example: `createUser()`       | Example: `new User()`          |

Conclusion: Factory functions make object creation simple, reusable, and easy to manage in JavaScript.