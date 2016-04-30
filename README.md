# PageXray

[![Build status][travis-image]][travis-url]

Convert a HAR to a summary of a page, describing what's important of a web page in a performance perspective to a page. This is a part of the coming sitespeed.io 4.0 but you can use it standalone.

## What do we collect?
 * The size and the number of requests per content type
 * The size and requests per domain
 * The number of requests per response code
 * The base domain and the httpVersion used for the base asset (the main HTML document)
 * All assets (responses) with the following data: type, url, size, expires (a normalized expires convering max-age/expires to just expires in seconds), status (response code), timeSinceLastModified (using the last modified field in the reponse header and normalizing to seconds), httpVersion and all request and response headers.

## Install
```bash
npm install pagexray -g
```

## Run
```bash
pagexray /path/to/my.har
```

Or if you want to prettify the HAR
```bash
pagexray --pretty /path/to/my.har
```
And if you want to get info per request/response:
```bash
pagexray -includeAssets /path/to/my.har
```

If you want to use it in node, use it like this:
```node
let pagexray = require('pagexray');
let har = // your HAR
let pages = pagexray.convert(har);
```
## Output
All sizes are in bytes. Expires and timeSinceLastModified are in seconds.

```json
[
  {
    "url": "https://run.sitespeed.io/",
    "finalUrl": "https://run.sitespeed.io/",
    "baseDomain": "run.sitespeed.io",
    "documentRedirects": -1,
    "redirectChain": [],
    "transferSize": 102069,
    "contentSize": 102069,
    "headerSize": 6480,
    "requests": 11,
    "httpType": "h2",
    "httpVersion": "HTTP/2.0",
    "contentTypes": {
      "html": {
        "transferSize": 12311,
        "contentSize": 12311,
        "headerSize": 582,
        "requests": 1
      },
      "javascript": {
        "transferSize": 26285,
        "contentSize": 26285,
        "headerSize": 347,
        "requests": 1
      },
      "image": {
        "transferSize": 11855,
        "contentSize": 11855,
        "headerSize": 984,
        "requests": 2
      },
      "svg": {
        "transferSize": 45100,
        "contentSize": 45100,
        "headerSize": 3923,
        "requests": 6
      },
      "favicon": {
        "transferSize": 6518,
        "contentSize": 6518,
        "headerSize": 644,
        "requests": 1
      }
    },
    "assets": [],
    "responseCodes": {
      "200": 11
    },
    "domains": {
      "run.sitespeed.io": {
        "requests": 9,
        "transferSize": 75749,
        "contentSize": 75749,
        "headerSize": 5788
      },
      "www.google-analytics.com": {
        "requests": 2,
        "transferSize": 26320,
        "contentSize": 26320,
        "headerSize": 692
      }
    },
    "expireStats": {
      "min": "0",
      "p10": "0",
      "median": "31536000",
      "p90": "31536000",
      "p99": "31536000",
      "max": "31536000"
    },
    "lastModifiedStats": {
      "min": "15293097",
      "p10": "18613493",
      "median": "18613493",
      "p90": "566681353",
      "p99": "566681353",
      "max": "566681353"
    }
  }
]

```

[travis-image]: https://img.shields.io/travis/sitespeedio/pagexray.svg?style=flat-square
[travis-url]: https://travis-ci.org/sitespeedio/pagexray
