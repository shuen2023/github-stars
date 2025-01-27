---
project: napajs
stars: 9240
description: Napa.js: a multi-threaded JavaScript runtime
url: https://github.com/microsoft/napajs
---

Napa.js
=======

Napa.js is a multi-threaded JavaScript runtime built on V8, which was originally designed to develop highly iterative services with non-compromised performance in Bing. As it evolves, we find it useful to complement Node.js in CPU-bound tasks, with the capability of executing JavaScript in multiple V8 isolates and communicating between them. Napa.js is exposed as a Node.js module, while it can also be embedded in a host process without Node.js dependency.

Installation
------------

Install the latest stable version:

```
npm install napajs
```

Other options can be found in Build Napa.js.

Quick Start
-----------

const napa \= require('napajs');
const zone1 \= napa.zone.create('zone1', { workers: 4 });

// Broadcast code to all 4 workers in 'zone1'.
zone1.broadcast('console.log("hello world");');

// Execute an anonymous function in any worker thread in 'zone1'.
zone1.execute(
    (text) \=> text, 
    \['hello napa'\])
    .then((result) \=> {
        console.log(result.value);
    });

More examples:

-   Estimate PI in parallel
-   Max sub-matrix of 1s with layered parallelism
-   Parallel Quick Sort
-   Recursive Fibonacci with multiple JavaScript threads
-   Synchronized loading

Features
--------

-   Multi-threaded JavaScript runtime.
-   Node.js compatible module architecture with NPM support.
-   API for object transportation, object sharing and synchronization across JavaScript threads.
-   API for pluggable logging, metric and memory allocator.
-   Distributed as a Node.js module, as well as supporting embed scenarios.

Documentation
-------------

-   Napa.js Home
-   API Reference
-   FAQ

Contribute
==========

You can contribute to Napa.js in following ways:

-   Report issues and help us verify fixes as they are checked in.
-   Review the source code changes.
-   Contribute to core module compatibility with Node.
-   Contribute bug fixes.

This project has adopted the Microsoft Open Source Code of Conduct.  
For more information see the Code of Conduct FAQ or contact opencode@microsoft.com with any additional questions or comments.

License
=======

Copyright (c) Microsoft Corporation. All rights reserved.

Licensed under the MIT License.
