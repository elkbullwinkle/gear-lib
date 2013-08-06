# gear-lib

## Collection of common [Gear.js](/yahoo/gear) tasks

Useful tasks to lint, minify, and deploy assets.

[![Build Status](https://secure.travis-ci.org/twobit/gear-lib.png)](http://travis-ci.org/twobit/gear-lib)

[![NPM](https://nodei.co/npm/gear-lib.png?downloads=true)](https://nodei.co/npm/gear-lib/)

## Installation

```bash
$ npm install gear-lib
```

## Quick Examples

### Deploy to S3

```javascript
new Queue({registry: new Registry({module: 'gear-lib'})})
    .read(['foo.js', 'bar.js', 'baz.js'])
    .concat()
    .jslint({config: {nomen: true}})
    .jsminify()
    .s3({name: 'foobarbaz.js', client: {
        key: '<key>',
        secret: '<secret>',
        bucket: 'gearjs'
    }})
    .run();
```

## Documentation

### Tasks

 * [jslint](#jslint)
 * [jsminify](#jsminify)
 * [csslint](#csslint)
 * [cssminify](#cssminify)
 * [less](#cssminify)
 * [replace](#replace)
 * [glob](#glob)
 * [s3](#s3)

## Tasks

<a name="jslint" />
### jslint()

Lint Javascript files.

__Arguments__

 * options.config - Options for JSLint.

__Example__

```javascript
.jslint({config: {nomen: true}})
```

---------------------------------------

<a name="jsminify" />
### jsminify()

Minify Javascript files.

__Arguments__

 * options.config - Options for uglify-js.

__Example__

```javascript
.jsminify()
```

---------------------------------------

<a name="csslint" />
### csslint()

Lint CSS files.

__Arguments__

 * options.config - Options for CSSLint.

__Example__

```javascript
.csslint({config: {'duplicate-properties': true}})
```

---------------------------------------

<a name="cssminify" />
### cssminify()

Minify CSS files.

__Aliased as less()__

__Example__

```javascript
.cssminify()

// Compile LESS stylesheets without minifying
.less({compress: false})
```

---------------------------------------

<a name="replace" />
### replace()

Replace strings using RegExp.

__Arguments__

 * options.regex - RegExp object or string.
 * options.flags - RegExp flags if using string.

__Example__

```javascript
.replace({
    regex: "Y.log\\(.+?\\);?",
    replace: '',
    flags: 'mg'
})

.replace({
    regex: /Y.log\(.+?\);?/mg,
    replace: ''
})
```

---------------------------------------

<a name="glob" />
### glob()

Read files using wildcards. See [Glob package](https://github.com/isaacs/node-glob)

__Arguments__

 * options.pattern - Glob pattern.
 * options.options - Glob options.

__Example__

```javascript
.glob({
    pattern: "*.js"
})
```

---------------------------------------

<a name="s3" />
### s3()

Deploy file to S3.

__Arguments__

 * options.name - Filename to write to S3.
 * options.client.key - S3 key.
 * options.client.secret - S3 secret.
 * options.client.bucket - S3 bucket.

__Example__

```javascript
 .s3({name: 'foobarbaz.js', client: {
    key: '<key>',
    secret: '<secret>',
    bucket: 'gearjs'
 }})
```
