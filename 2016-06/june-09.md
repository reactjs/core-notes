## June 9 ([discuss](https://github.com/reactjs/core-notes/pull/19))

### Attendees

* [Alex](https://twitter.com/alex_frantic) (React Native)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Sebastian

##### New Reconciler Plan

* Making progress on the incremental reconciler ([PRs](https://github.com/facebook/react/pulls?utf8=%E2%9C%93&q=+fiber+is%3Apr+is%3Aclosed+author%3Asebmarkbage+)).
* The next step is to support forking for pausing and cancelling reconciliation.
* After that, the new reconciler needs to implement flushing changes (e.g. to the DOM).
* This would take the bulk of the month, and then will be working towards reaching feature parity with existing reconciler.

##### Observations about `setState()`

* We currently [support](https://facebook.github.io/react/docs/component-api.html#setstate) `setState(callback: (state, props) => nextState)`.
* It is not entirely clear how well that would work with incremental reconciler.
* The issue is that props become very much “spread in time”: last render could be a while ago, and next render might be in the future.
* Hard to say if this will turn out to be a problem, worth doing more investigation.

#### Jim

* Fixed a few issues in React DOM. ([#6986](https://github.com/facebook/react/pull/6986), [#7002](https://github.com/facebook/react/pull/7002), [#7003](https://github.com/facebook/react/pull/7003))
* Proposed a PR that warns if people mutate `props.children`. ([#7001](https://github.com/facebook/react/pull/7001))
* We will probably take this PR, Sebastian will be taking another look at it.

#### Dan

* Working on internal Facebook code to get rid of some of the most common mixins.

#### Ben

* Ben is enabling class property transform in the internal Facebook build pipeline.

### Keyan

* Error code work is finished! ([#6882](https://github.com/facebook/react/pull/6882), [#6946](https://github.com/facebook/react/pull/6946), [#6948](https://github.com/facebook/react/pull/6948))
* Will start working on a new codemod to convert more components to classes with property initializers.

## Discussions

### Warning for Mutating Children ([#7001](https://github.com/facebook/react/pull/7001))

* In general, this seems like a good idea, but people are using children in a ton of crazy ways in the wild.
* We have to figure out if the introduction of this warning is a breaking change or not.
* We will enable it on Facebook website to see how many callsites are affected.

### Current Progress on ES6 Classes

* Ben is working on enabling property initializers in Facebook codebase.
* Keyan is working on a new `createClass` → ES class component transform that uses property initializers (rather than binding in the constructor).
* Dan is working on getting rid of some of the internal mixins on Facebook websites.
* Still need to figure out what to do with `PureRenderMixin`.
* Property initializers are currently extremely verbose with Flow, and this needs to be fixed.

### Proposals Champion Process

* We might want to adopt a proposal champion process similar to TC39.
* Everyone has an idea of what they want to add / change / fix, but once you start digging into it, there’s just so much context needed, and it’s so hard to change.
* We’d like to have internal champions the same way TC39 has champions.
* The responsibility of that person is to answer any question that arises.
* At TC39, you are expected to have all the answers to the questions, or the thing you’re pushing through gets delayed.
* Secondary champions can step up to champion other peoples’ ideas (e.g. helping to move a community proposal forward).

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/19).
