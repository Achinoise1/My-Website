# Taro 源码系列（一）

## Taro 源码构建微信小程序的过程

使用 Taro 框架编写微信小程序时，需要运行代码生成 dist 目录，才能在微信开发者工具中加载出小程序页面，查看编写的成果。一般来说，开发过程中使用的是 `npm run dev:weapp`，开发完成打包使用的是 `npm run build:weapp`。

在项目的 package.json 中可以看到命令在运行时的解析：

```json
"scripts": {
    "build:weapp": "taro build --type weapp",
    ...
    "dev:weapp": "npm run build:weapp -- --watch",
    ...
  }
``` 

### 

下面分别讲述 build:weapp 和 dev:weapp 的构建过程。

### build:weapp

```json
{
    _: ['build'],
    version: false,
    v: false,
    help: false,
    h: false,
    type: 'weapp'
}
```

### dev:weapp

如果开发过程中使用 `npm build:weapp` 命令，那么每更新一次代码就需要一次打包，不便于开发。因此通常使用 `npm run dev:weapp`。事实上，`dev:weapp` 等效于

```bash
taro build --type weapp --watch
```

其中，`--watch` 代表监听热加载。通过xxxx命令打印接收到的内置命令：

```json
{
    _: ['build'],
    version: false,
    v: false,
    help: false,
    h: false,
    type: 'weapp',
    watch:true
}
```