## April 7 ([discuss](https://github.com/reactjs/core-notes/pull/3))

### Releasing React 15

#### Shipping Today

* React 15 is shipping! 🎉
* Docs should be in good shape.
* Just need to proofread the [blog post](https://github.com/facebook/react/pull/6396) and ship it.

#### Relay Test Failure

* We changed React to use `object-assign` npm [ponyfill](https://ponyfoo.com/articles/polyfills-or-ponyfills) that falls back to native `Object.assign`. ([#6376](https://github.com/facebook/react/pull/6376))
* This caused a Relay test to fail internally because native `Object.assign` did not preserve key ordering.
* Test will be fixed to not rely on this.
* This won’t block React 15 release.

#### React Native Issue

* `react-native init` installs `react@latest` which would break when we release React 15.
* Sorted out with [James Ide](https://twitter.com/ji).
* Since we communicate with [Exponent](https://twitter.com/exponentjs) frequently, we were able to fix this preemptively.
* We’ll release 15 but keep 0.14 `latest` on npm for a while (hopefully a few hours) until React Native gets a fix.
* It will take some time to update React Native to use React 15, just like before.

#### Branch Planning

* At a high level, things will be slightly different than they’ve been historically because we now have actual minor versions.
* We’ll need to maintain both a patch release and a minor release going forward, so we need to figure out how many releases we’re going to support officially.
* This was also a common question from the community (what is our official story around support of past releases?).
* Node does labels on every request, we’ll need to figure out what our strategy will be so we cherry-pick all the changes correctly.
* [Paul](https://twitter.com/zpao) will study how Node does it and come up with a plan.

#### Rolling Changelog

* Let’s maintain a continuously updated changelog so we don’t have to spend hours (sometimes days!) writing release blog entries.
* We need to figure out how to where to put “unreleased” entries, how to handle merge conflicts, etc.
* Leaning towards having an oncall or whoever merges things updating the changelog.
* What if whenever we sync React master internally to Facebook (once a couple of weeks), we also generate the changelog?
  * This means that whoever does the sync has to do a little more work.
  * Combination of the batched approach + human discretion.
* Will start this process with the next internal sync.

### Browser Tests

* React attempts to normalize behavior across browsers but we don’t have any browser tests. ([#5703](https://github.com/facebook/react/issues/5703))
* We used to have them with Sauce Labs but they were super flaky and we removed them. ([#4393](https://github.com/facebook/react/pull/4393))
* Most of our tests aren’t tied to Jest and we should be able to get them running in the browser again.
* Should we run the existing tests, or are there new types of things we want to test?
  * The types of things we care about with browser tests are often different.
  * Usually we don’t need Jest-isms like clearing the module registry in these tests as they only work with public API.
  * Example: Input selection should not jump to end of input when focusing a controlled input (or something like this).
* Should we be worried tests will get flaky again?
  * We’ll start with a few very focused tests and see how it goes.
* Let’s decide on a test runner and write some tests.
  * Let’s pick a recent regression and try to write a test for it.
  * [Jim](https://github.com/jimfb) will work on this.


### Attributes vs Properties

* In React 15, we switched to using DOM attributes by default and using properties only in special cases.
* This fixed a few issues but then introduced a few other issues.
* While we patched over those regressions and 15 looks good, there is no consensus yet on whether this was the right call.

#### Reasons to Use Attributes over Properties

* Attributes currently match our desired behavior for more or less all supported props, including SVG. In the future properties might support more structured data but there’s nothing there we _currently_ want to take advantage of.
* 0.14 already created HTML strings on initial render, and attributes are the closest alternative.
* If we use attributes for everything we could just drop the whitelist completely (and treat only form components specially), which we may or may not want to do but it seems appealing.
* For the specific regression that relying on attributes introduced ([not setting `value=""` on option tags](https://github.com/facebook/react/issues/6219)), we _can’t_ use properties because there is a semantic difference between `value=""` and no attribute, but `.value` is `''` in both cases.
* We’re not currently invested into designing a rich API for React DOM props right now so less maintenance burden there seems beneficial.

#### Reasons to Use Properties over Attributes

* Attributes seem to only match our wanted behavior for “metadata”, i.e. things that the DOM doesn’t actually really care about. The exception is SVG.
* Attributes for initial render is a waste of resources (`toString` / `parse`) but semantically is OK. They also make sense for server rendering since the point of attributes is to provide an initial value. However this is not a good argument for why they should be used for values that change over time.
* The addition of new elements and features leads to more controlled values and richer data types. Attributes are the legacy, not properties.
* If there are any semantic differences that depend on attributes, we should flag those to standard committees. Then we can polyfill those using attributes, and then eventually remove the fix.
* Maybe we should find someone to actually design this rich API mapping for React DOM props and maintain it. We aren’t busy with this now but this doesn’t mean the problem isn’t worthwhile. Hopefully one day it might be standardized in some form or just considered the canonical declarative bindings to the DOM.

#### Conclusion

* No conlusion yet. We plan to come back to this next week.
* React 15 uses attributes.
* The regressions in RCs appear fixed.

#### Relevant Issues and Pull Requests

* [#1431](https://github.com/facebook/react/issues/1431)
* [#1510](https://github.com/facebook/react/pull/1510)
* [#4618](https://github.com/facebook/react/issues/4618)
* [#5666](https://github.com/facebook/react/pull/5666)
* [#5680](https://github.com/facebook/react/pull/5680)
* [#5907](https://github.com/facebook/react/pull/5907)
* [#5966](https://github.com/facebook/react/issues/5966)
* [#6119](https://github.com/facebook/react/issues/6119)
* [#6219](https://github.com/facebook/react/issues/6219)
* [#6228](https://github.com/facebook/react/pull/6228)
* [#6406](https://github.com/facebook/react/pull/6406)

### Recent Pull Requests

#### `ReactDOM.render()` return value being <s>deprecated</s> legacy ([#6400](https://github.com/facebook/react/pull/6400))

* It’s not deprecated yet and we don’t have a solid plan. But new code should avoid it.
* We still rely on it heavily in our tests (basically all of them!)
  * We might need a separate reconciler for tests anyway.
* We want to encourage people to move away from it because, if we implement incremental reconciler, we might not be able to always resolve nodes synchronously.
* The only thing we know for sure is that this is a potential stumbling block going forward.

#### [Sebastian](https://twitter.com/sebmarkbage) is moving some files from React Native to React ([#6338](https://github.com/facebook/react/pull/6338))

* This adds a new package called `react-native-renderer`.
* It doesn’t block 15 and won’t need to wait until 16.
* We might also split out the `react-dom-renderer` from `react-dom` in the future.
* React Native repo will then contain components and the bridge, but not the parts that integrate tightly with React core.
* Are all React Native engineers going to start pushing to the React repository now?
  * This is mostly stable React code, so shouldn’t churn much.
  * But yes, this is something we’ll have to figure out.
  * Waiting until Sebastian is back to provide an answer here.
* Why are we doing this?
  * Ultimate goal is to make it so React core is separate from each of the renderers.
  * Wherever there’s overlap, we want to be able to iterate and ship independently.
  * A small change to React DOM should not necessarily trigger a new React release.
* Versioning
  * We've started separating different packages, but they’re all still versioned at the same time.
  * Is this going to change? Yes, but not right now.
  * Again, we should be able to iterate on React core and downstream dependencies of React core independently.
  * Lots left to figure out here.
