## May 26 ([discuss](https://github.com/reactjs/core-notes/pull/17))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Christopher](https://twitter.com/vjeux) (React Native)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Shayne](https://github.com/shayne) (React Native)
* [Tom](https://twitter.com/tomocchino) (React)

### ES2016 Classes

#### Class Property Initializers ([proposal](https://github.com/jeffmo/es-class-fields-and-static-properties))

* ES classes for React components don’t feel good without them.
* We haven’t used them internally at Facebook enough to push externally.
* For now, we’ll push for more internal adoption of ES classes.
* We don’t want to hinder the proposal by pushing too hard for it now.
* After the proposal is further along, we can update our internal code and start pushing externally.

#### Documentation and Tutorial

* We need to figure out how to make the docs reflect the fact that you can use either `createClass` or ES classes.
* Proposal: the docs will continue to show `createClass` as the default, but will include a switcher to show examples using classes.
* Eventually, we will flip the default.
* In the tutorial we’ll start out introducing functional components (using function declarations).
* [Dan](https://twitter.com/dan_abramov) and [Paul](https://twitter.com/zpao) will work on this.

#### What About Mixins?

* Technically you can use [this approach](https://www.npmjs.com/package/es6-react-mixins) for mixins with ES classes.
* We won’t officially recommend it though because we think existing use cases for mixins have better solutions.
* We’ll start by getting rid of mixins in the Facebook codebase.
* Then we’ll write a page detailing how to get rid of different kinds of mixins.

#### Higher Order Components ([article](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750))

* They solve some of the mixin use cases.
* We should post about them in the official React blog and/or documentation.
* They have their own problems, such as not proxying methods.
* One solution would be to [allow forwarding callback refs](https://github.com/facebook/react/issues/4213).
* Not clear if we want this, but it would make higher order components more convenient to use.

### `ReactTestUtils` and Incremental Reconciler

* [Incremental reconciler](https://github.com/facebook/react/issues/6170) is going to be asynchronous.
* However `ReactTestUtils.renderIntoDocument()` is synchronous.
* It is not entirely clear if test utils should emulate a simpler always-sync environment, or real world.

### Error Codes

* [Keyan](https://twitter.com/keyanzhang) continues work on the PRs that let people decode error messages:
  - [#6874](https://github.com/facebook/react/pull/6874)
  - [#6882](https://github.com/facebook/react/pull/6882)

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/17).
