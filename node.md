# Node基础

## 各大浏览器的js引擎

![image-20210603155510163](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603155510163.png)

每个浏览器中都内置了BOM DOM AJAX这样的API函数,用js去调用这些API

### 运行环境

运行环境是指代码正常运行所需的必要环境

浏览器就是js的一种运行环境

 ![image-20210603160135869](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603160135869.png)

- v8引擎负责解析和执行JS代码
- 内置API是由运行环境提供的特殊接口, 只能在所属的运行环境中被调用。

js可以做后端开发，但需要依靠node.js

## Node.js

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。(v8的效率最高)

![image-20210603160712024](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603160712024.png)

- 浏览器是 JavaScript 的前端运行环境。
- Node.js 是 JavaScript 的后端运行环境。
- Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API。

### Node.js可以做什么

Node.js 作为一个 JavaScript 的运行环境，仅仅提供了基础的功能和 API。然而，基于 Node.js 提供的这些基础能，很多强大的工具和框架如雨后春笋，层出不穷，所以学会了 Node.js ，可以让前端程序员胜任更多的工作和岗位：

①基于 Express 框架（http://www.expressjs.com.cn/），可以快速构建 Web 应用

②基于 Electron 框架（https://electronjs.org/），可以构建跨平台的桌面应用

③基于 restify 框架（http://restify.com/），可以快速构建 API 接口项目

④读写和操作数据库、创建实用的命令行工具辅助前端开发、etc…

### Node.js 的学习路径

JavaScript 基础语法 + Node.js 内置 API 模块（fs、path、http等）+ 第三方 API 模块（express、mysql 等）

### Node.js的安装

如果希望通过 Node.js 来运行 Javascript 代码，则必须在计算机上安装 Node.js 环境才行。

安装包可以从 Node.js 的官网首页直接下载，进入到 Node.js 的官网首页（**https://nodejs.org/en/**），点击绿色的按钮，下载所需的版本后，双击直接安装即可(LTS是长期稳定版,Current为新特性不稳定版本)

![image-20210603162732503](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603162732503.png)

查看已安装的Node.js版本号可以在cmd中执行

```
node -v
```

![image-20210603162428886](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603162428886.png)

下载之后就可以使用终端powershell或者cmd来操作node.js了

vscode里面可以直接使用终端

### 使用node.js来执行JS文件

两种办法 

第一种是在该js文件的目录下按住shift的情况下鼠标右键点击空白处,选择在此处运行powershell,然后执行 node 对应的文件名![image-20210603164120203](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603164120203.png)(可以使用tab来自动补全文件名)

第二种是使用一些编译器如vscode,点击![image-20210603164232602](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603164232602.png)之后执行node操作![image-20210603164259518](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603164259518.png)

## fs文件系统模块

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求

例如：

- fs.readFile() 方法，用来读取指定文件中的内容
- fs.writeFile() 方法，用来向指定的文件中写入内容

如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

```js
const fs = require('fs')
```

### fs.readFile()

使用 fs.readFile() 方法，可以读取指定文件中的内容，语法格式如下：[]中为非必填项

```js
fs.readFile(path,[option],callback)
```

path:字符串,表示文件路径

option:表示以何种编码格式来读取文件

callback:文件读取完成后,通过回调函数拿到读取的结果

示例:

使用utf8的编码来读取1.txt中的内容并打印出来

```js
const fs = require('fs')
fs.readFile('1.txt','utf8',function(err,result){
	if(err){
		return console.log("文件读取失败"+err.message);
	}
	console.log('文件读取成功,内容为'+result);
})
//1.txt中存放的内容我们提前写好 你好 我就是内容
```

执行结果为:

![image-20210603164913285](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603164913285.png)

### fs.writeFile()

使用 fs.writeFile() 方法，可以向指定的文件中写入内容，语法格式如下：

```js
fs.writeFile(path,data,[option],callback)
```

path:字符串,表示文件路径

data:表示要写入的内容

option:表示以何种编码格式来读取文件

callback:文件读取完成后,通过回调函数拿到读取的结果

示例:

将text变量里的内容以utf8的形式写入到1.txt中

