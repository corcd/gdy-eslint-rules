# gdy-eslint-rules

广电云前端团队 ESLint 静态检查规则（2019-10-31）

## 使用方法

1. 首先执行 shell 目录下对应包管理的脚本文件安装必要模块
2. 然后执行 shell 目录下 init 脚本
3. 最后将目录下 .eslintrc.js 内的 rules 属性替换，执行 npm serve/yarn serve 即可

### 针对于 vue-cli 2

访问 `build\webpack.base.config.js` 文件新增：

```js
module: {
  rules: [
    ...{
      test: /\.(js|vue)$/,
      loader: 'eslint-loader',
      enforce: 'pre',
      include: [resolve('src'), resolve('test')],
      options: {
        formatter: require('eslint-friendly-formatter')
      }
    }
  ]
}
```

### 针对于 vue-cli 3

cli 已集成安装 ESLint ，运行 shell 目录下 init 脚本即可

### 自动化修复

访问 `package.json` 文件新增

```js
"scripts": {
  "lint": "eslint --fix --ext .js,.vue src",
  "format": "prettier-eslint --write \"src/**/*.js\" \"src/**/*.vue\""
}
```

> 推荐使用 vue-cli 的内置 ESLint 配置方法
