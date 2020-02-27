---
title: "React学习笔记3"
date: 2020-02-03T09:38:48+08:00
draft: true
---

# State Hook

> 吾生也有涯，而知也无涯。——庄子

接着学习一下React的State Hook。

通过State hook，可以直接通过function来构建有状态的组件，只要引入useState方法即可。

写了一个小例子，包含一个输入和列表，分别通过两个function实现。
输入的数据通过一个列表展示：

```
import React, { useState } from 'react';


function Input({ addName }) {
  const [name, setName] = useState("hello");

  return (
    <div>
      <label for="">name</label>
      <input type="text" name="" value={name} onChange={(e) => { setName(e.target.value) }} />
      <button type="button" name="button" onClick={() => { addName(name); }}>click me!</button>
    </div>
  );
}

function List({ nameList }) {
  return (

    <ul>
      {nameList.map(n => <li>{n}</li>)}
    </ul>
  );
}

function NameTool() {


  const [list, setList] = useState([]);

  const add = name => {

    const newList = [...list];
    newList.push(name);
    setList(newList);


  };

  return (<div>
    <Input addName={add} />
    <List nameList={list} />
  </div>);
}

function App() {
  return <NameTool />;
}


```
React的useState用到了destructing解析赋值的语法。声明了一个state和修改state的方法。

另外需要注意的是，通过定义个方法然后传给子组件来更新状态，是非常常见的用法。

## 参考阅读

- https://reactjs.org/docs/hooks-state.html
