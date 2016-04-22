## April 21 ([discuss](https://github.com/reactjs/core-notes/pull/6))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Shayne](https://github.com/shayne) (React Native)
* [Tom](https://twitter.com/tomocchino) (React)

### 15.0 Post Mortem

#### Release was pretty rocky
* We didn’t have a cohesive enough story around what was to be included in the release.
* Now that we have more dependants (RN, many teams internally and externally) it’s becoming an issue.
* Examples of changes that should we should have planned better:
  * [SVG attributes were passed through without a whitelist in RC1](https://github.com/facebook/react/pull/5714), then [we reverted this in RC2](https://github.com/zpao/react/commit/08fa7fe50707d4c7fe06861e0875b3fab00ea048).
  * We [switched to using attributes](https://github.com/facebook/react/pull/1510) by default but haven’t tested this as thoroughly as we should have, and it caused a few regressions, plus later it turned out that we didn’t all agree on this change ([Sebastian](https://twitter.com/sebmarkbage) was out of the loop).
* Our default in the past has been to just work on everything individually.
  * [Ben](https://twitter.com/soprano) created a special GitHub group so that we can auto-subscribe all of us to some big picture issues.
* We should have shipped an RC3.
  * But why did we get to RC2?
  * Having browser tests ([Jim](https://github.com/jimfb)) and planning releases ([Paul](https://twitter.com/zpao)) more thoroughly should fix this.
* We should make the release process easier.
  * Right now there’s too much manual work involved.
  * If it was just one command, maybe we would have been more open to releasing RC3.

### Releasing 15.0.2

* Either this Friday or early next week.
* We merged some changes to [bring the `react-native-renderer` into the React repo](https://github.com/facebook/react/pull/6338) so we can change React internals more freely without breaking RN.
* What else should get into 15.0.2?
  * [Fix for the `optgroup`s](https://github.com/facebook/react/pull/6442).
  * [CSS warning fix](https://github.com/facebook/react/pull/6458).
  * [TestUtils fix](https://github.com/facebook/react/pull/6362).
* Right now we just run master on Facebook.
* In six months, master and 15.x can diverge significantly.
* We need to figure out a better story around syncing React with:
  * The Facebook website.
  * React Native.
* [Paul](https://twitter.com/zpao) will write up how we’re going to do releases moving forward.

### Universal Components

* [Nicolas](https://github.com/necolas) from Twitter created [React Native Web](https://github.com/necolas/react-native-web).
* [Leland](https://github.com/lelandrichardson) from Airbnb maintains [a fork](https://github.com/lelandrichardson/react-native-web).
* It is not clear how to create universal components.
* For example, if you depend on `View` from `react-native`, you pull in the whole `react-native`.
* How do you create a component that is renderable both in React Native and React Native Web?
  * Some registration system?
  * Injectable components?
  * Strings?
* No conclusion, lots to think about.

### Adding Flow to React

* Flow has helped engineers at Facebook immensely, and it might help us here:
  * WeЪd like to be more confident in the changes we want to make.
  * Might help newcomers be more comfortable making changes in the codebase.
  * [Ben](https://twitter.com/soprano) might experiment with adding it in some places, but we might want to hold off.
* [Sebastian](https://twitter.com/sebmarkbage)’s concerns:
  * [The work on incremental reconciler](https://github.com/facebook/react/issues/6170) is going to be very invasive.
  * Forcing addition of Flow in places where it’s very hard to type should be a non-goal as there’s a lot of meta-programming.

### Who’s Working on What

* [Ben](https://twitter.com/soprano): Working on some education material for React that could end up in the docs.
* [Dan](https://twitter.com/dan_abramov): After a chat with Sebastian, [submitted another PR](https://github.com/facebook/react/pull/6549) for the future ReactPerf and DevTools revamp. 
* [Jim](http://github.com/jimfb): Mostly still fixing regressions.
* [Paul](https://twitter.com/zpao): [Flat bundles](https://github.com/facebook/react/issues/6351), modernizing our build process, thinking about the new release process.
* [Sebastian](https://twitter.com/sebmarkbage): Bug fixes to make React Native to work with React 15.
* [Shayne](https://github.com/shayne): React Native relies on npm, so we need a better way of consuming npm modules internally at Facebook.


------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/6).
