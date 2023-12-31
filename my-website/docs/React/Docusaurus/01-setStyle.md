# Docusaurus中编写markdown

## 表格

编写表格有两种方式：markdown原生表格或使用html标签

### markdown原生表格

如果只是简单列个表格，且数据量不大的情况下，可以用原生表格填写，以下给出的是一个三行两列（不含表头）的居中表格。

```markdown
| col1  | col2  |
| :---: | :---: |
|       |       |
|       |       |
|       |       |
```

### html标签

如果想要设计一个美观一点的表格，或者是有复杂单元格的处理，那么建议使用html标签，以下给出的是一个三行两列（不含表头）的表格。

```html
<table>
    <thead>
        <tr>
            <th></th>
            <th></th>
        </tr>
    </thead>
    <tbody >
        <tr >
            <td></td>
            <td></td>
        </tr>
        <tr >
            <td></td>
            <td></td>
        </tr>
        <tr >
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>
```
:::important

如果想要自定义样式，需要按照jsx格式编写

✖️ `<div style='width: 100%'>content</div>`  
✔️ `<div style={{width: '100%'}}>content</div>`  

✖️ `<div class={col-4}>content</div>`  
✔️ `<div className={col-4}>content</div>`  
:::

如果希望**横向**合并单元格，可以使用如下代码：
```html
<table>
    <thead>
        <tr>
            <th>col1</th>
            <th>col2</th>
        </tr>
    </thead>
    <tbody >
        <tr >
            <td colspan="2">test</td>
        </tr>
    </tbody>
</table>
```
效果如下
<table>
    <thead>
        <tr>
            <th>col1</th>
            <th>col2</th>
        </tr>
    </thead>
    <tbody >
        <tr >
            <td colspan="2">test</td>
        </tr>
        <tr >
            <td>here</td>
            <td>here</td>
        </tr>
    </tbody>
</table>

**纵向**合并单元格
```html
<table>
    <thead>
        <tr>
            <th>col1</th>
            <th>col2</th>
        </tr>
    </thead>
    <tbody >
        <tr >
            <td rowspan="2">test</td>
            <td>here</td>
        </tr>
        <tr >
            <td>here</td>
        </tr>
    </tbody>
</table>
```
效果如下
<table>
    <thead>
        <tr>
            <th>col1</th>
            <th>col2</th>
        </tr>
    </thead>
    <tbody >
        <tr >
            <td rowspan="2">test</td>
            <td>here</td>
        </tr>
        <tr >
            <td>here</td>
        </tr>
    </tbody>
</table>


### 表格中插入代码

如果代码数量较少，可以使用行内代码展示。但存在展示大量代码的情况，如果直接把所有代码放入行内代码符号中，会出现报错，正确操作如下：

```html
<td>
    <pre>
        <code>
            ...
        </code>
    </pre>
</td>
```

## 代码块

### 折叠代码块

有些时候希望能够折叠大量代码，用户想要查看时再自行点击展开。Docusaurus 官方没有提供相关的插件，可以直接用 markdown 自带代码折叠，用法如下：

```md
<details>
  <summary>折叠显示文字</summary>
  <!--
    ```lang
    your code```
  -->
</details>
```

<details>
  <summary>折叠显示文字</summary>
```py
print('hello world')
```
</details>