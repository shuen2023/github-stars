---
project: ratchet
stars: 14623
description: Build mobile apps with simple HTML, CSS, and JavaScript components. 
url: https://github.com/twbs/ratchet
---

Ratchet
=======

Build mobile apps with simple HTML, CSS, and JS components.

Table of contents
-----------------

-   Getting started
-   Documentation
-   Support
-   Contributing
-   Troubleshooting
-   Versioning
-   Maintainers
-   License

Getting started
---------------

-   Clone the repo with `git clone https://github.com/twbs/ratchet.git` or just download the bundled CSS and JS
-   Read the docs to learn about the components and how to get a prototype on your phone
-   Check out examples

Take note that our master branch is our active, unstable development branch and that if you're looking to download a stable copy of the repo, check the tagged downloads.

### What's included

Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations. You'll see something like this:

```
ratchet/
├── css/
│   ├── ratchet.css
│   ├── ratchet.min.css
│   ├── ratchet-theme-android.css
│   ├── ratchet-theme-android.min.css
│   ├── ratchet-theme-ios.css
│   └── ratchet-theme-ios.min.css
├── js/
│   ├── ratchet.js
│   └── ratchet.min.js
└── fonts/
    ├── ratchicons.eot
    ├── ratchicons.svg
    ├── ratchicons.ttf
    └── ratchicons.woff
```

We provide compiled CSS and JS (`ratchet.*`), as well as compiled and minified CSS and JS (`ratchet.min.*`). The Ratchicon fonts are included, as are the optional Android and iOS platform themes.

Documentation
-------------

Ratchet's documentation is built with Jekyll and publicly hosted on GitHub Pages at http://goratchet.com. The docs may also be run locally.

### Running documentation locally

1.  If necessary, install Jekyll (requires v3.0.x).

-   **Windows users:** Read this unofficial guide to get Jekyll up and running without problems.

1.  Install the Ruby-based syntax highlighter, Rouge, with `gem install rouge`.
2.  From the root `/ratchet` directory, run `jekyll serve` in the command line.
3.  Open http://localhost:4000 in your browser, and boom!

Learn more about using Jekyll by reading its documentation.

### Documentation for previous releases

Documentation for v1.0.2 has been made available for the time being at http://goratchet.com/1.0.2/ while folks transition to Ratchet 2.

Previous releases and their documentation are also available for download.

Support
-------

Questions or discussions about Ratchet should happen in the Google group or hit us up on Twitter @GoRatchet.

Contributing
------------

Please file a GitHub issue to report a bug. When reporting a bug, be sure to follow the contributor guidelines.

Troubleshooting
---------------

A small list of "gotchas" is provided below for designers and developers starting to work with Ratchet.

-   Ratchet is designed to respond to touch events from a mobile device. In order to use mouse click events (for desktop browsing and testing), you have a few options:
    -   Enable touch event emulation in Chrome (found in the overrides tab in the web inspector preferences)
    -   Use a JavaScript library like fingerblast.js to emulate touch events (ideally only loaded from desktop devices)
-   Script tags containing JavaScript will not be executed on pages that are loaded with push.js. If you would like to attach event handlers to elements on other pages, document-level event delegation is a common solution.
-   Ratchet uses XHR requests to fetch additional pages inside the application. Due to security concerns, modern browsers prevent XHR requests when opening files locally (aka using the `file://` protocol); consequently, Ratchet does not work when opened directly as a file.
    -   A common solution to this is to simply serve the files from a local server. One convenient way to achieve this is to run `python -m SimpleHTTPServer <port>` to serve up the files in the current directory to `http://localhost:<port>`

Versioning
----------

For transparency into our release cycle and in striving to maintain backward compatibility, Ratchet is maintained under the Semantic Versioning guidelines. Sometimes we screw up, but we'll adhere to these rules whenever possible.

Releases will be numbered with the following format:

`<major>.<minor>.<patch>`

And constructed with the following guidelines:

-   Breaking backward compatibility **bumps the major** while resetting minor and patch
-   New additions without breaking backward compatibility **bumps the minor** while resetting the patch
-   Bug fixes and misc changes **bumps only the patch**

For more information on SemVer, please visit http://semver.org/.

Maintainers
-----------

Connor Sears

-   https://twitter.com/connors
-   https://github.com/connors

Created by Connor Sears, Dave Gamache, and Jacob Thornton.

License
-------

Ratchet is licensed under the MIT License.
