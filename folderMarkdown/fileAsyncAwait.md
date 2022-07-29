# ASYNC / AWAIT

There’s a special syntax to work with promises in a more comfortable fashion, called “async/await” or "asynchronous functions". It’s surprisingly easy to understand and use.

Asynchronous functions are created by using the `async` keyword. It can be placed before a function, like this:

```javascript
const functionAsynchronous = async function() {
  return 1;
};
```

In practical terms, asynchronous functions have two distinguishing characteristics, which we will discuss in more detail:

* They always return a promise.
* They acept the await keyword.

For instance, the following function returns a resolved promise with the result of 1. Let's test it:

```javascript
const functionAsynchronous = async function () {
    return 1;
};

const promiseObject = functionAsynchronous();
console.log(promiseObject);
```

We could explicitly return a promise, which would be the same:

```javascript
const functionAsynchronous = function () {
    return new Promise((resolve)=>{
        resolve(1);
    });
};

const promiseObject = functionAsynchronous();
console.log(promiseObject);
```

So, async ensures that the function returns a promise, and wraps non-promises in it. Simple enough, right? But not only that. There’s also the `await` keyword, that works only inside async functions and  makes JavaScript wait until that promise settles and returns its result.

```javascript
const promiseObject = new Promise((resolve) => {
    setTimeout(() => resolve("DONE"), 3000);
});

const functionAsynchronous = async function () {
    const stringResult = await promiseObject; // WAIT UNTIL THE PROMISE RESOLVES (*).
    console.log(stringResult); // "DONE".
};

console.log("BEFORE");
functionAsynchronous();
console.log("AFTER");
```

The function execution “pauses” at the line (*) and resumes when the promise settles, with result becoming its result. Let’s emphasize: `await` literally suspends the function execution until the promise settles, and then resumes it with the promise result. Meanwhile, the JavaScript engine can do other jobs: execute other scripts, handle events, etc. It’s just a more elegant syntax of getting the promise result than promise `.then`. And, it’s easier to read and write.

It's worth noting that if we try to use the `await` keyword in a non-asyn function, there would be a syntax error. As stated earlier, **await only works inside an async function**.
