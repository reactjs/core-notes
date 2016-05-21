## May 19 ([discuss](https://github.com/reactjs/core-notes/pull/15))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Christopher](https://twitter.com/vjeux) (React Native)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### `createClass()` vs ES2015 Classes

#### Why Use Classes?

* `createClass()` API feels outdated, and can be implemented entirely in userland if needed.
* ES6 classes are less of an API, possibly simpler.
* ES6 classes are friendlier to static analysis.
* ES6 classes offer performance improvements in large apps.
* We are in the business of UI components, not type systems.

#### What’s Holding Us Back?

##### Autobinding

* [Class properties](https://github.com/jeffmo/es-class-fields-and-static-properties) solve this.
* However they’re not moving forward at TC39 yet as [Jeff](https://github.com/jeffmo) is busy preparing for React Europe.
* Downside: nobody wants experimental syntax in the documentation.
* We could just always bind in constructor in the documentation.

##### Mixins

* A lot of components on Facebook website still use mixins, but mostly the same ones.
* If we decided to deprecate `createClass` in the future, we would need to fix them first.
* Possible temporary workaround: apply them on top of ES6 class like [react-mixin](https://github.com/brigand/react-mixin) does.

#### Next Steps

* We should update the documentation to use ES6 classes and functional components wherever possible.
* Eventually we should deprecate `createClass`, possibly move it into a separate package.
* We need to have a good solution for folks who don’t want to use a transpiler.

### Separating Out `PropTypes`

* [Jordan](https://twitter.com/ljharb) and some Airbnb folks asked about separating `PropTypes` into a generic validation library.
* One concern might be that as a separate project `PropTypes` could become incompatible (as a type system) with Flow or TypeScript.
* Internally long term we’d like to avoid `PropTypes` usage and rely on static typing instead.
* Some checks can’t easily be expressed statically (e.g. ranges or colors).
* Conclusion: anyone can take `PropTypes` code and put it on npm.
* If it enforces a generic enough contract, we might try to replace `PropTypes` with it in the future, but no guarantees.
* Our internal plan will be to focus on ES6 classes and Flow.

### New Release Proposal

* React Native is releasing RC, so [we’re shipping 15.1.0](https://github.com/facebook/react/blob/619b3e850998ad24b9750c83ca20bb95e7638957/CHANGELOG.md#1510-may-20-2016).
* Originally we planned to ship 15.0.3 and 15.1.0, but we don’t plan to maintain two branches anyway, so not worth doing now.
* We will release React versions every two weeks, a couple of days before React Native RCs.
* We might start using [Lerna](https://lernajs.io), it works great for Babel.
* Do we ship from a branch or from master? No conlusion yet.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/15).
