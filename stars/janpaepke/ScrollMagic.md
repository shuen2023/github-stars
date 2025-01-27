---
project: ScrollMagic
stars: 14926
description: The javascript library for magical scroll interactions.
url: https://github.com/janpaepke/ScrollMagic
---

ScrollMagic v2.0.8
==================

### The javascript library for magical scroll interactions.

**Quicklinks:** About | Download | Installation | Usage | Help | Compatibility | Author | License | Thanks

* * *

### 🚨 **ScrollMagic 3.0 is on the horizon.** Helpers & Testers wanted! 🚨

* * *

ScrollMagic helps you to easily react to the user's current scroll position.  
It's the perfect library for you, if you want to ...

-   animate based on scroll position – either trigger an animation or synchronize it to the scrollbar movement (like a playback scrub control).
-   pin an element starting at a specific scroll position – either indefinitely or for a limited amount of scroll progress (sticky elements).
-   toggle CSS classes of elements on and off based on scroll position.
-   effortlessly add parallax effects to your website.
-   create an infinitely scrolling page (ajax load of additional content).
-   add callbacks at specific scroll positions or while scrolling past a specific section, passing a progress parameter.

Check out the demo page, browse the examples or read the documentation to get started.  
If you want to contribute please get in touch and let me know about your specialty and experience.

About the Library
-----------------

ScrollMagic is a scroll interaction library.

It's a complete rewrite of its predecessor Superscrollorama by John Polacek.  
A plugin-based architecture offers easy customizability and extendability.

To implement animations, ScrollMagic can work with multiple frameworks. The recommended solution is the Greensock Animation Platform (GSAP) due to its stability and feature richness. For a more lightweight approach, the VelocityJS framework is also supported. Alternatively, custom extensions can be implemented or the necessity of a framework can be completely avoided by animating simply using CSS and class toggles.

ScrollMagic was developed with these principles in mind:

-   optimized performance
-   lightweight (6KB gzipped)
-   flexibility and extendibility
-   mobile compatibility
-   event management
-   support for responsive web design
-   object-oriented programming and object chaining
-   readable, centralized code, and intuitive development
-   support for both x and y direction scrolling (even both on one page)
-   support for scrolling inside div containers (even multiple on one page)
-   extensive debugging and logging capabilities
-   detailed documentation
-   many application examples

**Is ScrollMagic the right library for you?**  
ScrollMagic takes an object-oriented approach using a controller for each scroll container and attaching multiple scenes defining what should happen at what part of the page. While this offers a great deal of control, it might be a little confusing, especially if you're just starting out with javascript.  
If the above points are not crucial for you and you are just looking for a simple solution to implement css animations I would strongly recommend taking a look at the awesome skrollr project. It almost solely relies on element attributes and thus requires minimal to no javascript knowledge.

Availability
------------

To get your copy of ScrollMagic you have the choice between four options:

**Option 1: GitHub**  
Download a zip file containing the source code, demo page, all examples and documentation from the GitHub releases page or clone the package to your machine using the git command line interface:

git clone https://github.com/janpaepke/ScrollMagic.git

**Option 2: Bower**  
ScrollMagic is also available on bower and will only install the necessary source code, ignoring all example and documentation files.  
Please mind that since they are not core dependencies, you will have to add frameworks like GSAP, jQuery or Velocity manually, should you choose to use them.

bower install scrollmagic

**Option 3: npm**  
If you prefer the node package manager, feel free to use it.  
Keep in mind that like with bower non-crucial files will be ignored (see above).

npm install scrollmagic

**Option 4: CDN**  
If you don't want to host ScrollMagic yourself, you can include it from cdnjs:

```
https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.8/ScrollMagic.min.js
```

All plugins and uncompressed files are also available on cdnjs.  
For example:

```
https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.8/plugins/debug.addIndicators.js
https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.8/plugins/debug.addIndicators.min.js
```

Installation
------------

Include the **core** library in your HTML file:

<script src\="js/scrollmagic/uncompressed/ScrollMagic.js"\></script\>

And you're ready to go!  
For deployment use the minified version **instead**:

<script src\="js/scrollmagic/minified/ScrollMagic.min.js"\></script\>

_**NOTE:** The logging feature is removed in the minified version due to file size considerations._

To use **plugins** like the indicators visualization, simply include them in addition to the main library:

<script src\="js/scrollmagic/uncompressed/plugins/debug.addIndicators.js"\></script\>

To learn how to configure **RequireJS**, when using AMD, please read here.

Usage
-----

The basic ScrollMagic design pattern is one controller, which has one or more scenes attached to it.  
Each scene is used to define what happens when the container is scrolled to a specific offset.

Here's a basic workflow example:

// init controller
var controller \= new ScrollMagic.Controller();

// create a scene
new ScrollMagic.Scene({
	duration: 100, // the scene should last for a scroll distance of 100px
	offset: 50, // start this scene after scrolling for 50px
})
	.setPin('#my-sticky-element') // pins the element for the the scene's duration
	.addTo(controller); // assign the scene to the controller

To learn more about the ScrollMagic code structure, please read here.

Help
----

To get started, check out the available learning resources in the wiki section.  
Be sure to have a look at the examples to get source code pointers and make use of the documentation for a complete reference.

If you run into trouble using ScrollMagic please follow the Troubleshooting guide.

**Please do not post support requests in the github issue section**, as it's reserved for issue and bug reporting. If all the above options for self-help fail, please use Stack Overflow or the ScrollMagic Premium Support.

Browser Support
---------------

ScrollMagic aims to support all major browsers even in older versions:  
Firefox 26+, Chrome 30+, Safari 5.1+, Opera 10+, IE 9+

About the Author
----------------

I am a creative coder based in Vienna, Austria.

Learn more on my website or Follow me on Twitter

License
-------

ScrollMagic is dual licensed under the MIT license and GPL.  
For more information click here.

Thanks
------

This library was made possible by many people who have supported it with passion, donations, or advice. Special thanks go out to John Polacek, Jack Doyle, Paul Irish, Nicholas Cerminara, Kai Dorschner, Petr Tichy and Dennis Gaebel.
