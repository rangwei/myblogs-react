---
title: "React学习笔记6"
date: 2020-02-06T09:38:48+08:00
draft: true
---

React学习笔记6-快速构建一个动态全球独角兽列表网站(1)

# 设计和架构

下面来通过React实战构建一个关于全球独角兽列表的网站。
主要就是作为一个小练习实践一下从前端到后端的web开发技术。

## 界面设计
最快的方式当然直接用Bootstrap搞定，大概如下：


网页布局主要包含三个部分：导航栏， 主要内容，翻页条。

React的翻页功能有很多库已经可以直接用，但是出于学习的目的，这里还是手工写一个，逻辑也不复杂。

## 后台数据格式
数据结构比较简单，从网上抓取的，主要包含：
独角兽名称，国家，最后一轮融资日期，总融资金额，创建年份，类别，估值，数据示例：

```
{
    "name": "BAIC BJEV",
    "country": "CHN",
    "last_funding_on": "2017-08-01",
    "total_equity_funding": 1660000000,
    "founded_on": 2009,
    "category": "Transportation",
    "post_money_val": 4200000000
  },
  {
    "name": "Intarcia Therapeutics",
    "country": "USA",
    "last_funding_on": "2017-09-01",
    "total_equity_funding": 1400000000,
    "founded_on": 1997,
    "category": "Health Care",
    "post_money_val": 4100000000
  }
```

## 技术架构
后端采用sails.js快速API，前端通过React+Bootstrap实现。

## 项目代码

https://github.com/rangwei/unicorns-bootstrap
