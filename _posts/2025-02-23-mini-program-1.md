---
title: "小程序的项目结构"
date: 2025-02-23
excerpt: "博文中涵盖了小程序的基本项目结构。"
layout: post
---
# 小程序的项目结构
- pages用来存放所有小程序的页面；
- utils用来存放工具性质的模块；
- `app.js`是小程序项目的入口文件；
- `app.json`是小程序项目的全局配置文件；
- `app.wxss`是小程序项目的全局样式文件；
- `project.config.json`项目的配置文件。

## Pages
官方建议把所有小程序的页面都放在Pages目录中，以单独的文件夹存在。每个页面由**四个基本文件**组成：`.js`（页面脚本文件，存放事件处理函数）`.json`（当前页面的配置文件，配置窗口的外观等）`.wxml`（结构文件）`.wxss`（样式文件）。

- `json`是一种数据格式，小程序中作为配置文件
    - `app.json`，**全局配置文件**，包括小程序所有页面路径、窗口外观、界面表现、底部tab等
        ```json
        {
        "pages": [ // 记录所有页面的路径
            "pages/index/index", 
            "pages/logs/logs"
        ],
        "window": { // 全局定义小程序所有页面的背景色、文字颜色等
            "navigationBarTextStyle": "black",
            "navigationBarTitleText": "Weixin",
            "navigationBarBackgroundColor": "#ffffff"
        },
        "style": "v2", // 全局定义小程序组件所使用的样式版本
        "componentFramework": "glass-easel",
        "sitemapLocation": "sitemap.json", // 指明sitemap.json文件存放的位置
        "lazyCodeLoading": "requiredComponents"
        }
        ```
    - `project.config.json`项目配置文件，记录对**小程序开发工具所做的个性化配置**，例如`setting`字段保存了编译相关的配置，`projectname`中保存项目的名称等。
    现在又出现了一个`project.private.config.json`文件，**项目私有配置文件**，此文件中的内容会覆盖`project.config.json`中的相同字段，**项目的改写优先写到该文件中**。[对应文档](https://developers.weixin.qq.com/miniprogram/dev/devtools/projectconfig.html)
    