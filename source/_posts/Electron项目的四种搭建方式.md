---
title: Electron项目的四种搭建方式
date: 2020-04-29 22:48:12
tags:
---

在 GitHub 上搜索 `create electron` 会出现很多结果, 列举几个星数较多的:

- generator-electron
- electron-with-create-react-app
- electron-forge
- electron-boilerplate
- menubar
- ...

这里面有生成器, 有模版, 下面简单列举几个我用过的搭建方式

``` bash
# 镜像
ELECTRON_MIRROR="https://cdn.npm.taobao.org/dist/electron/"
```

## 原生

<https://github.com/ccforeverd/electron-tmp>

<https://github.com/electron/electron-quick-start>

所谓原生, 就是官网文档的 `quick start`

``` bash
yarn add electron
mkdir app
touch app/index.js

```

然后我又加上了 `Vue`

``` bash
vue create .
```

把链接更换一下

``` js
mainWindow.loadUrl('http://localhost:8080')
```

使用两个命令行同时打开

``` bash
yarn serve // terminal1
yarn start // terminal2
```

## electron-forge

<https://github.com/ccforeverd/electron-tmp2>

<https://github.com/electron-userland/electron-forge>

根据官网的文档配置, 加入多个页面, 加入preload

## vue-electron-builder

<https://github.com/ccforeverd/electron-tmp2>

使用vue插件安装

``` bash
vue create . # 初始化
vue add electron-builder # 安装electron插件
yarn electron:serve # 开发
```

## electron-webpack

<https://github.com/ccforeverd/electron-tmp2>

<https://github.com/electron-userland/electron-webpack-quick-start>

## 总结

- 使用原生搭建项目
  - 需要将两个命令行合二为一
  - app内文件无法编译
  - 打包时要去掉原生node和electron包的引入
- 使用 electron-forge 搭建项目
  - 可分多个页面
  - 支持 preload
  - 对字体文件引入有问题, 无法解决
- 使用 vue-cli 搭建项目
  - 是单页应用, 如果分多个页面, 配置要麻烦许多
  - 不支持 preload, 待研究
- 使用 webpack-electron 搭建项目
  - 是单页应用, 不支持多个分页, 只有一个 renderer
  - 对 preload 的支持很蛋疼, 要么无法引入, 要么没有编译

目前选用的是 `electron-forge` 的方式, 因为 `preload` 很重要, 跨项目包壳就靠它

__很多问题都出在webpack配置上__, 如果真的想要舒适的开发, 必须深入研究webpack
