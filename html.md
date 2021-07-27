  # HTML 基础知识归纳

------

## 五大浏览器及其内核

IE: trindent  后来edge也用了谷歌的内核

Firefox: Gecko

safari : webkit

chrome: webkit 后blink

opera: presto 后webkit  blink

## HTML基础知识

```js
<html>   
    <head>     
        <title>我的第一个页面</title>
    </head>
    <body>
           内容
    </body>
</html>
```



![image-20210602163036286](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602163036286.png)

### 单标签和双标签

双标签:常规的一般为双标签,该语法中“<标签名>”表示该标签的作用开始，一般称为“开始标签（start tag）”，“</标签名>” 表示该标签的作用结束，一般称为“结束标签（end tag）”。

```html
<标签名> 内容 </标签名>   比如 <body>  我是文字  </body>
```

单标签:空元素用单标签来表示， 简单点说，就是里面不需要包含内容， 只有一个开始标签不需要关闭。

```html
<标签名 />  比如  <br />
```

### 标签关系

嵌套关系

```html
<head> 

  <title> </title> 

</head>
```

并列关系

```html
<head></head>

<body></body>
```

### HMTL骨架结构

vscode生成页面骨架结构有两种快捷方式,可以生成如下的代码

- html: 5    按下tab键  
-  !    按下tab键 

```
<!DOCTYPE html>            //文档类型  <!DOCTYPE> 声明位于文档中的最前面的位置，处于 <html> 标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范
<html lang="en">     //语言种类  en为英语 zh-CN为中文
<head>            
	<meta charset="UTF-8">               //字符集 
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>
	
</body>
</html>
```

### 字符集

utf-8是目前最常用的字符集编码方式，常用的字符集编码方式还有gbk和gb2312。

* gb2312 简单中文  包括6763个汉字  GUO BIAO
* BIG5   繁体中文 港澳台等用
* GBK包含全部中文字符    是GB2312的扩展，加入对繁体字的支持，兼容GB2312
* UTF-8则基本包含全世界所有国家需要用到的字符

### HMTL标签语义化

1. 方便代码的阅读和维护
2. 同时让浏览器或是网络爬虫可以很好地解析，从而更好分析其中的内容 
3. 使用语义化标签会具有更好地搜索引擎优化 

### HTML常用标签

#### 标题标签

```
<h> </h>
```

HTML提供了6个等级的标题，加了标题的文字会变的加粗，字号也会变大，其中一号标题为最大。

```
<h1>   标题文本   </h1>
<h2>   标题文本   </h2>
<h3>   标题文本   </h3>
<h4>   标题文本   </h4>
<h5>   标题文本   </h5>
<h6>   标题文本   </h6>
```

#### 段落标签

p标签是HTML文档中最常见的标签，默认情况下，文本在一个段落中会根据浏览器窗口的大小自动换行。

```
<p>  文本内容  </p>
```

#### div和span标签

div   span    是没有语义的     是我们网页布局主要的2个盒子   想必你听过  css+div

div 就是  division  的缩写   分割， 分区的意思  其实有很多div 来组合网页。

span   跨度，跨距；范围    

语法格式：

```html
<div> 这是头部 </div>    <span>今日价格</span>
```

他们两个都是盒子，用来装我们网页元素的， 只不过他们有区别，现在我们主要记住使用方法和特点就好了

* div标签  用来布局的，但是现在一行只能放一个div
* span标签  用来布局的，一行上可以放好多个span

#### 排版标签总结

|    标签名     |    定义    |                 说明                  |
| :-----------: | :--------: | :-----------------------------------: |
|   <hx></hx>   |  标题标签  |   作为标题使用，并且依据重要性递减    |
|    <p></p>    |  段落标签  |    可以把 HTML 文档分割为若干段落     |
|    <hr />     | 水平线标签 |        没啥可说的，就是一条线         |
|    <br />     |  换行标签  |                                       |
|  <div></div>  |  div标签   | 用来布局的，但是现在一行只能放一个div |
| <span></span> |  span标签  |  用来布局的，一行上可以放好多个span   |

#### 图像标签

```
<img src="图像URL" />
```

![image-20210602165102899](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602165102899.png)

