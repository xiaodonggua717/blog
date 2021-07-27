# Express

------

## 概念

**什么是Express**

官方给出的概念：Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。

通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。

**Express** **的本质**：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

Express 的中文官网：[ http://www.expressjs.com.cn/](http://www.expressjs.com.cn/)

**Express** **能做什么**

对于前端程序员来说，最常见的两种服务器，分别是：

-  Web 网站服务器：专门对外提供 Web 网页资源的服务器。
-  API 接口服务器：专门对外提供 API 接口的服务器。

使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器。

## 基本使用

### 安装

```
npm i express@4.17.1
```

### 创建基本的web 服务器

```js
const express = require('express');
const app = express();
app.listen(80, () => {
	console.log('express server is running');
})
```

### 监听GET/POST请求

通过 app.get() 方法，可以监听客户端的 GET 请求，

通过 app.post() 方法，可以监听客户端的 POST 请求

通过 res.send() 方法，可以把处理好的内容，发送给客户端

```js
//监听客户端的GET和POST请求,并向客户端响应具体的内容
app.get('/user',function(req,res){
    //调用res.send()方法,并向客户端响应一个JSON对象
	res.send({
		name:"xiaodonggua"
	})
})
//参数1:客户端请求的URL地址
//参数2: 请求对应的处理函数  req:请求对象  res:响应对象

```

### 获取URL中携带的查询参数

通过 req.query 对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数

```js
app.get('/user', function (req, res) {
	console.log(req.query);
})
```

默认情况下req.query为一个空对象.

如果使用 [localhost/user?name=123](http://localhost/user?name=123)来访问

则会打印一个

![image-20210605173245245](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210605173245245.png)

### 获取 URL 中的动态参数

通过 req.params 对象，可以访问到 URL 中，通过 **:** 匹配到的动态参数:

## 托管静态资源

### express.static()

express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器，例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了

```js
app.use(express.static('./file'));


```

Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。

因此，存放静态文件的目录名不会出现在 URL 中。

**那么如何托管多个静态资源目录呢?**

多次调用 express.static() 函数即可，访问静态资源文件时，如果多个文件夹中有相同的文件名，express.static() 函数会根据目录的添加顺序查找所需的文件。

那么如果我就是想指定查找某个文件夹里的内容呢？

可以使用

```js
app.use('/public',express.static('public'))
```

来挂载路径前缀

## nodemon

在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。

现在，我们可以使用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试。

### 安装

在终端中，运行如下命令，即可将 nodemon 安装为全局可用的工具：

```js
npm instal -g nodemon 
```

### 使用

当基于 Node.js 编写了一个网站应用的时候，传统的方式，是运行 node app.js 命令，来启动项目。这样做的坏处是：代码被修改之后，需要手动重启项目。

现在，我们可以将 node 命令替换为 nodemon 命令，使用 nodemon app.js 来启动项目。这样做的好处是：代码被修改之后，会被 nodemon 监听到，从而实现自动重启项目的效果。

```js
nodemon app.js
```

## Express 路由

广义上来讲，路由就是映射关系

在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数，格式如下：

 ```js
app.method(path,handler)
 ```

例子:

```js
app.get('/',function(req,res){
    res.send('hello');
})
```

### 路由的匹配过程

每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

![image-20210605205556100](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210605205556100.png)

路由匹配的注意点：

①按照定义的先后顺序进行匹配

②请求类型和请求的URL同时匹配成功，才会调用对应的处理函数

### 路由的使用

1.在 Express 中使用路由最简单的方式，就是把路由挂载到服务器实例上。

```js
app.get('./', (req, res) => {
	res.send('hello world')
})
```

2.模块化路由

为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到实例上，而是推荐将路由抽离为单独的模块。

将路由抽离为单独模块的步骤如下：

1. 创建路由模块对应的 .js 文件
2. 调用 express.Router() 函数创建路由对象
3. 向路由对象上挂载具体的路由
4. 使用 module.exports 向外共享路由对象
5. 使用 app.use() 函数注册路由模块

```js
//导入路由模块
var expres = require('express')
//创建路由对象
var router = express.Router()
//挂载具体路由
router.get('/user/list',function(req,res){
	res.send('Get user list')
})
router.post('/user/add',function(req,res){
	res.send('Add new user')
})
//向外导出路由
module.exports = router;

//导入路由模块
const userRouter = require('./router/user.js')
app.use(userRouter)
```

为路由模块添加前缀

```js
const userRouter = require('./router/user.js')
app.use('/api',userRouter)
```

 ## Express中间件

### 定义

中间件（Middleware ），特指业务流程的中间处理环节。

**生活中的例子:**

处理污水的时候，一般都要经过三个处理环节，从而保证处理过后的废水，达到排放标准。

![image-20210606133507764](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210606133507764.png)

处理污水的这三个中间处理环节，就可以叫做中间件。

### 调用流程及格式

Express中间件的调用流程

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

![image-20210606133622231](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210606133622231.png)

Express 的中间件，本质上就是一个 **function** **处理函数**，Express 中间件的格式如下：

```js
app.get('/',function(req,res,next){
    next();
})
```

中间件函数的形参列表中,必须包含next参数。而路由处理函数中只包含req和res。

### next函数的作用

**next** **函数**是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

### 全局生效的中间件

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。

通过调用 app.use(中间件函数)，即可定义一个全局生效的中间件。

```js
app.use(function (req, res, next) {
	console.log('简单的中间件函数'); 
    next();
})
```

### 中间件的作用

多个中间件之间，**共享同一份** **req** **和** **res**。基于这样的特性，我们可以在上游的中间件中，**统一**为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

### 定义多个中间件

可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用，示例代码如下：

 ```js
app.use(function(req,res,next){
   console.log('简单的中间件函数1'); 
    next();  
})

app.use(function(req,res,next){
   console.log('简单的中间件函数2'); 
    next();  
})


 ```

### 局部生效的中间件

```js
const mw1 = (req,res,next)=>{
	console.log('局部生效的中间件');
}

//该中间件函数只会影响该路由
app.get('/',mw1,(req,res)=>{
	res.send('你好');
})

//这个路由不会被影响
app.get('/user',mw1,(req,res)=>{
	res.send('你好');
})
```

### 使用多个局部中间件

```js
//两种方式都可以
app.get('/',mw1,mw2,(req,res)=>{
	res.send('你好');
})

app.get('/',[mw1,mw2],(req,res)=>{
    res.send('你好');
})
```

注意事项:

- 一定要在路由之前注册中间件
- 客户端发送过来的请求，可以连续调用多个中间件进行处理
- 执行完中间件的业务代码之后，不要忘记调用 next() 函数
- 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
- 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

###  中间件的分类

为了方便大家理解和记忆中间件的使用，Express 官方把常见的中间件用法，分成了 5 大类，分别是：

- 应用级别的中间件
- 路由级别的中间件
- 错误级别的中间件
- Express 内置的中间件
-  第三方的中间件

**应用级别的中间件**

通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件

**路由级别的中间件**

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上。

**错误级别的中间件**

错误级别中间件的**作用**：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。错误级别的中间件，必须注册在所有路由之后.

```js
app.use(function(err,req,res,next){
   console.log('发生了错误'+err.message); 
   res.send('发生了错误'+err.message)  
})
```

**Express内置的中间件**

自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：

-  express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
- express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
- express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

**第三方的中间件**

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。

例如：在 express@4.16.0 之前的版本中，经常使用 body-parser 这个第三方中间件，来解析请求体数据。使用步骤如下：

①运行 npm install body-parser 安装中间件

②使用 require 导入中间件

③调用 app.use() 注册并使用中间件

Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。

**自定义中间件**

自己手动模拟一个类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据。

实现步骤：

- 定义中间件
- 监听 req 的 data 事件
- 监听 req 的 end 事件
- 使用 querystring 模块解析请求体数据
- 将解析出来的数据对象挂载为 req.body
- 将自定义中间件封装为模块

## 接口的跨域问题

解决接口跨域问题的方案主要有两种：

CORS（主流的解决方案，推荐使用）

JSONP（有缺陷的解决方案：只支持 GET 请求）

### 使用cors中间件来解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

使用步骤分为如下 3 步：

- 运行 npm install cors 安装中间件
- 使用 const cors = require('cors') 导入中间件
- 在路由之前调用 app.use(cors()) 配置中间件

### Cors是什么

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，**这些** **HTTP** **响应头决定浏览器是否阻止前端** **JS** **代码跨域获取资源**。

浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。

**注意:**

- CORS 主要在服务器端进行配置。客户端浏览器**无须做任何额外的配置**，即可请求开启了 CORS 的接口。
- CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。

### Cors的响应头

**CORS** **响应头部** **- Access-Control-Allow-Origin** 

响应头部中可以携带一个 **Access-Control-Allow-Origin** 字段，其语法如下:

```js
Access-Control-Allow-Origin:<origin>|*
```

其中，origin 参数的值指定了允许访问该资源的外域 URL。

例如，下面的字段值将**只允许**来自http://xxx.cn的请求：

```js
res.setHeader('Access-Control-Allow-Origin','http://xxx.cn')
```

若指定了 Access-Control-Allow-Origin 字段的值为通配符 *****，表示允许来自任何域的请求

```js
res.setHeader('Access-Control-Allow-Origin','*')
```

**CORS** **响应头部** **- Access-Control-Allow-Headers**

默认情况下，CORS **仅**支持客户端向服务器发送如下的 9 个请求头：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

```js
res.setHeader('Access-Control-Allow-Headers','Content-Type,X-Custom-Header')
```



**CORS** **响应头部** **- Access-Control-Allow-Methods**

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。

```js
res.setHeader('Access-Control-Allow-Methonds','POST,GET,DELETE,HEAD')
```



### Cors的分类

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：

- 简单请求
- 预检请求

**简单请求**

同时满足以下两大条件的请求，就属于简单请求：

- 请求方式：GET、POST、HEAD 三者之一
-  HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）



**预检请求**

只要符合以下任何一个条件的请求，都需要进行预检请求：

① 请求方式为 GET、POST、HEAD 之外的请求 Method 类型

② 请求头中包含自定义头部字段

③ 向服务器发送了 application/json 格式的数据

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据



**简单请求和预检请求的区别**

**简单请求的特点**：客户端与服务器之间只会发生一次请求。

**预检请求的特点**：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。



### JSONP的概念与特点

概念：浏览器端通过script标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。

特点：

- JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。
- JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。
- 如果项目中已经配置了 CORS 跨域资源共享，为了**防止冲突**，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则 JSONP 接口会被处理成开启了 CORS 的接口。



### 实现 **JSONP** **接口的步骤**

1. 获取客户端发送过来的回调函数的名字
2. 得到要通过 JSONP 形式发送给客户端的数据 
3. 根据前两步得到的数据，拼接出一个函数调用的字符串
4. 把上一步拼接得到的字符串，响应给客户端的script标签进行解析执行





































































