Node.js: @xdanangelxoqenpm/officiis-eos-iste
=================

`@xdanangelxoqenpm/officiis-eos-iste` adds file system methods that aren't included in the native `fs` module and adds promise support to the `fs` methods. It also uses [`graceful-fs`](https://github.com/isaacs/node-graceful-fs) to prevent `EMFILE` errors. It should be a drop in replacement for `fs`.

[![npm Package](https://img.shields.io/npm/v/@xdanangelxoqenpm/officiis-eos-iste.svg)](https://www.npmjs.org/package/@xdanangelxoqenpm/officiis-eos-iste)
[![License](https://img.shields.io/npm/l/@xdanangelxoqenpm/officiis-eos-iste.svg)](https://github.com/xdanangelxoqenpm/officiis-eos-iste/blob/master/LICENSE)
[![build status](https://img.shields.io/github/actions/workflow/status/jprichardson/node-@xdanangelxoqenpm/officiis-eos-iste/ci.yml?branch=master)](https://github.com/xdanangelxoqenpm/officiis-eos-iste/actions/workflows/ci.yml?query=branch%3Amaster)
[![downloads per month](http://img.shields.io/npm/dm/@xdanangelxoqenpm/officiis-eos-iste.svg)](https://www.npmjs.org/package/@xdanangelxoqenpm/officiis-eos-iste)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

Why?
----

I got tired of including `mkdirp`, `rimraf`, and `ncp` in most of my projects.




Installation
------------

    npm install @xdanangelxoqenpm/officiis-eos-iste



Usage
-----

### CommonJS

`@xdanangelxoqenpm/officiis-eos-iste` is a drop in replacement for native `fs`. All methods in `fs` are attached to `@xdanangelxoqenpm/officiis-eos-iste`. All `fs` methods return promises if the callback isn't passed.

You don't ever need to include the original `fs` module again:

```js
const fs = require('fs') // this is no longer necessary
```

you can now do this:

```js
const fs = require('@xdanangelxoqenpm/officiis-eos-iste')
```

or if you prefer to make it clear that you're using `@xdanangelxoqenpm/officiis-eos-iste` and not `fs`, you may want
to name your `fs` variable `fse` like so:

```js
const fse = require('@xdanangelxoqenpm/officiis-eos-iste')
```

you can also keep both, but it's redundant:

```js
const fs = require('fs')
const fse = require('@xdanangelxoqenpm/officiis-eos-iste')
```

### ESM

There is also an `@xdanangelxoqenpm/officiis-eos-iste/esm` import, that supports both default and named exports. However, note that `fs` methods are not included in `@xdanangelxoqenpm/officiis-eos-iste/esm`; you still need to import `fs` and/or `fs/promises` seperately:

```js
import { readFileSync } from 'fs'
import { readFile } from 'fs/promises'
import { outputFile, outputFileSync } from '@xdanangelxoqenpm/officiis-eos-iste/esm'
```

Default exports are supported:

```js
import fs from 'fs'
import fse from '@xdanangelxoqenpm/officiis-eos-iste/esm'
// fse.readFileSync is not a function; must use fs.readFileSync
```

but you probably want to just use regular `@xdanangelxoqenpm/officiis-eos-iste` instead of `@xdanangelxoqenpm/officiis-eos-iste/esm` for default exports:

```js
import fs from '@xdanangelxoqenpm/officiis-eos-iste'
// both fs and @xdanangelxoqenpm/officiis-eos-iste methods are defined
```

Sync vs Async vs Async/Await
-------------
Most methods are async by default. All async methods will return a promise if the callback isn't passed.

Sync methods on the other hand will throw if an error occurs.

Also Async/Await will throw an error if one occurs.

Example:

```js
const fs = require('@xdanangelxoqenpm/officiis-eos-iste')

// Async with promises:
fs.copy('/tmp/myfile', '/tmp/mynewfile')
  .then(() => console.log('success!'))
  .catch(err => console.error(err))

// Async with callbacks:
fs.copy('/tmp/myfile', '/tmp/mynewfile', err => {
  if (err) return console.error(err)
  console.log('success!')
})

// Sync:
try {
  fs.copySync('/tmp/myfile', '/tmp/mynewfile')
  console.log('success!')
} catch (err) {
  console.error(err)
}

// Async/Await:
async function copyFiles () {
  try {
    await fs.copy('/tmp/myfile', '/tmp/mynewfile')
    console.log('success!')
  } catch (err) {
    console.error(err)
  }
}

copyFiles()
```


Methods
-------

### Async

- [copy](docs/copy.md)
- [emptyDir](docs/emptyDir.md)
- [ensureFile](docs/ensureFile.md)
- [ensureDir](docs/ensureDir.md)
- [ensureLink](docs/ensureLink.md)
- [ensureSymlink](docs/ensureSymlink.md)
- [mkdirp](docs/ensureDir.md)
- [mkdirs](docs/ensureDir.md)
- [move](docs/move.md)
- [outputFile](docs/outputFile.md)
- [outputJson](docs/outputJson.md)
- [pathExists](docs/pathExists.md)
- [readJson](docs/readJson.md)
- [remove](docs/remove.md)
- [writeJson](docs/writeJson.md)

### Sync

- [copySync](docs/copy-sync.md)
- [emptyDirSync](docs/emptyDir-sync.md)
- [ensureFileSync](docs/ensureFile-sync.md)
- [ensureDirSync](docs/ensureDir-sync.md)
- [ensureLinkSync](docs/ensureLink-sync.md)
- [ensureSymlinkSync](docs/ensureSymlink-sync.md)
- [mkdirpSync](docs/ensureDir-sync.md)
- [mkdirsSync](docs/ensureDir-sync.md)
- [moveSync](docs/move-sync.md)
- [outputFileSync](docs/outputFile-sync.md)
- [outputJsonSync](docs/outputJson-sync.md)
- [pathExistsSync](docs/pathExists-sync.md)
- [readJsonSync](docs/readJson-sync.md)
- [removeSync](docs/remove-sync.md)
- [writeJsonSync](docs/writeJson-sync.md)


**NOTE:** You can still use the native Node.js methods. They are promisified and copied over to `@xdanangelxoqenpm/officiis-eos-iste`. See [notes on `fs.read()`, `fs.write()`, & `fs.writev()`](docs/fs-read-write-writev.md)

### What happened to `walk()` and `walkSync()`?

They were removed from `@xdanangelxoqenpm/officiis-eos-iste` in v2.0.0. If you need the functionality, `walk` and `walkSync` are available as separate packages, [`klaw`](https://github.com/jprichardson/node-klaw) and [`klaw-sync`](https://github.com/manidlou/node-klaw-sync).


Third Party
-----------

### CLI

[fse-cli](https://www.npmjs.com/package/@atao60/fse-cli) allows you to run `@xdanangelxoqenpm/officiis-eos-iste` from a console or from [npm](https://www.npmjs.com) scripts.

### TypeScript

If you like TypeScript, you can use `@xdanangelxoqenpm/officiis-eos-iste` with it: https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/@xdanangelxoqenpm/officiis-eos-iste


### File / Directory Watching

If you want to watch for changes to files or directories, then you should use [chokidar](https://github.com/paulmillr/chokidar).

### Obtain Filesystem (Devices, Partitions) Information

[fs-filesystem](https://github.com/arthurintelligence/node-fs-filesystem) allows you to read the state of the filesystem of the host on which it is run. It returns information about both the devices and the partitions (volumes) of the system.

### Misc.

- [@xdanangelxoqenpm/officiis-eos-iste-debug](https://github.com/jdxcode/@xdanangelxoqenpm/officiis-eos-iste-debug) - Send your @xdanangelxoqenpm/officiis-eos-iste calls to [debug](https://npmjs.org/package/debug).
- [mfs](https://github.com/cadorn/mfs) - Monitor your @xdanangelxoqenpm/officiis-eos-iste calls.



Hacking on @xdanangelxoqenpm/officiis-eos-iste
-------------------

Wanna hack on `@xdanangelxoqenpm/officiis-eos-iste`? Great! Your help is needed! [@xdanangelxoqenpm/officiis-eos-iste is one of the most depended upon Node.js packages](http://nodei.co/npm/@xdanangelxoqenpm/officiis-eos-iste.png?downloads=true&downloadRank=true&stars=true). This project
uses [JavaScript Standard Style](https://github.com/feross/standard) - if the name or style choices bother you,
you're gonna have to get over it :) If `standard` is good enough for `npm`, it's good enough for `@xdanangelxoqenpm/officiis-eos-iste`.

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

What's needed?
- First, take a look at existing issues. Those are probably going to be where the priority lies.
- More tests for edge cases. Specifically on different platforms. There can never be enough tests.
- Improve test coverage.

Note: If you make any big changes, **you should definitely file an issue for discussion first.**

### Running the Test Suite

@xdanangelxoqenpm/officiis-eos-iste contains hundreds of tests.

- `npm run lint`: runs the linter ([standard](http://standardjs.com/))
- `npm run unit`: runs the unit tests
- `npm run unit-esm`: runs tests for `@xdanangelxoqenpm/officiis-eos-iste/esm` exports
- `npm test`: runs the linter and all tests

When running unit tests, set the environment variable `CROSS_DEVICE_PATH` to the absolute path of an empty directory on another device (like a thumb drive) to enable cross-device move tests.


### Windows

If you run the tests on the Windows and receive a lot of symbolic link `EPERM` permission errors, it's
because on Windows you need elevated privilege to create symbolic links. You can add this to your Windows's
account by following the instructions here: http://superuser.com/questions/104845/permission-to-make-symbolic-links-in-windows-7
However, I didn't have much luck doing this.

Since I develop on Mac OS X, I use VMWare Fusion for Windows testing. I create a shared folder that I map to a drive on Windows.
I open the `Node.js command prompt` and run as `Administrator`. I then map the network drive running the following command:

    net use z: "\\vmware-host\Shared Folders"

I can then navigate to my `@xdanangelxoqenpm/officiis-eos-iste` directory and run the tests.


Naming
------

I put a lot of thought into the naming of these functions. Inspired by @coolaj86's request. So he deserves much of the credit for raising the issue. See discussion(s) here:

* https://github.com/xdanangelxoqenpm/officiis-eos-iste/issues/2
* https://github.com/flatiron/utile/issues/11
* https://github.com/ryanmcgrath/wrench-js/issues/29
* https://github.com/substack/node-mkdirp/issues/17

First, I believe that in as many cases as possible, the [Node.js naming schemes](http://nodejs.org/api/fs.html) should be chosen. However, there are problems with the Node.js own naming schemes.

For example, `fs.readFile()` and `fs.readdir()`: the **F** is capitalized in *File* and the **d** is not capitalized in *dir*. Perhaps a bit pedantic, but they should still be consistent. Also, Node.js has chosen a lot of POSIX naming schemes, which I believe is great. See: `fs.mkdir()`, `fs.rmdir()`, `fs.chown()`, etc.

We have a dilemma though. How do you consistently name methods that perform the following POSIX commands: `cp`, `cp -r`, `mkdir -p`, and `rm -rf`?

My perspective: when in doubt, err on the side of simplicity. A directory is just a hierarchical grouping of directories and files. Consider that for a moment. So when you want to copy it or remove it, in most cases you'll want to copy or remove all of its contents. When you want to create a directory, if the directory that it's suppose to be contained in does not exist, then in most cases you'll want to create that too.

So, if you want to remove a file or a directory regardless of whether it has contents, just call `fs.remove(path)`. If you want to copy a file or a directory whether it has contents, just call `fs.copy(source, destination)`. If you want to create a directory regardless of whether its parent directories exist, just call `fs.mkdirs(path)` or `fs.mkdirp(path)`.


Credit
------

`@xdanangelxoqenpm/officiis-eos-iste` wouldn't be possible without using the modules from the following authors:

- [Isaac Shlueter](https://github.com/isaacs)
- [Charlie McConnel](https://github.com/avianflu)
- [James Halliday](https://github.com/substack)
- [Andrew Kelley](https://github.com/andrewrk)




License
-------

Licensed under MIT

Copyright (c) 2011-2024 [JP Richardson](https://github.com/jprichardson)

[1]: http://nodejs.org/docs/latest/api/fs.html


[jsonfile]: https://github.com/jprichardson/node-jsonfile
