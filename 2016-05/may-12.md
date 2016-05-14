## May 12 ([discuss](https://github.com/reactjs/core-notes/pull/14))

### Attendees

* [Alex](https://twitter.com/alex_frantic) (React Native)
* [Ben](https://twitter.com/soprano) (React)
* [Christoph](https://twitter.com/cpojer) (Jest)
* [Christopher](https://twitter.com/vjeux) (React Native)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Shayne](https://github.com/shayne) (React Native)
* [Tom](https://twitter.com/tomocchino) (React)

### Inline Styles Update

* [Christopher](https://twitter.com/vjeux) is going on a parental leave and will continue [his experiments](https://github.com/reactjs/core-notes/blob/master/2016-04/april-28.md#experimenting-with-stylesheetcreate-on-the-web) in July.
* Don’t forget that this is tied to Facebook build asset pipeline, and is not directly applicable to React.
* However lessons learned from this work may influence our thinking about inline styles in the future.

### Error Messages

* People have been complaining about [the lack of error messages in production React](https://github.com/facebook/react/issues/2686).
* Many of them aren’t actionable anyway, but some [can be useful](https://github.com/facebook/react/issues/2686#issuecomment-218017606).
* We might want to consider an [error code system](https://github.com/facebook/react/issues/2686#issuecomment-209171272).

#### Error Code System

* Babel transform annotates every callsite with a number that’s known statically.
* Sentry (and others!) can look up that number in a map.
* A new intern will be working on this!

### New Intern!

* Keyan will be working on the React team as an intern.
* [Ben](https://twitter.com/soprano) will be mentoring him.
* The plan is for him to work on the error code system described above.
* Another thing he might work on is a “yellow box” a la React Native.

#### Yellow Box

* Where should it go? fbjs?
* Could be a more effective vector for communication between the React core team and users of React than console warnings.
* To be practical, we would need to have warning levels and some way of suppressing them.
* This is just an idea, the details would need to be fleshed out.

### `shouldComponentUpdate()` Breaks Context

* A [longstanding issue](https://github.com/facebook/react/issues/2517) with a very long thread.
* [Sebastian](https://twitter.com/sebmarkbage) has been thinking about this (just this morning!)
* With the [incremental reconciler](https://github.com/facebook/react/issues/6170), we think we’ll solve this.

#### Can We Fix It Now?

* It will make things a lot more inefficient.
* Only some libraries use context for dynamically updating values, but enabling deep subscriptions by default will hurt performance for everyone.

#### Hacky Workaround

* For now, React Router 3.0 adds a hacky [workaround](https://github.com/reactjs/react-router/blob/5f3387a91d427aec1368e68cd9605797aa076bb7/modules/ContextUtils.js).
* [@taion](https://github.com/taion) plans to pull it out in a generic module for other affected libraries.
* Nobody is really happy about it, but hopefully it should be easy to pull it out later.
* It [uses mixins](https://github.com/reactjs/react-router/issues/3439#issuecomment-217887475) so it’s easier to pull it out, and it doesn’t trash React DevTools view.
* Hopefully eventually React fixes this, and React Router can <s>unpublish</s> stop using that package.

### Incremental Progress vs Long-Term Vision

* Long-term ideas and features often block incremental and external contributions.
* We might want to spend more time just supporting features the community is asking for, even if we don't use them.
* One concern is that the proposed solution often will leave us in a worse place than where we were before.
* This is often not obvious in the beginning, and unfortunately a lot of work may get done before we realize this.

#### Focus on One Thing

* Maybe as a team we can focus on one area at a time.
* For example, let’s just do one thing, do it well, and ship it.
* Better than letting ourselves get overwhelmed.

#### Avoid Wasted Effort

* We can focus on external needs, but we also need to make sure that external folks are willing to support our needs internally.
* This requires that we better communicate our needs and priorities.
* There’s a long unwritten list of constraints, and we often reactively provide that list.
* But it’s hard for contributors to know before they work on their big PR what that list is.

#### RFCs

* We should adopt an RFC process!
* Long discussions should start before folks submit a PR.
* In some cases, they can start after, but not in the PR itself.
* Let’s use the [Rust](https://github.com/rust-lang/rfcs/blob/master/libs_changes.md#is-an-rfc-required) / [Ember](https://github.com/emberjs/rfcs#when-you-need-to-follow-this-process) RFC process.

### Snapshot Testing

* [Cristian](https://github.com/kentaromiura) in London is working on [snapshot testing](https://github.com/facebook/jest/pull/1000) in Jest.
* [Ben](https://twitter.com/soprano) has been prototyping a full React test renderer that can render everything both on React Native and DOM.
* Unlike shallow renderer, it is stateful and renders deeply.
* Things won’t actually render to React Native or to the DOM, but rather to an intermediate representation.
* This will give us the ability to diff representations.
* (Basically we’re pretty-printing JSX and then doing textual diffs.)
* It is not clear if the intermediate representation should include information about composite components (the “DevTools tree”).
* Maybe this could be configurable.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/14).
