---
layout: post
title:      "Javascript Fetch & Promises"
date:       2019-01-10 22:55:18 +0000
permalink:  javascript_fetch_and_promises
---

JavaScript's native Fetch API is used to send data requests over the web. In its simplest use, `fetch()` requests data from an external source, such as with `fetch('http://www.petsapi.com')`.

To see fetch in action, let's create simple action and reducer functions to go along with the fetch request:

```
// ./src/actions/fetchPets.js 

export function fetchPets() {
  const pets = fetch('http://www.petsapi.com');
  return {
    type: 'FETCH_PETS',
    pets
  };
};
 
 
// ./src/reducers/petsReducer.js

function petsReducer(state = [], action) {
  switch (action.type) {
    case 'FETCH_PETS':
      return action.pets
 
    default:
      return state;
  }
};
```

In the `fetchPets` function, a fetch request is made to the API, returning an object of all the pets from the server. These requests are **asynchronous**, meaning that each process runs independently of other concurrent processes within the same function. As a result, the second line of code will run before the data response is received from the request! 

To counter this asynchronicity, a `fetch()` request returns a  **promise**. A **promise** is an object that represents a value that can be used at a later time. When the promise is successful, or resolved, the data becomes available with the chaining of a `then()` function onto the `fetch()` call. This promise is called within `fetchPets()` like so:

```
export function fetchPets() {
  const pets = fetch('http://www.petsapi.com')
	           .then(response => response.json())
  return {
    type: 'FETCH_PETS',
    pets
  };
}
```

## Scope Example

Another way to see how promises work is to look at the scope within a `fetch()` request.

```
//Example.js:

handleFetch = () => {
 console.log('A')
 
 fetch(http://localhost:3000/api/example`)
  .then(response => {
    console.log('B')
    return response.json()
  })
  .then(example => console.log('C', example)
 
 console.log('D')
}

//Printed to console
A, D, B, C
```

Looking at the code above, `handleFetch()` calls a fetch request to an API and returns a couple promise functions when the fetch is resolved. Within the code, we are logging strings to the console to see the order of each returned response.

'A' is returned first, as it is the first line of code within the function, as well as independent of any other code. Similarily, 'D' is the second returned string, as it is the only other line of code not within the fetch function, which does not depend on the returned value of the fetch request. Now, within the fetch call, once the promises are resolved, the strings are printed out top to bottom. Therefore, as 'B' is within the first `then()` function, it is called third, and finally 'C' is the final string printed to the console.  

Understanding the fetch function and the implementation of promises within are important concepts for requesting and receiving data from an external source, as well as manipulating it for application use.

