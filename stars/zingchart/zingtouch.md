---
project: zingtouch
stars: 2128
description: A JavaScript touch gesture detection library for the modern web
url: https://github.com/zingchart/zingtouch
---

ZingTouch
=========

https://zingchart.github.io/zingtouch

A modern JavaScript touch gesture library. The library allows developers to configure pre-existing gestures as well as create their own using ZingTouch's life cycle.

### Quick Links

-   Demos
-   Codebase Documentation
-   CDN

### Table of Contents

-   Overview
-   Getting Started
-   Usage
-   Browser Compatibility
-   Pitfalls
-   Contributing
-   License

Overview
========

ZingTouch is built to make implementing gestures for the browser as easy or complex as you need it to be. ZingTouch comes with 6 main gestures :

-   Tap
-   Swipe
-   Distance
-   Pan
-   Rotate

These gestures can be customized including the number of inputs it accepts, or how sensitive the gesture is to be recognized.

ZingTouch is also has lifecycle events that you can hook into to create new Gestures or to act upon certain touch events. We know supporting touch events across multiple browsers can be a pain; ZingTouch makes it easy by defining 3 hooks to pass callbacks to :

-   start
-   move
-   end

Getting Started
===============

### Include the library

_**Node / CommonJS**_

var ZingTouch \= require('zingtouch');

or

_**Include the file**_

<script src\='./path/to/zingtouch.min.js'\></script\>

or

_**ES6**_

import ZingTouch from 'zingtouch';

### Create a Region

var zt \= new ZingTouch.Region(document.body);

### Bind an element to a gesture

var myElement \= document.getElementById('my-div');

zt.bind(myElement, 'tap', function(e){
	//Actions here
}, false);

Usage
=====

Table of Contents
-----------------

**Constructs**

-   Region

**Gestures**

-   Tap
-   Pan
-   Swipe
-   Distance
-   Rotate
-   Gesture

**Methods**

-   Region.bind
-   Region.bindOnce
-   Region.unbind
-   Region.register
-   Region.unregister

Constructs
----------

### Region

new Region(element, \[capture\], \[preventDefault\])

-   element - The element to set the listener upon
-   capture - Whether the region listens for captures or bubbles.
-   preventDefault - Disables browser functionality such as scrolling and zooming over the region.

Regions specify an area to listen for all window events. ZingTouch needs to listen to all window events in order to determine if a gesture is recognized. Note that you can reuse regions for multiple elements and gesture bindings. They simply specify an area where to listen for gestures.

Suppose you had an element that you wanted to track gestures on. We set the region on that element along with binding it to a gesture.

var touchArea \= document.getElementById('toucharea');
var myRegion \= new ZingTouch.Region(touchArea);

myRegion.bind(touchArea, 'swipe', function(e){
	console.log(e.detail);
});

The shaded area in blue shows the area where ZingTouch will now listen for events such as touchstart, touchmove, touchend, etc.

But humans aren't perfect. Suppose the element #toucharea were to listen for the `Swipe` gesture. The tracking of the window events will stop when the user reaches the edges of #toucharea. But what if the user didn't finish until say 10-50px _**outside**_ the element? Regions are here to help.

Suppose you set the Region to the parent of the #toucharea element instead.

var parentTouchArea \= document.getElementById('parent-toucharea')
var touchArea \= document.getElementById('toucharea')
var myRegion \= new ZingTouch.Region(parentTouchArea);

myRegion.bind(touchArea, 'swipe', function(e){
	console.log(e.detail);
});

ZingTouch now tracks the swipe gesture inside the `#toucharea` element AND the #parent-toucharea. This allows some forgiveness when the user tries to swipe on the `#toucharea`, but lifts their finger somewhere in the `#parent-toucharea`.

**Note:** The swipe gesture can only be initiated on the area it is bound to. This means the user has to being touching the `#toucharea` element first, but can move out and end within `#parent-toucharea` and including `#toucharea`.

### Multiple Regions

Regions only are aware of themselves and their contents, not across regions. This allows for control at a larger scale so you can group similar gestures together. While you can throw a Region on top of the `document.body`, we suggest splitting up your application into regions for better performance -- the less bindings a single region has to iterate through to detect a gesture, the better.

Gestures
--------

Gesture classes can be instatiated to generate modified versions.

### Tap

A tap is detected when the user touches the screen and releases in quick succession.

#### Options

-   `options.maxDelay` _optional_ - The maximum delay between a start and end event. This number is measured in milliseconds.
    -   default: 300
-   `options.numInputs` _optional_ - The number of inputs to trigger the tap event.
    -   default: 1
-   `options.tolerance` _optional_ - A tolerance value which allows the user to move their finger about a radius measured in pixels. This allows the Tap gesture to be triggered more easily since a User might move their finger slightly during a tap event.
    -   default: 10

#### Example

new ZingTouch.Tap({
	maxDelay: 200,
	numInputs: 2,
	tolerance: 125
})

#### Emits

-   `interval` - a time measured in milliseconds between the start of the gesture, and the end.

* * *

### Swipe

A swipe is detected when the user touches the screen and moves in a relatively increasing velocity, leaving the screen at some point before it drops below a certain velocity.

