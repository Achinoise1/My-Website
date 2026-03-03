# 报错对应解决方案

## EPERM: operation not permitted, rename ...

<details>
<summary>完整报错结果</summary>

```bash
PS F:\Desktop_From_C\design\code\uniapp\myApp> pnpm add @taroify/core
 WARN  Moving @babel/core that was installed by a different package manager to "node_modules/.ignored"
 WARN  Moving @pmmmwh/react-refresh-webpack-plugin that was installed by a different package manager to "node_modules/.ignored"
 WARN  Moving @tarojs/cli that was installed by a different package manager to "node_modules/.ignored"
 WARN  Moving @tarojs/taro-loader that was installed by a different package manager to "node_modules/.ignored"
 WARN  Moving @tarojs/test-utils-react that was installed by a different package manager to "node_modules/.ignored"
 WARN  46 other warnings
 EPERM  EPERM: operation not permitted, rename 'F:\Desktop_From_C\design\code\uniapp\myApp\node_modules\@tarojs\plugin-platform-weapp' -> 'F:\Desktop_From_C\design\code\uniapp\myApp\node_modules\.ignored\@tarojs\plugin-platform-weapp'
```

</details>

此时需要检查是否正在运行 `npm run dev:weapp`，如果是，则需要 `Ctrl+C` 终止运行后再重新运行 pnpm 命令。