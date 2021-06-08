# Axios-Patterns

A quick reference guide modelling the core patterns used when utilising async/await, try/catch blocks with specific error handling provisions.

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

There are many **request** config options that can be used, some of the more commonly used ones below:

```js
url: `/url`; // Can be used either absolutely or prefixed with the below baseURL

baseURL: `prepended to the above url`; // PUT, POST, PATCH, DELETE

headers: {
} // Used to send custom headers

params: {
} // URL parameters sent with request, either a plain object or URLSearchParams object

data: {
} //
```
