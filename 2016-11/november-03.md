## November 3 ([discuss](https://github.com/reactjs/core-notes/pull/36))

### Attendees

* [Andrew](https://twitter.com/acdlite) (React)
* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Paul](https://twitter.com/zpao) (Open Source Tools)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Andrew

* Working on batching updates. `setState` is normally asynchronous in Fiber but it should be synchronous inside `componentDidMount` and `componentDidUpdate`. Also implementing opt-in `ReactDOM.unstable_batchedUpdates` for feature parity. ([#8193](https://github.com/facebook/react/pull/8193))
* It turned out to be significantly easier in Fiber to call `setState` callbacks right after `componentDidUpdate` rather than at the very end of all updates. We’re going to change the existing reconciler to match this behavior in React 16. (Ben will make the change in [#8204](https://github.com/facebook/react/pull/8204))

#### Ben

* Wrote a script that keeps track of which tests [fail](https://github.com/facebook/react/blob/master/scripts/fiber/tests-failing.txt) and [pass](https://github.com/facebook/react/blob/master/scripts/fiber/tests-passing.txt) in Fiber.
* New PRs now need to run `scripts/fiber/record-tests` so that we can catch unexpected Fiber regressions.
* Working on infrastructure to ignore tests that just check for warnings, as they’re less important while we work on Fiber feature parity.

#### Dan

* Fixed a few issues in Fiber scheduler. ([#8172](https://github.com/facebook/react/pull/8172), [#8187](https://github.com/facebook/react/pull/8187))
* Collaborating with Andrew on error boundaries and batching in Fiber. ([#8193](https://github.com/facebook/react/pull/8193), [#8210](https://github.com/facebook/react/pull/8210))

#### Paul

* Visiting from Seattle to meet with his new team, stopped by to attend the meeting.
* Gave us an overview of new Facebook open source pipeline: [facebookexperimental](https://github.com/facebookexperimental) → [facebookincubator](https://github.com/facebookincubator) → [facebook](https://github.com/facebook).
* At his new team, Paul will work to encourage more open source projects at Facebook.

#### Sebastian

* Working on a major refactoring of the event system. ([#8176](https://github.com/facebook/react/pull/8176), [#8190](https://github.com/facebook/react/pull/8190), [#8192](https://github.com/facebook/react/pull/8192), [#8229](https://github.com/facebook/react/pull/8229))
* The goal is to change it to attach event listeners at the root of the tree instead of the document. ([#8117](https://github.com/facebook/react/pull/8117))
* The next step is integrating the event system into Fiber.

### Discussions

#### Shipping 15.4.0

* React Native integration has been rocky because it now ships with its own copy of the reconciler, but we’re close.

#### Fiber Milestones

* We added an internal opt-in flag for employees to render Facebook.com with Fiber. Everything is broken right now but we can now focus on getting simple components working.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/36).
