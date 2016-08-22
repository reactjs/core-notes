## July 21 ([discuss](https://github.com/reactjs/core-notes/pull/24))

### Attendees

* [Ben](https://twitter.com/soprano) (React)
* [Christopher](https://twitter.com/vjeux) (React)
* [Dan](https://twitter.com/dan_abramov) (React)
* [Keyan](https://twitter.com/keyanzhang) (React, intern)
* [Paul](https://twitter.com/zpao) (React)
* [Sebastian](https://twitter.com/sebmarkbage) (React)
* [Tom](https://twitter.com/tomocchino) (React)

### Hackathon

* Team members worked on tangential/random projects last week.
* [Sebastian](https://twitter.com/sebmarkbage) showed a demo of text layout in JS.
* [Dan](https://twitter.com/dan_abramov) and [Christopher](https://twitter.com/vjeux) introduced [Create React App](https://github.com/facebookincubator/create-react-app).

### Update on `createClass` Codemod

* We are continuing work on moving Facebook.com codebase away from `createClass`.
* Discovered an issue with automocking of bound functions working differently, fixing the internal tests manually.
* [`PureComponent`](https://github.com/facebook/react/pull/7195) didn’t quite work in Flow, fixed in [0.30.0](https://github.com/facebook/flow/releases/tag/v0.30.0).
* Plan to run the [`createClass` codemod](https://github.com/reactjs/react-codemod#class) on Facebook.com codebase this weekend.
* It touches 1/7 of all files in the Facebook.com JS codebase!

### Introducing [Create React App](https://github.com/facebookincubator/create-react-app)

* Started at a hackathon last week.
* Ready to release tomorrow with a live stream.
* Using `import` for CSS is somewhat controversial.
* [Ben](https://twitter.com/soprano) is concerned that it is non-standard.
* [Dan](https://twitter.com/dan_abramov) and [Christopher](https://twitter.com/vjeux) think upsides of using one bundler for all assets outweigh the downsides.
* We’ll add a note to the [howto](https://github.com/facebookincubator/create-react-app/blob/master/template/README.md#adding-a-stylesheet) explaining how this works, and that it is not required for React.
* We don’t have this problem at Facebook because we have a custom CSS pipeline, but we aren’t entirely happy with it either.

### React Release Manager

* [Paul](https://twitter.com/zpao) is getting close to finishing React Release Manager.
* The goal is to make it easy for anyone to release a new version of React.
* It automates all the steps we are doing before every release so React Native folks or community members can cut releases.
* It has a slick interactive CLI!
* If you’re curious, there’s a README [here](https://github.com/facebook/react/blob/73f24269493bad75b64e8417675c1d76f6007ef0/scripts/release-manager/Readme.md).

------------

Please feel free to discuss these notes in the [corresponding pull request](https://github.com/reactjs/core-notes/pull/24).
