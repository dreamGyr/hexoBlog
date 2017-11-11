---
title: node-fs
copyright: true
password:
top: 101
---
## fs 模块##
#### 一、同步 和 异步 ####
> Node.js 文件系统（fs 模块）模块中的方法均有异步和同步版本，例如读取文件内容的函数有异步的 fs.readFile() 和同步的 fs.readFileSync()。
异步的方法函数最后一个参数为回调函数，回调函数的第一个参数包含了错误信息(error)。
建议大家是用异步方法，比起同步，异步方法性能更高，速度更快，而且没有阻塞。

1. readFile读取文件

创建 input.txt 文件，内容如下：
`line one`

在text.txt相同目录中有一个readfile.js，内容如下

>readFile的回调函数接收两个参数：
1. err是读取文件出错时触发的错误对象，
2. data是从文件读取的数据。

~~~
var fs = require('fs'); // 引入fs模块
fs.readFile('./test.txt', function(err, data) {
    // 读取文件失败/错误
    if (err) {
        throw err;
    }
    // 读取文件成功
    console.log(data);
});
~~~

$ node readfile.js运行结果
~~~
<Buffer 6c 69 6e 65 20 6f 6e 65 0a 6c 69 6e 65 20 74 77 6f 0a>
~~~

这是原始二进制数据在缓冲区中的内容。

要显示文件内容可以使用toString()或者设置输出编码。

toString()写法：
~~~
// 使用toString()
fs.readFile('./test.txt', function(err, data) {
    // 读取文件失败/错误
    if (err) {
        throw err;
    }
    // 读取文件成功
    console.log(data.toString());
});
~~~
设置utf-8编码写法：
`// 设置编码格式
fs.readFile('./test.txt', 'utf-8', function(err, data) {
    // 读取文件失败/错误
    if (err) {
        throw err;
    }
    // 读取文件成功
    console.log('utf-8: ', data.toString());
　　//直接用console.log(data);也可以
});`

readFile同步的写法就是没有回调函数：`fs.readFileSync(filename,[options])。`