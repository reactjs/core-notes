## June 2 ([discuss](https://github.com/reactjs/core-notes/pull/18))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Jim](http://github.com/jimfb) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Shayne](https://github.com/shayne) (React Native)
* [Tom](https://twitter.com/tomocchino) (React)

### Getting Rid of `PureRenderMixin`

* This is one of the most commonly used mixins.
* We need to have a good story around applying it to classes and SFCs (**stateless functional components**).
* Let’s consider a few alternatives.

#### Proposal 1: `PureComponent` and heuristics for SFCs

* Create `React.PureComponent` base class (kinda like a class with `PureRenderMixin`).
* Make SFCs “inherit” their purity from the closest class-based parent.
* This works because if the class above is pure, SFC wouldn’t re-render anyway.
* Implemented in [#6914](https://github.com/facebook/react/pull/6914) with some additional explanation [here](https://github.com/facebook/react/pull/6914#issuecomment-222364942).

##### Concerns

* Any heuristics based model will probably not work in 100% of cases, and could cause confusion.
* If you pass children through, you don’t know anything about them, including whether they use mutation.

##### Potential Mitigations

* Warn if a `PureComponent` takes in a child element (or child element which changes).
* In dev mode, do dry-run reconciliation past all `shouldComponentUpdate`s and warn if `shouldComponentUpdate` lied to React.

#### Proposal 2: SFCs Always Shallowly Compare Props

* Effectively a `PureRenderMixin` on every SFC.

##### Concerns

* Means that component authors generally can’t / shouldn’t use SFCs because `PureRenderMixin` shouldn’t be used with components that take children.
* Intuitively, people expect SFCs to behave like functions. The bailout would be surprising, and there isn’t a particularly good way of discovering why the function isn’t behaving like a normal JavaScript function.
* Performance. It’s not clear that adding `PureRenderMixin` to every SFC would actually improve overall performance (because it means extra reads/compares, retaining objects longer and into subsequent GC generations, etc).

#### Proposal 3: `createPureElement`

* Provide some flag on components at the calling side to denote that they should be pure.
* This would tell React to effectively “use `PureRenderMixin`” on that particular instance, *not all instances*.
* Many syntax possibilities: `pure={true}`, or `<*Component />`, `React.createPureElement()`, etc.

### ES Class Progress

* [Ben](https://twitter.com/soprano) is leading the effort to port Facebook codebase to ES classes.
* We plan to enable property initializer syntax internally, and codemod all methods except lifecycles to it.

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/18).
