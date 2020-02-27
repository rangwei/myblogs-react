---
title: "React学习笔记7"
date: 2020-02-07T09:38:48+08:00
draft: true
---

# 后端API开发

通过Sails.js可以快速构建一个后端的服务。

## 建模

通过下面这条命令来新建一个model:
```
sails generate api Unicorns
```
建模，修改Unicorns.js:
```
module.exports = {

  attributes: {

    name: { type: 'string', required: true },
    country: { type: 'string' },
    last_funding_on: { type: 'string', columnType: 'date' },
    total_equity_funding: { type: 'number' },
    founded_on: { type: 'number' },
    category: { type: 'string' },
    post_money_val: { type: 'number' }
  },

};

```
对于数据的CRUD操作，Sails.js的Bluprint立刻自动生成了RESTFul的API。
可以通过http://localhost:1337/Unicorns来访问服务。

## 数据库中导入数据
通过下面这条命令来新建一个action:
```
sails generate action import
```

import.js:
```
const data = require('../../tools/unicorns');

module.exports = {


  friendlyName: 'Import',


  description: 'Import something.',


  inputs: {

  },


  exits: {

  },


  fn: async function (inputs) {

    const unicorns = [...data];

    unicorns.forEach(
        u => {
            delete u.logo_url;
            delete u.permalink;
            delete u.tag_page;
            delete u.unicorn_bday;
            delete u.unicorn_exit;
            delete u.rumored;
            delete u.valuation_change;
            delete u.date_of_valuation;

            if (u.total_equity_funding === null) {
              u.total_equity_funding = 0;
            }

        }
    );

    const result = await Unicorns.createEach(unicorns);
    return result;

  }


};

```
修改route.js文件：

```
'/api/v1/import' : {action: 'import'},
```

通过http://localhost:1337/api/v1/import可以从准备的测试数据中自动把数据导入到数据库。
## 定制api

通过下面这条命令来新建一个action:
```
sails generate action count
```

count.js:
```
module.exports = {


  friendlyName: 'Count',


  description: 'Count something.',


  inputs: {

  },


  exits: {

  },


  fn: async function (inputs) {

    const result = await Unicorns.count();

    return { total: result };

  }


};

```
修改route.js文件：

```
 '/api/v1/count' : {action: 'count'}
```
通过http://localhost:1337/api/v1/count可以获取到数据的条数。

## 全部API清单:

1. Unicorns CRUD:
http://localhost:1337/unicorns

2. 导入测试数据:
http://localhost:1337/api/v1/Import

3. 数据条数:
http://localhost:1337/api/v1/count

## 项目代码

https://github.com/rangwei/unicorns-sails
