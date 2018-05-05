---
title: "React+Redux+TypescriptでTodoListを作る"
date: 2018-05-05T21:36:32+09:00
draft: false
Tags:
    - javascript
    - react
---

create-react-appのTypescript版で[react-scripts-ts](https://www.npmjs.com/package/react-scripts-ts)があるので、それを使ってTodoListを作る。

```
$ create-react-app todo-list --scripts-version=react-scripts-ts
$ cd todo-list
$ npm install redux react-redux --save
$ npm install @types/react-redux -dev
```

これでReact+Redux+Typescriptの開発環境が整う。webpackのconfigとか一から書く必要がないのは本当に素晴らしい。

そのままでも良いけど、tslint.jsonを[react-redux-typescript-guide](https://github.com/piotrwitek/react-redux-typescript-guide)を参考に編集。

```
{
  "extends": ["tslint:recommended", "tslint-react", "tslint-config-prettier"],
  "rules": {
    "arrow-parens": false,
    "arrow-return-shorthand": [false],
    "comment-format": [true, "check-space"],
    "import-blacklist": [true, "rxjs"],
    "interface-over-type-literal": false,
    "interface-name": false,
    "max-line-length": [true, 120],
    "member-access": false,
    "member-ordering": [true, { "order": "fields-first" }],
    "newline-before-return": false,
    "no-any": false,
    "no-empty-interface": false,
    "no-import-side-effect": [true],
    "no-inferrable-types": [true, "ignore-params", "ignore-properties"],
    "no-invalid-this": [true, "check-function-in-method"],
    "no-null-keyword": false,
    "no-require-imports": false,
    "no-submodule-imports": [true, "@src", "rxjs"],
    "no-this-assignment": [true, { "allow-destructuring": true }],
    "no-trailing-whitespace": true,
    "no-unused-variable": [true, "react"],
    "object-literal-sort-keys": false,
    "object-literal-shorthand": false,
    "one-variable-per-declaration": [false],
    "only-arrow-functions": [true, "allow-declarations"],
    "ordered-imports": [false],
    "prefer-method-signature": false,
    "prefer-template": [true, "allow-single-concat"],
    "quotemark": [true, "single", "jsx-double"],
    "semicolon": [true, "always"],
    "trailing-comma": [true, {
      "singleline": "never",
      "multiline": {
        "objects": "always",
        "arrays": "always",
        "functions": "never",
        "typeLiterals": "ignore"
      },
      "esSpecCompliant": true
      }],
      "triple-equals": [true, "allow-null-check"],
      "type-literal-delimiter": true,    
      "typedef": [true,"parameter", "property-declaration"],
      "variable-name": [true, "ban-keywords", "check-format", "allow-pascal-case", "allow-leading-underscore"],
      // tslint-react
      "jsx-no-multiline-js": false,
      "jsx-no-lambda": false
  },
  "linterOptions": {
    "exclude": [
      "config/**/*.js",
      "node_modules/**/*.ts"
    ]
  }
}
```

あとは、[TodoList簡易版@Typescript+React+Redux](https://qiita.com/knknkn1162/items/94543bf8c0701f25ac77)を参考にComponentやAction、Reducerを作っていく。

最終的なコードはこんな感じ。<br>
https://github.com/renoinn/react-todo-list
