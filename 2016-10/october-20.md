## October 20 ([discuss](https://github.com/reactjs/core-notes/pull/34))

### Attendees

* [Andrew](https://twitter.com/acdlite) (React)
* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Andrew

* Finishing Facebook Bootcamp and finally ready to join the team!

#### Ben

* Helping [Tim](https://twitter.com/yungsters) get React 15.4.0 (not published yet) into React Native.
* This will be the first release where [React Native ships with its own copy of React, and `react` package won't include the reconciler](https://github.com/reactjs/core-notes/blob/master/2016-07/july-28.md#changes-to-bundling).

#### Dan

* Built a visual debugger to better understand how Fiber works. ([#8033](https://github.com/facebook/react/pull/8033))
* Not clear if this is useful, but it helped Dan better understand what's going on, and may help future contributors.

#### Sebastian

* Working on `setState` and lifycle hooks in Fiber. ([#8015](https://github.com/facebook/react/pull/8015))
* Documented some principles important for contributing to Fiber. ([#7942](https://github.com/facebook/react/issues/7942))

#### Discussions

##### New Lifecycle Sequences in Fiber

Since Fiber supports interrrupting an update and resuming it later, there are some funny new lifecycle sequences.

* For example, `componentWillMount()` may fire, but then the update might get deprioritized. Later the component might receive different props but we can't call `componentWillReceiveProps()` yet because the component has not mounted. Therefore, we will throw away the existing instance, create a new one with the new props, and call `componentWillMount()` on it. This will likely introduce memory leaks in components that subscribe to something in `componentWillMount()`, but this is already how React works on the server, so at least it's consistent.
* Another fun consequence is that `componentWillUpdate()` and `componentWillReceiveProps()` may be called multiple times before the update is finally flushed and `componentDidUpdate()` is called. Each of those times `componentWillUpdate()`, `componentWillReceiveProps()`, and `shouldComponentUpdate()` will receive intermediate pending props which have not yet been flushed as `prevProps` and `nextProps`. However, `prevProps` in `componentDidUpdate()` will correspond to the last flushed props, so they might be older than the `prevProps` you got in `componentWillUpdate()`! All of this makes sense in isolation but may seem surprising.
* To sum it up, if your components don't do anything too funny in lifecycles, they should work fine in Fiber. Fiber does its best to match the current semantics of lifecycle methods even when that leads to strange consequences. However some components relying on exact lifecycle order might break with Fiber. This is fine, as it's going to be a major release and likely opt-in at first. Eventually we'll probably want to redesign lifecycle methods to be more declarative and more aware of the specific use cases (e.g. subscriptions, data fetching, DOM manipulation, etc).

#### Web Components, Properties and Attributes

* There is a good discussion about enabling event support for Web Components. ([#7901](https://github.com/facebook/react/issues/7901))
* It seems like the tides are shifting towards using properties over attributes, as properties are richer.
* We have an opportunity to make Web Components work better with React by adopting a "best practice" convention like the one [described here](https://github.com/webcomponents/react-integration).
* [Rob Dodson](https://github.com/robdodson) of Polymer helps drive the discussion.

#### Fiber Milestones

* We need an actionable plan for developing and shipping Fiber.
* We restructured an umbrella task for Fiber into "phases". ([#7925](https://github.com/facebook/react/issues/7925))

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/34).
