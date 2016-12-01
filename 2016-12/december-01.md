## December 1 ([discuss](https://github.com/reactjs/core-notes/pull/38))

### Attendees

* [Andrew](https://twitter.com/acdlite) (React)
* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Andrew

* Finished a very long PR with new error boundary semantics for Fiber. If there is an error, the error boundary renders `null` first. After reconciliation is complete, the error boundary gets an `unstable_handleError(error)` call and has a chance to `setState()` there to render the error message. If there are no boundaries and the error is unhandled, the whole tree gets unmounted (which prevents data corruption via broken UI). We might consider keeping the UI in some form in the future (for example, with `visibility: hidden`) but for now unmounting is easier. The next step will be to get rid of nested `try` / `catch`es in the scheduler to avoid performance issues. ([#8304](https://github.com/facebook/react/pull/8304))

#### Ben

* Switched Facebook to use Fiber by default **for the React team**. It kinda works! **Nobody else sees it in production** but we can start dogfooding it and [add FB-specific issues to the umbrella task](https://github.com/facebook/react/issues/7925) so that we can fix them before dogfooding Fiber in other teams. 🎉

#### Dan

* Added `ReactDOM.unstable_createPortal(domNode)` to replace `ReactDOM.unstable_renderContainerToSubtree()` in Fiber. The old API isn’t going away yet but will be phased out after Fiber is released. ([#8386](https://github.com/facebook/react/pull/8386))
* Added support for iterables (e.g. Immutable lists) to Fiber and refactored existing tests to test the public API instead of internal helpers. ([#8446](https://github.com/facebook/react/pull/8446))
* Added some tests for error boundaries and uncaught errors to prevent regressions. ([#8462](https://github.com/facebook/react/pull/8462))
* Working on adding support for SVG to Fiber. ([#8417](https://github.com/facebook/react/pull/8417), [#8475](https://github.com/facebook/react/pull/8475))

#### Sebastian

* Currently at the TC39 meeting.

### Fiber Kinda Works

This is fully rendered with [Fiber](https://github.com/acdlite/react-fiber-architecture):

![Fiber recording](https://d17oy1vhnax1f7.cloudfront.net/items/0m262R3W3Q3k0o2I1T24/Screen%20Recording%202016-12-01%20at%2008.20%20pm.gif?v=cce24841)

**Note: Only the React team members are currently opted into using Fiber at Facebook. We need to dogfood it for a while and find most bugs before we can start officially integrating it into the products. Only then can we start thinking about an official release, as [many things are still missing](https://github.com/facebook/react/issues/7925).**


------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/38).
