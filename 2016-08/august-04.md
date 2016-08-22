## August 4 ([discuss](https://github.com/reactjs/core-notes/pull/26))

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

* Participated in [React Application Architecture](https://twitter.com/soprano/status/759177157755019264) panel at [ForwardJS](https://forwardjs.com).
* Reviewing [Keyan](https://twitter.com/keyanzhang)’s pull request that adds a UI for displaying warnings with “snooze”. ([#7360](https://github.com/facebook/react/pull/7360))
* Also reviewing [Sebastian](https://twitter.com/sebmarkbage)’s [pull requests](https://github.com/facebook/react/pulls?q=is%3Apr+author%3Asebmarkbage+fiber+is%3Aclosed) for the new [“Fiber” reconciler](https://github.com/reactjs/core-notes/blob/master/2016-06/june-23.md#update-on-fiber).

#### Dan

* Shipped more updates to [Create React App](https://github.com/facebookincubator/create-react-app).
* There was more discussion about including Jest in the community.
* [Christoph](https://twitter.com/cpojer) is working super hard to [turn Jest perception around](https://github.com/facebookincubator/create-react-app/pull/250#issuecomment-237098619) and make it a good test runner.
* [Dan](https://twitter.com/dan_abramov) still has some concerns about Jest usability and will communicate them to [Christoph](https://twitter.com/cpojer) so they get fixed before Create React App officially includes testing.

#### Keyan

* Working on the new UI for warnings. ([#7360](https://github.com/facebook/react/pull/7360))
* Fixed an issue with inputs in mobile browsers. ([#7397](https://github.com/facebook/react/pull/7397))
* Also fixed a memory leak in server rendering in development. ([#7410](https://github.com/facebook/react/pull/7410))

#### Paul

* Shipped [React 15.3.0](https://github.com/facebook/react/releases/tag/v15.3.0).
* Working on internal codemods that remove code directly `import`ing modules from React on Facebook.com.
* Switched the documentation to use [npmcdn](https://npmcdn.com/#/). ([#7394](https://github.com/facebook/react/pull/7394))

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/26).
