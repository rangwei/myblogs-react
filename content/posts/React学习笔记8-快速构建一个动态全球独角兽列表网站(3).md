---
title: "React学习笔记8"
date: 2020-02-08T09:38:48+08:00
draft: true
---

# 页面开发

页面开发很简单。分为两个部分。
通过React的Function Component来实现列表和翻页条。

## 列表显示
List.js:

```
import React, { useState } from 'react';


export default function List({unicorns}) {
    return (
        <table class="table table-light table-hover table-bordered">
            <thead>
                <tr>
                    <th scope="col">Name</th>
                    <th scope="col">Country</th>
                    <th scope="col">Founded on</th>
                    <th scope="col">Category</th>
                </tr>
            </thead>
            <tbody>
                {
                    unicorns.map(
                        (item) => <tr>
                            <td>{item.name}</td>
                            <td>{item.country}</td>
                            <td>{item.founded_on}</td>
                            <td>{item.category}</td>
                        </tr>
                    )
                }

            </tbody>
        </table>

    );
}

```
## 翻页条
根据当前的页面总数来展示，并且高亮显示当前页。

Page.js:

```
import React, { Component } from 'react';

// import unicorns from './data/unicorns.json';
import { Link } from 'react-router-dom';


export default function Page(props) {

    const total = props.totalNumbers;
    const pages = Math.ceil(total / 50);
    const current = props.currentPage;

    let pageNumbers = [];

    for (let i = 1; i <= pages; i++) {
        pageNumbers.push(i);
    }

    return (
        <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item" key="previous"><a class="page-link" href="#">Previous</a></li>

                {
                    pageNumbers.map(
                        // number => <li class="page-item"><a class="page-link" href="/unicorns/">{number}</a></li>
                        number => {

                            if (number === Number(current)) {
                                return <li class="page-item active" key={number} ><Link class="page-link" to={"/unicorns/" + number} onClick={() => { props.handleClick(number); }}>{number}</Link></li>;
                            } else {
                                return <li class="page-item" key={number} ><Link class="page-link" to={"/unicorns/" + number} onClick={() => { props.handleClick(number); }}>{number}</Link></li>;
                            }
                        }
                    )
                }

                <li class="page-item" key="next"><a class="page-link" href="#">Next</a></li>
            </ul>
        </nav>

    );
}
```

## 项目代码

https://github.com/rangwei/unicorns-react-bootstrap
