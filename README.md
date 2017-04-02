# api documentation for  [busboy (v0.2.14)](https://github.com/mscdex/busboy#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-busboy.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-busboy) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-busboy.svg)](https://travis-ci.org/npmdoc/node-npmdoc-busboy)
#### A streaming parser for HTML form data for node.js

[![NPM](https://nodei.co/npm/busboy.png?downloads=true)](https://www.npmjs.com/package/busboy)

[![apidoc](https://npmdoc.github.io/node-npmdoc-busboy/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-busboy_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-busboy/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-busboy/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Brian White",
        "email": "mscdex@mscdex.net"
    },
    "bugs": {
        "url": "https://github.com/mscdex/busboy/issues"
    },
    "dependencies": {
        "dicer": "0.2.5",
        "readable-stream": "1.1.x"
    },
    "description": "A streaming parser for HTML form data for node.js",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "6c2a622efcf47c57bbbe1e2a9c37ad36c7925453",
        "tarball": "https://registry.npmjs.org/busboy/-/busboy-0.2.14.tgz"
    },
    "engines": {
        "node": ">=0.8.0"
    },
    "homepage": "https://github.com/mscdex/busboy#readme",
    "keywords": [
        "uploads",
        "forms",
        "multipart",
        "form-data"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "http://github.com/mscdex/busboy/raw/master/LICENSE"
        }
    ],
    "main": "./lib/main",
    "maintainers": [
        {
            "name": "mscdex",
            "email": "mscdex@mscdex.net"
        }
    ],
    "name": "busboy",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/mscdex/busboy.git"
    },
    "scripts": {
        "test": "node test/test.js"
    },
    "version": "0.2.14"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module busboy](#apidoc.module.busboy)
1.  [function <span class="apidocSignatureSpan">busboy.</span>super_ (options)](#apidoc.element.busboy.super_)
1.  object <span class="apidocSignatureSpan">busboy.</span>utils

#### [module busboy.utils](#apidoc.module.busboy.utils)
1.  [function <span class="apidocSignatureSpan">busboy.utils.</span>Decoder ()](#apidoc.element.busboy.utils.Decoder)
1.  [function <span class="apidocSignatureSpan">busboy.utils.</span>basename (path)](#apidoc.element.busboy.utils.basename)
1.  [function <span class="apidocSignatureSpan">busboy.utils.</span>decodeText (text, textEncoding, destEncoding)](#apidoc.element.busboy.utils.decodeText)
1.  [function <span class="apidocSignatureSpan">busboy.utils.</span>parseParams (str)](#apidoc.element.busboy.utils.parseParams)



# <a name="apidoc.module.busboy"></a>[module busboy](#apidoc.module.busboy)

#### <a name="apidoc.element.busboy.super_"></a>[function <span class="apidocSignatureSpan">busboy.</span>super_ (options)](#apidoc.element.busboy.super_)
- description and source-code
```javascript
function Writable(options) {
  // Writable ctor is applied to Duplexes, too.
  // 'realHasInstance' is necessary because using plain 'instanceof'
  // would return false, as no '_writableState' property is attached.

  // Trying to use the custom 'instanceof' for Writable here will also break the
  // Node.js LazyTransform implementation, which has a non-trivial getter for
  // '_writableState' that would lead to infinite recursion.
  if (!(realHasInstance.call(Writable, this)) &&
      !(this instanceof Stream.Duplex)) {
    return new Writable(options);
  }

  this._writableState = new WritableState(options, this);

  // legacy.
  this.writable = true;

  if (options) {
    if (typeof options.write === 'function')
      this._write = options.write;

    if (typeof options.writev === 'function')
      this._writev = options.writev;
  }

  Stream.call(this);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.busboy.utils"></a>[module busboy.utils](#apidoc.module.busboy.utils)

#### <a name="apidoc.element.busboy.utils.Decoder"></a>[function <span class="apidocSignatureSpan">busboy.utils.</span>Decoder ()](#apidoc.element.busboy.utils.Decoder)
- description and source-code
```javascript
function Decoder() {
  this.buffer = undefined;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.busboy.utils.basename"></a>[function <span class="apidocSignatureSpan">busboy.utils.</span>basename (path)](#apidoc.element.busboy.utils.basename)
- description and source-code
```javascript
function basename(path) {
  var f = splitPathPosix(path)[2];
  if (f === path)
    f = splitPathWindows(path)[2];
  return f;
}
```
- example usage
```shell
...

var Busboy = require('busboy');

http.createServer(function(req, res) {
if (req.method === 'POST') {
  var busboy = new Busboy({ headers: req.headers });
  busboy.on('file', function(fieldname, file, filename, encoding, mimetype) {
    var saveTo = path.join(os.tmpDir(), path.basename(fieldname));
    file.pipe(fs.createWriteStream(saveTo));
  });
  busboy.on('finish', function() {
    res.writeHead(200, { 'Connection': 'close' });
    res.end("That's all folks!");
  });
  return req.pipe(busboy);
...
```

#### <a name="apidoc.element.busboy.utils.decodeText"></a>[function <span class="apidocSignatureSpan">busboy.utils.</span>decodeText (text, textEncoding, destEncoding)](#apidoc.element.busboy.utils.decodeText)
- description and source-code
```javascript
function decodeText(text, textEncoding, destEncoding) {
  var ret;
  if (text && jsencoding.encodingExists(destEncoding)) {
    try {
      ret = jsencoding.TextDecoder(destEncoding)
                      .decode(new Buffer(text, textEncoding));
    } catch(e) {}
  }
  return (typeof ret === 'string' ? ret : text);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.busboy.utils.parseParams"></a>[function <span class="apidocSignatureSpan">busboy.utils.</span>parseParams (str)](#apidoc.element.busboy.utils.parseParams)
- description and source-code
```javascript
function parseParams(str) {
  var res = [],
      state = 'key',
      charset = '',
      inquote = false,
      escaping = false,
      p = 0,
      tmp = '';

  for (var i = 0, len = str.length; i < len; ++i) {
    if (str[i] === '\\' && inquote) {
      if (escaping)
        escaping = false;
      else {
        escaping = true;
        continue;
      }
    } else if (str[i] === '"') {
      if (!escaping) {
        if (inquote) {
          inquote = false;
          state = 'key';
        } else
          inquote = true;
        continue;
      } else
        escaping = false;
    } else {
      if (escaping && inquote)
        tmp += '\\';
      escaping = false;
      if ((state === 'charset' || state === 'lang') && str[i] === "'") {
        if (state === 'charset') {
          state = 'lang';
          charset = tmp.substring(1);
        } else
          state = 'value';
        tmp = '';
        continue;
      } else if (state === 'key'
                 && (str[i] === '*' || str[i] === '=')
                 && res.length) {
        if (str[i] === '*')
          state = 'charset';
        else
          state = 'value';
        res[p] = [tmp, undefined];
        tmp = '';
        continue;
      } else if (!inquote && str[i] === ';') {
        state = 'key';
        if (charset) {
          if (tmp.length) {
            tmp = decodeText(tmp.replace(RE_ENCODED, encodedReplacer),
                             'binary',
                             charset);
          }
          charset = '';
        }
        if (res[p] === undefined)
          res[p] = tmp;
        else
          res[p][1] = tmp;
        tmp = '';
        ++p;
        continue;
      } else if (!inquote && (str[i] === ' ' || str[i] === '\t'))
        continue;
    }
    tmp += str[i];
  }
  if (charset && tmp.length) {
    tmp = decodeText(tmp.replace(RE_ENCODED, encodedReplacer),
                     'binary',
                     charset);
  }

  if (res[p] === undefined) {
    if (tmp)
      res[p] = tmp;
  } else
    res[p][1] = tmp;

  return res;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
