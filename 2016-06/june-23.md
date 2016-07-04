## June 23 ([discuss](https://github.com/reactjs/core-notes/pull/21))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Jim](http://github.com/jimfb) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Update on `createClass` → ES classes

* [Dan](https://twitter.com/dan_abramov) finished working on a codemod for internal Facebook code that converts 800 files to remove one of the common mixins we used.
* While doing so, Dan found an issue with inconsistent order of resolving refs during updates.
* Ideally code should not depend on ref resolution order.
* Unfortunately some Facebook components rely on it so for now we [fixed this in React](https://github.com/facebook/react/pull/7101).

### JSON Test Renderer

* [Ben](https://twitter.com/soprano) added a [new test renderer intended for snapshot testing](https://github.com/facebook/react/pull/6944).
* For now, we don’t document it, as we might want to change the API.
* We *don’t* want people to rely on the renderer output or test against JSON.
* This renderer is *only* intended for comparing snapshots, not analyzing them.
* It is also not clear how to dispatch events with it.
* Jest plans to add a guide on using it later on [its blog](https://facebook.github.io/jest/blog/) after it is more stable.

### Update on 15.2.0

* We cut the RC last week and React Native RC uses it.
* It contains a lot of commits but not too many substantial changes.
* Will be released within two weeks.

### Update on Release Process

* [Paul](https://twitter.com/zpao) started writing a maintainer’s guide to document the entire release process.
* He ran the 15.2.0 RC release using a new tool he’s working on.
* The process relies on us assigning semver labels (e.g. “major”, “patch”) but not specific milestones.
* The tool will automate the release process based on those labels.
* This should enable us to cut releases more often and let other people (e.g. React Native members) do it.

### Fast Path

* This is a hypothetical optimization [Jim](http://github.com/jimfb) wanted to try.
* What if we took functional components that render only to DOM components and precompiled them to fast path “templates”?
* This could be an optimization specific to the DOM renderer. It would use `document.createElement` or `cloneNode()`.
* However most components use other components so it’s unclear if there are any benefits to doing this.
* [Sebastian](https://twitter.com/sebmarkbage) had a more generic idea about component folding but it requires whole program analysis.
* There is nothing conclusive here and this is not something we actively investigate.

### Testing with Feature Flags

* We currently test server rendering by enabling the client side renderer to do server side rendering ([we set `useCreateElement` to `false` and re-run the suite](https://github.com/facebook/react/blob/24dfb56113a214d98f29f69e2c26f67d7e947067/.travis.yml#L80-L81)).
* We’d like to decouple client side from server side rendering.
* [Sebastian](https://twitter.com/sebmarkbage)’s experimental “Fiber” reconciler does not yet support server rendering.
* We need to split out server rendering before switching to Fiber.

### Update on [Fiber](https://github.com/facebook/react/pulls?q=is%3Apr+fiber+is%3Aclosed)

* This is [Sebastian](https://twitter.com/sebmarkbage)’s work on [new core algorithm](https://github.com/facebook/react/issues/6170).
* Its main goal is to render tree in chunks to avoid dropping frames on large updates.
* It sort of works but far from feature parity.
* Need to add support for a lot of things: lifecycle, refs, state.
* It should be possible to keep `ReactDOM` and `ReactDOMFiber` separate.
* It would be great to test it in isolation on a single product.

### Flow with Property Initializers

[Jeff](https://twitter.com/lbljeffmo) will release a Flow version that infers the types from the initializers so we can write the types inline instead of specifying the type of the whole expression:

```js
class Foo {
  doStuff = (x: number): boolean => {
    return true;
  };
}
```

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/21).
