# 打包

## 必备文件

```bash
dist/   # xxx命令打包得到
```

## 流程

首先进入项目位置，打开终端运行命令：

```bash
npm run build:weapp
```

其中 weapp 值的是微信小程序，其他小程序参数如下：

|  平台  |  参数  |
| :----: | :----: |
|  微信  | weapp  |
|  百度  |  swan  |
| 支付宝 | alipay |
|  抖音  |   tt   |
|   QQ   |   qq   |
|  京东  |   jd   |
|   H5   |   h5   |


## 可能会遇到的问题

### Error: Cannot find module 'webpack-bundle-analyzer'
运行 `npm run build:weapp` 时报错：

<details>
  <summary>完整报错内容</summary>

```bash
Error: Cannot find module 'webpack-bundle-analyzer'
Require stack:
- F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\config\prod.js
- F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\config\index.js
- C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\node_modules\@tarojs\service\dist\Config.js
- C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\node_modules\@tarojs\service\dist\index.js
- C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\node_modules\@tarojs\service\index.js
- C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\dist\cli.js
- C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\bin\taro
    at Function.Module._resolveFilename (node:internal/modules/cjs/loader:1077:15)
    at Function.Module._load (node:internal/modules/cjs/loader:922:27)
    at Module.require (node:internal/modules/cjs/loader:1143:19)
    at require (node:internal/modules/cjs/helpers:110:18)
    at Object.<anonymous> (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\config\prod.js:1:13)
    at Module._compile (node:internal/modules/cjs/loader:1256:14)
    at Module._compile (C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\node_modules\pirates\lib\index.js:117:24)
    at Module._extensions..js (node:internal/modules/cjs/loader:1310:10)
    at Object.newLoader [as .js] (C:\Users\xxx\AppData\Roaming\npm\node_modules\@tarojs\cli\node_modules\pirates\lib\index.js:121:7)
    at Module.load (node:internal/modules/cjs/loader:1119:32) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [
    'F:\\Desktop_From_C\\TodoMVC-react\\TodoMVC-react\\config\\prod.js',
    'F:\\Desktop_From_C\\TodoMVC-react\\TodoMVC-react\\config\\index.js',
    'C:\\Users\\xxx\\AppData\\Roaming\\npm\\node_modules\\@tarojs\\cli\\node_modules\\@tarojs\\service\\dist\\Config.js',
    'C:\\Users\\xxx\\AppData\\Roaming\\npm\\node_modules\\@tarojs\\cli\\node_modules\\@tarojs\\service\\dist\\index.js',
    'C:\\Users\\xxx\\AppData\\Roaming\\npm\\node_modules\\@tarojs\\cli\\node_modules\\@tarojs\\service\\index.js',
    'C:\\Users\\xxx\\AppData\\Roaming\\npm\\node_modules\\@tarojs\\cli\\dist\\cli.js',
    'C:\\Users\\xxx\\AppData\\Roaming\\npm\\node_modules\\@tarojs\\cli\\bin\\taro'
  ]
}
找不到插件依赖 "@tarojs/plugin-platform-weapp"，请先在项目中安装，项目路径：F:\Desktop_From_C\TodoMVC-react\TodoMVC-react
```
</details>

提示缺少依赖，需要使用对应命令安装依赖：

```bash
npm install -save-dev webpack-bundle-analyzer
```

安装完成后再次运行 `npm run build:weapp`

### Error: error:0308010C:digital envelope routines::unsupported

<details>
  <summary>完整报错内容</summary>

