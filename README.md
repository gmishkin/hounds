#hounds

![](https://media.giphy.com/media/TVCqfX7rLyMuY/giphy.gif)

A utility to smoke test a site by releasing hounds to follow all internal links and log any console errors. Uses [nightmare](https://github.com/segmentio/nightmare) to fire up an Electron webkit browser (with optional UI).

[![CircleCI](https://circleci.com/gh/justinjmoses/hounds.svg?style=svg)](https://circleci.com/gh/justinjmoses/hounds)

##Upcoming Releases

Currently
[![npm version](https://badge.fury.io/js/hounds.svg)](https://badge.fury.io/js/hounds)
[![GitHub version](https://badge.fury.io/gh/justinjmoses%2Fhounds.svg)](https://badge.fury.io/gh/justinjmoses%2Fhounds)

> Note: Currently only returns errors within the actual URL (no link following just yet)

* ~~`0.2.0` Supports a single url with a promise~~
* ~~`0.3.0` Stream support (instead of promises)~~
    * ~~`0.3.1` Migrated to [nightmare](https://github.com/segmentio/nightmare) - 3x faster than Webdriver/Phantom2 and option to open up devTools~~
    * ~~`0.3.2` Stream usage cleanup~~
* `0.4.0` Handle console errors that occur after `DOMContentLoaded` (with configurable timeout)
* `0.5.0` Follow and track all internal links
* `0.6.0` Allow for `setup`/`teardown` actions in nightmare (such as login) (or perhaps just use cookies) 

##Usage

`npm i hounds`

```javascript
const hounds = require('hounds')
const hunt = hounds.release({ url: 'http://localhost:8080' })
    .on('error', console.error)
    .on('end', process.exit)

const quarry = new Writable({
    objectMode: true,
    write: (chunk, enc, next) => {
        console.dir(chunk)P
        next()
    }
})

hunt.pipe(quarry)
```