#### Options

-   `options.numInputs` _optional_ - The number of inputs to trigger the event.
    -   Default: 1
-   `options.escapeVelocity` _optional_ - The minimum velocity (px/ms) that the gesture has to obtain by the end event.
    -   Default: 0.2
-   `options.maxRestTime` _optional_ - The amount of time allowed in milliseconds inbetween events before a the motion becomes inelligible to be a swipe.
    -   Default: 100

#### Example

new ZingTouch.Swipe({
	numInputs: 2,
	maxRestTime: 100,
	escapeVelocity: 0.25
});

#### Emits

An array of data objects containing:

-   `velocity` - The value in units of pixels per millisecond the gesture was travelling until it's ending point.
-   `currentDirection` - The angle the swipe ended at in degrees, relative to the unit circle. (e.g. straight down is 270deg while straight left is 180deg).

Each index represents an input that participated in the event.

* * *

### Distance

A distance gesture is detected when the user has two inputs on the screen moving either closer or away from the other input.

#### Example

new ZingTouch.Distance()

#### Emits

-   `distance` - The distance in pixels between the two inputs.
-   `center` - The X/Y coordinates of the gesture's center
-   `change` - The amount of pixels changed from the last emitted event. Positive implies an "expand" gesture while a negative value implies a "pinch".

### Pan

A pan is detected when the user touches the screen and moves about the area.

#### Options

-   `options.numInputs` _optional_ - The number of inputs to trigger the event.
    -   Default: 1
-   `options.threshold` _optional_ - The minimum number of pixels the input has to move to trigget this gesture.
    -   Default: 1

#### Example

new ZingTouch.Pan({
	numInputs: 2
})

#### Emits

An array of data objects containing:

-   `distanceFromOrigin` - The distance in pixels traveled from the current position from the starting position.
-   `directionFromOrigin` - The angle of the pan in degrees, relative to the unit circle.(e.g. straight down is 270deg while straight left is 180deg). The starting point of where the input began during the "start" event denotes the origin point.
-   `currentDirection` - The angle of the pan gesture in degrees, relative to the unit circle. The previously emitted point is used as an origin point.

Each index represents an input that participated in the event.

* * *

### Rotate

A Rotate is detected when:

-   the user has two inputs moving about a circle on the edges of a diameter.
-   the user has one input moving in a circular motion around the center point of the bound target element.

#### Example

new ZingTouch.Rotate()

#### Emits

-   `angle` - The angle of the initial right most input, in relation to the unit circle.
-   `distanceFromOrigin` - The angular distance travelled by the initial right most input.
-   `distanceFromLast` - The change of angle between the last position and the current position. Positive denotes a counter-clockwise motion, while negative denotes a clockwise motion.

* * *

### Gesture

A generic gesture. By default, this gesture does not emit but is useful for hooking into ZingTouch's life cycle. See ZingTouch Life Cycle for more information.

#### Example

new ZingTouch.Gesture()

Methods
-------

### Region.bind(element, gesture, handler, \[capture\])

Binds a single element to a gesture, executing the handler when the gesture is emitted.

**Parameters**

-   element - A DOM element
-   gesture - Either the key (string) of a default or registered gesture, or an instance of the `Gesture` class itself.
-   handler - A function to be called every time the gesture is emitted.
    -   The handler function has an Event object emitted from the CustomEvent interface. Any information relavant to the gesture will be in `event.detail`.
-   `capture` - An optional boolean to designate the event to be fired on the capture or bubbling phase.

**Example #1**

var myRegion \= new ZingTouch.Region(document.body);
var myElement \= document.getElementById('some-div');

myRegion.bind(myElement, 'tap', function(e) {
	console.log('Tap gesture emitted: ' + e.detail.interval);
});

**Example #2**

var myElement \= document.getElementById('some-div');
var myTapGesture \= new ZingTouch.Tap({ maxDelay : 100 });
var myRegion \= new ZingTouch.Region(document.body);

myRegion.bind(myElement, myTapGesture, function(e) {
	console.log('Custom Tap gesture emitted: ' + e.detail.interval);
}, false);

**Notes**

1.  Instance Gestures that are passed to bind will be stored and maintained in memory, therefore it is reccomended to reuse gestures object where possible, or to use the `Region.register` syntax -- they essentially do the same thing. Either works fine, but try to avoid using the following pattern where an instance variable is created at every bind :

//Poor performance
var delay \= 100;
for (var i \= 0; i < 100; i++){
	myRegion.bind(myElement, new ZingTouch.Tap({maxDelay : delay}),function(e){...});
}

//Better performance
var delay \= 100;
var customTap \= new ZingTouch.Tap({maxDelay : delay});
for (var i \= 0; i < 100; i++){
	myRegion.bind(myElement, customTap, function(e){...});
}

* * *

### Region.bind(element)

Passing a qualified DOM element to the bind function will return an object that can be chainable with the 6 main gestures, or any other gestures that you may have registered with `Region.register`

**Parameters**

-   element - A DOM element

**Returns**

