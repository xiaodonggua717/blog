# 服务器的基本概念与ajax

------

## 客户端与服务器

存放和对外提供资源的电脑叫 服务器

获取和消费资源的电脑叫 客户端

URL :统一资源定位符

一般由三部分组成: 通信协议+服务器名称+资源在服务器上具体的存放位置

![image-20210520115850456](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210520115850456.png)

## 客户端和服务器的通信过程

客户端请求服务器 ->

服务器处理这次请求 {

1.服务器接收到客户端发来的资源请求

2.服务器在内部处理这次请求,找到相关资源

3.服务器把找到的资源响应给客户端

}

分为三个步骤 请求->处理->响应 每一个资源都是如此得到的

### 分析通信过程

![image-20210520120231648](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210520120231648.png)

### 服务器提供的资源

文 图 音 视频

数据也是一种资源

#### 网页如何请求数据

用到了XMLHttpRequest 对象 (xhr)是浏览器提供的js成员,可以通过它来请求服务器上的数据资源

举例应用: 

```js
var xhrobj = new XMLHttpRequest()
```

资源的请求方式

get:获取服务器资源 比如根据url地址从服务器获取各种文件数据等

post:向服务器提交数据 如登录信息,注册信息,用户信息等等

## AJAX

![image-20210520121446306](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210520121446306.png)

作用:实现网页与服务器之间的数据交互

### ajax的应用场景

用户名检测:注册用户的时候通过ajax的形式来动态检测用户名是否被占用

搜索提示:输入搜索关键字的时候,通过ajax的形式,动态加载搜索提示列表 

数据分页:动态刷新表格的数据

### jquery中的ajax

因为XMLHttpRequest的用法比较复杂,所以jquery对其进行了封装,降低了ajax的使用难度

jQuery发起ajax请求的三个常用方法

$.get()

$.post()

$.ajax()

### $.get()

发起get请求 

语法: $.get(url,[data],[callback])

![image-20210520132436804](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210520132436804.png)

$.get()发起不带参数的请求,则直接提供url和回调函数即可

### $.post()

$.post(url,[data],[callback])

![image-20210520133916611](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210520133916611.png)

### $.ajax()

$ajax({type,url,data,success})

使用$.ajax发起get()请求 只需要将type设置为'GET'

使用$.ajax发起post()请求 只需要将type设置为'POST'

## 接口

使用ajax请求数据时,被请求的url地址就叫数据接口,也叫接口,每个接口必须有请求方式

### 分析接口的请求过程

1. get()  

用户与网页进行交互  -> 网页向服务器发起get请求-> 服务器响应网页的get请求->响应结果填充到网页上

2. post()

用户与网页进行交互  -> 网页向服务器发起post请求-> 服务器响应网页的post请求->响应结果填充到网页上

### 接口测试工具

PostMan 

### 接口文档

接口文档就是接口的说明文档,调用接口的一个依据,包含了接口的URL,参数以及输出内容的说明.

1. 接口名称
2. 接口URL
3. 调用方式
4. 参数格式
5. 响应格式
6. 返回示例