**注意: **

1. 标签可以拥有多个属性，必须写在开始标签中，位于标签名后面。
2. 属性之间不分先后顺序，标签名与属性、属性与属性之间均以空格分开。
3. 采取  键值对 的格式   key="value"  的格式  

#### 链接标签

```
<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
```

| 属性   | 作用                                                         |
| ------ | :----------------------------------------------------------- |
| href   | 用于指定链接目标的url地址，（必须属性）当为标签应用href属性时，它就具有了超链接的功能 |
| target | 用于指定链接页面的打开方式，其取值有_self和_blank两种，其中_self为默认值，__blank为在新窗口中打开方式。 |

**注意：**

1. 外部链接 需要添加 http:// www.baidu.com
2. 内部链接 直接链接内部页面名称即可 比如 < a href="index.html"> 首页 </a >
3. 如果当时没有确定链接目标时，通常将链接标签的href属性值定义为“#”(即href="#")，表示该链接暂时为一个空链接。
4. 不仅可以创建文本超链接，在网页中各种网页元素，如图像、表格、音频、视频等都可以添加超链接。

#### html中的注释方法

快捷键是    ctrl + /       

语法格式为:

```
   <!-- 注释语句 -->  
```

一般情况下注释独占一行

### HTML表格

#### 表格基本格式

```
<table>
   <caption>我是表格标题</caption>
  <tr>
    <th>姓名</th>
    <th>年龄</th>
    <th>性别</th>
  </tr>
  <tr>
    <td>小明</td>
    <td>30</td>
    <td>男</td>
  </tr>
    <tr>
    <td>小红</td>
    <td>18</td>
    <td>女</td>
  </tr>
</table>
```

解释:

1. table用于定义一个表格标签。
2. caption 元素定义**表格标题**，通常这个标题会被居中且显示于表格之上。
3. tr标签 用于定义表格中的行，必须嵌套在 table标签中。
4. th 一般表头单元格位于表格的第一行或第一列，并且文本加粗居中
5. td 用于定义表格中的单元格，必须嵌套在<tr></tr>标签中。
6. 字母 td 指表格数据（table data），即数据单元格的内容，现在我们明白，表格最合适的地方就是用来存储数据的。

![image-20210602165637989](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602165637989.png)

#### 表格的属性

![image-20210602165901253](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602165901253.png)

![image-20210602170000207](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602170000207.png)

#### 合并单元格

* 跨行合并：rowspan="合并单元格的个数"      

* 跨列合并：colspan="合并单元格的个数"

  

  **先上 后下   先左  后右的原则**:合并时会将右侧或下侧的合并到本单元格。

  

  **步骤:**

1. 先确定是跨行还是跨列合并

2. 根据 先上 后下   先左  后右的原则找到目标单元格    然后写上 合并方式 还有 要合并的单元格数量  比如 ：

    <td colspan="3">   </td>

3. 删除多余的单元格 单元格 （原理为本单元格加长、加宽了多少，会占用原本的其他单元格面积，所以要删除被占的单元格）

### HTML列表 表单

#### 列表标签

列表分为三类： 无序列表ul 有序列表ol 自定义列表dl

**无序列表**：各个列表项之间没有顺序级别之分，是并列的。其基本语法格式如下：

```html
<ul>
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ......
</ul>
```

```
 1. <ul></ul>中只能嵌套<li></li>，直接在<ul></ul>标签中输入其他标签或者文字的做法是不被允许的。
 2. <li>与</li>之间相当于一个容器，可以容纳所有元素。
```

**有序列表**：即为有排列顺序的列表，其各个列表项按照一定的顺序排列定义，有序列表的基本语法格式如下：

```html
<ol>
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ......
</ol>
```

  所有特性基本与ul 一致。  但是实际中比 无序列表 用的少很多。

**自定义列表**：常用于对术语或名词进行解释和描述，定义列表的列表项前没有任何项目符号。其基本语法如下：

```html
<dl>
  <dt>名词1</dt>
  <dd>名词1解释1</dd>
  <dd>名词1解释2</dd>
  ...
  <dt>名词2</dt>
  <dd>名词2解释1</dd>
  <dd>名词2解释2</dd>
  ...
</dl>
```