-   A chainable object that takes two parameters :
    -   `handler` - A function to be called every time the gesture is emitted.
        
        -   The chainable object has 6 methods available at all times : `.tap()` ,`.swipe()` ,`.pinch()` ,`.expand()` ,`.pan()` ,`.rotate()`. Custom Gesture are accessible using the `ZingTouch.register` method.
        -   The handler function has an Event object emitted from the CustomEvent interface. Any information relavant to the gesture will be in `event.detail`.
    -   `capture` - An optional boolean to designate the event to be fired on the capture or bubbling phase.
        

**Example**

var myElement \= document.getElementById('mydiv');
var myRegion \= new ZingTouch.Region(myElement);
var chainableObject \= myRegion.bind(myElement);

chainableObject
	.tap(function(e){
		console.log(e.detail);
	})
	.swipe(function(e){
		console.log(e.detail);
	}, true)

* * *

### Region.bindOnce()

Identical to both method signatures of bind, but is "bound once" meaning the event will only be captured once before it is destroyed.

See Region.bind

* * *

### Region.unbind(element, \[gesture\])

Unbinds an element from a specific gesture, or all gestures if none is specified.

**Parameters**

-   `element` - A DOM element
-   `gesture` _optional_ - Either a registered gesture's key (String) or the gesture object used to bind the element.

**Returns**

-   array - An array of bindings containing the gestures that were unbound.

**Examples**

Unbind from a specific gesture

var myElement \= document.getElementById('mydiv');
myRegion.unbind(myElement, 'tap');

Unbind from all gestures

var myElement \= document.getElementById('mydiv');
myRegion.unbind(myElement);

Unbind from a gesture instance.

var myElement \= document.getElementById('mydiv');
var myRegion \= new ZingTouch.Region(document.body);
var myTapGesture \= new ZingTouch.Tap({ maxDelay : 100 });

myRegion.bind(myElement, myTapGesture, function(e) {});

myRegion.unbind(myElement, myTapGesture);

* * *

### Region.register(key, gesture)

Register a gesture of the Gesture class to each Region. Allows the newly registered Gesture to be accessible in the bind/unbind syntax including the chainable object of bind.

**Parameters**

-   `key` - A string to identify the new gesture.
-   `gesture` - An instance of the Gesture class

**Returns**

-   The gesture object registered

**Examples**

var myTapGesture \= new ZingTouch.Tap({ maxDelay : 60 });

var myRegion \= new ZingTouch.Region(document.body);
myRegion.register('shortTap', myTapGesture);

And the usages :

myRegion.bind(myElement, 'shortTap', function(e){});

myRegion.bind(myElement).shortTap(function(e){});

* * *

### Region.unregister(key)

Unregisters a gesture that was previously registered. Unregistering a gesture will automatically unbind any elements that were bound to this gesture.

**Parameters**

-   `key` - A string to identify the gesture that will be unregistered.

**Returns**

-   The gesture that was unregistered.

**Example**

myRegion.unregister('shortTap');

* * *

ZingTouch Life Cycle
====================

Utilizing ZingTouch's life cycle (start, move, end) allows you to create new gestures and to interface with the mobile event cycle in a much finer detail. It will allow you to hook into events and to apply external functions during events. Imagine the `Pan` gesture allowing in-between events to be triggered:

-   Pan - start
-   Pan - move
-   Pan - end
-   Pan -> Event detected.

The syntax for utilizing the life cycle is still to be determined, but will be released in the near future.

* * *

Pitfalls
========

**Binding an event and DOM mutation to an element** ZingTouch treats a gesture as a non-mutable event, meaning that the element is bound to is not expected to change between the start and end. Binding a transformation of an element's bounding box to the middle of a gesture event could provide unwanted results.

Example: Binding a pan event directly to an element that you want to move around every time the callback is fired. The initial state of when the gesture was registered changes throughout the event, and the initial reference point is no longer valid.

Solution: Attach the gesture listener to a non-mutating element such as a parent container, and modify your target element in the callback. This will provide a more predictable state that zingtouch can recognize.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Contributing
============

**Build dependencies**

-   Build Tool: Webpack
    -   `npm install -g webpack`
-   ES6 translator : Babel

**Comments and Documentation**

-   We follow JSDoc guidelines but utilize ESDoc to output documentation. We find ESDoc to be friendlier with ES6/class structured codebases.

**Testing**

-   Mocha
-   Chai (Expect)

### npm scripts

-   `npm run build:dev` - Builds the unminified library with webpack
-   `npm run build:prod` - Builds the minified library with webpack
-   `npm run docs` - Builds the docs with esdocs
-   `npm run test` - Run the tests

Browser Compatibility
---------------------

Below is a list of confirmed browser and device compatibility that I have confirmed either though the physical device or by way of a Virtual Machine. If you have any issues or would like to contribute to this list, please pull request onto this readme file.

**Confirmed browser compatibility with:**

-   Chrome 22+
-   Firefox 18+
-   Safari 7+
-   Edge 13+

**Tested/ Developed on :**

-   iPhone 4, 5, 6, 6+
-   iPad Pro
-   Samsung Galaxy s6
-   Microsoft Surface Book

* * *

License
=======

MIT License

© 2017 ZingChart, Inc.
