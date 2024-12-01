---
project: gitalk
stars: 7031
description: Gitalk is a modern comment component based on Github Issue and Preact.
---

Gitalk
======

Gitalk is a modern comment component based on GitHub Issue and Preact.

Features
--------

-   Authentication with github account
-   Serverless, all comments will be stored as github issues
-   Both personal and organization github projects can be used to store comments
-   Localization, support multiple languages \[en, zh-CN, zh-TW, es-ES, fr, ru, de, pl, ko, fa, ja\]
-   Facebook-like distraction free mode (Can be enabled via the `distractionFreeMode` option)
-   Hotkey submit comment (cmd|ctrl + enter)

中文说明 Demo

Install
-------

Two ways.

-   links

  <link rel\="stylesheet" href\="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css"\>
  <script src\="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"\></script\>

  <!-- or -->

  <link rel\="stylesheet" href\="https://unpkg.com/gitalk/dist/gitalk.css"\>
  <script src\="https://unpkg.com/gitalk/dist/gitalk.min.js"\></script\>

-   npm install

npm i --save gitalk

import 'gitalk/dist/gitalk.css'
import Gitalk from 'gitalk'

Usage
-----

Firstly, you need choose a public github repository (existed or create a new one) for store comments,

Then create A **GitHub Application** if you don't have one, Click here to register a new one. **Note:** You must specify the website domain url in the `Authorization callback URL` field.

Lastly, you can choose how to apply to the page as below:

### Method One

Add a container to your page:

<div id\="gitalk-container"\></div\>

Then use the Javascript code below to generate the gitalk plugin:

const gitalk \= new Gitalk({
  clientID: 'GitHub Application Client ID',
  clientSecret: 'GitHub Application Client Secret',
  repo: 'GitHub repo',      // The repository of store comments,
  owner: 'GitHub repo owner',
  admin: \['GitHub repo owner and collaborators, only these guys can initialize github issues'\],
  id: location.pathname,      // Ensure uniqueness and length less than 50
  distractionFreeMode: false  // Facebook-like distraction free mode
})

gitalk.render('gitalk-container')

### Method Two: Use in React

Import the Gitalk with

import GitalkComponent from "gitalk/dist/gitalk-component";

And use the component like

<GitalkComponent options\={{
  clientID: "...",
  // ...
  // options below
}} /\>

Options
-------

-   **clientID** `String`
    
    **Required**. GitHub Application Client ID.
    
-   **clientSecret** `String`
    
    **Required**. GitHub Application Client Secret.
    
-   **repo** `String`
    
    **Required**. GitHub repository.
    
-   **owner** `String`
    
    **Required**. GitHub repository owner. Can be personal user or organization.
    
-   **admin** `Array`
    
    **Required**. GitHub repository owner and collaborators. (Users who having write access to this repository)
    
-   **id** `String`
    
    Default: `location.href`.
    
    The unique id of the page. Length must less than 50.
    
    Note: You can use regex to extract certain path of the URL as the id. E.g., `location.href.match('/(?<=posts/)(.*)(?=/)/')[1]`
    
-   **number** `Number`
    
    Default: `-1`.
    
    The issue ID of the page, if the `number` attribute is not defined, issue will be located using `id`.
    
-   **labels** `Array`
    
    Default: `['Gitalk']`.
    
    GitHub issue labels.
    
-   **title** `String`
    
    Default: `document.title`.
    
    GitHub issue title.
    
-   **body** `String`
    
    Default: `location.href + header.meta[description]`.
    
    GitHub issue body.
    
-   **language** `String`
    
    Default: `navigator.language || navigator.userLanguage`.
    
    Localization language key, support \[`en`, `zh-CN`, `zh-TW`, `es-ES`, `fr`, `ru`, `de`, `pl`, `ko`, `fa`, `ja`\].
    
-   **perPage** `Number`
    
    Default: `10`.
    
    Pagination size, with maximum 100.
    
-   **distractionFreeMode** `Boolean`
    
    Default: false.
    
    Facebook-like distraction free mode.
    
-   **pagerDirection** `String`
    
    Default: 'last'
    
    Comment sorting direction, available values are `last` and `first`.
    
-   **createIssueManually** `Boolean`
    
    Default: `false`.
    
    By default, Gitalk will create a corresponding github issue for your every single page automatically when the logined user is belong to the `admin` users. You can create it manually by setting this option to `true`.
    
-   **proxy** `String`
    
    Default: `https://cors-anywhere.azm.workers.dev/https://github.com/login/oauth/access_token`.
    
    GitHub oauth request reverse proxy for CORS. Why need this?
    
-   **flipMoveOptions** `Object`
    
    Default:
    
      {
        staggerDelayBy: 150,
        appearAnimation: 'accordionVertical',
        enterAnimation: 'accordionVertical',
        leaveAnimation: 'accordionVertical',
      }
    
    Comment list animation. Reference
    
-   **enableHotKey** `Boolean`
    
    Default: `true`.
    
    Enable hot key (cmd|ctrl + enter) submit comment.
    

Instance Methods
----------------

-   **render(String/HTMLElement)**
    
    Init render and mount plugin.
    

TypeScript
----------

TypeScript definitions for options and Gitalk class come with the package and should be automatically detected.

Definitions for React component usage are not included.

Contributing
------------

1.  Fork the repository and create your branch from master
2.  If you've added code that should be tested, add tests!
3.  If you've changed APIs, update the documentation.
4.  Ensure the test suite passes (npm test).
5.  Make sure your code lints (npm run lint).
6.  Commit your changes (git commit) Commit Message Format Reference

Similar Projects
----------------

-   gitment
-   vssue

LICENSE
-------

MIT