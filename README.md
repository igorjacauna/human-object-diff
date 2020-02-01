# human-object-diff

[![build status](https://img.shields.io/travis/com/Spence-S/human-object-diff.svg)](https://travis-ci.com/Spence-S/human-object-diff)
[![code coverage](https://img.shields.io/codecov/c/github/Spence-S/human-object-diff.svg)](https://codecov.io/gh/Spence-S/human-object-diff)
[![code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![made with lass](https://img.shields.io/badge/made_with-lass-95CC28.svg)](https://lass.js.org)
[![license](https://img.shields.io/github/license/Spence-S/human-object-diff.svg)](LICENSE)
[![npm downloads](https://img.shields.io/npm/dt/human-object-diff.svg)](https://npm.im/human-object-diff)

> Configurable Human Readable Difference Between Two Plain Objects


## Table of Contents

* [Install](#install)
* [Usage](#usage)
* [Configuring](#configuring)
  * [Options](#options)
  * [Support for Dates](#support-for-dates)
  * [Prefiltering](#prefiltering)
* [Contributors](#contributors)
* [License](#license)


## Install

[npm][]:

```bash
npm install human-object-diff
```

[yarn][]:

```bash
yarn add human-object-diff
```


## Usage

```js
const humanDiff = require('human-object-diff');

const lhs = { foo: 'bar' };
const rhs = { foo: 'baz' };
const options = {};

const diff = humanDiff(lhs, rhs, options);

console.log(humanObjectDiff.renderName());
// -> ['Foo", with a value of "bar" (at Obj.foo) was changed to "baz"']
```


## Configuring

### Options

`human-object-diff` supports a variety of options to allow you to take control over the output of your object diff. Future versions will allow users to fully customize sentence structure.

| Option       | type        | Default              | Description                                                                                     |
| ------------ | ----------- | -------------------- | ----------------------------------------------------------------------------------------------- |
| objectName   | String      | 'Obj'                | This is the object name when presented in the path. ie... "Obj.foo" ignored if hidePath is true |
| prefilter    | Array\|Func |                      | see [prefiltering](#prefiltering)                                                               |
| dateFormat   | String      | 'MM/dd/yyyy hh:mm a' | dateFns format string see [below](#support-for-dates)                                           |
| futureTense  | Bool        | 'past'               | If set to true, sentences will output "will be" changed instead of "was changed"                |
| hidePath     | Bool        | false                | If set to true, path..ie "(Obj.foo)".. is suppressed making the output less technical           |
| ignoreArrays | Bool        | false                | If array differences aren't needed. Set to true and skip processing                             |

### Support for Dates

`human-object-diff` uses `date-fns` format function under the hood to show human readable date differences. We also supply a `dateFormat` option where you can supply your own date formatting string. Please note, that date-fns format strings are different from moment.js format strings. Please refer to the documentation [here](https://date-fns.org/v2.8.1/docs/format) and [here](https://github.com/date-fns/date-fns/blob/master/docs/unicodeTokens.md)

### Prefiltering

There may be some paths in your object diffs that you'd like to ignore. You can do that with prefiltering. As a convenience, ou can add this option as an array of strings, which are the keys of the base path of the object.

for instance

```js
const lhs = { foo: 'bar', biz: { foo: 'baz' } };
const rhs = { foo: 'bar', biz: { foo: 'buzz' } };

hrDiff(lhs, rhs, ['foo']);
```

You would still see the diffs for `biz.foo` but you would ignore the diff for `foo`.

You can also pass a function for this option which will be directly passed to the [underlying diff library](https://www.npmjs.com/package/deep-diff).

The prefilter function takes a signature of `function(path, key)`


## Contributors

| Name               | Website                    |
| ------------------ | -------------------------- |
| **Spencer Snyder** | <http://spencersnyder.io/> |


## License

[MIT](LICENSE) © [Spencer Snyder](http://spencersnyder.io/)


## 

[npm]: https://www.npmjs.com/

[yarn]: https://yarnpkg.com/
