# api documentation for  [gulp-remember (v0.3.1)](http://github.com/ahaurw01/gulp-remember)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-remember.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-remember) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-remember.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-remember)
#### Adds previously seen files back into the stream.

[![NPM](https://nodei.co/npm/gulp-remember.png?downloads=true)](https://www.npmjs.com/package/gulp-remember)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-remember/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-remember_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-remember/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-remember/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-remember/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Aaron Haurwitz",
        "email": "aaron.haurwitz@gmail.com",
        "url": "http://aaron.haurwitz.com/"
    },
    "bugs": {
        "url": "https://github.com/ahaurw01/gulp-remember/issues"
    },
    "dependencies": {
        "gulp-util": "^3.0.1",
        "through2": "^0.5.0"
    },
    "description": "Adds previously seen files back into the stream.",
    "devDependencies": {
        "mocha": "~1.18.2",
        "should": "~3.2.0",
        "sinon": "^1.12.1"
    },
    "directories": {},
    "dist": {
        "shasum": "5776b6f64c5a1c5c4d4555406723ec8e2b0407e7",
        "tarball": "https://registry.npmjs.org/gulp-remember/-/gulp-remember-0.3.1.tgz"
    },
    "engineStrict": true,
    "engines": {
        "node": ">= 0.10"
    },
    "gitHead": "cf9fa7a16e7e3aaf47684fd446ecc9f5c3dc1b58",
    "homepage": "http://github.com/ahaurw01/gulp-remember",
    "keywords": [
        "gulpplugin"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "http://github.com/ahaurw01/gulp-remember/raw/master/LICENSE"
        }
    ],
    "main": "./index.js",
    "maintainers": [
        {
            "name": "ahaurw01",
            "email": "aaron.haurwitz@gmail.com"
        }
    ],
    "name": "gulp-remember",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/ahaurw01/gulp-remember.git"
    },
    "scripts": {
        "test": "mocha --reporter spec"
    },
    "version": "0.3.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-remember](#apidoc.module.gulp-remember)
1.  [function <span class="apidocSignatureSpan">gulp-remember.</span>cacheFor (cacheName)](#apidoc.element.gulp-remember.cacheFor)
1.  [function <span class="apidocSignatureSpan">gulp-remember.</span>forget (cacheName, path)](#apidoc.element.gulp-remember.forget)
1.  [function <span class="apidocSignatureSpan">gulp-remember.</span>forgetAll (cacheName)](#apidoc.element.gulp-remember.forgetAll)



# <a name="apidoc.module.gulp-remember"></a>[module gulp-remember](#apidoc.module.gulp-remember)

#### <a name="apidoc.element.gulp-remember.cacheFor"></a>[function <span class="apidocSignatureSpan">gulp-remember.</span>cacheFor (cacheName)](#apidoc.element.gulp-remember.cacheFor)
- description and source-code
```javascript
cacheFor = function (cacheName) {
  if (arguments.length === 0) {
    cacheName = defaultName;
  }
  if (typeof cacheName !== 'number' && typeof cacheName !== 'string') {
    throw new util.PluginError(pluginName, 'Usage: require("gulp-remember").cacheFor(cacheName); where cacheName is undefined, number
 or string');
  }
  return caches[cacheName];
}
```
- example usage
```shell
...

Type: 'String'

The name of the remember cache you want to wipe. You do not need to pass this if you want to operate on the default remember cache
.

**Note:** If the name does not refer to a cache that exists, a warning is logged.

### remember.cacheFor(name)

Get a raw remember cache. This can be useful for checking state of the cache, like whether or not a file has been seen before.

**Note:** Remembering or forgetting files by interacting directly with this returned object is not recommended.

#### name (optional)
...
```

#### <a name="apidoc.element.gulp-remember.forget"></a>[function <span class="apidocSignatureSpan">gulp-remember.</span>forget (cacheName, path)](#apidoc.element.gulp-remember.forget)
- description and source-code
```javascript
forget = function (cacheName, path) {
  if (arguments.length === 1) {
    path = cacheName;
    cacheName = defaultName;
  }
  path = path.toLowerCase();
  if (typeof cacheName !== 'number' && typeof cacheName !== 'string') {
    throw new util.PluginError(pluginName, 'Usage: require("gulp-remember").forget(cacheName, path); where cacheName is undefined
, number or string and path is a string');
  }
  if (caches[cacheName] === undefined) {
    util.log(pluginName, '- .forget() warning: cache ' + cacheName + ' not found');
  } else if (caches[cacheName][path] === undefined) {
    util.log(pluginName, '- .forget() warning: file ' + path + ' not found in cache ' + cacheName);
  } else {
    delete caches[cacheName][path];
  }
}
```
- example usage
```shell
...
});

gulp.task('watch', function () {
  var watcher = gulp.watch(scriptsGlob, ['scripts']); // watch the same files in our scripts task
  watcher.on('change', function (event) {
    if (event.type === 'deleted') { // if a file is deleted, forget about it
      delete cache.caches['scripts'][event.path];
      remember.forget('scripts', event.path);
    }
  });
});
'''

## API
...
```

#### <a name="apidoc.element.gulp-remember.forgetAll"></a>[function <span class="apidocSignatureSpan">gulp-remember.</span>forgetAll (cacheName)](#apidoc.element.gulp-remember.forgetAll)
- description and source-code
```javascript
forgetAll = function (cacheName) {
  if (arguments.length === 0) {
    cacheName = defaultName;
  }
  if (typeof cacheName !== 'number' && typeof cacheName !== 'string') {
    throw new util.PluginError(pluginName, 'Usage: require("gulp-remember").forgetAll(cacheName); where cacheName is undefined,
number or string');
  }
  if (caches[cacheName] === undefined) {
    util.log(pluginName, '- .forget() warning: cache ' + cacheName + ' not found');
  } else {
    caches[cacheName] = {};
  }
}
```
- example usage
```shell
...

**Important note!** The path you pass to 'forget' must be the path of the *processed* file. You may encounter instances where your
 source file is 'some/path/script.coffee' while the processed file is 'some/path/script.js'. Because anything could happen before
 you 'remember' a file, it is up to you to know how you need to 'forget' it with the correct path.

If you want to 'forget' files using their name history, you might want to use [gulp-remember-history](https://www.npmjs.com/package
/gulp-remember-history).

**Another note:** If the path does not match a file object that exists in the given cache, a warning is logged. Thanks to @jcppman
 for this.

### remember.forgetAll(name)

Drops all files from a remember cache.

#### name (optional)

Type: 'String'
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
