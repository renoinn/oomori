---
title: "React to Reactnative"
date: 2018-05-13T16:26:48+09:00
draft: true
---

先日作ったTodoListをReactNativeでアプリにしてみる。
ひとまずプロジェクト作成

```
create-react-native-app todolist-rn --scripts-version=react-native-scripts-ts
cd todolist-rn
sudo sysctl -w kern.maxfiles=5242880
sudo sysctl -w kern.maxfilesperproc=524288
npm run ios
```

action, reducer, statesはそのまま使えそう。問題はcomponent周りなのでReactNative用に書き換えていく。
