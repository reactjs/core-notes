## July 28 ([discuss](https://github.com/reactjs/core-notes/pull/25))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Christopher](https://twitter.com/vjeux) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Kevin](https://twitter.com/lacker) (Developer Advocacy)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Individual Updates

#### Ben

* Ran the [`createClass` codemod](https://github.com/reactjs/react-codemod#class) on the Facebook.com codebase.
* ES6 class usage is up from 30% to 80% in it!
* More good news: [Public Class Fields](https://github.com/tc39/proposal-class-public-fields) (aka “Class Properties”) ES proposal has [advanced to Stage 2](https://github.com/tc39/proposals).

#### Paul

* Continued work on the [React release manager](https://github.com/reactjs/core-notes/blob/master/2016-07/july-21.md#react-release-manager).
* Busy reviewing two pull requests: one from [Keyan](https://twitter.com/keyanzhang) and one from [Sebastian](https://twitter.com/sebmarkbage).
* [Keyan](https://twitter.com/keyanzhang)’s pull request [changes React build process to use Rollup](https://github.com/facebook/react/pull/7178).
* [Sebastian](https://twitter.com/sebmarkbage)’s pull request [significantly changes how React packages are bundled internally](https://github.com/facebook/react/pull/7168).
* Unfortunately those changes conflict, and we are going with [Sebastian](https://twitter.com/sebmarkbage)’s pull request first.
* See the section below explaining these changes in more detail.

#### Dan

* Released [Create React App](https://github.com/facebookincubator/create-react-app).
* Lots of positive feedback.
* Working on 0.2.0 that fixes issues with cloud editors and busy ports.
* Missing features for calling it 1.0: testing, [proxying API requests](https://github.com/facebookincubator/create-react-app/blob/master/template/README.md#proxying-api-requests-in-development).
* We merged [Jest support](https://github.com/facebookincubator/create-react-app/pull/250) but people are concerned because it lost a ton of community trust in the first year.
* We want to use Jest because we’re excited about [Snapshot Testing](https://facebook.github.io/jest/blog/2016/07/27/jest-14.html) and are committed to improving Jest.
* [Dan](https://twitter.com/dan_abramov) will make sure the testing experience is good before releasing it officially.

#### Kevin

* React never had people working on developer advocacy and community outreach.
* We feel it is time to improve this, and [Kevin](https://twitter.com/lacker) will help us.
* He already worked on [revamping React Native docs](https://facebook.github.io/react-native/docs/getting-started.html) which was highly successful.
* Things that need addressing: React docs, GitHub issue management.

### Changes to Bundling

* Sebastian prepared a series of PRs that *really* split `react` and `react-dom` packages. ([#7164](https://github.com/facebook/react/pull/7164), [#7168](https://github.com/facebook/react/pull/7168), [#7173](https://github.com/facebook/react/pull/7173))
* `react-dom` package implementation used to live inside of `react` package for legacy reasons.
* Now they are separated: `react` only contains “renderer-agnostic” things like `React.Component`, `React.createElement`, and `React.Children`.
* This is still work in progress, and there are many weird hacks we have to do, but we’ll reduce them over time.

#### Plan for Reconcilers and Renderers

* Paradoxically, `react` package won’t include the React algorithm (“reconciler”) anymore.
* For example, `React.createElement()` and `React.Component` stay there, but not the reconciler itself.
* This makes sense because components relying on `react` don’t actually care how reconciler is implemented.
* The React reconciler will exist in renderer packages such as `react-dom` and `react-native`.
* Since almost nobody uses two renderers at the same time, each renderer will use a *copy* of the reconciler code.
* This makes it possible for `react-native` and `react-dom` to move at different speeds and temporarily “fork” the reconciler code if needed.
* This also makes it possible for `react-dom` to offer the new experimental [“Fiber” reconciler](https://github.com/reactjs/core-notes/blob/master/2016-06/june-23.md#update-on-fiber) behind a flag without changing all the third-party components that depend on `react`.
* This sounds confusing but we think it’ll work better in practice.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/25).
