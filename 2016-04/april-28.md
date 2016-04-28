## April 28 ([discuss](https://github.com/reactjs/core-notes/pull/10))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Christopher](https://twitter.com/vjeux) (React / React Native)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Shayne](https://github.com/shayne) (React Native)
* [Tom](https://twitter.com/tomocchino) (React)

### Release Process and React Native

#### We want to release to React Native more frequently

* Can we push more frequently like we do with the Facebook website?
* What if we ship React minor releases (or patch releases) every two weeks?
* We should be using a public stable release of React (either a minor or patch) on the website.
* This would coincide with the React Native release process.

#### React Native users have way more third-party dependencies

* These won’t be compatible with “pre-release” or bleeding edge versions of React.
* The only people that use RC are folks that have something that was fixed (usually by them) in the RC.
* Otherwise, upgrading so frequently is incredibly draining.

#### Should we have feature flags, like Ember does?

* Maybe this would help catch regressions earlier.
* On the other hand, this causes an explosion of possible build configurations.

#### If we’re releasing more frequently we need to be testing React Native more

* We need to be testing the React release in React Native.
* Everyone on the team needs to have a working React Native setup on their machines.

#### Should we publish nightly releases?

* Can React Native lock itself into whatever nightly it wants?
* But we don’t want React Native to be pegged to a specific commit.
* This is pretty much what we started doing in 15.x with `alpha` releases for patches.

#### Current plan

* Going to publish `alpha`s, which can be released as frequently as we want, even like 4 a day.
* Once something is stable and we’re confident it's working in React Native, we’ll cut an actual release.
* React Native and Relay always reference a stable release in their dependencies.

#### What will our messaging be about alphas?

* Alpha = use at your own risk.
* If you depend on an alpha due to an urgent fix you need, pin it to a specific version.
* Guidance should be “never publish anything to npm with an alpha dependency”.

#### Open question: where does the breaking change development happen?

* Are we on `15.1.0-dev` or `16.0.0-dev`?
* Do we merge breaking changes to master?
* Currently we cherry-pick commits to `15-stable` but this is frustrating because 99% changes are not breaking.
* Need to discuss more, no conclusion yet.

### Experimenting with `StyleSheet.create()` on the web

* [Christopher](http://twitter.com/vjeux) continues experimenting with `StyleSheet.create()` on the Facebook website codebase.
* He made a proof of concept compiling these calls into CSS sheets compatible with Facebook internal asset pipeline.
* Maintaining correct specifity with `StyleSheet.create()` is not an easy problem, but it may be solved by throwing errors early during development when there is a potential specificity issue, and providing a clear way for the developer to work around it.
* Compiling `StyleSheet.create()` to emitting real CSS files through our internal asset pipeline lets us move a bit closer to experimenting with real inline styles without having to bet on them right now.
* Nothing is certain, and Christopher will continue experimenting this month.
* If it doesn’t turn out to be valuable, this will not make it into React! Don’t get too excited.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/10).