```js
const fs = require('fs');
var text = "这就是要写进去的东西"
fs.writeFile('1.txt', text, 'utf8', function (err) {
	if (err) {
		return console.log("文件写入失败" + err.message);
	}
	console.log('文件写入成功');
});
```

执行结果为:

![image-20210603165748421](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210603165748421.png)

**注意:**fs.writeFile()写入时会将目标文件的内容清空后写入。

### fs常见问题

在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。

原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。

解决方案：

- 在使用 fs 模块操作文件时，直接提供完整的路径，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题。(但是这样会导致移植性很差，不利于维护。不建议使用)
- 使用 __dirname表示当前文件的目录

## path路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

例如：

- path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
- path.basename() 方法，用来从路径字符串中，将文件名解析出来

如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：

```js
const path = require('path')
```

### path.join()

使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：

```js
path.join([..paths])
```

...paths string 路径片段的序列

返回值 string

示例：

```js
const  path = require('path');
const path1 = path.join('/a','/b','../','/c')   ../表示退回一层 会抵消掉上一层的路径
console.log(path1);
// 输出结果为 \a\c

const path2 = path.join(__dirname,'/a');
console.log(path2);
//输出结果为 当前目录\a

```

今后凡是涉及到路径拼接的操作，都要使用 path.join() 方法进行处理。不要直接使用 + 进行字符串的拼接。

### path.basename()

使用 path.basename() 方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

```js
path.basename(path,[ext])
```

path 表示一个路径的字符串

ext  表示文件拓展名

示例

```js
const path2 = path.join(__dirname,'/nodeTry','1.txt');
var fullName = path.basename(path2);
console.log(fullName);  //输出 1.txt
```

### path.extname()

使用 path.extname() 方法，可以获取路径中的扩展名部分，语法格式如下：

```js
path.extname(path)
```

path 表示一个路径的字符串

返回值为得到的扩展名字符串

示例:

```js
const path2 = path.join(__dirname,'/nodeTry','1.txt');
var extName = path.extname(path2);
console.log(extName);  //输出 .txt
```

## http模块

http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。通过 http 模块提供的 http.createServer() 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```js
const http = require('http');
```

### 理解

服务器和普通电脑的**区别**在于，服务器上安装了 web 服务器软件，例如：IIS、Apache 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。

在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件。因为我们可以基于 Node.js 提供的 http 模块，**通过几行简单的代码，就能轻松的手写一个服务器软件**，从而对外提供 web 服务。

### 创建基本的web服务器

导入http 

创建web服务器实例

绑定request事件来监听客户端的请求

启动服务器

```js
const http = require('http');     //导入http模块
const server = http.createServer();     //调用 http.createServer() 方法，即可快速创建一个 web 服务器实例
server.on('request', (req, res) => {   //为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求
	console.log('something visit our web server.');
})
server.listen(80,()=>{               //调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例
	console.log('http server running');
})
```

其中 

- req为客户端所相关的属性 请求对象  req.url是客户端请求的urlreq.method 为客户端method 类型
- res为响应对象 是服务器相关的数据或属性  res.end()可以向客户端发送信息

### 中文乱码问题

当调用 res.end() 方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式：

```js
const http = require('http');
const server = http.createServer();
server.on('request', (req, res) => {
	console.log('something visit our web server.');
	const str = '你好';
    //设置响应头Content-Type的值为text/html;charset=utf-8
	res.setHeader('Content-Type','text/html;charset=utf-8');   
	console.log(res.end(str));
})
server.listen(80,()=>{
	console.log('http server running');
})
```

### 根据不同的url响应不同的html内容

实现步骤:

①获取请求的 url 地址

②设置默认的响应内容为 404 Not found

③判断用户请求的是否为 / 或 /index.html 首页

④判断用户请求的是否为 /about.html 关于页面

⑤设置 Content-Type 响应头，防止中文乱码

⑥使用 res.end() 把内容响应给客户端

```js
const http = require('http');
const server = http.createServer();
server.on('request',(req,res)=>{
	let content ='404 Not Found';
	if(req.url == '/' || req.url == '/index.html'){
		content = '首页';
	}else if(req.url == '/about.html'){
		content = '关于';
	}
	res.setHeader('Content-Type','text/html;charset=utf-8');
	res.end(content);
})
server.listen(80,()=>{
		console.log('http server running');
})
```

