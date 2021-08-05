# Node.js

## 概念

Node.js是运行在服务端的JavaScript

## NPM

npm是随同nodejs一起安装的包管理工具，能解决Nodejs代码部署上的很多问题

1、相关命令

显示npm版本

```java
npm -v
```

升级npm

```java
npm install npm -g
```

package.json

package.json位于模块目录下，用于定义包的属性。

## 回调函数

## 模块化编程

导出

```js
export.add=funtion(a,b){
  return a+b;
}
```

引入

```js
var demo=require('./demo');
console.log(demo.add(400,600));		
```

## Buffer缓冲区

JavaScript语言自身只有字符串类型数据没有二进制数据类型，buffer实例一般用于表示编码字符的序列，比如UTF_8、UCS2、Base64等编码

```
const buf=Buffer.from('runoob','ascil');

console.log(buf.toString('hex'));

console.log(buf.toString('base64'));
```

## Stream流

```javascript
var fs = require("fs");
var data = '';

// 创建可读流
var readerStream = fs.createReadStream('input.txt');

// 设置编码为 utf8。
readerStream.setEncoding('UTF8');

// 处理流事件 --> data, end, and error
readerStream.on('data', function(chunk) {
   data += chunk;
});

readerStream.on('end',function(){
   console.log(data);
});

readerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

