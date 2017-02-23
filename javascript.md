# Javascript

**1. General**

**1.1 Versions**

- **ECMAScript 5** : very good all round browser support. From 2009.
- **ECMAScript 6** : aka ECMAScript 2015. Next version to be added. Some support, can use babel. Adds cases and modules, and more.
- **ECMAScript 7** : aka ECMAScript 2016, very little support.
- **ECMAScript 8** : still very early days, but many OO suggestions, and data manipulators.

**2. Libraries**

**2.1 Dependencies**

CommonJS came first, but AMD has fixed some of its problems with not too many drawbacks. CommonJS Is often used server side, AMD usually for client-side code. Node chose CommonJS, and brown adherents flocked to AMD, due to it&#39;s non-blocking nature and dynamic friendly loading.

Usually the best solution is to use ES6 format, and compile to any module format of your choice.

CommonJS

Synchronous, but easier to read. Can has slow load times on client-side

var jQuery = require(&#39;jquery&#39;);

AMD

Allows for async decencies, but can be harder to read. RequireJS is an implementation of AMD.

define([&#39;jquery&#39;], function($) {

        …

});

ES6 import

Will be converted into commonJS by Babel

import { $ } from &#39;jquery&#39;;

**2.1 Module Loaders**

When choosing a module loader for your next project, be careful of falling prey to analysis paralysis. Try the simplest possible solution first: there&#39;s nothing wrong with skipping a loader entirely and sticking with plain old script tags. If you really do need a loader, [RequireJS+Almond](http://requirejs.org/docs/faq-optimization.html) is a solid, performant, well supported choice. Browersify leads if you need CommonJS support. Only upgrade to a bleeding edge entry like SystemJS or Webpack if there&#39;s a problem you absolutely can&#39;t solve with one of the others. The documentation for these bleeding-edge systems is arguably still lacking. So use all the time you save by using a loader appropriate to your needs to deliver some cool features instead.

RequireJS - Wide support

Is an implementation of AMD. Has very wide support, despite its idiosyncrasies.

requirejs(&#39;entryPoint.js&#39;, function (eP) {

        // startup code

});

Single page app: [https://github.com/volojs/create-template](https://github.com/volojs/create-template)

Multi-page app: [https://github.com/requirejs/example-multipage](https://github.com/requirejs/example-multipage)

Browerify - Good if you need CommonJS support

Allows you to use CommonJS formatted modules in the browser. It is less of a module loader, but a module bundler. Will include all the modules into one file. Going strong still.

&lt;script src=&quot;browserifyBundle.js&quot;&gt;&lt;/script&gt;

Webpack - Bleeding edge only if need

Also a module bundler, but also allows you to replace Gulp/Grunt build systems. Supports both CommonJS, AMD, ES6, and non-script assets such as stylesheets, images and HTML templates.

ES6 transpiration is handled natively, as is SCSS.

Can be very opinionated.

Used to build a single-page application, it plays well with React.

&lt;script src=&quot;webpackChunk.js&quot;&gt;&lt;/script&gt;

SystemJS - Bleeding edge only if need

It is similar to RequireJS, in that it uses the script tag. SystemJS is used by Angular 2, and also supports non-JS file types with loader plugins.

System.import(&#39;entryPoint.js&#39;).then(function (eP) {

        // startup code

});

[https://appendto.com/2016/06/the-short-history-of-javascript-module-loaders/](https://appendto.com/2016/06/the-short-history-of-javascript-module-loaders/)



**2.3 Tests**

Tape



**2.4 Libraries**

Angular, React and Vue.js all now have ShadowDOM support.

Angular

- Version 2 has made a lot of improvements.
- Has a strong community.
- Opinionated

Knockout.js

- Slightly out of date, slow dev
- Some interfaces are clunky

**React**

- Focused on what it does, needs other companion libraries
- Has a very strong community.
- Unopinonated
- Larger ecosystem, i.e. more support and tools
- Better at scale

React&#39;s immutable application data may not be as succinct, but it shines in larger application when transparency and testability become critical

Vue.js

- Not as popular, but has some of the best of both Angular and React. But has a fast learning time.
- It outperforms both Angular and React, and is smaller than both. It renders faster than React.
- Has CSS modules support.
- Makes good use of template files, which can be more usable than include HTML
- The size of the library is much smaller :)
- Flexible options for templates or render functions
- Simplicity in syntax and setup
