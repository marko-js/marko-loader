marko-loader
============

A [marko](http://markojs.com/) template loader for [webpack](https://github.com/webpack/webpack).

## Installation

Install required packages:

```bash
npm install marko --save
npm install marko-loader --save-dev
```

And then register the marko loader in your webpack configuration file:

_webpack.config.js:_

```javascript
const options = {
    // ...
    module: {
        loaders: [
            { test: /\.marko$/, loader: 'marko-loader' }
        ]
    }
};

module.exports = options;
```

## Usage

With this loader installed, you can then require `./template.marko` files as shown below:

_./template.marko:_

```xml
<div>
    <h1>Hello ${data.name}!</h1>
</div>
```

_./index.js:_

```javascript
var template = require('./template.marko')
var html = template.renderToString({ name: 'Frank' });
```

### Compilation target

`marko-loader` will automatically detect your webpack target and output the appropriately compiled Marko code.
If you wish to override this behaviour simply add the `target` field in the options for this loader.

### Hydrate & dependencies for server-rendered pages

When rendering a Marko template serverside, only components that can re-render need their full template in the browser.
This loader supports only loading the needed parts to hydrate with two options:

- `?dependencies` includes only the dependencies that are needed in the browser (css, dynamic components)
- `?hydrate` includes these dependencies and also kicks off hydration & component initialization

_webpack.config.js:_
```js
module.exports = {
    entry: "./path/to/page.marko?hydrate",
    /* ... */
}
```

## Additional resources

- Sample app: [marko-webpack](https://github.com/marko-js-samples/marko-webpack)

## License

MIT
