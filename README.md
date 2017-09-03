# Polymer Local Storage demo app

This app demoes an issue with the [WebComponents polyfill](https://github.com/webcomponents/webcomponentsjs/) introduced in the version 1.0.8. The issue causes the app to fail in IE11. Most likely, the root cause is closure-compiler/#2640, but for some reason the issue did not surface with the polyfill versions 1.0.7 and before.

## Run the demo locally

First, make sure you have [Node](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) installed. Then clone the repo and run `yarn install` to get all dependencies loaded.

Build the application with `yarn build` and then start with `yarn start`. The app will start at http://localhost:8081.

## Check the online demo

The online demo is deployed to this repo's GitHub pages: https://vlukashov.github.io/polymer-local-storage/.

## Issue details

When viewing the app in Internet Explorer 11, it fails to load at `Polymer.AppStorageBehavior._enqueueTransaction`:
```javascript
return this.__transactionQueueAdvances = this.__transactionQueueAdvances.then(transaction).catch(function (error) {
  this._error('Error performing queued transaction.', error);
}.bind(this));
```

The error in console says: `Object doesn't support property or method 'catch'`.


## Workaround

Pin the version of the WebComponents polyfill to 1.0.7 or below.
