# @zibuthe7j11/porro-quasi-at <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Define multiple non-enumerable properties at once. Uses `Object.defineProperty` when available; falls back to standard assignment in older engines.
Existing properties are not overridden. Accepts a map of property names to a predicate that, when true, force-overrides.

## Example

```js
var define = require('@zibuthe7j11/porro-quasi-at');
var assert = require('assert');

var obj = define({ a: 1, b: 2 }, {
	a: 10,
	b: 20,
	c: 30
});
assert(obj.a === 1);
assert(obj.b === 2);
assert(obj.c === 30);
if (define.supportsDescriptors) {
	assert.deepEqual(Object.keys(obj), ['a', 'b']);
	assert.deepEqual(Object.getOwnPropertyDescriptor(obj, 'c'), {
		configurable: true,
		enumerable: false,
		value: 30,
		writable: false
	});
}
```

Then, with predicates:
```js
var define = require('@zibuthe7j11/porro-quasi-at');
var assert = require('assert');

var obj = define({ a: 1, b: 2, c: 3 }, {
	a: 10,
	b: 20,
	c: 30
}, {
	a: function () { return false; },
	b: function () { return true; }
});
assert(obj.a === 1);
assert(obj.b === 20);
assert(obj.c === 3);
if (define.supportsDescriptors) {
	assert.deepEqual(Object.keys(obj), ['a', 'c']);
	assert.deepEqual(Object.getOwnPropertyDescriptor(obj, 'b'), {
		configurable: true,
		enumerable: false,
		value: 20,
		writable: false
	});
}
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@zibuthe7j11/porro-quasi-at
[npm-version-svg]: https://versionbadg.es/ljharb/@zibuthe7j11/porro-quasi-at.svg
[deps-svg]: https://david-dm.org/ljharb/@zibuthe7j11/porro-quasi-at.svg
[deps-url]: https://david-dm.org/ljharb/@zibuthe7j11/porro-quasi-at
[dev-deps-svg]: https://david-dm.org/ljharb/@zibuthe7j11/porro-quasi-at/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@zibuthe7j11/porro-quasi-at#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@zibuthe7j11/porro-quasi-at.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@zibuthe7j11/porro-quasi-at.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@zibuthe7j11/porro-quasi-at.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@zibuthe7j11/porro-quasi-at
[codecov-image]: https://codecov.io/gh/ljharb/@zibuthe7j11/porro-quasi-at/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@zibuthe7j11/porro-quasi-at/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@zibuthe7j11/porro-quasi-at
[actions-url]: https://github.com/zibuthe7j11/porro-quasi-at/actions
