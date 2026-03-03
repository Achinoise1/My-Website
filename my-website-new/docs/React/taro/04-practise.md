# 实战

## 自定义设计

### fontawesome 图标导入

<details>
<summary>完整报错内容</summary>

```bash
Error: Module build failed (from ./node_modules/mini-css-extract-plugin/dist/loader.js):
HookWebpackError: Module build failed (from ./node_modules/postcss-loader/dist/cjs.js):
Error: Failed to find '~@fortawesome/fontawesome-svg-core/styles.css
```

```bash
页面【pages/data/index]错误:
 ReferenceError: faHeart is not defined
    at Object../node_modules/@tarojs/taro-loader/lib/entry-cache.js?name=pages/data/index!./src/pages/data/index.jsx (index.jsx?c5e8:16)
    at __webpack_require__ (webpack_bootstrap:19)
    at Object../src/pages/data/index.jsx (index.jsx?c5e8:55)
    at __webpack_require__ (webpack_bootstrap:19)
    at __webpack_exec__ (._src_pages_data_index.jsx:9)
    at ._src_pages_data_index.jsx:9
    at Function.__webpack_require__.O (webpack_runtime_chunk loaded:25)
    at ._src_pages_data_index.jsx:9
    at webpackJsonpCallback (webpack_runtime_jsonp chunk loading:73)
    at index.js:3(env: Windows,mp,1.06.2401020; lib: 3.3.2)
```

</details>

## 页面跳转

### Taro.navigateTo

保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面。使用 Taro.navigateBack 可以返回到原页面。小程序中页面栈最多十层，否则爆栈，具体报错如下：

<details>
<summary>完整报错内容</summary>

```bash
Error: MiniProgramError
{"errMsg":"navigateTo:fail webview count limit exceed"}
    at Object.errorReport (WAServiceMainContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at Function.thirdErrorReport (WAServiceMainContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at Object.thirdErrorReport (WAServiceMainContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at i (WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at Object.cb (WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at V._privEmit (WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at V.emit (WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1
    at n (WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1)
    at Le (WASubContext.js?t=wechat&s=1708243447939&v=3.3.2:1)(env: Windows,mp,1.06.2401020; lib: 3.3.2)
```

</details>

因此谨慎使用。与之搭配的还有 `Taro.navigateBack` 函数。

```jsx
Taro.navigateTo({
  url: 'test?id=1',     // 必填
})
```

`url` 为指定跳转地址。该地址必须包含在 `app.config.js` 的 pages 块。

```js
export default defineAppConfig({
  pages: [
    'pages/...',
    'pages/....',
  ],
  window: {
    backgroundTextStyle: 'light',
    navigationBarBackgroundColor: '#fff',
    navigationBarTitleText: 'WeChat',
    navigationBarTextStyle: 'black'
  }
})
```

否则报 page 注册错误

### Taro.navigateBack

关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages 获取当前的页面栈，决定需要返回几层。

```jsx
Taro.navigateBack({
  delta: 2      // 非必填
})
```

其中，`delta` 是返回的页面数，如果 delta 大于现有页面数，则返回到首页。

### Taro.redirectTo

关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面。

## 可能出现的错误

### Error: Minified React error #321;
<details>
<summary>完整报错内容</summary>

```bash
Error: Minified React error #321; 
visit https://reactjs.org/docs/error-decoder.html?invariant=321 for the full message or use the non-minified dev environment for full errors and additional helpful warnings
```

</details>

### TypeError: Cannot read property 'mount' of null

### page 注册错误