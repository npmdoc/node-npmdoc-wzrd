# npmdoc-wzrd

#### api documentation for  [wzrd (v1.5.0)](https://github.com/maxogden/wzrd)  [![npm package](https://img.shields.io/npm/v/npmdoc-wzrd.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-wzrd) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-wzrd.svg)](https://travis-ci.org/npmdoc/node-npmdoc-wzrd)

#### Super minimal browserify development server. Inspired by [beefy](http://npmjs.org/beefy) but with less magic

[![NPM](https://nodei.co/npm/wzrd.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/wzrd)

- [https://npmdoc.github.io/node-npmdoc-wzrd/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-wzrd/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-wzrd/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-wzrd/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-wzrd/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-wzrd/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "max ogden"
    },
    "bin": {
        "wzrd": "bin.js"
    },
    "bugs": {
        "url": "https://github.com/maxogden/wzrd/issues"
    },
    "dependencies": {
        "concat-stream": "^1.4.7",
        "ecstatic": "^1.4.1",
        "minimist": "^1.1.0",
        "npm-execspawn": "^1.0.6",
        "pem": "^1.4.4",
        "portfinder": "^0.4.0",
        "routes-router": "^4.1.1"
    },
    "description": "Super minimal browserify development server. Inspired by [beefy](http://npmjs.org/beefy) but with less magic",
    "devDependencies": {
        "request": "^2.51.0",
        "standard": "^7.1.2",
        "tape": "^3.0.3",
        "through2": "^0.6.3",
        "tree-kill": "0.0.6",
        "win-spawn": "^2.0.0"
    },
    "directories": {
        "test": "test"
    },
    "dist": {
        "shasum": "9694a5cd9a934dcb0a8c8e1adcaabe03fa259dd3",
        "tarball": "https://registry.npmjs.org/wzrd/-/wzrd-1.5.0.tgz"
    },
    "gitHead": "30781cf9548e5773809a30c3150096c2c906583c",
    "homepage": "https://github.com/maxogden/wzrd",
    "keywords": [
        "browserify",
        "beefy"
    ],
    "license": "BSD",
    "main": "index.js",
    "maintainers": [
        {
            "name": "maxogden"
        },
        {
            "name": "mafintosh"
        }
    ],
    "name": "wzrd",
    "optionalDependencies": {},
    "preferGlobal": true,
    "repository": {
        "type": "git",
        "url": "git+https://github.com/maxogden/wzrd.git"
    },
    "scripts": {
        "test": "standard && node test/index.js"
    },
    "version": "1.5.0"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
