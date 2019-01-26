[![npm (scoped)](https://img.shields.io/npm/v/@xpack/es6-promisifier.svg)](https://www.npmjs.com/package/@xpack/es6-promisifier) 
[![license](https://img.shields.io/github/license/xpack/es6-promisifier-js.svg)](https://github.com/xpack/es6-promisifier-js/blob/xpack/LICENSE) 
[![Standard](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com/)
[![Travis](https://img.shields.io/travis/xpack/es6-promisifier-js.svg?label=linux)](https://travis-ci.org/xpack/es6-promisifier-js)
[![AppVeyor](https://ci.appveyor.com/api/projects/status/f11aw2irha640ank?svg=true)](https://ci.appveyor.com/project/ilg-ul/es6-promisifier-js)

## An ES6 promisifier wrapper

A Node.js module with a class providing a static function to wrap 
standard Node.js callback functions into ES6 promises.

## Prerequisites

A recent [Node.js](https://nodejs.org) (>7.x), since the ECMAScript 6 
class syntax is used.

## Easy install

The module is available as 
[`@xpack/es6-promisifier`](https://www.npmjs.com/package/@xpack/es6-promisifier)
from the public repository, use `npm` to install it inside the module 
where it is needed:

```bash
$ npm install @xpack/es6-promisifier --save
```

The module does not provide any executables, and generally there are
few reasons to install it globally.

The development repository is available from the GitHub 
[`xpack/es6-promisifier-js`](https://github.com/xpack/es6-promisifier-js) 
project.

## User info

The module can be included in any applications and the `Promisifier` 
class can be used to access the `promisify()` functions.

```javascript
const Promisifier = require('@xpack/es6-promisifier').Promisifier

// Promisify functions from the Node.js callbacks library.
// The new functions have similar names, but suffixed with `Promise`,
// or below a `promises` object.
Promisifier.promisifyInPlace(fs, 'open')

// New use case:
//   const fsPromises = fs.promises_
//   await fsPromises.open()

// Old use case:
//   await fs.openPromise()

// Note: using `promises_` is a workaround to avoid the `fs.promises`
// warning.

// Promisify a single function from a third party simple module.
const mkdirpPromise = Promisifier.promisify(require('mkdirp'))
```

## Developer info

### Git repo

```console
$ git clone https://github.com/xpack/es6-promisifier-js.git es6-promisifier-js.git
$ cd es6-promisifier-js.git
$ npm install
```

```console
$ sudo npm link 
$ ls -l /usr/local/lib/node_modules/@xpack
```

or without sudo, on Windows or if installed in home folder:

```console
$ npm link
```

A link to the development folder should be present in the global 
`node_modules` folder.

In projects that use this module under development, link back from 
the global location:

```console
$ npm link @xpack/es6-promisifier
```

### Tests

The tests use the [`node-tap`](http://www.node-tap.org) framework 
(_A Test-Anything-Protocol library for Node.js_, written by Isaac Schlueter).

As for any `npm` package, the standard way to run the project tests 
is via `npm test`:

```console
$ cd es6-promisifier-js.git
$ npm install
$ npm run test
```

A typical test result looks like:

```console
$ npm run test

> @xpack/es6-promisifier@1.0.0 test /Users/ilg/My Files/MacBookPro Projects/xPack/npm-modules/es6-promisifier-js.git
> standard && npm run test-tap -s

test/tap/promisify.js ............................... 37/37
total ............................................... 37/37

  37 passing (629.494ms)

  ok
```

To run a specific test with more verbose output, use `npm run tap`:

```console
$ npm run tap test/tap/promisify.js -s

test/tap/promisify.js
  original success
    ✓ null error
    ✓ returned value

  original error
    ✓ have error
    ✓ error message match
    ✓ no returned value

  promisify success
    ✓ returned value

  promisify error
    ✓ exception message

  promisify success await
    ✓ returned value

  promisify error await
    ✓ exception message

  promisify multi success
    ✓ result is array
    ✓ first value
    ✓ second value

  promisify multi error
    ✓ exception message

  promisify multi success await
    ✓ result is array
    ✓ first value
    ✓ second value

  promisify multi error await
    ✓ exception message

  promisify single success
    ✓ result is not array
    ✓ value

  promisify single error
    ✓ exception message

  promisify single success await
    ✓ result is not array
    ✓ value

  promisify single error await
    ✓ exception message

  promisify already success await
    ✓ returned value

  promisify already error await
    ✓ exception message

  promisify thisArg success await
    ✓ returned value
    ✓ context value

  promisify thisArg error await
    ✓ exception message

  constructor
    ✓ assert

  promisify in place
    ✓ promise not there
    ✓ promise now available
    ✓ promise in promises now available
    ✓ promise still there
    ✓ promise in promises still there
    ✓ promise not there
    ✓ promise in promises now available
    ✓ promise in promises still there


  37 passing (608.459ms)
```

### Coverage tests

Coverage tests are a good indication on how much of the source files is 
exercised by the tests. Ideally all source files should be covered 100%, 
for all 4 criteria (statements, branches, functions, lines).

To run the coverage tests, use `npm run test-coverage`:

```console
$ npm run test-coverage

> @xpack/es6-promisifier@1.0.0 test-coverage /Users/ilg/My Files/MacBookPro Projects/xPack/npm-modules/es6-promisifier-js.git
> tap --coverage --reporter=classic --timeout 600 --no-color "test/tap/*.js"

test/tap/promisify.js ............................... 37/37
total ............................................... 37/37

  37 passing (1s)

  ok
----------------------------|----------|----------|----------|----------|-------------------|
File                        |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
----------------------------|----------|----------|----------|----------|-------------------|
All files                   |      100 |      100 |      100 |      100 |                   |
 es6-promisifier-js.git     |      100 |      100 |      100 |      100 |                   |
  index.js                  |      100 |      100 |      100 |      100 |                   |
 es6-promisifier-js.git/lib |      100 |      100 |      100 |      100 |                   |
  promisifier.js            |      100 |      100 |      100 |      100 |                   |
----------------------------|----------|----------|----------|----------|-------------------|
```

### Continuous Integration (CI)

The continuous integration tests are performed via [Travis CI](https://travis-ci.org/xpack/es6-promisifier-js) and [AppVeyor](https://ci.appveyor.com/project/ilg-ul/es6-promisifier-js).

To speed up things, the `node_modules` folder is cached between builds.

### Standard compliance

The module uses ECMAScript 6 class definitions.

As style, it uses the [JavaScript Standard Style](https://standardjs.com/), 
automatically checked at each commit via Travis CI.

Known and accepted exceptions:

- none.

To manually fix compliance with the style guide (where possible):

```console
$ npm run fix

> @xpack/es6-promisifier@1.0.0 fix /Users/ilg/My Files/MacBookPro Projects/xPack/npm-modules/es6-promisifier-js.git
> standard --fix
```

### Documentation metadata

The documentation metadata follows the [JSdoc](http://usejsdoc.org) tags.

To enforce checking at file level, add the following comments right after 
the `use strict`:

```js
'use strict'
/* eslint valid-jsdoc: "error" */
/* eslint max-len: [ "error", 80, { "ignoreUrls": true } ] */
```

Note: be sure C style comments are used, C++ styles are not parsed by 
[ESLint](http://eslint.org).

### How to publish

* `npm run fix`
* commit all changes
* `npm run test-coverage`
* update `CHANGELOG.md`; commit with a message like _CHANGELOG: prepare v1.2.3_
* `npm version patch` (bug fixes), `npm version minor` (compatible API 
  additions), `npm version major` (incompatible API changes)
* push all changes to GitHub; this should trigger CI
* wait for CI tests to complete
* `npm publish` (use `--access public` when publishing for the first time)

## License

The original content is released under the 
[MIT License](https://opensource.org/licenses/MIT), with all rights reserved to
[Liviu Ionescu](https://github.com/ilg-ul).
