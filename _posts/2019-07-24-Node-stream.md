---
layout: post
title: "Node stream"
date: 2019-07-24
tags: HTML  
---


# Node常用内置模块

## stream(流)

文件流读取文本内容

```
"use strict";

var fs = require("fs");
var rs = fs.createReadStream("sample.txt","utf-8");

rs.on("data",function(chunk){
	console.log("data:"+chunk)
});

rs.on("end",function(chunk){
	console.log("end");
});

rs.on("error",function(chunk){
	console.log(err);
});
```



流的形式写入文件

```
"use strict"

var fs = require("fs");

var ws1 = fs.createWriteStream("out1.txt","utf-8");
ws1.write('使用Stream写入文本数据...\n');
ws1.write('END.');
ws1.end();

var ws2 = fs.createWriteStream("out2.txt");
ws2.write(new Buffer('使用Stream写入二进制数据...\n', 'utf-8'));
ws2.write(new Buffer('END.', 'utf-8'));
ws2.end();
```

所有可以读取数据的流都继承自`stream.Readable`，

所有可以写入的流都继承自`stream.Writable`。



pipe

用`pipe()`把一个文件流和另一个文件流串起来，这样源文件的所有数据就自动写入到目标文件里了，所以，这实际上是一个复制文件的程序：

```
"use strict"

var fs = require("fs");
var rs  = fs.createReadStream("1.txt");
var ws = fs.createWriteStream("2.txt");
rs.pipe(ws);
```

默认情况下，当`Readable`流的数据读取完毕，`end`事件触发后，将自动关闭`Writable`流。如果我们不希望自动关闭`Writable`流，需要传入参数：

```
readable.pipe(writable, { end: false });
```

