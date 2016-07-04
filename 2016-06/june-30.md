## June 30 ([discuss](https://github.com/reactjs/core-notes/pull/22))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Fiber Demo

* If you missed what Fiber is, [look here](https://github.com/reactjs/core-notes/blob/master/2016-06/june-23.md#update-on-fiber).
* Not very exciting.. but it can render a `<div>`!
* Basically this is all that [Sebastian](https://twitter.com/sebmarkbage) showed us so far.
* You can find the demo [here](https://github.com/facebook/react/blob/24dfb56113a214d98f29f69e2c26f67d7e947067/examples/fiber/index.html) but you’d need to compile React DOM to point to the [fiber version](https://github.com/facebook/react/blob/24dfb56113a214d98f29f69e2c26f67d7e947067/src/renderers/dom/fiber/ReactDOMFiber.js).

### Update on `createClass` → ES classes

* We are moving towards not using `createClass` in the internal Facebook components.
* [Keyan](https://twitter.com/keyanzhang) is working on an open source [codemod](https://github.com/reactjs/react-codemod/pull/54) to automate the transition.
* The codemod converts `createClass` calls to ES classes with experimental [property initializers](https://github.com/jeffmo/es-class-fields-and-static-properties) proposal and Flow.
* We *don’t* officially recommend this yet because the proposal has not advanced yet but we want to dogfood it internally.
* There are more things to figure out with Flow (e.g. we might need to annotate state properties).
* [Dan](https://twitter.com/dan_abramov) ran the codemod that removes one very common mixin we had, so now we have more convertible classes.
* It is essential that we add some version of [`PureComponent`](https://github.com/facebook/react/pull/6914) to React because a lot of components use `PureRenderMixin`.

### `React.PureComponent`

#### Naming

* We’ve been assuming we’d call it `React.PureComponent`.
* However “pure” really means something different in computer science.
* What we try to express is that component `props` are immutable so the output is safe to memoize.
* Other suggestions: `MemoizedComponent`, `MemoizableComponent`.
* It’s hard to spell!
* We *don’t* want people to use it everywhere so more complicated name might be fine.
* We can bikeshed on this forever.

#### Heuristics

* It seems that [proposed heuristic generated a lot of confusion](https://github.com/facebook/react/pull/6914) and [potential issues](https://github.com/facebook/react/pull/6914#issuecomment-229574637).
* We can drop the heuristic from the proposal and just get the class in. Then decide later.

### Splitting [Addons](https://facebook.github.io/react/docs/addons.html)

* After the internal `createClass` deprecation, can we drop the addons?
* We [haven’t](https://github.com/facebook/react/pulls?q=is%3Apr+reacttransitiongroup+is%3Aclosed) been maintaining `ReactTransitionGroup` and other addons well.
* We should transfer ownership to folks that are actually relying on them.
* Almost everything can be decoupled except `Perf` and `TestUtils`.
* This should happen before [flat bundling](https://github.com/facebook/react/issues/6351).
* Should we move `React.createFragment` into React?
  - No, this was an upgrade path, shouldn’t need to use it anymore.
  - It could have been the way you specify render methods without a single return value but we didn’t implement this.
* [Paul](https://twitter.com/zpao) and [Dan](https://twitter.com/dan_abramov) will come up with a plan for each addon.

### React Hot Loader 3

* It is popular in the community but the last stable version doesn’t work with functional components.
* There is a new version that solves these problems but it isn’t quite stable yet.
* [Dan](https://twitter.com/dan_abramov) will take a week to fix a few issues and release a stable version with docs.

### Releasing 15.2.0

* [Paul](https://twitter.com/zpao) planned to release today.
* [Dan](https://twitter.com/dan_abramov) noticed it would be better to [deduplicate](https://github.com/facebook/react/issues/7152) the new DOM unknown attribute warning. 
* We will let the community fix it and then cut 15.2.0.
* [Jim](http://github.com/jimfb) wrote about the reasons and the strategies for fixing this warning [in the related gist](https://gist.github.com/jimfb/d99e0678e9da715ccf6454961ef04d1b).
* Some useful discussions about this change: [erikras/redux-form#1249](https://github.com/erikras/redux-form/issues/1249), [Hacker0x01/react-datepicker#517](https://github.com/Hacker0x01/react-datepicker/issues/517).
* We won’t do a blog post about this release (and about most patch and minor releases in general).
* Instead, you can find changes in the [changelog](https://github.com/facebook/react/blob/master/CHANGELOG.md#1520-july-1-2016).

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/22).
