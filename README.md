[![power-assert][power-assert-banner]][power-assert-url]

[![Build Status][travis-image]][travis-url]

`babel-plugin-empower-assert` is a [Babel](https://babeljs.io/) plugin to convert [assert](https://nodejs.org/api/assert.html) to [power-assert](https://github.com/power-assert-js/power-assert) at compile time.


INSTALL
---------------------------------------

```
$ npm install --save-dev babel-plugin-empower-assert
```


HOW TO USE
---------------------------------------


### via [Babel CLI](http://babeljs.io/docs/usage/cli/)

```
$ babel --plugins babel-plugin-empower-assert /path/to/src/target.js > /path/to/build/target.js
```

or shortly,

```
$ babel --plugins empower-assert /path/to/src/target.js > /path/to/build/target.js
```


### via [Babel API](http://babeljs.io/docs/usage/api/)

```javascript
var babel = require('babel-core');
var jsCode = fs.readFileSync('/path/to/src/target.js');
var transformed = babel.transform(jsCode, {
    presets: [...],
    plugins: ['babel-plugin-empower-assert']
});
console.log(transformed.code);
```


### via [.babelrc](http://babeljs.io/docs/usage/babelrc/)

```javascript
{
  "presets": [
    ...
  ],
  "env": {
    "development": {
      "plugins": [
        "babel-plugin-empower-assert"
      ],
    }
  }
}
```

```
$ babel /path/to/src/target.js > /path/to/build/target.js
```


EXAMPLE
---------------------------------------

For given `math.js` below,

```javascript
'use strict';

var assert = require('assert');

function add (a, b) {
    assert(!isNaN(a));
    assert.equal(typeof b, 'number');
    assert.ok(!isNaN(b));
    return a + b;
}
```

Run `babel` with `--plugins empower-assert` to transform code.

```
$ babel --plugins empower-assert /path/to/demo/math.js > /path/to/build/math.js
```

You will see `assert` is converted to `power-assert`.

```javascript
'use strict';

var assert = require('power-assert');

function add(a, b) {
    assert(!isNaN(a));
    assert.equal(typeof b, 'number');
    assert.ok(!isNaN(b));
    return a + b;
}
```


AUTHOR
---------------------------------------
* [Takuto Wada](https://github.com/twada)


LICENSE
---------------------------------------
Licensed under the [MIT](http://twada.mit-license.org/) license.


[power-assert-url]: https://github.com/power-assert-js/power-assert
[power-assert-banner]: https://raw.githubusercontent.com/power-assert-js/power-assert-js-logo/master/banner/banner-official-fullcolor.png

[travis-url]: https://travis-ci.org/twada/babel-plugin-empower-assert
[travis-image]: https://secure.travis-ci.org/twada/babel-plugin-empower-assert.svg?branch=master
