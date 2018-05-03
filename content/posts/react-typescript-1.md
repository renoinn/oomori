---
title: "create-react-appからTypescript+Reactで動かすまで"
date: 2018-05-03T12:48:44+09:00
draft: false
Tags:
    - javascript
    - react
---

```bash
$ create-react-app my-app
$ npm run eject
$ npm install -g webpack
$ npm install --save @types/react @types/react-dom
$ npm install --save-dev typescript ts-loader source-map-loader
$ vim tsconfig.json
```

`tsconfig.json`を作る。内容は下記。
```json
{
    "compilerOptions": {
        "outDir": "./dist/",
        "sourceMap": true,
        "noImplicitAny": true,
        "module": "commonjs",
        "target": "es5",
        "jsx": "react"
    },
    "include": [
        "./src/**/*"
    ]
}
```

`config/paths.js`のappIndexJsのパスをindex.tsxのパスに変更する。

```diff
// config after eject: we're in ./config/
module.exports = {
  dotenv: resolveApp('.env'),
  appBuild: resolveApp('build'),
  appPublic: resolveApp('public'),
  appHtml: resolveApp('public/index.html'),
-  appIndexJs: resolveApp('src/index.js'),
+  appIndexJs: resolveApp('src/index.tsx'),
  appPackageJson: resolveApp('package.json'),
  appSrc: resolveApp('src'),
  yarnLockFile: resolveApp('yarn.lock'),
  testsSetup: resolveApp('src/setupTests.js'),
  appNodeModules: resolveApp('node_modules'),
  publicUrl: getPublicUrl(resolveApp('package.json')),
  servedPath: getServedPath(resolveApp('package.json')),
};
```

modules.rules`に追加。

```
{                                                                                                                                            
  test: /\.(ts|tsx)$/,
  include: paths.appSrc,
  use: [ 
    { 
      loader: require.resolve('ts-loader'),
      options: { 
        // disable type checker - we will use it in fork plugin
        transpileOnly: true,
      },
    },
  ],
},
```

typescriptのドキュメント見るとawesome-typescript-loader使ってるんだけど、こいつがwebpackの4.x系に依存しているっぽくて、create-react−appにバンドルされてるwebpackが3.8.1なので

```
Module build failed: TypeError: Cannot read property 'watchRun' of undefined
```

こんな感じのエラーが出てしまう。依存関係解決しようとすると時間かかってしまいそうなので、ts−loaderでお茶を濁す。

あとは適当にindex.tsxを用意して、`npm run start`する。

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

## 追記
この作業している最中に見つけたのだけど、[create-react-app-typescript](https://github.com/wmonk/create-react-app-typescript)というパッケージが存在する。特に深く考えたくない時はこっちを利用した方が良さそう。

## 参考リンク
- [React & Webpack &middot; TypeScript](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)
- [React + TypeScript + Webpackの最小構成](https://qiita.com/uryyyyyyy/items/63969d6ed9341affdffb)
