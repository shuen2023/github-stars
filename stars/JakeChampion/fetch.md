---
project: fetch
stars: 25761
description: A window.fetch JavaScript polyfill.
url: https://github.com/JakeChampion/fetch
---

window.fetch polyfill
=====================

The `fetch()` function is a Promise-based mechanism for programmatically making web requests in the browser. This project is a polyfill that implements a subset of the standard Fetch specification, enough to make `fetch` a viable replacement for most uses of XMLHttpRequest in traditional web applications.

Table of Contents
-----------------

-   Read this first
-   Installation
-   Usage
    -   Importing
    -   HTML
    -   JSON
    -   Response metadata
    -   Post form
    -   Post JSON
    -   File upload
    -   Caveats
        -   Handling HTTP error statuses
        -   Sending cookies
        -   Receiving cookies
        -   Redirect modes
        -   Obtaining the Response URL
        -   Aborting requests
-   Browser Support

Read this first
---------------

-   If you believe you found a bug with how `fetch` behaves in your browser, please **don't open an issue in this repository** unless you are testing in an old version of a browser that doesn't support `window.fetch` natively. Make sure you read this _entire_ readme, especially the Caveats section, as there's probably a known work-around for an issue you've found. This project is a _polyfill_, and since all modern browsers now implement the `fetch` function natively, **no code from this project** actually takes any effect there. See Browser support for detailed information.
    
-   If you have trouble **making a request to another domain** (a different subdomain or port number also constitutes another domain), please familiarize yourself with all the intricacies and limitations of CORS requests. Because CORS requires participation of the server by implementing specific HTTP response headers, it is often nontrivial to set up or debug. CORS is exclusively handled by the browser's internal mechanisms which this polyfill cannot influence.
    
-   This project **doesn't work under Node.js environments**. It's meant for web browsers only. You should ensure that your application doesn't try to package and run this on the server.
    
-   If you have an idea for a new feature of `fetch`, **submit your feature requests** to the specification's repository. We only add features and APIs that are part of the Fetch specification.
    

Installation
------------

```
npm install whatwg-fetch --save
```

You will also need a Promise polyfill for older browsers. We recommend taylorhakes/promise-polyfill for its small size and Promises/A+ compatibility.

Usage
-----

### Importing

Importing will automatically polyfill `window.fetch` and related APIs:

import 'whatwg-fetch'

window.fetch(...)

If for some reason you need to access the polyfill implementation, it is available via exports:

import {fetch as fetchPolyfill} from 'whatwg-fetch'

window.fetch(...)   // use native browser version
fetchPolyfill(...)  // use polyfill implementation

This approach can be used to, for example, use abort functionality in browsers that implement a native but outdated version of fetch that doesn't support aborting.

For use with webpack, add this package in the `entry` configuration option before your application entry point:

entry: \['whatwg-fetch', ...\]

### HTML

fetch('/users.html')
  .then(function(response) {
    return response.text()
  }).then(function(body) {
    document.body.innerHTML \= body
  })

### JSON

fetch('/users.json')
  .then(function(response) {
    return response.json()
  }).then(function(json) {
    console.log('parsed json', json)
  }).catch(function(ex) {
    console.log('parsing failed', ex)
  })

### Response metadata

fetch('/users.json').then(function(response) {
  console.log(response.headers.get('Content-Type'))
  console.log(response.headers.get('Date'))
  console.log(response.status)
  console.log(response.statusText)
})

### Post form

var form \= document.querySelector('form')

fetch('/users', {
  method: 'POST',
  body: new FormData(form)
})

### Post JSON

fetch('/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'Hubot',
    login: 'hubot',
  })
})

### File upload

var input \= document.querySelector('input\[type="file"\]')

var data \= new FormData()
data.append('file', input.files\[0\])
data.append('user', 'hubot')

fetch('/avatars', {
  method: 'POST',
  body: data
})

### Caveats

-   The Promise returned from `fetch()` **won't reject on HTTP error status** even if the response is an HTTP 404 or 500. Instead, it will resolve normally, and it will only reject on network failure or if anything prevented the request from completing.
    