**总结：**

| 标签名    |     定义     | 说明                                                   |
| --------- | :----------: | :----------------------------------------------------- |
| <ul></ul> | **无序标签** | 里面只能包含li    没有顺序，我们以后布局中最常用的列表 |
| <ol></ol> |   有序标签   | 里面只能包含li    有顺序， 使用情况较少                |
| <dl></dl> |  自定义列表  | 里面有2个兄弟， dt 和 dd                               |

#### 表单

表单目的是为了收集用户信息。在我们网页中， 我们也需要跟用户进行交互，收集用户资料，此时也需要表单。

在HTML中，一个完整的表单通常由表单控件（也称为表单元素）、提示信息和表单域3个部分构成。

**表单控件： **

​       包含了具体的表单功能项，如单行文本输入框、密码输入框、复选框、提交按钮、重置按钮等。

 **提示信息：**

​        一个表单中通常还需要包含一些说明性的文字，提示用户进行填写和操作。

 **表单域：**  

​      他相当于一个容器，用来容纳所有的表单控件和提示信息，可以通过他定义处理表单数据所用程序的url地址，以及数据提交到服务器的方法。如果不定义表单域，表单中的数据就无法传送到后台服务器。

##### input（常用）

语法：

```html
<input type="属性值" value="你好">
```

- <input /&gt;标签为单标签
- type属性设置不同的属性值用来指定不同的控件类型

input的属性有：

![image-20210602171836528](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602171836528.png)

**type 属性**

* 这个属性通过改变值，可以决定了属于哪种input表单。
* 比如 type = 'text'  就表示 文本框 可以做 用户名， 昵称等。
* 比如 type = 'password'  就是表示密码框   用户输入的内容 是不可见的。

```html
用户名: <input type="text" /> 
密  码：<input type="password" />
```

 **value属性   值**

```html
用户名:<input type="text"  name="username" value="请输入用户名"> 
```

* value 默认的文本值。 有些表单想刚打开页面就默认显示几个文字，就可以通过这个value 来设置。

 **name属性**

~~~html
用户名:<input type="text"  name=“username” />  
~~~

name表单的名字， 这样，后台可以通过这个name属性找到这个表单。  页面中的表单很多，name主要作用就是用于区别不同的表单。

* name属性后面的值，是我们自己定义的。


* radio  如果是一组，我们必须给他们命名相同的名字 name   这样就可以多个选其中的一个啦

```html
<input type="radio" name="sex"  />男
<input type="radio" name="sex" />女
```

**checked属性**

* 表示默认选中状态。  较常见于 单选按钮和复选按钮。

```html
性    别:
<input type="radio" name="sex" value="男" checked="checked" />男
<input type="radio" name="sex" value="女" />女 
```

上面这个，表示就默认选中了 男 这个单选按钮

**input 属性小结**

| 属性    | 说明     | 作用                                                   |
| ------- | :------- | ------------------------------------------------------ |
| type    | 表单类型 | 用来指定不同的控件类型                                 |
| value   | 表单值   | 表单里面默认显示的文本                                 |
| name    | 表单名字 | 页面中的表单很多，name主要作用就是用于区别不同的表单。 |
| checked | 默认选中 | 表示那个单选或者复选按钮一开始就被选中了               |

##### label标签

label 标签为 input 元素定义标注（标签）。

 用于绑定一个表单元素, 当点击label标签的时候, 被绑定的表单元素就会获得输入焦点。

**如何绑定元素呢？**

1. 第一种用法就是用label直接包括input表单。

```html
<label> 用户名： <input type="radio" name="usename" value="请输入用户名">   </label>
```

   适合单个表单选择

2. 第二种用法 for 属性规定 label 与哪个表单元素绑定。

```html
<label for="sex">男</label>
<input type="radio" name="sex"  id="sex">
```

##### textarea控件

- 语法：

```html
<textarea >
  文本内容
</textarea>
```

- 作用：

  通过textarea控件可以轻松地创建多行文本输入框.

  cols="每行中的字符数" rows="显示的行数"  实际开发不常用

##### select

