---
title: 'issvue: Everything about it'
tags:
  - blog
  - Originals
number: 5
date: 2017-04-17 16:17:11
---

## 有话说

一直都觉得用issue写blog简直是懒人福音。
但是github issue的层级太深，一直不大像一个blog。
于是有了这个idea。

这个idea出来之后前后花了一天把它实现了。

做完还是挺有成就感的> <

## 关于安装

开始之前，你需要star本项目[issvue](https://github.com/cogons/issvue) （手动滑稽）

首先，你需要有node。

然后，你需要把[项目](https://github.com/cogons/issvue)下载或clone到本地。
`$ git clone https://github.com/cogons/issvue.git`

然后，安装相关包。
`$ cd issvue && npm install`。

然后，把./src/config.js中的配置改成你自己的。
`$ vi ./src/config.js`

然后，生成blog。
`$ npm run build`。

最后，把生成的dist文件夹部署到github-pages，once and for all。

## 项目你所能了解的

- vue-cli
- axios
- Promise
- sessionStorage
- Other minor things ..
