# tsify

[Browserify](http://browserify.org/) plugin for compiling [Typescript](http://www.typescriptlang.org/) 1.0

[![NPM version](https://badge.fury.io/js/tsify.png)](http://badge.fury.io/js/tsify)
[![build status](https://secure.travis-ci.org/smrq/tsify.png)](http://travis-ci.org/smrq/tsify)
[![Dependency status](https://david-dm.org/smrq/tsify.png)](https://david-dm.org/smrq/tsify) [![devDependency Status](https://david-dm.org/smrq/tsify/dev-status.png)](https://david-dm.org/smrq/tsify#info=devDependencies)



# example usage

On the command line:

``` sh
$ browserify main.ts -p [ tsify --noImplicitAny ] > bundle.js
```

With the Browserify API:

``` js
browserify()
    .add('main.ts')
    .plugin('tsify', { noImplicitAny: true })
    .bundle();
```

# installation

Just plain ol' [npm](https://npmjs.org/) installation:

``` sh
npm install tsify
```

# options

* **tsify** will generate sourcemaps if the `--debug` option is set on Browserify.
* **tsify** supports the following options from the Typescript compiler (via [ts-compiler](https://github.com/jedmao/ts-compiler)):

#### --noImplicitAny

Warn on expressions and declarations with an implied `any` type.

#### --removeComments

Do not emit comments to output.

#### --target=*version*

Specify ECMAScript target version: 'ES3' (default), or 'ES5'

# why a plugin?

There are several Typescript compilation transforms available on npm, all with various issues.  The Typescript compiler automatically performs dependency resolution on module imports, much like Browserify itself.  Browserify transforms are not flexible enough to deal with multiple file outputs given a single file input, which means that any working Typescript compilation transform either skips the resolution step (which is necessary for complete type checking) or performs multiple compilations of source files further down the dependency graph.

**tsify** avoids this problem by using the power of plugins to perform a single compilation of the Typescript source up-front, using Browserify to glue together the resulting files.

# license

MIT
