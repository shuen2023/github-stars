---
project: Magnific-Popup
stars: 11390
description: Light and responsive lightbox script with focus on performance.
url: https://github.com/dimsemenov/Magnific-Popup
---

**Important note** This jQuery plugin is deprecated, only critical or security bug fixes will be released in future. Use native `<dialog>` element if you need a basic dialog/modal/popup, or my PhotoSwipe library if you need an advanced image gallery. Feel free to email me if you need assistance.

Magnific Popup Repository
=========================

Fast, light and responsive lightbox plugin, for jQuery and Zepto.js.

-   Documentation and getting started guide.
-   Examples and plugin home page.
-   More examples in CodePen collection.

Optionally, install via Bower `bower install magnific-popup` or npm: `npm install magnific-popup`. Ruby gem: `gem install magnific-popup-rails`.

Extensions
----------

-   WordPress plugin - under development.
-   Drupal module.
-   Concrete5 add-on.
-   Redaxo add-on.
-   Contao extension.

If you created an extension for some CMS, email me and I'll add it to this list.

Location of stuff
-----------------

-   Generated popup JS and CSS files are in folder dist/. (Online build tool is on documentation page).
-   Source files are in folder src/. They include Sass CSS file and js parts (edit them if you wish to submit commit).
-   Website (examples & documentation) is in folder website/.
-   Documentation page itself is in website/documentation.md (contributions to it are very welcome).

Using Magnific Popup?
---------------------

If you used Magnific Popup in some interesting way, or on site of popular brand, I'd be very grateful if you email me a link to it.

Build
-----

To compile Magnific Popup by yourself, first of make sure that you have Node.js, Grunt.js, Ruby and Jekyll installed, then:

1.  Copy repository
    
    git clone https://github.com/dimsemenov/Magnific-Popup.git
    
2.  Go inside Magnific Popup folder that you fetched and install Node dependencies
    
    cd Magnific-Popup && npm install
    
3.  Now simply run `grunt` to generate JS and CSS in folder `dist` and site in folder `_site/`.
    
    grunt
    

Optionally:

-   Run `grunt watch` to automatically rebuild script when you change files in `src/` or in `website/`.
-   If you don't have and don't want to install Jekyll, run `grunt nosite` to just build JS and CSS files related to popup in `dist/`.

Changelog
---------

License
-------

Script is MIT licensed and free and will always be kept this way. But has a small restriction from me - please do not create public WordPress plugin based on it(or at least contact me before creating it), because I will make it and it'll be open source too (want to get notified?).

Created by @dimsemenov & contributors.

Bugs & contributing
-------------------

Please report bugs via GitHub and ask general questions through Stack Overflow. Feel free to submit commit pull-request, even the tiniest contributions to the script or to the documentation are very welcome.