-   For maximum browser compatibility when it comes to sending & receiving cookies, always supply the `credentials: 'same-origin'` option instead of relying on the default. See Sending cookies.
    
-   Not all Fetch standard options are supported in this polyfill. For instance, `redirect` and `cache` directives are ignored.
    
-   `keepalive` is not supported because it would involve making a synchronous XHR, which is something this project is not willing to do. See issue #700 for more information.
    

#### Handling HTTP error statuses

To have `fetch` Promise reject on HTTP error statuses, i.e. on any non-2xx status, define a custom response handler:

function checkStatus(response) {
  if (response.status \>= 200 && response.status < 300) {
    return response
  } else {
    var error \= new Error(response.statusText)
    error.response \= response
    throw error
  }
}

function parseJSON(response) {
  return response.json()
}

fetch('/users')
  .then(checkStatus)
  .then(parseJSON)
  .then(function(data) {
    console.log('request succeeded with JSON response', data)
  }).catch(function(error) {
    console.log('request failed', error)
  })

#### Sending cookies

For CORS requests, use `credentials: 'include'` to allow sending credentials to other domains:

fetch('https://example.com:1234/users', {
  credentials: 'include'
})

The default value for `credentials` is "same-origin".

The default for `credentials` wasn't always the same, though. The following versions of browsers implemented an older version of the fetch specification where the default was "omit":

-   Firefox 39-60
-   Chrome 42-67
-   Safari 10.1-11.1.2

If you target these browsers, it's advisable to always specify `credentials: 'same-origin'` explicitly with all fetch requests instead of relying on the default:

fetch('/users', {
  credentials: 'same-origin'
})

Note: due to limitations of XMLHttpRequest, using `credentials: 'omit'` is not respected for same domains in browsers where this polyfill is active. Cookies will always be sent to same domains in older browsers.

#### Receiving cookies

As with XMLHttpRequest, the `Set-Cookie` response header returned from the server is a forbidden header name and therefore can't be programmatically read with `response.headers.get()`. Instead, it's the browser's responsibility to handle new cookies being set (if applicable to the current URL). Unless they are HTTP-only, new cookies will be available through `document.cookie`.

#### Redirect modes

The Fetch specification defines these values for the `redirect` option: "follow" (the default), "error", and "manual".

Due to limitations of XMLHttpRequest, only the "follow" mode is available in browsers where this polyfill is active.

#### Obtaining the Response URL

Due to limitations of XMLHttpRequest, the `response.url` value might not be reliable after HTTP redirects on older browsers.

The solution is to configure the server to set the response HTTP header `X-Request-URL` to the current URL after any redirect that might have happened. It should be safe to set it unconditionally.

\# Ruby on Rails controller example
response.headers\['X-Request-URL'\] \= request.url

This server workaround is necessary if you need reliable `response.url` in Firefox < 32, Chrome < 37, Safari, or IE.

#### Aborting requests

This polyfill supports the abortable fetch API. However, aborting a fetch requires use of two additional DOM APIs: AbortController and AbortSignal. Typically, browsers that do not support fetch will also not support AbortController or AbortSignal. Consequently, you will need to include an additional polyfill for these APIs to abort fetches:

import 'yet-another-abortcontroller-polyfill'
import {fetch} from 'whatwg-fetch'

// use native browser implementation if it supports aborting
const abortableFetch \= ('signal' in new Request('')) ? window.fetch : fetch

const controller \= new AbortController()

abortableFetch('/avatars', {
  signal: controller.signal
}).catch(function(ex) {
  if (ex.name \=== 'AbortError') {
    console.log('request aborted')
  }
})

// some time later...
controller.abort()

Browser Support
---------------

-   Chrome
-   Firefox
-   Safari 6.1+
-   Internet Explorer 10+

Note: modern browsers such as Chrome, Firefox, Microsoft Edge, and Safari contain native implementations of `window.fetch`, therefore the code from this polyfill doesn't have any effect on those browsers. If you believe you've encountered an error with how `window.fetch` is implemented in any of these browsers, you should file an issue with that browser vendor instead of this project.
