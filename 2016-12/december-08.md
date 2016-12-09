## December 8 ([discuss](https://github.com/reactjs/core-notes/pull/39))

This meeting is special for three reasons!

* [Brian](https://twitter.com/brian_d_vaughn) of [React Virtualized](https://bvaughn.github.io/react-virtualized/) fame **has joined the team!** 🎉
* [IsFiberReadyYet.com](http://isfiberreadyyet.com/) is now **rendered with Fiber**.
* We are sharing **our goals and areas of focus for the first half of 2017** (read below!)

### Attendees

* [Adam Wolff](https://twitter.com/dmwlff) (Front End Infrastructure)
* [Andrew](https://twitter.com/acdlite) (React)
* [Ben](https://twitter.com/soprano) (React)
* [Brian](https://twitter.com/brian_d_vaughn) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Invididual Updates

#### Andrew

* Landed a big restructuring of Fiber scheduler that avoids excessive `try` / `catch`es. ([#8479](https://github.com/facebook/react/pull/8479))
* Will keep working on improving Fiber scheduler. ([#8538](https://github.com/facebook/react/pull/8538))

#### Ben

* Keeping track of Fiber bugs we found testing Fiber at Facebook. ([#7925](https://github.com/facebook/react/issues/7925))

#### Brian

* Ported [React ART](https://github.com/reactjs/react-art) to Fiber using the new renderer API. ([#8521](https://github.com/facebook/react/pull/8521))

#### Dan

* Been bikeshedding on how to implement SVG with Sebastian for a while. ([#8417](https://github.com/facebook/react/pull/8417), [#8475](https://github.com/facebook/react/pull/8475))
* Settled on the approach and landed an imperfect version of SVG support to iterate later. ([#8490](https://github.com/facebook/react/pull/8490))

#### Sebastian

* Fixing different bugs in Fiber.

#### Tom

* Now that we have SVG, ported [IsFiberReadyYet.com](http://isfiberreadyyet.com/) to use Fiber.

----------------------

## Plan for the First Half of 2017

### Goals

* Deliver on the promise of Fiber
* Understand and improve byte-size and runtime performance

### Prerequisite work

See the [Fiber umbrella issue](https://github.com/facebook/react/issues/7925) for a more detailed list of remaining work on the new version of the React core (aka “Fiber”), which will replace the old version (aka “Stack”) in 2017. In summary:

* Do performance testing on Facebook products
* Implement developer facing warnings
* Fix remaining bugs and failing unit tests
* Implement the React Native Fiber renderer
* Figure out what to do about server-side rendering

Note that while Fiber is a complete rewrite of React, it strives to maintain backwards compatibility wherever possible. We are already testing existing products on it with little to no changes to their code.

### Start to deliver on the promise of Fiber

In addition to being a complete rewrite to the React core that we hope will be smaller and faster, Fiber gives us the ability to fix long standing issues and add long requested features:

* Return multiple components from render (aka fragments)
* Return text from render
* Proper and comprehensive support for error boundaries
* New API for portals that unifies scheduling of different subtrees
* Much, much easier to write custom renderers for React (web, native, canvas, GL, etc)

We will release the above along with the rollout of Fiber in early 2017, and will then shift our focus toward other projects which will help to realize some of the future promise of our investment:

### Understand and improve byte-size and runtime performance

Fiber allows us to make more sophisticated scheduling decisions to improve perceived performance and user experience. To reduce UI stalls and jank, we can make two changes to how React functions:

* Change default rendering mode to async so high-priority user interactions can interrupt other low-priority rendering work
* Expose developer accessible hooks to allow more sophisticated control of rendering priorities

We’ve seen an increasing number of libraries inspired by React that promise to be faster and smaller than React. This half we will do an investigation into byte-size and initialization time and use that knowledge to improve React's start-up time. We will also investigate more sophisticated compilation techniques.

### Additional work and stretch goals

After releasing Fiber broadly, we will begin work to remove the old React core, which will require that we have complete feature parity with the existing React core. This will require that we:

* Implement React DevTools support in Fiber
* Figure out and communicate subtle timing differences between Stack and Fiber
* Move the shallow and test renderers off of the old Stack reconciler
* Create a plan to support server-side rendering with Fiber

In addition to the above we may also focus on these important areas as stretch goals:

* Design new functional component API with declarative data subscriptions
* Publicly deprecate `createClass`
* Clean up old addons and cyclic dependencies
* Make release process more straightforward
* Make implementation safer with Flow

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/39).
