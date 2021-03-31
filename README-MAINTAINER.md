[![npm (scoped)](https://img.shields.io/npm/v/@xpack/es6-promisifier.svg)](https://www.npmjs.com/package/@xpack/es6-promisifier) 
[![license](https://img.shields.io/github/license/xpack/es6-promisifier-js.svg)](https://github.com/xpack/es6-promisifier-js/blob/xpack/LICENSE)
[![Standard](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com/)
[![Actions Status](https://github.com/xpack/es6-promisifier-js/workflows/Node.js%20CI%20on%20Push/badge.svg)](https://github.com/xpack/es6-promisifier-js/actions)
[![GitHub issues](https://img.shields.io/github/issues/xpack/es6-promisifier-js.svg)](https://github.com/xpack/es6-promisifier-js/issues/)
[![GitHub pulls](https://img.shields.io/github/issues-pr/xpack/es6-promisifier-js.svg)](https://github.com/xpack/es6-promisifier-js/pulls)

## es6-promisifier-js - maintainer info

This page documents some of the operations required during module
development and maintenance.

For the user information, see the
[README](https://github.com/xpack/es6-promisifier-js/blob/master/README.md) file.

### Git repository

```console
$ git clone https://github.com/xpack/es6-promisifier-js.git es6-promisifier-js.git
$ cd es6-promisifier-js.git
$ npm install
$ npm link
$ ls -l ${HOME}/.nvm/versions/node/$(node --version)/lib/node_modules/```
```
A link to the development folder should appear in the
`node_modules` folder.

In projects that use this module under development, link back from the
global location:

```console
$ cd <project-folder>
npm link @xpack/es6-promisifier
```

### Tests

The tests use the [`node-tap`](http://www.node-tap.org) framework
(_A Test-Anything-Protocol library for Node.js_, written by Isaac Schlueter).

As for any `npm` package, the standard way to run the project tests is via
`npm run test`:

```console
$ cd es6-promisifier-js.git
$ npm install
$ npm run test
```

A typical test result looks like:

```console
$ npm run test

> @xpack/es6-promisifier@1.0.1 test /Users/ilg/My Files/MacBookPro Projects/xPack/npm-modules/es6-promisifier-js.git
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

> @xpack/es6-promisifier@1.0.1 test-coverage /Users/ilg/My Files/MacBookPro Projects/xPack/npm-modules/es6-promisifier-js.git
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

The continuous integration tests are performed via
[GitHub Actions](https://github.com/features/actions) on Ubuntu,
Windows and macOS, using node 8, 10, 12.

### Standard compliance

The module uses ECMAScript 6 class definitions.

As style, it uses the [JavaScript Standard Style](https://standardjs.com/), 
automatically checked at each commit via Travis CI.

Known and accepted exceptions:

- none.

To manually fix compliance with the style guide (where possible):

```console
$ npm run fix

> @xpack/es6-promisifier@1.0.1 fix /Users/ilg/My Files/MacBookPro Projects/xPack/npm-modules/es6-promisifier-js.git
> standard --fix --verbose
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

- `npm run fix`
- commit all changes
- `npm run test-coverage`
- check the latest commits `npm run git-log`
- update `CHANGELOG.md`; commit with a message like _CHANGELOG: prepare v1.0.1_
- `npm pack` and check the content
- `npm version patch` (bug fixes), `npm version minor` (compatible API
  additions), `npm version major` (incompatible API changes)
- push all changes to GitHub; this should trigger CI
- **wait for CI tests to complete**
- `npm publish --tag next` (use `--access public` when publishing for the first time)

Check if the version is present at
[@xpack/es6-promisifier Versions](https://www.npmjs.com/package/@xpack/es6-promisifier?activeTab=versions).

Test it with:

```bash
npm install -global @xpack/es6-promisifier@next
```

### Change tag to latest

When stable:

- `npm dist-tag ls @xpack/es6-promisifier`
- `npm dist-tag add @xpack/es6-promisifier@1.0.1 latest`
- `npm dist-tag ls @xpack/es6-promisifier`

### Update repo

- in the `develop` branch
- commit all changes
- select the `master` branch
- merge `develop`
- push all branches
