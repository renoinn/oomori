---
title: "ReactNative+Redux+Realmでアプリを作る"
date: 2018-07-22T12:59:19+09:00
draft: true
---

```
npm install -g react-native-cli
npm install -g create-react-native-app
```

```
$ create-react-native-app my-native
$ cd my-native
$ npm run ios
```
最初は起動時にこのコマンド実行しろと怒られるので素直に実行する。
```
$ sudo sysctl -w kern.maxfiles=5242880
$ sudo sysctl -w kern.maxfilesperproc=524288
```
これでひとまず起動はするようになる。
次にreduxをインストール。
```
$ npm install redux react-redux --save
```
今回はrealmを使う予定なので、realmをインストールする。
```
$ npm install --save realm
```
普通にインストールされるもんだと思ってたらまさかのエラー発生。
```
node-pre-gyp ERR! Tried to download(404): https://static.realm.io/node-pre-gyp/2.13.0/realm-v2.13.0-node-v64-darwin-x64.tar.gz 
```
とかメッセージが出てる。いろいろ探してたら原因はNodeのバージョンだった。

[Support Node 10. WAS: Realm fails to install via yarn or npm, with the error Failed to execute node-gyp build --fallback-to-build --module=[hidden_path]/node_modules/realm/compiled/node-v64_darwin_x64/realm.node](https://github.com/realm/realm-js/issues/1813)

どうやらrealmのJS版はNode v10.xをサポートしていないらしい。今後サポートする予定ではあるっぽいけど、ひとまずNodeのバージョンを下げてインストールする。
```
$ nodebrew install v9.11.2
$ nodebrew use v9.11.2
$ npm install --save realm
$ react-native link realm
```
