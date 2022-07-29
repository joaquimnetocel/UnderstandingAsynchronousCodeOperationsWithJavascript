# FETCH

## NETWORK REQUESTS

JavaScript can send network requests to the server and load new information whenever it’s needed. Furthermore, this can be done without reloading the page! For example, we can use a network request to:

* Submit an order,
* Load user information,
* Receive latest updates from the server,

There’s an umbrella term “AJAX” (abbreviated Asynchronous JavaScript And XML) for network requests from JavaScript. We don’t have to use XML though: the term comes from old times, that’s why that word is there. You may have heard that term already.

## THE FETCH METHOD

There are multiple ways to send a network request and get information from the server. Here we will se a modern and versatile one: the `fetch`. The basic usage is:

```javascript
const promiseFetch = fetch(stringUrl, objectOptions);
```

Where:

* `stringUrl` is a URL string to access.
* `objectOptions` is an optional object with parameters: method, headers, etc.
* `promiseFetch` is a promise that the calling code should use to get the result.

Without the optional argument, this is a simple GET request, downloading the contents of the URL.

Here is an example that gets data from the [SUPE HERO API](./https://akabab.github.io/superhero-api/api/):

```javascript
const promiseFetch = fetch("https://cdn.jsdelivr.net/gh/akabab/superhero-api@0.3.0/api/id/1.json");
console.log(promiseFetch);
```

## GETTING THE FETCH RESPONSE

Let’s see below how to get the fetch response with the Promise syntax. Here, we are going to focus on JSON responses (other types of answers will not be exemplified, only mentioned).

```javascript
const promiseFetch = fetch("https://cdn.jsdelivr.net/gh/akabab/superhero-api@0.3.0/api/id/1.json");

const functionFirstHandle = function(argResponse){
    console.log(argResponse.status); // HTTP STATUS CODE.
    console.log(argResponse.ok); // BOOLEAN: true IF THE HTTP STATUS CODE IS BETWEEN 200 AND 299.
    if (argResponse.ok) {
        return argResponse.json(); // NEW PROMISE TO GET THE RESPONSE BODY IN JSON FORMAT.
    } else {
        alert("HTTP-Error: " + response.status);
    }
};

const functionSecondHandle = function(argResponse){
    console.log(argResponse);
};

promiseFetch.then(functionFirstHandle).then(functionSecondHandle);
```

We can also get the same result with the surprisingly easy async/await:

```javascript
const functionAsynchronous = async function () {
    const responseResult = await fetch("https://cdn.jsdelivr.net/gh/akabab/superhero-api@0.3.0/api/id/1.json");
    const jsonResult = await responseResult.json();
    console.log(jsonResult);
};

functionAsynchronous();
```

As wee can see, getting a response is usually a two-stage process.

First, the promise, returned by `fetch`, resolves with an object of the built-in _Response class_ as soon as the server responds with headers. At this stage we can check HTTP status, to see whether it is successful or not, check headers, but don’t have the body yet. The promise rejects if the fetch was unable to make HTTP-request, e.g. network problems, or there’s no such site. Abnormal HTTP-statuses, such as 404 or 500 do not cause an error. We can see HTTP-status in response properties:

* `status`: HTTP status code, e.g. 200.
* `ok`: boolean, true if the HTTP status code is 200-299.

Second, to get the response body, we need to use an additional method call.

Response provides multiple promise-based methods to access the body in various formats:

* `response.text()`: read the response and return as text.
* `response.json()` – parse the response as JSON.
* `response.formData()` – return the response as FormData object (explained in the next chapter).
* `response.blob()` – return the response as Blob (binary data with type).
* `response.arrayBuffer()` – return the response as ArrayBuffer (low-level representation of binary data).

[BACK](../README.md)
