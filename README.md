# gdy-eslint-rules

广电云前端团队 ESLint 静态检查规则（2019-11-01）

> 推荐使用 vue-cli 的内置 ESLint 配置方法，vs code 格式化工具推荐 beautify & prettier

## 使用方法

### 工程集成

访问 `package.json` 文件新增：

```json
// package.json
"scripts": {
  "lint": "eslint --fix --ext .js,.vue src", // vue-cli 工程可以使用默认 lint
  "format": "prettier-eslint --write \"src/**/*.js\" \"src/**/*.vue\""
}
```

### 针对于非 vue-cli 工程

1. 首先执行 shell 目录下对应包管理的脚本文件安装必要模块
2. 然后执行 shell 目录下 init 脚本
3. 最后根据当前项目内的模板文件，将目录下 .eslintrc.js 内的 rules 属性替换，同时配置好相应的规则 env、parserOptions、plugins），执行 npm run lint / yarn lint 即可

其中需要访问 `webpack.config.js` 文件新增：

```js
// webpack.config.js
module.exports = {
  entry: '',
  output: {},
  module: {
    rules: [
      {
        test: /\.js$/,
        use: ['babel-loader', 'eslint-loader']
      }
    ]
  },
  plugins: [],
  devServer: {}
}
```

### 针对于 vue-cli 工程

> vue-cli 推荐升级至 v3 或 v4，需安装依赖 eslint-plugin-html、eslint-plugin-prettier

1. cli 已集成安装 ESLint ，运行 shell 目录下 init 脚本即可; 若工程初始化时未加入 ESLint，可运行 `vue add eslint` 添加
2. 根据当前项目内的模板文件，将目录下 .eslintrc.js 内的 rules 属性替换，同时配置好相应的规则（env、parserOptions、plugins），执行 npm run lint / yarn lint 即可

### 特殊情况

当遇到特殊情况，不得不对工程内指定文件、指定行、指定代码块不使用 ESLint 语法检查时：

#### 整个文件范围内禁止规则出现警告

将/_ eslint-disable _/放置于文件最顶部

```js
/* eslint-disable */
alert('foo')
```

#### 在文件中临时禁止规则出现警告

将需要忽略的代码块用注释包裹起来

```js
/* eslint-disable */
alert('foo')
/* eslint-enable */
```

#### 对指定规则的启用或者禁用警告

将需要忽略的代码块用注释包裹起来

```js
/* eslint-disable no-alert, no-console */
alert('foo')
console.log('bar')
/* eslint-enable no-alert, no-console */
```

#### 对指定行禁用规则警告

此类方法有两种形式（下同）：

```js
alert('foo') // eslint-disable-line

// eslint-disable-next-line
alert('foo')
```

#### 在指定行上禁用指定的某个规则

```js
alert('foo') // eslint-disable-line no-alert

// eslint-disable-next-line no-alert
alert('foo')
```

#### 在某个特定的行上禁用多个规则

```js
alert('foo') // eslint-disable-line no-alert, quotes, semi

// eslint-disable-next-line no-alert, quotes, semi
alert('foo')
```
