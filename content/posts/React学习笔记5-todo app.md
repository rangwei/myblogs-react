---
title: "React学习笔记5"
date: 2020-02-05T09:38:48+08:00
draft: true
---

# TODO App

> 三人行，必有我师焉。择其善者而从之，其不善者而改之。 ——孔子

现在通过前面学到的React基础知识快速构建一个简单的TODO APP。

主要包含三个部分： 输入部分，未完成的事项，已经完成事项。

## 输入部分

```
function Input({ addName }) {

    const [name, setName] = useState("hello");

    return (
        <div>
            <h1>todo App</h1>
            <br />
            <input type="text" name="" value={name} onChange={(e) => setName(e.target.value)} />
            <button type="button" name="button" onClick={() => addName(name)}>add todo</button>
        </div>
    );
}
```
输入部分包含一个输入框和一个按钮。

## 未完成事项

```
function TodoList({ list, change }) {

    return (

        <ul>
            {list.map(item => <li><input type="checkbox" name="" checked={item.completed} value={item.name} onChange={(e) => change(e.target.value)} />{item.name}</li>)}
        </ul>
    );
}
```
未完成部分是一个列表每一行包含了一个复选框和内容。

## 已完成事项

```
function CompleteList({ list, change }) {

    return (
        <div>
            <p>Completed tasks</p>
            <ul>

                {list.map(
                    item => <li><input type="checkbox" name="" checked={item.completed} value={item.name}  onChange={(e) => change(e.target.value)} />{item.name}</li>
                )}
            </ul>
        </div>
    );
}
```
已经完成部分也是一个列表，每一行包含一个输入框和内容。

## TODOApp

```
function TodoApp() {

    const todos = [
        { "name": "aaa", "completed": false },
        { "name": "bbb", "completed": false },
        { "name": "ccc", "completed": false },
    ];

    const [list, setList] = useState(todos);

    const add = name => {

        const item = { name, completed: false };
        const newList = [...list];
        newList.push(item);

        setList(newList);

    };

    const change = name => {

        const newList = [];

        for (let item of list) {

            if (item.name === name) {

                item.completed = !item.completed
            }
            newList.push(item);
        }
        setList(newList);
    }

    return (
    <div>
        <Input addName={add} />
        <TodoList list={list.filter(u => !u.completed)} change={change} />
        <CompleteList list={list.filter(u => u.completed)} change={change} />
    </div>);
}
```
app的逻辑很简单，在输入内容后增加到列表中。然后根据完成状态分别在两个不同的列表组件中显示。

## 小结

React的设计思想非常棒。先写好每个组件的内容，然后增加事件的代码。
通过function component，可以让代码看起来更加简洁，bug也会更少。

# 参考阅读
- https://reactjs.org/
