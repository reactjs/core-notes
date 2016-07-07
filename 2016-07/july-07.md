## July 07 ([discuss](https://github.com/reactjs/core-notes/pull/23))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Fragments

* We don’t currently allow returning multiple elements from `render()` method.
* This has been a [long requested feature](https://github.com/facebook/react/issues/2127) in the community.
* We generally agree that it should be implemented but we found it to be hard with our existing architecture.

#### Existing Solutions

* There exists a [fork](https://github.com/facebook/react/issues/2127#issuecomment-216401555) that implements fragments but we don’t want to take this implementation.
* It introduces them only for React DOM which would make React features inconsistent across renderers.
* It also introduces some complexity we would like to avoid because we might start breaking other things with it.

#### Our Plans

* [Fiber](https://github.com/reactjs/core-notes/blob/master/2016-06/june-23.md#update-on-fiber) supports fragments but it’s far from done.
* We will include work on fragments in our plan for the second half of 2016.
* Since we want this feature anyway, we can implement it in existing reconciler independently of Fiber.

### Build Size

* We think that React provides good value for its build size (~45kB min+gzip).
* However we understand everybody has different constraints, especially with small apps.
* We intend to be [more mindful](https://github.com/facebook/react/issues/7205) of the build size to avoid accidental regressions.

#### Rollup

* [Keyan](https://twitter.com/keyanzhang) is investigating using [Rollup](http://rollupjs.org/) for our UMD builds. ([#7178](https://github.com/facebook/react/pull/7178))
* After [#7178](https://github.com/facebook/react/pull/7178) is merged, the minified post-gzip size will reduce by 14%. (46kB → 39kB)
* For now, we will use [a hack](https://github.com/facebook/react/pull/7178#issuecomment-230379738) to transpile CommonJS to ES Modules so Rollup understands them.
* Longer term, we’d like to use ES Modules in the source but Facebook internal bundlers don’t understand them yet.

#### Event System

* [Dan](https://twitter.com/dan_abramov) asked why the event system is so large.
* It accounts for a noticeable chunk of React build size.
* Looking at other “React-like” libraries, no one has an event system like ours. Why?

##### Why We Need It

* The intention was to normalize events with weird behavior like `mouseenter` or `focus` across browsers.
* This lets component authors not worry about inconsistencies with bubbling and input events, making ecosystem better.
* The React Native gesture handling system is also built around it.
* The browsers have improved, so we will keep re-evaluating it once in a while, but for now we find it useful.

##### What We Can Improve

* It is overabstracted, and we can simplify code by baking support for some [“plugins”](https://github.com/facebook/react/tree/1a0e3a32150468223d6f9fd0125db0f8503b76d6/src/renderers/dom/client/eventPlugins) right into it.
* There is some code duplication we can reduce in [the event whitelist](https://github.com/facebook/react/blob/1a0e3a32150468223d6f9fd0125db0f8503b76d6/src/renderers/dom/client/eventPlugins/SimpleEventPlugin.js).
* Some weird patterns like [`keyOf()`](https://github.com/facebook/react/blob/1a0e3a32150468223d6f9fd0125db0f8503b76d6/src/renderers/dom/client/eventPlugins/SimpleEventPlugin.js#L40-L41) exist to be compatible with [GCC](https://www.google.co.uk/search?q=google+closure+compiler&gws_rd=cr&ei=O7x-V_66AonOgAbov6GACA). Perhaps we could find another way to fix this?

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/23).
