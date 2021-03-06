---
title: 在 Laravel 8.0 整合 Vue CLI
permalink: 在-Laravel-8-0-整合-Vue-CLI
date: 2020-10-08 09:19:23
tags: ["程式設計", "PHP", "Laravel", "Vue"]
categories: ["程式設計", "PHP", "Laravel"]
---

## 做法

建立專案。

```BASH
laravel new laravel-vue-cli-example
```

刪除與前端有關的檔案與目錄。

```BASH
rm -rf package.json \
  webpack.mix.js \
  resources/views/welcome.blade.php \
  resources/{js,sass}
```

進到 `resources` 資料夾，新增 Vue 專案。

```BASH
cd resources
vue create js
```

在 Vue 專案中建立 `vue.config.js` 檔：

```JS
module.exports = {
  outputDir: '../../public',
  indexPath: process.env.NODE_ENV === 'production'
    ? '../resources/views/app.blade.php'
    : 'index.html',
};
```

修改 Vue 專案中的 `package.json` 檔：

```JSON
{
  "name": "laravel-vue-cli-example",
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "rm -rf ../../public/{js,css,img} && vue-cli-service build --no-clean",
    "lint": "vue-cli-service lint"
  }
}
```

修改後端的 `web.php` 路由：

```PHP
Route::get('/{any}', function () {
    return view('app');
})->where('any', '.*');
```

修改根目錄的 `.gitignore` 檔：

```ENV
/public/js
/public/css
/public/img
/resources/views/app.blade.php
```

## 編譯

進到 Vue 專案，啟動服務。

```BASH
yarn serve
```

進到 Vue 專案，編譯靜態檔案。

```BASH
yarn build
```

## 參考資料

- [laravel-vue-cli-3](https://github.com/yyx990803/laravel-vue-cli-3)

## 程式碼

- [laravel-vue-cli-example](https://github.com/memochou1993/laravel-vue-cli-example)
