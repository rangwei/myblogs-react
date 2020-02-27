---
title: "React学习笔记2"
date: 2020-02-02T09:38:48+08:00
draft: true
---

# Function Component

> 学无止境。——荀子

接着学习一下React的function component。

之前React主要通过class的方式来构建UI组件，但是可能在很多项目中存在一些弊端。Facebook设计了React Hook的方式，可以不通过class的方式来完成同样的功能。也就是只需要通过function component即可，这样带来的好处是代码更简单，bug更少。

## 简单的Component

先看看一个简单的function component:

```
import React from 'react';

function Welcome({name}) {
  return <h1>{name}</h1>;
}

function App() {
  return (
    <Welcome name="abc"/>
  );
}

export default App;

```
这里Welcome({name})用到了destructing解析赋值的语法。

## Component组合

function component 可以组合， 把之前做的问卷调查小Demo重构一下：

```
import React, { useState } from 'react';


function Question({question, name, change}) {
  return (
    <div>
      <label for="">{question}</label>
      <input type="radio" id="1" name={name} value="0" onChange={change}/>
      <label for="">超级满意</label>
      <input type="radio" id="2" name={name} value="1" onChange={change}/>
      <label for="">比较满意</label>
      <input type="radio" id="3" name={name} value="2" onChange={change}/>
      <label for="">满意</label>
      <input type="radio" id="4" name={name} value="3" onChange={change}/>
      <label for="">不满意</label>
      <input type="radio" id="5" name={name} value="4" onChange={change}/>
      <label for="">超级不满意</label>
    </div>
  );
}

function SimpleSurvey({questions}) {


  let result = [];

  for (let q in questions) {
    result.push(0);
  }

  const handleChange = (e) => {

      let index = questions.indexOf(e.target.name);

      result[index] = e.target.value;

  };

  const onSubmit = (e) => {

    e.preventDefault();

    console.log(result);
  }

  return (

    <form onSubmit= {onSubmit}>

      {
        questions.map(q=> <Question question={q} name={q} change={handleChange}/>)
      }

      <input type="submit" value="提交"/>

    </form>

  );
}

function App() {
  return <SimpleSurvey questions={["q1", "q2", "q3", "q4"]}/>;
}

export default App;

```

## 参考阅读

- https://reactjs.org/
- https://blog.csdn.net/starshus/article/details/104393826
