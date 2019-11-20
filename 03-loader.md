# 03-loader模块
loader模块是加载其他不同语言转换成为typescript的或者将图片转换成为dataURL. 甚至在JS模块import css文件的操作!   

### webpack加载不同格式文件之前要先安装对应的loader:   

```cmd
npm i -D css-loader // -D 开发需要, 打包之后不需要
npm i -D ts-loader
```
然后在webpack配置.css文件用css-loader .ts文件用ts-loader
```js
module.exports = {
  module: {
    rules: [
      {test: /\.css$/, use: 'css-loader'},
      {test: /\.ts$/, use: 'ts-loader'}
    ]
  }
}
```
* rules(规则数组) 
  当创建模块是, 匹配请求规则的数组. 这些规则能修改模块的创建方式, 对模块应用loader, 或者修改解析器parser
  其中rules表示每一种匹配的测试方式和使用loader的不同
  * test:  匹配特定条件。一般是提供一个正则表达式或正则表达式的数组，但这不是强制的 
  * and:  必须匹配数组中的所有条件
  * or:     匹配数组中任何一个条件 
  *  not : 必须排除这个条件 

```js
module.exports = {
  module: {
    rules: [
      {
        or: [/\.css$/, /\.sass/],
        use: [
          {loader: "css-loader"}
        ]
      },
      {
        test: /\.ts$/, 
        use: [ // 这是准确写法
          {loader: "ts-loader"} 
        ]
      }
    ]
  }
}
```

* 
