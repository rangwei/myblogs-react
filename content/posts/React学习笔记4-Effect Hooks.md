---
title: "React学习笔记4"
date: 2020-02-04T09:38:48+08:00
draft: true
---

# Effect Hooks

> 由俭入奢易，由奢入俭难。——司马光

之前通过class来编写Component，一些辅助的方法是通过componentDidMount, componentDidUpdate来实现。通过React的effect hook可以实现类似的功能。

比如现在在组件显示之前需要通过网络加载一下数据，还是通过之前用的users api来demo:

```
import React, { useState, useEffect } from 'react';

export default function UserList () {

    const [users, setUsers] = useState([]);

    useEffect(
        () => {
            fetch('https://reqres.in/api/users')
            .then(res => res.json())
            .then(data => setUsers(data.data))
            .catch(e => console.log(e));
        }, []
    );

    return (<ul>{users.map(u => <li>{u.email}</li>)}</ul>);
}
```
这里传给useEffect第二个参数为一个空数组，这样就表示只需要在初始化的时候运行即可，不用每次render都调用。

## 参考阅读
- https://reactjs.org/docs/hooks-effect.html
