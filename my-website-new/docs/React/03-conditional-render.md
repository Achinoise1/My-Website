# 条件渲染

在多数应用场景下都需要进行条件渲染，例如不同角色不同权限等等。React 中的条件渲染可以根据所处位置，大致分为两种情况：

1. `return` 外的条件渲染
2. `return` 内的条件渲染

本篇的内容都基于 hook 函数举例介绍，此处的 `return` 如下列代码所示：

```jsx
function Test(){
    ...
    return(
        ...
    )
}
```

举例如下，示例网站在未登录情况下导航栏显示 Login ，登录后显示为 Profile，这里姑且称为 Login-Profile 例子。

![LI](img/03/loginIcon.jpg)
![PI](img/03/profileIcon.jpg)

其中，`getUser()` 用于获取用户信息，如果返回的内容存在信息，那么此时显示为 Profile，否则显示为 Login。

## `return` 外的条件渲染

有两种情况，一种直接在 `return` 外部进行判断并渲染，举例如下：

```jsx
import { Spin } from 'antd'
function Test(){
    if (data == null) return <Spin/>
    else return ...
}
```
或者编写函数式常量并调用，顺着 Login-Profile 例子，编写代码如下：
```jsx
function Test(){
    // 可自行决定是否传参，这里是传参版本
    const conRender = (userInfo) => {
        if (typeof (userInfo) == 'object' && Object.keys(userInfo).length == 0) {
            return (
                <li className="nav-item active">
                    <a className="nav-link" href="/login">Login <span className="sr-only">(current)</span> </a>
                </li>
            )
        } else {
            return (
                <li className="nav-item active">
                    <a className="nav-link" href="/profile">Profile <span className="sr-only">(current)</span> </a>
                </li>
            )
        }
    }
    return (
        <div>
            {conRender(...)}
        </div>
    )
}
```

`return` 内不能直接使用 js 代码，调用外部内容也需要用 `{}` 包裹代码。

## `return` 内的条件渲染

### 两种渲染内容——三元运算符

如果只有两种情况的渲染，可以使用如下代码结构。其中，`true-condition` 和 `false-condition` 中为 html 代码。
```jsx
function xxx(){
    return(
        <div>
            {(condition)?(true-condition):(false-condition)}
        </div>
    )
}

// 实例
function Test(){
    return (
        <div>
            {(typeof getUser() === 'object' && Object.keys(getUser()).length === 0) ? (
                <li className="nav-item active">
                    <a className="nav-link" href="/login">Login <span className="sr-only">(current)</span> </a>
                </li>
            ) : (
                <li className="nav-item active">
                    <a className="nav-link" href="/profile">Profile <span className="sr-only">(current)</span> </a>
                </li>
            )}
        </div>
    )
}
```

### 三种及以上的渲染内容

可以通过写函数式常量，然后调用该常量的方法结果（见上），这里主要介绍如何直接写，简单举例如下：

```jsx
function Test() {
    const number = 2;
    return (
        <div>
            {(() => {
                if (number == 2) {
                    return <h1>two</h1>
                } else if (number == 3) {
                    return <h1>three</h1>
                } else if (number == 4) {
                    return <h1>four</h1>
                } else {
                    return <h1>number</h1>
                }
            })()}
        </div>
    )
}
```

这里用到了匿名函数，需要注意的是，在 `(()=>{...})` 后需要加一个 `()`，才能执行函数。

```jsx
(()=>{
    ...
})() // ()不可省略，否则看不到输出内容
```

如果省略括号，代码将不会执行函数，而是返回函数本身。React 使用的是JSX，与 JS 的区别是，JS 中的函数可以像其他任何值一样进行操作，可以被赋值给变量，传递给其他函数等；而在 JSX 中，只有函数调用才会返回有效的 JSX 元素。











