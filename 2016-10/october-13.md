## October 13 ([discuss](https://github.com/reactjs/core-notes/pull/33))

### Attendees

* [Dan](https://twitter.com/dan_abramov) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Team Changes

* [Jim](https://github.com/jimfb) has left Facebook to pursue other projects. Thanks to Jim for all his hard work and contributions!
* [Paul](https://twitter.com/zpao) has left the React team to work on open source infrastructure at Facebook. Thanks to Paul for all the thankless work triaging issues and managing the release process!
* [Christopher](https://twitter.com/vjeux) has switched to working on developer experience in Nuclide. Thanks to Christopher for his work on the React team (including inspiring and starting Create React App)!
* [Andrew](http://twitter.com/acdlite) is going through the Bootcamp and will join the React team soon.

The React core team now consists of:

* [Andrew](https://twitter.com/acdlite)
* [Ben](https://twitter.com/soprano)
* [Dan](https://twitter.com/dan_abramov)
* [Sebastian](https://twitter.com/sebmarkbage)
* [Tom](https://twitter.com/tomocchino) (manager)

### Discussion

#### Next Focus: Shipping Fiber

We are shifting our focus and will spend the rest of the year working on [Fiber](https://github.com/facebook/react/issues/6170). This means we won't be working on JavaScript styles as originally planned. It seems like Fiber is our best shot at fixing many long-standing issues with React, and we are going to place all our effort into either replacing existing reconciler with Fiber, or failing spectacularly with it (and learning from that).

#### New React Docs

* Dan published [Codebase Overview](https://facebook.github.io/react/contributing/codebase-overview.html) and [Implementation Notes](https://facebook.github.io/react/contributing/implementation-notes.html) as he planned for a long time.
* Andrew, Ben, Dan, [Héctor](https://github.com/hramos), [Eric](https://twitter.com/ericnakagawa), and [Kevin](http://twitter.com/lacker) are working on the new documentation for the React website ([#7864](https://github.com/facebook/react/pull/7864)). We rewrote all of the introductory content to use modern APIs and consistent terminology, and also rewrote some of the advanced content. Ben wrote a new tutorial that we've been using internally at Facebook for a while. Kevin drives this effort, will land next week.

#### Releasing 15.4.0

* Sebastian separated `React` from `ReactDOM` in [#7164](https://github.com/facebook/react/pull/7164) and this will get into 15.4.0.
* This means that projects reaching into `react/lib/*` (which was never supported!) will break.
* We published an RC and ask people to try it and file issues with breaking projects. ([#7770](https://github.com/facebook/react/issues/7770#issuecomment-253899837))

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/33).
