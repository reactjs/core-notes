## October 27 ([discuss](https://github.com/reactjs/core-notes/pull/35))

### Attendees

* [Andrew](https://twitter.com/acdlite) (React)
* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Andrew

* Implemented string refs on top of callback refs in Fiber. ([#8099](https://github.com/facebook/react/pull/8099))
* Implemented support for `PureComponent` to Fiber. ([#8118](https://github.com/facebook/react/pull/8118))
* Working on making `ReactDOM.render()` synchronous by default in Fiber, and adding support for `unstable_batchedUpdates()` to Fiber. ([#8127](https://github.com/facebook/react/pull/8127))
* Will work again on something like [#7457](https://github.com/facebook/react/pull/7457) so that `setState()` inside low priority trees does not cause them to get a high priority.

#### Ben

* We are already [tracking](https://github.com/facebook/react/blob/facts/fiber-tests.txt) how many tests as passing on Fiber. Working on setting up infrastructure so we know which tests exactly are failing, and make sure we don't regress on old tests as we add new features.

#### Dan

* Merged [Jim](https://github.com/jimfb)'s pull request for making error boundaries work for updates in the existing reconciler, and added more tests. They are still hidden behind an `unstable_` API prefix as they are not fully supported. ([#7949](https://github.com/facebook/react/pull/7949))
* Working on supporting error boundaries in Fiber. It already implements more cases than error boundaries in the existing reconciler. ([#8095](https://github.com/facebook/react/pull/8095))

#### Sebastian

* Fixed a few bugs in Fiber and implemented `findDOMNode()` and `isMounted()`. ([#8083](https://github.com/facebook/react/pull/8083))
* Working on adding DOM attributes and events to Fiber.
* Working with [Christopher](https://twitter.com/vjeux) on getting [#8117](https://github.com/facebook/react/pull/8117) merged. Chistopher needs it for Nuclide.

#### Tom

* Made a website to track our progress working on Fiber: [isfiberreadyyet.com](http://isfiberreadyyet.com/).

### Discussions

#### Release Process

* [Paul](https://twitter.com/zpao) has left the team and will work on open source tooling at Facebook. Somebody needs to take over the release process. Ben agreed to help with 15.4.0.
* Paul was working on a [release manager](https://github.com/facebook/react/pull/7330) so releasing is more automated. However nobody used it yet. We'll probably need some help from Paul to demo it to us when he's back from a vacation.


------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/35).
