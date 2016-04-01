## March 31

### Fostering external collaboration

#### What would a React roadmap look like?

* Need to document “what we want” so we have something to point back to
* Either a single document (roadmap?), or a set of issues with tags
* Suggestion: create a separate repo for RFCs (like Ember)

#### PRs should not get stale

* Closed a bunch of old PRs recently
* If we don’t want something, we should close it sooner and communicate why
* Major source of confusion is that no one knows which release a particular PR or issue is a priority for
* Having a roadmap would help this tremendously, but even if we don’t have one, just tagging PRs with milestones would help ensure timely responses, etc

#### Linking to PRs from our release notes

* Makes sense for high level things
* For bugs and whatnot, this might be super noisy
* Could boost morale for contributors
* Right now it’s hard to compare the difference between different versions, this could help
* We’ll try it for the v15 release notes and see how it feels

### Releasing 15

* A few blockers related to `setAttribute`:
  * https://github.com/facebook/react/issues/6219
  * https://github.com/facebook/react/issues/6119
* Paul is going to write up a final tracking issue
* Final 15 should be released next week

### Separating Addons

* We don’t use them much internally, and have been letting feature requests and issues get stale
* How do we separate them?
  * If we move them to a different repo we will never look at it again
  * We don’t currently look at them, but we at least feel guilty about it
  * Should we be less afraid to disown code?
* `update()` is simple because it’s tiny
* `ReactTransitionGroup` is really complicated
* Have to figure out the logistics here, but we’re going to move them into their own [reactjs](http://github.com/reactjs) repo
  * If there’s already something better, we should link to that instead

### Trying JavaScript Styles in Internal Facebook Infra

* There are *tons* of different ways to render JS styles (see Radium, CSS Modules, React Native Web, etc)
* One of the biggest things we need to figure out is performance
* Chris is experimenting with converting internal transforms at Facebook to output JS instead of CSS
* The plan is to convert some of the Facebook products to use JS styles and profile different approaches
* If there are good results we might eventually consider supporting something like this in React DOM
* **This work is tied to internal infra, is very experimental, and might not give any results**
