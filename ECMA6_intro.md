# ECMAScript (javascript6)
http://es6.ruanyifeng.com/#README

ECMAScript 6 入门
作者：阮一峰

授权：署名-非商用许可证

## ES2016 2016年6(新增了数组实例的includes方法和指数运算符)
## 现阶段ES6还没有完全支持，可以利用babel转码器进行转码，转为ES5

# Babel

### 配置文件.babelrc
该文件用来设置转码规则和插件，基本格式如下。
``` javascript
{
  "presets": [],//字段设定转码规则
  "plugins": []
}
```

``` javascript
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```
然后将这些规则加入.babelrc
``` javascript
{
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```

### 以下所有Babel工具和模块的使用，都必须先写好.babelrc。

#### babel-cli命令行转码

安装命令
$ npm install --global babel-cli

``` javascript
// 基本用法
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```
上面代码是在全局环境下，进行Babel转码。这意味着，如果项目要运行，全局环境必须有Babel，也就是说项目产生了对环境的依赖。另一方面，这样做也无法支持不同项目使用不同版本的Babel。

解决的办法：一个解决办法是将babel-cli安装在项目之中。

$ npm install --save-dev babel-cli

然后改写package.json

``` javascript
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}
```

转码的时候执行

$ npm run build

具体操作详情于顶部网址链接