如果有多个选项让用户选择，为了节约空间，我们可以使用select控件定义下拉列表.

**语法：**

```html
<select>
  <option>选项1</option>
  <option>选项2</option>
  <option>选项3</option>
  ...
</select>
```

* 注意：

1. &lt;select&gt;  中至少包含一对 option 
2. 在option 中定义selected =" selected "时，当前项即为默认选中项。

### form表单域

在HTML中，form标签被用于定义表单域，以实现用户信息的收集和传递，form中的所有内容都会被提交给服务器。

**语法: **

```html
<form action="url地址" method="提交方式" name="表单名称">
  各种表单控件
</form>
```

**常用属性：**

| 属性   | 属性值   | 作用                                               |
| ------ | :------- | -------------------------------------------------- |
| action | url地址  | 用于指定接收并处理表单数据的服务器程序的url地址。  |
| method | get/post | 用于设置表单数据的提交方式，其取值为get或post。    |
| name   | 名称     | 用于指定表单的名称，以区分同一个页面中的多个表单。 |

常与ajax后台交互配合使用

## XHTML

### 什么是XHTML

XHTML 是更严格更纯净的 HTML 代码。

- XHTML 指**可扩展超文本标签语言**（EXtensible HyperText Markup Language）。
- XHTML 的目标是取代 HTML。
- XHTML 与 HTML 4.01 几乎是相同的。
- XHTML 是更严格更纯净的 HTML 版本。
- XHTML 是作为一种 XML 应用被重新定义的 HTML。
- XHTML 是一个 W3C 标准。

### HTML和 XHTML之间有什么区别?

- XHTML 指的是可扩展超文本标记语言
- XHTML 与 HTML 4.01 几乎是相同的
- XHTML 是更严格更纯净的 HTML 版本
- XHTML 是以 XML 应用的方式定义的 HTML
- XHTML 是 2001 年 1 月发布的 W3C 推荐标准
- XHTML 得到所有主流浏览器的支持
- XHTML 元素是以 XML 格式编写的 HTML 元素。XHTML是严格版本的HTML，例如它要求标签必须小写，标签必须被正确关闭，标签顺序必须正确排列，对于属性都必须使用双引号等。

# HMTL5

## 什么是HTML5

HTML5 的概念与定义 

- 定义：`HTML5` 定义了 `HTML` 标准的最新版本，是对 `HTML` 的第五次重大修改，号称下一代的 `HTML` 
- 两个概念：
  - 是一个新版本的 `HTML` 语言，定义了新的标签、特性和属性
  - 拥有一个强大的技术集，这些技术集是指： `HTML5` 、`CSS3` 、`javascript`, 这也是广义上的 `HTML5`

所有现代浏览器都支持 HTML5。

此外，所有浏览器，不论新旧，都会自动把未识别元素当做行内元素来处理。

正因如此，可以帮助老式浏览器处理”未知的“ HTML 元素。

## HTML5扩展了哪些内容

- 语义化标签
- 本地存储
- 兼容特性
- `2D`、`3D` 
- 动画、过渡
- `CSS3` 特性
- 性能与集成

## HMTL5新增标签

新增了语义化标签

- `header`   ---  头部标签
- `nav`        ---  导航标签
- `article` ---   内容标签
- `section` ---   块级标签
- `aside`     ---   侧边栏标签
- `footer`   ---   尾部标签

![image-20210602174208702](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602174208702.png)

  1.  使用语义化标签的注意

      - 语义化标签主要针对搜索引擎
      - 新标签可以使用一次或者多次
      - 在 `IE9` 浏览器中，需要把语义化标签都转换为块级元素
      - 语义化标签，在移动端支持比较友好，
      - 另外，`HTML5` 新增的了很多的语义化标签，随着课程深入，还会学习到其他的

### 多媒体音频标签

1. 多媒体标签有两个，分别是

   - 音频  -- `audio`
   - 视频  -- `video`

2. `audio` 标签说明

   - 可以在不使用标签的情况下，也能够原生的支持音频格式文件的播放，
   - 但是：播放格式是有限的

3. audio 支持的音频格式

   - audio 目前支持三种格式

     

   <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/04-06 移动Web网页开发/01-H5C3 进阶资料/01-HTML5CSS3_day01/01-笔记/images/audio.png">

