# 00 webpack基本概念
## 1. webpack是什么?
  webpack是一个javascript的静态模块打包器(module bundler), 他会递归地构建一个`依赖关系图`, 包含项目依赖的每一个模块, 然后打包输出一个或者多个`bundle`.   
## 2. webpack的四个核心概念
  * 入口(entry)   
    * 表示webpack使用哪个模块作为构建依赖的开始, 进入入口之后webpack会找出和入口关联(直接, 间接)的依赖   
    * 可以在`webpack.config.js`中配置`entry`指定入口起点. 默认为`./src`
    ```js
    module.exports = {
      entry: "./path/to/entry/file.js"
    }
    ```
  * 出口(output)   
    * 指定webpack创建输出文件`bundles`的位置,以及命名规范, 默认路径为 `./dist`, 整个程序结构都会被编译到指定输出的文件夹中, 用`output`字段来配置处理过程
    ```js
    // 路径模块
    const path = require("path")
    module.exports = {
      entry: "./path/to/entry/file.js",
      output: {
        // 生成地址
        path: path.resolve(__dirname, "dist"),
        // 文件名称
        filename: "my-webpack.bundle.js"
      }
    }
    ```
  * 加载器(loader)   
    * 处理非JS文件的, loader可以将所有类型的文件转换成webpack能处理的有效模块. 在处理的时候loader有两种属性: 
    1. `test` 属性: 检测满足条件的文件
    2. `use`  属性: 转换的时候使用那种`loader`   
    webpack.config.js
    ```js
    const path = require("path")
    module.exports = {
      entry: "./path/to/entry/file.js",
      output: {
        // 生成地址
        path: path.resolve(__dirname, "dist"),
        // 文件名称
        filename: "my-webpack.bundle.js"
      },
      module: {
        rules: [
          {test: /\.txt$/, use: 'raw-loader'}
        ]
      }
    }
    ```
  * 插件(plugins)
    * 从打包优化和压缩，一直到重新定义环境中的变量。可以用来处理各种各样的任务。   
    * 通过`require`引入, 添加到`plugins`数组中, 多数插件可以通过选项(option)自定义。你也可以在一个配置文件中因为不同目的而多次使用同一个插件，这时需要通过使用 new 操作符来创建它的一个实例。
    ```js
    const HtmlWebpackPlugin = require('html-webpack-plugin')
    const webpack = require('webpack') // 用于访问内置插件

    const config = {
      module: {
        rules: [
          { test: /\.txt$/, use: 'raw-loader' }
        ]
      },
      plugins: [
        new HtmlWebpackPlugin({template: './src/index.html'})
      ]
    }

    module.exports = config;
    ```
## 模式
通过选择 development 或 production 之中的一个，来设置 mode 参数，你可以启用相应模式下的 webpack 内置的优化
```js
module.exports = {
  mode: 'production' //or development 
};
```
