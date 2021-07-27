# form表单与模板引擎 2021.5.20

------

## 表单 

表单负责数据采集 

### 表单的组成部分

表单标签

表单域

表单按钮

#### 表单标签的属性

- **action** : 规定向哪里发送表单数据  即URL地址 未指定时为当前地址  
- **target**:规定在哪打开url     1._self 自身打开    2._blank 新窗口
- **method:**以何种方式把表单数据提交action URL  get()和post()  少的用get() 多的用post()
- **enctype**: 发送表单数据之前如何对数据进行编码

### 表单的同步提交

点击submit来触发表单提交的操作并且使页面跳转到URL的行为叫表单的同步提交.

表单同步提交的缺点:

- 提交后页面会跳转,影响用户体验
- 提交后页面的状态和数据会丢失

解决方案:表单只负责采集数据,由ajax来提交数据到服务器



## 通过ajax来提交表单数据

```js
两种监控方式
1.
$('#form').on('submit',function(e){
    
})

2.
$('#form').submit(function(e){
    
})
```

### 阻止表单的默认提交行为

使用e.preventDefault() 

### 快速获取表单中数据

serialize()

可以一次性获取到表单中所有的数据

## 模板引擎

模板引擎，顾名思义，它可以根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面

①减少了字符串的拼接操作

②使代码结构更清晰

③使代码更易于阅读与维护 

2.art-template的使用步骤

导入art-template  ->定义数据 ->定义模板 ->调用template函数 -> 渲染html结构

如

```js
 	<div id="container"> </div>
	<script type="text/html" id="tpl-user">
		<h1>{{name}}</h1>
	</script>
	<script>
		var data = {
			name: '张三',
			sex:"男"
		}
		var htmlStr = template('tpl-user',data);
		$('#container').html(htmlStr)
	</script>
```

输出结果为

![image-20210521150643665](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210521150643665.png)

### 标准语法-输出

在{{}}中可以进行变量的输出、对象属性的输出、三元表达式的输出、逻辑或的输出、加减乘除的输出

![image-20210521150529080](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210521150529080.png)

### 标准语法-原文输出

{{@ value}} 

如果value中有HTML标签结构,则需要使用@ html标签才会被正常渲染

### 标准语法-条件输出

可以在{{}}中使用if...elseif.../if的方式

{{if value}} 按需输出的内容 {{/if}}

{{if value}} 内容1 {{else if value}} 内容2 {{/if}}

### 标准语法-循环输出

```js
{{each arr}}

{{$index}} {{$value}}

{{/each}}
```

### 标准语法-过滤器

```js
{{value|filterName}}
template.defaults.imports.filterName =function(value){
    return   xxxxx;
}
```

## 模板引擎的实现原理

### 正则与字符串操作

1.基本语法:

exec() 用于检索字符串中的正则表达式的匹配, 如果有匹配的话,则返回该匹配值,否则返回NULL

RegExpObject.exec(string) 

2.分组:

正则表达式中 ( ) 包起来的内容表示一个分组，可以通过分组来**提取自己想要的内容**

3.替换

replace() 函数用于在字符串中用一些字符**替换**另一些字符

replace(a,b)即将a替换为b

4.使用while多次replace

5.实现

![image-20210521205622423](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210521205622423.png)

6.用replace()替换为真值

