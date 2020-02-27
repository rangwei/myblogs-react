---
title: "React学习笔记12"
date: 2020-02-12T09:38:48+08:00
draft: true
---

# 后台管理开发

后台管理开发也很简单，和前台的开发思路其实差不多，就是增加了几个页面。
新建数据、编辑数据、删除数据。

## 数据展示
在列表中生成了两个链接，分别是编辑和删除。

```
return (

            <div id="content-wrapper" class="mui--text-center">
                <div class="mui--appbar-height"></div>
                <br />
                <br />
                <div class="mui--text-display3">Global Unicorn</div>
                <br />
                <br />
                <table className="mui-table">
                    <thead>
                        <tr>
                            <td>id</td>
                            <td>name</td>
                            <td>country</td>
                            <td>last_funding_on</td>
                            <td>total_equity_funding</td>
                            <td>founded_on</td>
                            <td>category</td>
                            <td>post_money_val</td>
                            <td>operation</td>
                        </tr>
                    </thead>
                    <tbody>

                        {
                            this.props.data.map(
                                u => <tr>
                                    <td>{u.id}</td>
                                    <td>{u.name}</td>
                                    <td>{u.country}</td>
                                    <td>{u.last_funding_on}</td>
                                    <td>{u.total_equity_funding}</td>
                                    <td>{u.founded_on}</td>
                                    <td>{u.category}</td>
                                    <td>{u.post_money_val}</td>
                                    <Link to={"/edit/" + u.id}>edit</Link> | <a href="#" onClick={() => { this.props.delete(u.id) }}>delete</a>
                                </tr>
                            )
                        }
                    </tbody>
                </table>

            </div>
        );
```
## 新建数据
通过axios发送一个post请求来删除数据。
```
axios.post('http://localhost:1337/unicorns/', unicorn).then(
            res => console.log(res)
        );

```

## 编辑数据
通过axios发送一个patch请求来修改数据。
```
axios.patch(`http://localhost:1337/unicorns/${this.props.match.params.id}`, unicorn).then(
            res => console.log(res)
        );

```
## 删除数据
通过axios发送一个delete请求来删除数据。
```
axios.delete('/unicorns/' + id)
            .then(response => { console.log(response.data) });
```
## 翻页
之前自己做了一个简单的翻页。
现在换一种方式，调用react-paginate组件。主页包含了示例代码，用起来很简单。
```
return (
            <div>
                <List data={this.state.data} delete={this.deleteUnicorn} />

                <ReactPaginate
                    previousLabel={'previous'}
                    nextLabel={'next'}
                    breakLabel={'...'}
                    breakClassName={'break-me'}
                    pageCount={this.state.pageCount}
                    marginPagesDisplayed={2}
                    pageRangeDisplayed={5}
                    onPageChange={this.handlePageClick}
                    containerClassName={'pagination'}
                    subContainerClassName={'pages pagination'}
                    activeClassName={'active'}
                />
            </div>
        );
```
## 主应用
通过react-router-dom来实现router。
```
function App() {
  return (
    <Router>

      <Navbar />

      <div className="mui-container">

        <Route path="/" exact component={Unicorns} />
        <Route path="/create" component={Create} />
        <Route path="/edit/:id" component={Edit} />
      </div>
    </Router>
  );
}
```
## 项目代码

https://github.com/rangwei/unicorns-react-managmt