```bash
编译  发现入口  src/app.js
编译  发现页面  src/pages/index/index.js
⠙ 正在编译...Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:71:19)
    at Object.createHash (node:crypto:133:10)
    at module.exports (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\util\createHash.js:135:53)
    at TaroNormalModule._initBuildHash (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:417:16)
    at handleParseError (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:471:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:503:5
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:358:12
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:373:3
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:214:10)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:221:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:236:3
    at runSyncOrAsync (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:130:11)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:232:2)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:221:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:236:3
    at context.callback (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:111:13)
Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:71:19)
    at Object.createHash (node:crypto:133:10)
    at module.exports (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\util\createHash.js:135:53)
    at TaroNormalModule._initBuildHash (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:417:16)
    at handleParseError (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:471:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:503:5
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:358:12
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:373:3
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:214:10)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:221:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:236:3
    at runSyncOrAsync (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:130:11)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:232:2)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:221:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:236:3
    at context.callback (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:111:13)
node:internal/crypto/hash:71
  this[kHandle] = new _Hash(algorithm, xofLen);
                  ^

Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:71:19)
    at Object.createHash (node:crypto:133:10)
    at module.exports (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\util\createHash.js:135:53)
    at TaroNormalModule._initBuildHash (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:417:16)
    at handleParseError (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:471:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:503:5
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\webpack\lib\NormalModule.js:358:12
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:373:3
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:214:10)
    at iterateNormalLoaders (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:221:10)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:236:3
    at context.callback (F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\loader-runner\lib\LoaderRunner.js:111:13)
    at F:\Desktop_From_C\TodoMVC-react\TodoMVC-react\node_modules\babel-loader\lib\index.js:59:71 {
  opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
}

Node.js v18.16.1
```
</details>

提示版本支持 OpenSSL 出错。在参考[终极解决：Error: error:0308010C:digital envelope routines::unsupported]一文后尝试如下：

找到项目中的 `package.json` 文件，把 script 部分与 build 相关代码，在原有基础上增加如下内容

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>
<TabItem value="Windows" label="Windows">
    
```bash
set NODE_OPTIONS=--openssl-legacy-provider && <原始代码>
```

</TabItem>
<TabItem value="Mac" label="Mac">

```bash
export NODE_OPTIONS=--openssl-legacy-provider && <原始代码>
```
  
  </TabItem>
</Tabs>


整体改动如下：

```json
"scripts": {
    "build:rn": "set NODE_OPTIONS=--openssl-legacy-provider && taro build --type rn",
    "build:weapp": "set NODE_OPTIONS=--openssl-legacy-provider && taro build --type weapp",
    "build:h5": "set NODE_OPTIONS=--openssl-legacy-provider && taro build --type h5",
    "dev:rn": "set NODE_OPTIONS=--openssl-legacy-provider && npm run build:rn -- --watch",
    "dev:weapp": "set NODE_OPTIONS=--openssl-legacy-provider && npm run build:weapp -- --watch",
    "dev:h5": "set NODE_OPTIONS=--openssl-legacy-provider && npm run build:h5 -- --watch",
    ...(此处省略多余代码)
}
```


### Browserslist: caniuse-lite is outdated

<details>
<summary>完整报错内容</summary>

```bash
Browserslist: caniuse-lite is outdated. Please run:
  npx browserslist@latest --update-db
  Why you should do it regularly: https://github.com/browserslist/browserslist#browsers-data-updating
🙅   编译失败. 2024/2/16 22:31:49
```

</details>

按照提示运行命令即可：

```bash
npx browserslist@latest --update-db
```


### app.wxss from CssoWebpackPlugin

<details>
<summary>完整报错内容</summary>

```bash
app.wxss from CssoWebpackPlugin
You must provide the URL of lib/mappings.wasm by calling SourceMapConsumer.initialize({ 'lib/mappings.wasm': ... }) before using SourceMapConsumer Error: You must provide the URL of lib/mappings.wasm by calling SourceMapConsumer.initialize({ 'lib/mappings.wasm': ... }) before using SourceMapConsumer
    at async Promise.all (index 0)
    at async Promise.all (index 4)
```

</details>

```bash
npm i source-map -D
```

就可以了，为什么？

[终极解决：Error: error:0308010C:digital envelope routines::unsupported]:https://blog.csdn.net/m0_48300767/article/details/131450325