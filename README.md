# api documentation for  [wzrd (v1.5.0)](https://github.com/maxogden/wzrd)  [![npm package](https://img.shields.io/npm/v/npmdoc-wzrd.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-wzrd) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-wzrd.svg)](https://travis-ci.org/npmdoc/node-npmdoc-wzrd)
#### Super minimal browserify development server. Inspired by [beefy](http://npmjs.org/beefy) but with less magic

[![NPM](https://nodei.co/npm/wzrd.png?downloads=true)](https://www.npmjs.com/package/wzrd)

[![apidoc](https://npmdoc.github.io/node-npmdoc-wzrd/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-wzrd_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-wzrd/build/apidoc.html)

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
            "name": "maxogden",
            "email": "max@maxogden.com"
        },
        {
            "name": "mafintosh",
            "email": "mathiasbuus@gmail.com"
        }
    ],
    "name": "wzrd",
    "optionalDependencies": {},
    "preferGlobal": true,
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module wzrd](#apidoc.module.wzrd)
1.  [function <span class="apidocSignatureSpan">wzrd.</span>browserify (entry, opts, req, res)](#apidoc.element.wzrd.browserify)
1.  [function <span class="apidocSignatureSpan">wzrd.</span>generateIndex (entry, req, res)](#apidoc.element.wzrd.generateIndex)
1.  [function <span class="apidocSignatureSpan">wzrd.</span>http (opts)](#apidoc.element.wzrd.http)
1.  [function <span class="apidocSignatureSpan">wzrd.</span>https (opts, cb)](#apidoc.element.wzrd.https)
1.  [function <span class="apidocSignatureSpan">wzrd.</span>static (opts)](#apidoc.element.wzrd.static)



# <a name="apidoc.module.wzrd"></a>[module wzrd](#apidoc.module.wzrd)

#### <a name="apidoc.element.wzrd.browserify"></a>[function <span class="apidocSignatureSpan">wzrd.</span>browserify (entry, opts, req, res)](#apidoc.element.wzrd.browserify)
- description and source-code
```javascript
browserify = function (entry, opts, req, res) {
  res.setHeader('content-type', 'text/javascript')
  var cmd = ['browserify', entry]
  if (opts.browserifyArgs) cmd = cmd.concat(opts.browserifyArgs)
  cmd = cmd.join(' ')
  var proc = spawn(cmd)
  var start = Date.now()
  proc.stderr.pipe(concat(function error (err) {
    if (!err.length) return
    endLog()
    process.stderr.write(err.toString())
    res.statusCode = 500
    res.end()
  }))
  proc.stdout.pipe(concat(function done (buff) {
    if (!buff.length) return
    endLog()
    res.end(buff)
  }))
  function endLog () {
    console.log(JSON.stringify({url: req.url, type: 'bundle', command: cmd, elapsed: (Date.now() - start) + 'ms', time: new Date
()}))
  }
}
```
- example usage
```shell
...
      module.exports.generateIndex(firstEntry, req, res)
    }
  })
}

opts.entries.forEach(function (entry) {
  router.addRoute('/' + entry.to, function (req, res, params) {
    module.exports.browserify(entry.from, opts, req, res)
  })
})

router.addRoute('/', indexHtmlHandler)

router.addRoute('*', function (req, res, params) {
  console.log(JSON.stringify({url: req.url, type: 'static', time: new Date()}))
...
```

#### <a name="apidoc.element.wzrd.generateIndex"></a>[function <span class="apidocSignatureSpan">wzrd.</span>generateIndex (entry, req, res)](#apidoc.element.wzrd.generateIndex)
- description and source-code
```javascript
generateIndex = function (entry, req, res) {
  console.log(JSON.stringify({url: req.url, type: 'generated', time: new Date()}))
  res.setHeader('content-type', 'text/html')
  res.end('<!doctype html><head><meta charset="utf-8"></head><body><script src="' + entry + '"></script></body></html>')
}
```
- example usage
```shell
...
var indexHtmlHandler = function (req, res, params) {
  fs.exists(path.join(basedir, 'index.html'), function (exists) {
    var firstEntry = opts.entries[0].to
    if (exists) {
      req.url = '/index.html'
      return staticHandler(req, res)
    } else {
      module.exports.generateIndex(firstEntry, req, res)
    }
  })
}

opts.entries.forEach(function (entry) {
  router.addRoute('/' + entry.to, function (req, res, params) {
    module.exports.browserify(entry.from, opts, req, res)
...
```

#### <a name="apidoc.element.wzrd.http"></a>[function <span class="apidocSignatureSpan">wzrd.</span>http (opts)](#apidoc.element.wzrd.http)
- description and source-code
```javascript
http = function (opts) {
  var handler = module.exports.static(opts)
  return http.createServer(handler)
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.wzrd.https"></a>[function <span class="apidocSignatureSpan">wzrd.</span>https (opts, cb)](#apidoc.element.wzrd.https)
- description and source-code
```javascript
https = function (opts, cb) {
  var handler = module.exports.static(opts)
  pem.createCertificate({days: 999, selfSigned: true}, function (err, keys) {
    if (err) return cb(err)
    var server = https.createServer({key: keys.serviceKey, cert: keys.certificate}, handler)
    cb(null, server)
  })
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.wzrd.static"></a>[function <span class="apidocSignatureSpan">wzrd.</span>static (opts)](#apidoc.element.wzrd.static)
- description and source-code
```javascript
static = function (opts) {
  var basedir = opts.path || process.cwd()
  var staticHandler = ecstatic(basedir)
  var router = Router()

  var indexHtmlHandler = function (req, res, params) {
    fs.exists(path.join(basedir, 'index.html'), function (exists) {
      var firstEntry = opts.entries[0].to
      if (exists) {
        req.url = '/index.html'
        return staticHandler(req, res)
      } else {
        module.exports.generateIndex(firstEntry, req, res)
      }
    })
  }

  opts.entries.forEach(function (entry) {
    router.addRoute('/' + entry.to, function (req, res, params) {
      module.exports.browserify(entry.from, opts, req, res)
    })
  })

  router.addRoute('/', indexHtmlHandler)

  router.addRoute('*', function (req, res, params) {
    console.log(JSON.stringify({url: req.url, type: 'static', time: new Date()}))
    staticHandler(req, res, function () {
      if (opts.pushstate) return indexHtmlHandler(req, res)
      res.end('File not found. :(')
    })
  })

  return router
}
```
- example usage
```shell
...
var https = require('https')
var fs = require('fs')
var path = require('path')
var spawn = require('npm-execspawn')
var pem = require('pem')

module.exports.http = function (opts) {
var handler = module.exports.static(opts)
return http.createServer(handler)
}

module.exports.https = function (opts, cb) {
var handler = module.exports.static(opts)
pem.createCertificate({days: 999, selfSigned: true}, function (err, keys) {
  if (err) return cb(err)
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
