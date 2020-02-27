---
title: "React学习笔记9"
date: 2020-02-09T09:38:48+08:00
draft: true
---

# 动态数据展示

## Router
主程序代码，通过react-router-dom来实现页面的Router


App.js：
```
import React from 'react';

import Navbar from './Navbar';
import Unicorns from './Unicorns';
import Main from './Main';
import './master.css';

import { BrowserRouter as Router, Route} from "react-router-dom";

function App() {
  return (
    <Router>
      <Navbar/>
      <Route path="/" exact component={Main} />
      <Route path="/unicorns/:page" component={Unicorns} />
    </Router>

  );
}

export default App;

```

## 设置代理
修改package.json
增加：
```
"proxy": "http://localhost:1337"
```
这样React可以自动代理访问后台api服务。

## 主页面和显示逻辑

设置了几个state，主要用于翻页和获取数据的逻辑，然后通过axios来获取数据，然后通过列表显示。

Unicorns.js:
```
import React, { useState, useEffect } from 'react';

import List from './List';
import Page from './Page';

// import unicorns from './data/unicorns.json';

import axios from 'axios';

export default function Unicorns(props) {

    const [unicorns, setUnicorns] = useState([]);

    const [currentPage, setCurrentPage] = useState(props.match.params.page ? props.match.params.page : 1);

    const [totalNumbers, setTotalNumbers] = useState(0);

    const loadData = () => {
        axios.get('/api/v1/count').then(
            response => setTotalNumbers(
                response.data.total
            )
        ).catch( e => console.log(e));

        const skip = (currentPage - 1) * 50;
        const limit = 50;

        axios.get(`/unicorns?skip=${skip}&limit=${limit}`).then(
            response => setUnicorns(response.data)
        ).catch(e => console.log(e));
    }

    const  handleClick = (pageNumber) => {

        setCurrentPage(pageNumber);
    }

    useEffect(() => {
        loadData();
    }, [currentPage]);


    return (
        <main role="main" class="container">


            <div class="starter-template">
                <h1>全球独角兽</h1>
            </div>

            <List unicorns={unicorns} />

            <Page totalNumbers={totalNumbers} currentPage={currentPage} handleClick={handleClick} />
        </main>
    );
}

```

## 项目代码

https://github.com/rangwei/unicorns-react-bootstrap
