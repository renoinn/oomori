---
title: "nodebrewでnodejsをアップデートする"
date: 2018-05-01T17:32:27+09:00
draft: false
Tags:
    - javascript
    - nodejs
---

気付いたら最新版と自分の環境がかなり離れてしまったので、[nodebrew](https://github.com/hokaccha/nodebrew)で開発環境をアップデートする。

```
$ nodebrew install stable
$ nodebrew use stable
$ node -v
v10.0.0
```

ついでに、npmもアップデートする。

```
$ npm install -g npm
$ npm version
{ npm: '6.0.0',
  ares: '1.14.0',
  cldr: '33.0',
  http_parser: '2.8.0',
  icu: '61.1',
  modules: '64',
  napi: '3',
  nghttp2: '1.29.0',
  node: '10.0.0',
  openssl: '1.1.0h',
  tz: '2018c',
  unicode: '10.0',
  uv: '1.20.2',
  v8: '6.6.346.24-node.5',
  zlib: '1.2.11' }
```
