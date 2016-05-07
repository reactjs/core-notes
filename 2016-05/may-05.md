## May 5 ([discuss](https://github.com/reactjs/core-notes/pull/13))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Shayne](https://github.com/shayne) (React Native)
* [Tom](https://twitter.com/tomocchino) (React)

### ReactPerf Rewrite

* [Dan](https://twitter.com/dan_abramov) got his rewrite of `ReactPerf` [merged into React master](https://github.com/facebook/react/pull/6647).
* It is mostly functionally identical to the old one but is written in a more maintainable way.
* At Facebook, we don’t use the console `ReactPerf` API much so we’ll need community help testing this.
* There is a corresponding [React Native PR](https://github.com/facebook/react-native/pull/7283) that depends on these changes.
* The change removes `ReactPerf.measure()` wrappers and instead emits events (e.g. `onBeginLifeCycleTimer`).
* Related PRs: [#6549](https://github.com/facebook/react/pull/6549), [#6612](https://github.com/facebook/react/pull/6612), [#6633](https://github.com/facebook/react/pull/6633), [#6046](https://github.com/facebook/react/pull/6046).
* It will most likely go into `15.1.0-alpha` early next week.

### TestUtils and Enzyme

* Airbnb’s [Enzyme](https://github.com/airbnb/enzyme) is well maintained and supported.
* Our [`TestUtils`](https://facebook.github.io/react/docs/test-utils.html) are not in a great shape, and most people prefer Enzyme.
* Should Enzyme become the official `TestUtils`?

#### Challenges

* Ideally we want test runner to be a separate renderer.
* Tests should run consistently and often synchronously so we don’t want to run them with [incremental reconciler](https://github.com/facebook/react/issues/6170).
* We have no official renderer APIs yet so without `TestUtils` Enzyme would have to rely on React internals.

#### Risks

* If Enzyme is abandoned, we will have to maintain it.
  * Not a big deal because this is pretty much our situation with `TestUtils` now.
* Recommending it as an official solution might raise questions about “official solutions” to other problems.
  * (e.g. routing, state management)
* We don’t have guidelines for recommending something as an official solution.
* No conclusion yet, needs more discussion.

### Server Rendering

* After thinking more about incremental reconciliation, [Sebastian](https://twitter.com/sebmarkbage) has some renewed interest in server rendering.
* Whatever feature server rendering wants, it’s a good feature to have on the client as well.
* For example, if you have a component that’s unlikely to change:
  * Currently you have all those React internal instances in memory.
  * But if you remove those, and are able to recover…
  * It’s just like reviving a server rendered tree on the client.
* Current behavior for rehydration after server rendering:
  * It re-renders everything on the client to a string to verify the checksum, then throws it out.
  * If it’s the same, and we need the node or instance for any reason, at that point we climb the tree and figure out what instance it corresponds to lazily.
  * It doesn’t fix any inconsistencies it finds as it traverses back up.
  * This is what [@aickin](https://github.com/aickin) is trying to change in his [pull request](https://github.com/facebook/react/pull/6618).
* What does [#6618](https://github.com/facebook/react/pull/6618) help with?
  * We can loosen constraints on validation.
  * Markup doesn’t have to be character for character equivalent.
  * [Ben](https://twitter.com/soprano) has [concerns](https://github.com/facebook/react/pull/6618#issuecomment-217321531) about it.

### CSS Fallback Values

* We don’t have a way of letting people specify fallback values for vendor prefixes.
* People ask for something like this: `display: ['-webkit-box', '-moz-box', '-ms-flexbox', '-webkit-flex']`.
* Using arrays for this precludes supporting something like `margin: [0, 0]` in the future.
* We could use an opaque data structure for this, e.g. `ReactDOM.CSS.multi('-webkit-box', '-moz-box', ...)`.
* There’s a proof of concept in [#6701](https://github.com/facebook/react/pull/6701).
* Still needs more bikeshedding on the name but the idea is sound.
* We might want to look at autoprefixing again the next time we approach inline styles in the future.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/13).