4. audio 的参数

   

   <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/04-06 移动Web网页开发/01-H5C3 进阶资料/01-HTML5CSS3_day01/01-笔记/images/audiocanshu.png">

5、audio 代码演示

```css
<body>
  <!-- 注意：在 chrome 浏览器中已经禁用了 autoplay 属性 -->
  <!-- <audio src="./media/snow.mp3" controls autoplay></audio> -->

  <!-- 
    因为不同浏览器支持不同的格式，所以我们采取的方案是这个音频准备多个文件
   -->
  <audio controls>
    <source src="./media/snow.mp3" type="audio/mpeg" />
  </audio>
</body>
```

### 多媒体视频标签

1. video 视频标签

   - 目前支持三种格式

   

   <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/04-06 移动Web网页开发/01-H5C3 进阶资料/01-HTML5CSS3_day01/01-笔记/images/vedio.png">

2. 语法格式

   ```html
   <video src="./media/video.mp4" controls="controls"></video>
   ```

3. video 参数

   <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/04-06 移动Web网页开发/01-H5C3 进阶资料/01-HTML5CSS3_day01/01-笔记/images/videocanshu.png">

   

4. video 代码演示

   ```html
   <body>
     <!-- <video src="./media/video.mp4" controls="controls"></video> -->
   
     <!-- 谷歌浏览器禁用了自动播放功能，如果想自动播放，需要添加 muted 属性 -->
     <video controls="controls" autoplay muted loop poster="./media/pig.jpg">
       <source src="./media/video.mp4" type="video/mp4">
       <source src="./media/video.ogg" type="video/ogg">
     </video>
   </body>
   ```

5. 多媒体标签总结

   - 音频标签与视频标签使用基本一致
   - 多媒体标签在不同浏览器下情况不同，存在兼容性问题
   - 谷歌浏览器把音频和视频标签的自动播放都禁止了
   - 谷歌浏览器中视频添加 muted 标签可以自己播放
   - 注意：重点记住使用方法以及自动播放即可，其他属性可以在使用时查找对应的手册

### 新增 input 标签属性

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/04-06 移动Web网页开发/01-H5C3 进阶资料/01-HTML5CSS3_day01/01-笔记/images/h5input.png">

### 新增表单属性

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/04-06 移动Web网页开发/01-H5C3 进阶资料/01-HTML5CSS3_day01/01-笔记/images/newinput.png">

## HTML5本地存储

通过本地存储（Local Storage），web 应用程序能够在用户浏览器中对数据进行本地的存储。

在 HTML5 之前，应用程序数据只能存储在 cookie 中，包括每个服务器请求。本地存储则更安全，并且可在不影响网站性能的前提下将大量数据存储于本地。

与 cookie 不同，存储限制要大得多（至少5MB），并且信息不会被传输到服务器。

本地存储经由起源地（origin）（经由域和协议）。所有页面，从起源地，能够存储和访问相同的数据。

HTML 本地存储提供了两个在客户端存储数据的对象：

- window.localStorage - 存储没有截止日期的数据
- window.sessionStorage - 针对一个 session 来存储数据（当关闭浏览器标签页时数据会丢失）

### localStorage 对象

localStorage 对象存储的是没有截止日期的数据。当浏览器被关闭时数据不会被删除，在下一天、周或年中，都是可用的。

实例

```
// 存储
localStorage.setItem("lastname", "Gates");
// 取回
document.getElementById("result").innerHTML = localStorage.getItem("lastname");
```

### sessionStorage 对象

sessionStorage 对象等同 localStorage 对象，不同之处在于只对一个 session 存储数据。如果用户关闭具体的浏览器标签页，数据也会被删除。

下例在当前 session 中对用户点击按钮进行计数：

实例

```
if (sessionStorage.clickcount) {
    sessionStorage.clickcount = Number(sessionStorage.clickcount) + 1;
} else {
    sessionStorage.clickcount = 1;
}
document.getElementById("result").innerHTML = "在本 session 中，您已经点击这个按钮 " +
sessionStorage.clickcount + " 次。";
```