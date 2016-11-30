## November 10 ([discuss](https://github.com/reactjs/core-notes/pull/37))

### Attendees

* [Andrew](https://twitter.com/acdlite) (React)
* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Andrew

* Figuring out what the right behavior for error boundaries and uncaught errors should be in Fiber. For now, decided that we're going to unmount the whole tree when there is an uncaught error. We can potentially keep the DOM tree in the future. ([#8227](https://github.com/facebook/react/pull/8227))

#### Ben

* Working on infrastructure that lets us separate dev-only test failures (such as warning assertions) from real failures. This will help us focus on bugs in Fiber. Such assertions will be using `expectDev()` instead of `expect()`. ([#8228](https://github.com/facebook/react/pull/8228))

#### Dan

* Fixed a few minor issues in Fiber related to `TestUtils`.

#### Sebastian

* Working on integrating DOM properties and events into Fiber.

### Why So Little?

We’re focused on [getting Fiber ready](http://isfiberreadyyet.com/) and have [many remaining issues](https://github.com/facebook/react/issues/7925) to work on so we don’t talk as much. :-)

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/37).
