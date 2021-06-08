# Axios-Patterns

A reference guide modelling the core patterns used when utilising async/await, try/catch blocks with specific error handling provisions when using Axios.

The Axios patterns below are part of larger CRUD patterns when working with VueX.

ToC:

- **[Overview](#Overview)**
- **[Error Handling Pattern](#Error-Handling-Pattern)**
- **[GET Request Pattern](#GET-Request-Pattern)**

## Overview

Axios is installed via: `npm install axios` and imported with: `import axios from 'axios';`.
Axios can be used with the following patterns:

```js
axios({ config }); // When the 'method' and 'data' is defined within the config object

axios("url"); // When making a GET request

axios.request({ config });

axios.get("url", { config });

axios.delete("url", { config });

axios.head("url", { config });

axios.options("url", { config });

axios.post("url", { data }, { config });

axios.put("url", { data }, { config });

axios.patch("url", { data }, { config });
```

> There are many **request** config options that can be used, some of the more commonly used ones below:

```js
url: `/url`; // Can be used either absolutely or prefixed with the below baseURL

baseURL: `prepended to the above url`; // PUT, POST, PATCH, DELETE

headers: {
} // Used to send custom headers including Authorization headers

params: {
} // URL parameters sent with request, either a plain object or URLSearchParams object

data: {
} // The data to be sent as the request body

withCredentials: false // for cross-site Access-Control requests

auth: { // HTTP Basic auth to be used and sets the Authorization header
    username: 'janedoe',
    password: 's00pers3cret'
}


```

> The **response** back includes the following options:

```js
response.data; // An object

response.status; // HTTP status code

response.statusText; // HTTP status message ex. 'OK'

response.headers; // An object with the headers

response.headers["content-type"]; // example to access header value

response.config;

response.request;
```

## Error Handling Pattern

Straight out of the box Axios catches all errors and provides specific error details which simplifies error handling.

The below pattern shows some of the data types that could be used to gather information about an issue:

```js
catch (error) {
    console.log(error.message);
    if (error.request) {
        // Code to run...
        console.log(error.request);
    } else if (error.response) {
        // Code to run...
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.statusText);
        console.log(error.response.headers);
        console.log(error.toJSON);
    } else {
        // Code to run...
        console.log(error.toJSON);
    }
    ctx.commit("setError", "Sorry, unable to fetch todo list at this time");
    ctx.commit("setIsLoading", false);
}

```

# GET Request Pattern

```js
async fetchTodo(ctx) {
    ctx.commit("setIsLoading", true);
    ctx.commit("setError", "");
    try {
    const res = await axios.get(
        "URL"
    );
    ctx.commit("setTodosData", res.data);
    ctx.commit("setIsLoading", false);
    } catch (error) {
        console.log(error.message);
        if (error.request) {
            // Code to run...
            console.log(error.request);
        } else if (error.response) {
        // Code to run...
            console.log(error.response.data);
            console.log(error.response.status);
            console.log(error.response.statusText);
            console.log(error.response.headers);
            console.log(error.toJSON);
        } else {
            // Code to run...
            console.log(error.toJSON);
        }
    ctx.commit("setError", "Sorry, unable to fetch todo list at this time");
    ctx.commit("setIsLoading", false);
    }
},

```

# POST Request Pattern

```js
async addTodo(ctx, newTodo) {
    try {
    await axios.post(
        "URL",
        newTodo
    );
    const res = await axios(
        "URL/" + newTodo.id
    );
    const newArr = [...ctx.state.todos, res.data];
    ctx.commit("setTodosData", newArr);
    } catch (error) {
    console.log(error.message);
    if (error.request) {
        // Code to run...
        console.log(error.request);
    } else if (error.response) {
        // Code to run...
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.statusText);
        console.log(error.response.headers);
        console.log(error.toJSON);
    } else {
        // Code to run...
        console.log(error.toJSON);
    }
    }
},

```

# DELETE Request Pattern

```js
async deleteTodo(ctx, todo) {
    try {
    await axios.delete(
        "https://dev-test-api-one.herokuapp.com/todos/" + todo.id
    );

    const newArr = ctx.state.todos.filter((task) => task.id != todo.id);
    ctx.commit("setTodosData", newArr);
    } catch (error) {
    console.log(error.message);
    if (error.request) {
        // Code to run...
        console.log(error.request);
    } else if (error.response) {
        // Code to run...
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.statusText);
        console.log(error.response.headers);
        console.log(error.toJSON);
    } else {
        // Code to run...
        console.log(error.toJSON);
    }
    }
},

```

# PUT/PATCH Request Pattern

```js
async updateTodoText(ctx, todo) {
    try {
    await axios.patch(
        "URL/" + todo.id,
        {
        update: !todo.update,
        text: todo.text,
        complete: false,
        }
    );
    ctx.dispatch("fetchSingleTodo", todo);
    } catch (error) {
        console.log(error.message);
        if (error.request) {
          // Code to run...
          console.log(error.request);
        } else if (error.response) {
          // Code to run...
          console.log(error.response.data);
          console.log(error.response.status);
          console.log(error.response.statusText);
          console.log(error.response.headers);
          console.log(error.toJSON);
        } else {
          // Code to run...
          console.log(error.toJSON);
        }
      }
},

```
