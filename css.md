# CSS基础知识归纳

------

## 认识css

概念：

​	CSS(Cascading Style Sheets)  ，通常称为CSS样式表或层叠样式表（级联样式表）

作用：

- 主要用于**设置** HTML页面中的文本内容（字体、大小、对齐方式等）、图片的外形（宽高、边框样式、边距等）以及**版面的布局和外观显示样式。**
- CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制及整体排版等，而且还可以针对不同的浏览器设置不同的样式。  

### 引入方法

有三种引入方式：行内式 内部样式表 外部样式表

**行内式**

- 概念：

  ​	称行内样式、行间样式.

  ​	是通过标签的style属性来设置元素的样式


- 其基本语法格式如下：

```html
<标签名 style="属性1:属性值1; 属性2:属性值2; 属性3:属性值3;"> 内容 </标签名>
```

实际上任何HTML标签都拥有style属性，用来设置行内式。

**内部样式表**

- 概念：

  ​	称内嵌式

  ​	是将CSS代码集中写在HTML文档的head头部标签中，并且用style标签定义


- 其基本语法格式如下：

```html
<head>
<style type="text/CSS">
    选择器（选择的标签） { 
      属性1: 属性值1;
      属性2: 属性值2; 
      属性3: 属性值3;
    }
</style>
</head>
```

- 注意：
  - style标签一般位于head标签中，当然理论上他可以放在HTML文档的任何地方。
  - type="text/css"  在html5中可以省略。
  - 只能控制当前的页面

**外部样式表**

- 概念：

  ​	称链入式

  ​	是将所有的样式放在一个或多个以**.CSS**为扩展名的外部样式表文件中，

  ​	通过link标签将外部样式表文件链接到HTML文档中

- 其基本语法格式如下：

```html
<head>
  <link rel="stylesheet" type="text/css" href="css文件路径">
</head>
```

- 注意：  
  - link 是个单标签
  - link标签需要放在head头部标签中，并且指定link标签的三个属性

| 样式表     | 优点                     | 缺点                     | 使用情况       | 控制范围           |
| ---------- | ------------------------ | ------------------------ | -------------- | ------------------ |
| 行内样式表 | 书写方便，权重高         | 没有实现样式和结构相分离 | 较少           | 控制一个标签（少） |
| 内部样式表 | 部分结构和样式相分离     | 没有彻底分离             | 较多           | 控制一个页面（中） |
| 外部样式表 | 完全实现结构和样式相分离 | 需要引入                 | 最多，强烈推荐 | 控制整个站点（多） |

## css基础选择器

作用：找到特定的HTML页面元素

### 标签选择器

- 概念：

  标签选择器（元素选择器）是指用**HTML标签名**称作为选择器，按标签名称分类，为页面中某一类标签指定统一的CSS样式。

- 语法：

~~~
标签名{属性1:属性值1; 属性2:属性值2; 属性3:属性值3; } 
~~~

- 作用：

  标签选择器 可以把某一类标签**全部**选择出来  比如所有的div标签  和 所有的 span标签

- 优点：

  是能快速为页面中同类型的标签统一样式

- 缺点：

  不能设计差异化样式。

### 类选择器

类选择器使用“.”（英文点号）进行标识，后面紧跟类名.

- 语法：

  - 类名选择器

  ~~~
  .类名  {   
      属性1:属性值1; 
      属性2:属性值2; 
      属性3:属性值3;     
  }
  ~~~

  - 标签

  ~~~
  <p class='类名'></p>
  ~~~

- 优点：

  - 可以为元素对象定义单独或相同的样式。 可以选择一个或者多个标签 

- 注意

  - 类选择器使用“.”（英文点号）进行标识，后面紧跟类名(自定义，我们自己命名的)
  - 长名称或词组可以使用中横线来为选择器命名。
  - 不要纯数字、中文等命名， 尽量使用英文字母来表示。

命名是我们通俗约定的，但是没有规定必须用这些常用的命名。

#### 类选择器多类名用法

我们可以给标签指定多个类名，从而达到更多的选择目的。

注意：

- 各个类名中间用空格隔开。
- 多类名选择器在后期布局比较复杂的情况下，还是较多使用的。

```html
<div class="pink fontWeight font20">亚瑟</div>
<div class="font20">刘备</div>
<div class="font14 pink">安其拉</div>
<div class="font14">貂蝉</div>
```

### id选择器

id选择器使用`#`进行标识，后面紧跟id名

- 其基本语法格式如下：

  - id选择器

    ~~~
    #id名 {属性1:属性值1; 属性2:属性值2; 属性3:属性值3; }
    ~~~

  - 标签

    ~~~
    <p id="id名"></p>
    ~~~

- 元素的id值是唯一的，只能对应于文档中某一个具体的元素。

- 用法基本和类选择器相同。

####  id选择器和类选择器区别

 一个简单的例子：一个人的名字可以比作是类，因为可以有人与其同名。但一个人的身份证号则可以比作成为id，因为不可以有人与其身份证号一模一样。

- W3C标准规定，在同一个页面内，不允许有相同名字的id对象出现，但是允许相同名字的class。
  - 类选择器（class） 好比人的名字，  是可以多次重复使用的， 比如  张伟  王伟  李伟  李娜
  - id选择器     好比人的身份证号码，  全中国是唯一的， 不得重复。 只能使用一次。

***id选择器和类选择器最大的不同在于 使用次数上。***

### 通配符选择器

- 概念

  通配符选择器用`*`号表示，  *   就是 选择所有的标签      他是所有选择器中作用范围最广的，能匹配页面中所有的元素。

- 其基本语法格式如下：

```
* { 属性1:属性值1; 属性2:属性值2; 属性3:属性值3; }
```

例如下面的代码，使用通配符选择器定义CSS样式，清除所有HTML标记的默认边距。

```css
* {
  margin: 0;                    /* 定义外边距*/
  padding: 0;                   /* 定义内边距*/
}
```

- 注意：

  会匹配页面所有的元素，降低页面响应速度，不建议随便使用

###  基础选择器总结

| 选择器       | 作用                          | 缺点                     | 使用情况   | 用法                 |
| ------------ | ----------------------------- | ------------------------ | ---------- | -------------------- |
| 标签选择器   | 可以选出所有相同的标签，比如p | 不能差异化选择           | 较多       | p { color：red;}     |
| 类选择器     | 可以选出1个或者多个标签       | 可以根据需求选择         | 非常多     | .nav { color: red; } |
| id选择器     | 一次只能选择器1个标签         | 只能使用一次             | 不推荐使用 | #nav {color: red;}   |
| 通配符选择器 | 选择所有的标签                | 选择的太多，有部分不需要 | 不推荐使用 | * {color: red;}      |

提示：

- 尽量少用通用选择器 `*`
- 尽量少用 ID 选择器
- 不使用无具体语义定义的标签选择器 div span 

## CSS复合选择器

  CSS选择器分为 基础选择器 和 复合选择器 ，但是基础选择器不能满足我们实际开发中，快速高效的选择标签。

- 目的是为了可以选择更准确更精细的目标元素标签。
- 复合选择器是由两个或多个基础选择器，通过不同的方式组合而成的

### 后代选择器（重点）

- 概念：

  后代选择器又称为包含选择器

- 作用：

  用来选择元素或元素组的**子孙后代**

- 其写法就是把外层标签写在前面，内层标签写在后面，中间用**空格**分隔，先写父亲爷爷，再写儿子孙子。 

~~~
父级 子级{属性:属性值;属性:属性值;}
~~~

- 语法：

~~~
.class h3{color:red;font-size:16px;}
~~~



<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day02/笔记/media/hou.png" />

- 当标签发生嵌套时，内层标签就成为外层标签的后代。
- 子孙后代都可以这么选择。 或者说，它能选择任何包含在内 的标签。

### 子元素选择器

- 作用：

  子元素选择器只能选择作为某元素**子元素(亲儿子)**的元素。

- 其写法就是把父级标签写在前面，子级标签写在后面，中间跟一个 `>` 进行连接

- 语法：

~~~
.class>h3{color:red;font-size:14px;} 
~~~

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day02/笔记/media/zi1.png" />

```
 比如：  .demo > h3 {color: red;}   说明  h3 一定是demo 亲儿子。  demo 元素包含着h3。
```

### 交集选择器

- 条件

  交集选择器由两个选择器构成，找到的标签必须满足：既有标签一的特点，也有标签二的特点。

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day02/笔记/media/jiaoji.png" />

- 语法：

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day02/笔记/media/jiao.png" />

- 其中第一个为标签选择器，第二个为class选择器，两个选择器之间**不能有空格**，如h3.special。

**记忆技巧：**

交集选择器 是 并且的意思。  即...又...的意思

```
比如：   p.one   选择的是： 类名为 .one  的 段落标签。  
```

用的相对来说比较少，不太建议使用。

### 并集选择器（重点）

- 应用：
  - 如果某些选择器定义的相同样式，就可以利用并集选择器，可以让代码更简洁。
- 并集选择器（CSS选择器分组）是各个选择器通过`,`连接而成的，通常用于集体声明。
- 语法：



<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day02/笔记/media/bing.png" />

- 任何形式的选择器（包括标签选择器、class类选择器id选择器等），都可以作为并集选择器的一部分。

- 记忆技巧：

  并集选择器通常用于集体声明  ，逗号隔开的，所有选择器都会执行后面样式，逗号可以理解为 和的意思。

```
比如  .one, p , #test {color: #F00;}  
表示   .one 和 p  和 #test 这三个选择器都会执行颜色为红色。 
通常用于集体声明。  
```

### 链接伪类选择器（重点）

 伪类选择器：

 为了和我们刚才学的类选择器相区别
类选择器是一个点 比如 .demo {}   
而我们的伪类 用 2个点 就是 冒号  比如  :link{}     

作用：

用于向某些选择器添加特殊的效果。比如给链接添加特殊效果， 比如可以选择 第1个，第n个元素。

因为伪类选择器很多，比如链接伪类，结构伪类等等。我们这里先给大家讲解链接伪类选择器。

- a:link      /* 未访问的链接 */
- a:visited   /* 已访问的链接 */
- a:hover     /* 鼠标移动到链接上 */
- a:active    /* 选定的链接 */


  **注意**

* 写的时候，他们的顺序尽量不要颠倒  按照  lvha 的顺序。否则可能引起错误。  
* 因为叫链接伪类，所以都是 利用交集选择器  a:link    a:hover  
* 因为a链接浏览器具有默认样式，所以我们实际工作中都需要给链接单独指定样式。
* 实际工作开发中，我们很少写全四个状态，一般我们写法如下：

~~~css
a {   /* a是标签选择器  所有的链接 */
			font-weight: 700;
			font-size: 16px;
			color: gray;
}
a:hover {   /* :hover 是链接伪类选择器 鼠标经过 */
			color: red; /*  鼠标经过的时候，由原来的 灰色 变成了红色 */
}
~~~

### 复合选择器总结

| 选择器         | 作用                     | 特征                 | 使用情况 | 隔开符号及用法                          |
| -------------- | ------------------------ | -------------------- | -------- | --------------------------------------- |
| 后代选择器     | 用来选择元素后代         | 是选择所有的子孙后代 | 较多     | 符号是**空格** .nav a                   |
| 子代选择器     | 选择 最近一级元素        | 只选亲儿子           | 较少     | 符号是**>**   .nav>p                    |
| 交集选择器     | 选择两个标签交集的部分   | 既是 又是            | 较少     | **没有符号**  p.one                     |
| 并集选择器     | 选择某些相同样式的选择器 | 可以用于集体声明     | 较多     | 符号是**逗号** .nav, .header            |
| 链接伪类选择器 | 给链接更改状态           |                      | 较多     | 重点记住 a{} 和 a:hover  实际开发的写法 |

## css的三个特性

### CSS层叠性

- 概念：

  所谓层叠性是指多种CSS样式的叠加。

  是浏览器处理冲突的一个能力,如果一个属性通过两个相同选择器设置到同一个元素上，那么这个时候一个属性就会将另一个属性层叠掉

- 原则：

  - 样式冲突，遵循的原则是**就近原则。** 那个样式离着结构近，就执行那个样式。
  - 样式不冲突，不会层叠。

### CSS继承性

- 概念：

  子标签会继承父标签的某些样式，如文本颜色和字号。

   想要设置一个可继承的属性，只需将它应用于父元素即可。

简单的理解就是：  子承父业。

- **注意**：
  - 恰当地使用继承可以简化代码，降低CSS样式的复杂性。比如有很多子级孩子都需要某个样式，可以给父级指定一个，这些孩子继承过来就好了。
  - 子元素可以继承父元素的样式（**text-，font-，line-这些元素开头的可以继承，以及color属性**）

###  CSS特殊性

**优先级（重点）**

概念：

定义CSS样式时，经常出现两个或更多规则应用在同一元素上，此时，

* 如果选择器相同，则执行层叠性
* 如果选择器不同，就会出现优先级的问题。

#### 1). 权重计算公式

关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity（特殊性）

| 标签选择器             | 计算权重公式 |
| ---------------------- | ------------ |
| 继承或者 *             | 0,0,0,0      |
| 每个元素（标签选择器） | 0,0,0,1      |
| 每个类，伪类           | 0,0,1,0      |
| 每个ID                 | 0,1,0,0      |
| 每个行内样式 style=""  | 1,0,0,0      |
| 每个!important  重要的 | ∞ 无穷大     |

- 值从左到右，左面的最大，一级大于一级。
- 关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity（特殊性）
- div {
      color: pink!important;  
  }

#### 2). 权重叠加

我们经常用交集选择器，后代选择器等，是有多个基础选择器组合而成，那么此时，就会出现权重叠加。

就是一个简单的加法计算

- div ul  li   ------>      0,0,0,3
- .nav ul li   ------>      0,0,1,2
- a:hover      -----—>   0,0,1,1
- .nav a       ------>      0,0,1,1

 注意： 

1. 数位之间不是十进制 在查阅了相关资料后发现，权重的进制是并不是十进制，CSS 权重进制在 IE6 为 256，后来扩大到了 65536，现代浏览器则采用更大的数量。比如说： 0,0,0,5 + 0,0,0,5 =0,0,0,10 而不是 0,0, 1, 0， 所以不会存在10个div能赶上一个类选择器的情况。

#### 3). 继承的权重是0

这个不难，但是忽略很容易绕晕。其实，我们修改样式，一定要看该标签有没有被选中。

1） 如果选中了，那么以上面的公式来计权重。谁大听谁的。 
2） 如果没有选中，那么权重是0，因为继承的权重为0.

## CSS显示模式

### 什么是标签显示模式

- 什么是标签的显示模式？

  标签以什么方式进行显示，比如div 自己占一行， 比如span 一行可以放很多个

- 作用： 

  我们网页的标签非常多，再不同地方会用到不同类型的标签，以便更好的完成我们的网页。

- 标签的类型(分类)

  HTML标签一般分为块标签和行内标签两种类型，它们也称块元素和行内元素。

### 块级元素(block-level)

- 例：

```
常见的块元素有<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>等，其中<div>标签是最典型的块元素。
```

- 块级元素的特点

（1）比较霸道，自己独占一行

（2）高度，宽度、外边距以及内边距都可以控制。

（3）宽度默认是容器（父级宽度）的100%

（4）是一个容器及盒子，里面可以放行内或者块级元素。

- 注意：
  - 只有 文字才 能组成段落  因此 p  里面不能放块级元素，特别是 p 不能放div 
  - 同理还有这些标签h1,h2,h3,h4,h5,h6,dt，他们都是文字类块级标签，里面不能放其他块级元素。

### 行内元素(inline-level)

- 例：

```
常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中<span>标签最典型的行内元素。有的地方也成内联元素
```

- 行内元素的特点：

（1）相邻行内元素在一行上，一行可以显示多个。

（2）高、宽直接设置是无效的。

（3）默认宽度就是它本身内容的宽度。

（4）**行内元素只能容纳文本或则其他行内元素。**

 注意：

- 链接里面不能再放链接。
- 特殊情况a里面可以放块级元素，但是给a转换一下块级模式最安全。

### 行内块元素（inline-block）

- 例：

```
在行内元素中有几个特殊的标签——<img />、<input />、<td>，可以对它们设置宽高和对齐属性，有些资料可能会称它们为行内块元素。
```

- 行内块元素的特点：

  （1）和相邻行内元素（行内块）在一行上,但是之间会有空白缝隙。一行可以显示多个
  （2）默认宽度就是它本身内容的宽度。
  （3）高度，行高、外边距以及内边距都可以控制。

###  三种模式总结区别

| 元素模式   | 元素排列               | 设置样式               | 默认宽度         | 包含                     |
| ---------- | ---------------------- | ---------------------- | ---------------- | ------------------------ |
| 块级元素   | 一行只能放一个块级元素 | 可以设置宽度高度       | 容器的100%       | 容器级可以包含任何标签   |
| 行内元素   | 一行可以放多个行内元素 | 不可以直接设置宽度高度 | 它本身内容的宽度 | 容纳文本或则其他行内元素 |
| 行内块元素 | 一行放多个行内块元素   | 可以设置宽度和高度     | 它本身内容的宽度 |                          |

## CSS背景

### 背景颜色(color)

- 语法：

  ```
  background-color:颜色值;   默认的值是 transparent  透明的
  ```

### 背景图片(image)

- 语法： 

```css
background-image : none | url (url) 
```

| 参数 |              作用              |
| ---- | :----------------------------: |
| none |       无背景图（默认的）       |
| url  | 使用绝对或相对地址指定背景图像 |

```css
background-image : url(images/demo.png);
```

- 小技巧：  我们提倡 背景图片后面的地址，url不要加引号。

###  背景平铺（repeat）

- 语法： 

```css
background-repeat : repeat | no-repeat | repeat-x | repeat-y 
```

| 参数      |                 作用                 |
| --------- | :----------------------------------: |
| repeat    | 背景图像在纵向和横向上平铺（默认的） |
| no-repeat |            背景图像不平铺            |
| repeat-x  |         背景图像在横向上平铺         |
| repeat-y  |          背景图像在纵向平铺          |

### 背景位置(position) 重点

- 语法： 

```css
background-position : length || length

background-position : position || position 
```

| 参数     |                              值                              |
| -------- | :----------------------------------------------------------: |
| length   |         百分数 \| 由浮点数字和单位标识符组成的长度值         |
| position | top \| center \| bottom \| left \| center \| right   方位名词 |

- 注意：
  - 必须先指定background-image属性
  - position 后面是x坐标和y坐标。 可以使用方位名词或者 精确单位。
  - 如果指定两个值，两个值都是方位名字，则两个值前后顺序无关，比如left  top和top  left效果一致
  - 如果只指定了一个方位名词，另一个值默认居中对齐。
  - 如果position 后面是精确坐标， 那么第一个，肯定是 x  第二的一定是y
  - 如果只指定一个数值,那该数值一定是x坐标，另一个默认垂直居中
  - 如果指定的两个值是 精确单位和方位名字混合使用，则第一个值是x坐标，第二个值是y坐标

**实际工作用的最多的，就是背景图片居中对齐了。**

###  背景附着

- 背景附着就是解释背景是滚动的还是固定的

- 语法： 

  ```】
  background-attachment : scroll | fixed 
  ```

| 参数   |           作用           |
| ------ | :----------------------: |
| scroll | 背景图像是随对象内容滚动 |
| fixed  |       背景图像固定       |

###  背景简写

- background：属性的值的书写顺序官方并没有强制标准的。为了可读性，建议大家如下写：
- background: 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置;
- 语法：

```css
background: transparent url(image.jpg) repeat-y  scroll center top ;
```

案例：

导航栏案例

###  背景透明(CSS3)

- 语法：

```css
background: rgba(0, 0, 0, 0.3);
```

- 最后一个参数是alpha 透明度  取值范围 0~1之间
- 我们习惯把0.3 的 0 省略掉  这样写  background: rgba(0, 0, 0, .3);
- 注意：  背景半透明是指盒子背景半透明， 盒子里面的内容不受影响
- 因为是CSS3 ，所以 低于 ie9 的版本是不支持的。

### 背景总结

| 属性                  | 作用             | 值                                                           |
| --------------------- | :--------------- | :----------------------------------------------------------- |
| background-color      | 背景颜色         | 预定义的颜色值/十六进制/RGB代码                              |
| background-image      | 背景图片         | url(图片路径)                                                |
| background-repeat     | 是否平铺         | repeat/no-repeat/repeat-x/repeat-y                           |
| background-position   | 背景位置         | length/position    分别是x  和 y坐标， 切记 如果有 精确数值单位，则必须按照先X 后Y 的写法 |
| background-attachment | 背景固定还是滚动 | scroll/fixed                                                 |
| 背景简写              | 更简单           | 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置;  他们没有顺序 |
| 背景透明              | 让盒子半透明     | background: rgba(0,0,0,0.3);   后面必须是 4个值              |

## CSS注释方法

```
/* 要注释的内容 */
```

## CSS文字文本样式

### font-size:

- 作用：

  font-size属性用于设置字号

~~~css
p {  
    font-size:20px; 
}
~~~

- 单位：

  - 可以使用相对长度单位，也可以使用绝对长度单位。
  - 相对长度单位比较常用，推荐使用像素单位px，绝对长度单位使用较少。

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day01/笔记/media/dd.png" />

**注意：**

* 我们文字大小以后，基本就用px了，其他单位很少使用
* 谷歌浏览器默认的文字大小为16px
* 但是不同浏览器可能默认显示的字号大小不一致，我们尽量给一个明确值大小，不要默认大小。一般给body指定整个页面文字的大小

###  font-family:字体

- 作用：

  font-family属性用于设置哪一种字体。

~~~
p{ font-family:"微软雅黑";}
~~~

- 网页中常用的字体有宋体、微软雅黑、黑体等，例如将网页中所有段落文本的字体设置为微软雅黑
- 可以同时指定多个字体，中间以逗号隔开，表示如果浏览器不支持第一个字体，则会尝试下一个，直到找到合适的字体， 如果都没有，则以我们电脑默认的字体为准。

~~~
p{font-family: Arial,"Microsoft Yahei", "微软雅黑";}
~~~

常用技巧：

```
1. 各种字体之间必须使用英文状态下的逗号隔开。
2. 中文字体需要加英文状态下的引号，英文字体一般不需要加引号。当需要设置英文字体时，英文字体名必须位于中文字体名之前。
3. 如果字体名中包含空格、#、$等符号，则该字体必须加英文状态下的单引号或双引号，例如font-family: "Times New Roman";。
4. 尽量使用系统默认字体，保证在任何用户的浏览器中都能正确显示。
```

### CSS Unicode字体

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day01/笔记/media/shs.png" /

- 为什么使用 Unicode字体

  - 在 CSS 中设置字体名称，直接写中文是可以的。但是在文件编码（GB2312、UTF-8 等）不匹配时会产生乱码的错误。
  - xp 系统不支持 类似微软雅黑的中文。

- 解决：

  - 方案一： 你可以使用英文来替代。 比如` font-family:"Microsoft Yahei"`。

  - 方案二： 在 CSS 直接使用 Unicode 编码来写字体名称可以避免这些错误。使用 Unicode 写中文字体名称，浏览器是可以正确的解析的。

    ~~~
    font-family: "\5FAE\8F6F\96C5\9ED1";   表示设置字体为“微软雅黑”。
    ~~~

| 字体名称    | 英文名称        | Unicode 编码         |
| ----------- | --------------- | -------------------- |
| 宋体        | SimSun          | \5B8B\4F53           |
| 新宋体      | NSimSun         | \65B0\5B8B\4F53      |
| 黑体        | SimHei          | \9ED1\4F53           |
| 微软雅黑    | Microsoft YaHei | \5FAE\8F6F\96C5\9ED1 |
| 楷体_GB2312 | KaiTi_GB2312    | \6977\4F53_GB2312    |
| 隶书        | LiSu            | \96B6\4E66           |
| 幼园        | YouYuan         | \5E7C\5706           |
| 华文细黑    | STXihei         | \534E\6587\7EC6\9ED1 |
| 细明体      | MingLiU         | \7EC6\660E\4F53      |
| 新细明体    | PMingLiU        | \65B0\7EC6\660E\4F53 |

为了照顾不同电脑的字体安装问题，我们尽量只使用宋体和微软雅黑中文字体

###  font-weight:字体粗细

- 在html中如何将字体加粗我们可以用标签来实现
  - 使用 b  和 strong 标签是文本加粗。
- 可以使用CSS 来实现，但是CSS 是没有语义的。

| 属性值  | 描述                                                      |
| ------- | :-------------------------------------------------------- |
| normal  | 默认值（不加粗的）                                        |
| bold    | 定义粗体（加粗的）                                        |
| 100~900 | 400 等同于 normal，而 700 等同于 bold  我们重点记住这句话 |

提倡：

  我们平时更喜欢用数字来表示加粗和不加粗。

### font-style:字体风格

- 在html中如何将字体倾斜我们可以用标签来实现
  - 字体倾斜除了用 i  和 em 标签，
- 可以使用CSS 来实现，但是CSS 是没有语义的

font-style属性用于定义字体风格，如设置斜体、倾斜或正常字体，其可用属性值如下：

| 属性   | 作用                                                    |
| ------ | :------------------------------------------------------ |
| normal | 默认值，浏览器会显示标准的字体样式  font-style: normal; |
| italic | 浏览器会显示斜体的字体样式。                            |

小技巧： 

```
平时我们很少给文字加斜体，反而喜欢给斜体标签（em，i）改为普通模式。
```

### font:综合设置字体样式 (重点)

font属性用于对字体样式进行综合设置

- 基本语法格式如下：

```css
选择器 { font: font-style  font-weight  font-size/line-height  font-family;}
```

- 注意：
  - 使用font属性时，必须按上面语法格式中的顺序书写，不能更换顺序，各个属性以**空格**隔开。
  - 其中不需要设置的属性可以省略（取默认值），但必须保留font-size和font-family属性，否则font属性将不起作用。

##  font总结

| 属性        | 表示     | 注意点                                                       |
| :---------- | :------- | :----------------------------------------------------------- |
| font-size   | 字号     | 我们通常用的单位是px 像素，一定要跟上单位                    |
| font-family | 字体     | 实际工作中按照团队约定来写字体                               |
| font-weight | 字体粗细 | 记住加粗是 700 或者 bold  不加粗 是 normal 或者  400  记住数字不要跟单位 |
| font-style  | 字体样式 | 记住倾斜是 italic     不倾斜 是 normal  工作中我们最常用 normal |
| font        | 字体连写 | 1. 字体连写是有顺序的  不能随意换位置 2. 其中字号 和 字体 必须同时出现 |

## CSS外观属性

### color:文本颜色

- 作用：

  color属性用于定义文本的颜色，

- 其取值方式有如下3种：

| 表示表示       | 属性值                        |
| :------------- | :---------------------------- |
| 预定义的颜色值 | red，green，blue              |
| 十六进制       | #FF0000，#FF6600，#29D794     |
| RGB代码        | rgb(255,0,0)或rgb(100%,0%,0%) |

- 注意

  我们实际工作中， 用 16进制的写法是最多的，而且我们更喜欢简写方式比如  #f00 代表红色

### text-align:文本水平对齐方式

- 作用：

  text-align属性用于设置文本内容的水平对齐，相当于html中的align对齐属性

- 其可用属性值如下：

| 属性   |       解释       |
| ------ | :--------------: |
| left   | 左对齐（默认值） |
| right  |      右对齐      |
| center |     居中对齐     |

- 注意：

  是让盒子里面的内容水平居中， 而不是让盒子居中对齐

###  line-height:行间距

- 作用：

  line-height属性用于设置行间距，就是行与行之间的距离，即字符的垂直间距，一般称为行高。

- 单位：

  - line-height常用的属性值单位有三种，分别为像素px，相对值em和百分比%，实际工作中使用最多的是像素px

- 技巧：

```
一般情况下，行距比字号大7.8像素左右就可以了。
line-height: 24px;
```

### text-indent:首行缩进

- 作用：

  text-indent属性用于设置首行文本的缩进，

- 属性值

  - 其属性值可为不同单位的数值、em字符宽度的倍数、或相对于浏览器窗口宽度的百分比%，允许使用负值,
  - 建议使用em作为设置单位。

**1em 就是一个字的宽度   如果是汉字的段落， 1em 就是一个汉字的宽度**

~~~css
p {
      /*行间距*/
      line-height: 25px;
      /*首行缩进2个字  em  1个em 就是1个字的大小*/
      text-indent: 2em;  
 }
~~~

###  text-decoration 文本的装饰

text-decoration   通常我们用于给链接修改装饰效果

| 值           | 描述                                                  |
| ------------ | ----------------------------------------------------- |
| none         | 默认。定义标准的文本。 取消下划线（最常用）           |
| underline    | 定义文本下的一条线。下划线 也是我们链接自带的（常用） |
| overline     | 定义文本上的一条线。（不用）                          |
| line-through | 定义穿过文本下的一条线。（不常用）                    |

### CSS外观属性总结

| 属性            | 表示     | 注意点                                                  |
| :-------------- | :------- | :------------------------------------------------------ |
| color           | 颜色     | 我们通常用  十六进制   比如 而且是简写形式 #fff         |
| line-height     | 行高     | 控制行与行之间的距离                                    |
| text-align      | 水平对齐 | 可以设定文字水平的对齐方式                              |
| text-indent     | 首行缩进 | 通常我们用于段落首行缩进2个字的距离   text-indent: 2em; |
| text-decoration | 文本修饰 | 记住 添加 下划线  underline  取消下划线  none           |

## CSS盒子模型

所谓盒子模型：

- 就是把HTML页面中的布局元素看作是一个矩形的盒子，也就是一个盛装内容的容器。
- 盒子模型有元素的内容、边框（border）、内边距（padding）、和外边距（margin）组成。
- 盒子里面的文字和图片等元素是 内容区域
- 盒子的厚度 我们成为 盒子的边框 
- 盒子内容与边框的距离是内边距（类似单元格的 cellpadding)
- 盒子与盒子之间的距离是外边距（类似单元格的 cellspacing）

![image-20210602220844513](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210602220844513.png)

### 盒子边框 border

- 语法：

~~~css
border : border-width || border-style || border-color 
~~~

| 属性         |          作用          |
| ------------ | :--------------------: |
| border-width | 定义边框粗细，单位是px |
| border-style |       边框的样式       |
| border-color |        边框颜色        |

- 边框的样式：
  - none：没有边框即忽略所有边框的宽度（默认值）
  - solid：边框为单实线(最为常用的)
  - dashed：边框为虚线  
  - dotted：边框为点线

#### 边框综合设置

```
border : border-width || border-style || border-color 
```

例如：

~~~css
 border: 1px solid red;  没有顺序  
~~~

#### 盒子边框写法总结表

很多情况下，我们不需要指定4个边框，我们是可以单独给4个边框分别指定的。

| 上边框                     | 下边框                        | 左边框                      | 右边框                       |
| :------------------------- | :---------------------------- | :-------------------------- | :--------------------------- |
| border-top-style:样式;     | border-bottom-style:样式;     | border-left-style:样式;     | border-right-style:样式;     |
| border-top-width:宽度;     | border- bottom-width:宽度;    | border-left-width:宽度;     | border-right-width:宽度;     |
| border-top-color:颜色;     | border- bottom-color:颜色;    | border-left-color:颜色;     | border-right-color:颜色;     |
| border-top:宽度 样式 颜色; | border-bottom:宽度 样式 颜色; | border-left:宽度 样式 颜色; | border-right:宽度 样式 颜色; |

#### 表格的细线边框

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/表格边框.png">

- 通过表格的`cellspacing="0"`,将单元格与单元格之间的距离设置为0，

- 但是两个单元格之间的边框会出现重叠，从而使边框变粗

- 通过css属性：

  ~~~
  table{ border-collapse:collapse; }  
  ~~~

  - collapse 单词是合并的意思
  - border-collapse:collapse; 表示相邻边框合并在一起。

~~~css
<style>
	table {
		width: 500px;
		height: 300px;
		border: 1px solid red;
	}
	td {
		border: 1px solid red;
		text-align: center;
	}
	table, td {
		border-collapse: collapse;  /*合并相邻边框*/
	}
</style>
~~~

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/边框合并.png">

### 内边距（padding）

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/16内边距.png">

#### 内边距

​	padding属性用于设置内边距。 **是指 边框与内容之间的距离。**

#### 设置

| 属性           | 作用     |
| -------------- | :------- |
| padding-left   | 左内边距 |
| padding-right  | 右内边距 |
| padding-top    | 上内边距 |
| padding-bottom | 下内边距 |

当我们给盒子指定padding值之后， 发生了2件事情：

1. 内容和边框 有了距离，添加了内边距。
2. 盒子会变大了。

注意：  后面跟几个数值表示的意思是不一样的。

我们分开写有点麻烦，我们可以不可以简写呢？

| 值的个数 | 表达意思                                        |
| -------- | ----------------------------------------------- |
| 1个值    | padding：上下左右内边距;                        |
| 2个值    | padding: 上下内边距    左右内边距 ；            |
| 3个值    | padding：上内边距   左右内边距   下内边距；     |
| 4个值    | padding: 上内边距 右内边距 下内边距 左内边距 ； |

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/顺时针.jpg">

####  内盒尺寸计算（元素实际大小）

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/盒模型大小.png">

- 宽度

  Element Height = content height + padding + border （Height为内容高度）

- 高度

  Element Width = content width + padding + border （Width为内容宽度）

- 盒子的实际的大小 =   内容的宽度和高度 +  内边距   +  边框   

#### 内边距产生的问题

- 问题

  <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/31padding问题.png">

  会撑大原来的盒子

- 解决：

  通过给设置了宽高的盒子，减去相应的内边距的值，维持盒子原有的大小

  <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/32padding问题解决.png">

####  padding不影响盒子大小情况

> 如果没有给一个盒子指定宽度， 此时，如果给这个盒子指定padding， 则不会撑开盒子。

### 外边距

margin属性用于设置外边距。  margin就是控制**盒子和盒子之间的距离**

#### 设置

| 属性          | 作用     |
| ------------- | :------- |
| margin-left   | 左外边距 |
| margin-right  | 右外边距 |
| margin-top    | 上外边距 |
| margin-bottom | 下外边距 |

margin值的简写 （复合写法）代表意思  跟 padding 完全相同。

#### 块级盒子水平居中

- 可以让一个块级盒子实现水平居中必须：
  - 盒子必须指定了宽度（width）
  - 然后就给**左右的外边距都设置为auto**，

实际工作中常用这种方式进行网页布局，示例代码如下：

~~~css
.header{ width:960px; margin:0 auto;}
~~~

常见的写法，以下下三种都可以。

* margin-left: auto;   margin-right: auto;
* margin: auto;
* margin: 0 auto;

#### 文字居中和盒子居中区别

1.  盒子内的文字水平居中是  text-align: center,  而且还可以让 行内元素和行内块居中对齐
2.  块级盒子水平居中  左右margin 改为 auto 

~~~css
text-align: center; /*  文字 行内元素 行内块元素水平居中 */
margin: 10px auto;  /* 块级盒子水平居中  左右margin 改为 auto 就阔以了 上下margin都可以 */
~~~

#### 插入图片和背景图片区别

1. 插入图片 我们用的最多 比如产品展示类  移动位置只能靠盒模型 padding margin
2. 背景图片我们一般用于小图标背景 或者 超大背景图片  背景图片 只能通过  background-position

~~~css
 img {  
		width: 200px;/* 插入图片更改大小 width 和 height */
		height: 210px;
		margin-top: 30px;  /* 插入图片更改位置 可以用margin 或padding  盒模型 */
		margin-left: 50px; /* 插入当图片也是一个盒子 */
	}

 div {
		width: 400px;
		height: 400px;
		border: 1px solid purple;
		background: #fff url(images/sun.jpg) no-repeat;
		background-position: 30px 50px; /* 背景图片更改位置 我用 background-position */
	}
~~~

####  清除元素的默认内外边距(重要)

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/19清除内外边距.png">

为了更灵活方便地控制网页中的元素，制作网页时，我们需要将元素的默认内外边距清除

代码： 

~~~css
* {
   padding:0;         /* 清除内边距 */
   margin:0;          /* 清除外边距 */
}
~~~

注意：  

* 行内元素为了照顾兼容性， 尽量只设置左右内外边距， 不要设置上下内外边距。

#### 外边距合并

使用margin定义块元素的**垂直外边距**时，可能会出现外边距的合并。

#### (1). 相邻块元素垂直外边距的合并

- 当上下相邻的两个块元素相遇时，如果上面的元素有下外边距margin-bottom
- 下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和
- **取两个值中的较大者**这种现象被称为相邻块元素垂直外边距的合并（也称外边距塌陷）。

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/www.png" />

**解决方案：尽量给只给一个盒子添加margin值**。

#### (2). 嵌套块元素垂直外边距的合并（塌陷）

- 对于两个嵌套关系的块元素，如果父元素没有上内边距及边框
- 父元素的上外边距会与子元素的上外边距发生合并
- 合并后的外边距为两者中的较大者

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/n.png" />

**解决方案：**

1. 可以为父元素定义上边框。
2. 可以为父元素定义上内边距
3. 可以为父元素添加overflow:hidden。

### 圆角边框(CSS3)

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/圆角.png">

- 语法：

```css
border-radius:length;  
```

- 其中每一个值可以为 数值或百分比的形式。 

- 技巧： 让一个正方形  变成圆圈 

  ~~~
  border-radius: 50%;
  ~~~

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/radio.png" />

* <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/圆角.png">
* 以上效果图矩形的圆角， 就不要用 百分比了，因为百分比会是表示高度和宽度的一半。
* 而我们这里矩形就只用 用 高度的一半就好了。精确单位。

### 盒子阴影(CSS3)

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/阴影.png">

- 语法:

~~~css
box-shadow:水平阴影 垂直阴影 模糊距离（虚实）  阴影尺寸（影子大小）  阴影颜色  内/外阴影；
~~~

![1498467567011](H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day03/笔记/media/1498467567011.png)

- 前两个属性是必须写的。其余的可以省略。
- 外阴影 (outset) 是默认的 但是不能写           想要内阴影可以写  inset 

~~~css
div {
			width: 200px;
			height: 200px;
			border: 10px solid red;
			/* box-shadow: 5px 5px 3px 4px rgba(0, 0, 0, .4);  */
			/* box-shadow:水平位置 垂直位置 模糊距离 阴影尺寸（影子大小） 阴影颜色  内/外阴影； */
			box-shadow: 0 15px 30px  rgba(0, 0, 0, .4);
			
}
~~~



## 元素的显示与隐藏

- 目的

  让一个元素在页面中消失或者显示出来

- 场景

  类似网站广告，当我们点击关闭就不见了，但是我们重新刷新页面，会重新出现！

### display 显示（重点）

- display 设置或检索对象是否及如何显示。

  ~~~
  display: none 隐藏对象
  
  display：block 除了转换为块级元素之外，同时还有显示元素的意思。
  ~~~

- 特点： 隐藏之后，不再保留位置。

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/29none.png">

实际开发场景：

> 配合后面js做特效，比如下拉菜单，原先没有，鼠标经过，显示下拉菜单， 应用极为广泛

###  visibility 可见性 (了解)

- 设置或检索是否显示对象。

  ~~~
  visibility：visible ; 　对象可视
  
  visibility：hidden; 　  对象隐藏
  ~~~

- 特点： 隐藏之后，继续保留原有位置。（停职留薪）

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/30visibility.png">

### overflow 溢出(重点)

- 检索或设置当对象的内容超过其指定高度及宽度时如何管理内容。


| 属性值      | 描述                                       |
| ----------- | ------------------------------------------ |
| **visible** | 不剪切内容也不添加滚动条                   |
| **hidden**  | 不显示超过对象尺寸的内容，超出的部分隐藏掉 |
| **scroll**  | 不管超出内容否，总是显示滚动条             |
| **auto**    | 超出自动显示滚动条，不超出不显示滚动条     |

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/33overflow.png">

实际开发场景：

1. 清除浮动
2. 隐藏超出内容，隐藏掉,  不允许内容超过父盒子。

###   显示与隐藏总结

| 属性           | 区别                   | 用途                                                         |
| -------------- | ---------------------- | ------------------------------------------------------------ |
| **display**    | 隐藏对象，不保留位置   | 配合后面js做特效，比如下拉菜单，原先没有，鼠标经过，显示下拉菜单， 应用极为广泛 |
| **visibility** | 隐藏对象，保留位置     | 使用较少                                                     |
| **overflow**   | 只是隐藏超出大小的部分 | 1. 可以清除浮动 2. 保证盒子里面的内容不会超出该盒子范围      |

##  CSS用户界面样式

- 所谓的界面样式， 就是更改一些用户操作样式，以便提高更好的用户体验。
  - 更改用户的鼠标样式 (滚动条因为兼容性非常差，我们不研究) 
  - 表单轮廓等。
  - 防止表单域拖拽

### 鼠标样式cursor

 设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。

| 属性值          | 描述       |
| --------------- | ---------- |
| **default**     | 小白  默认 |
| **pointer**     | 小手       |
| **move**        | 移动       |
| **text**        | 文本       |
| **not-allowed** | 禁止       |

 鼠标放我身上查看效果哦：

```html
<ul>
  <li style="cursor:default">我是小白</li>
  <li style="cursor:pointer">我是小手</li>
  <li style="cursor:move">我是移动</li>
  <li style="cursor:text">我是文本</li>
  <li style="cursor:not-allowed">我是文本</li>
</ul>
```

### 轮廓线 outline

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/outline.png">

 是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。 

```css
 outline : outline-color ||outline-style || outline-width 
```

 但是我们都不关心可以设置多少，我们平时都是去掉的。 li  

最直接的写法是 ：  outline: 0;   或者  outline: none;

```html
 <input  type="text"  style="outline: 0;"/>
```

###  防止拖拽文本域resize

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/34textarea.png">

实际开发中，我们文本域右下角是不可以拖拽： 

```html
<textarea  style="resize: none;"></textarea>
```

### 用户界面样式总结

| 属性         | 用途                 | 用途                                                         |
| ------------ | -------------------- | ------------------------------------------------------------ |
| **鼠标样式** | 更改鼠标样式cursor   | 样式很多，重点记住 pointer                                   |
| **轮廓线**   | 表单默认outline      | outline 轮廓线，我们一般直接去掉，border是边框，我们会经常用 |
| 防止拖拽     | 主要针对文本域resize | 防止用户随意拖拽文本域，造成页面布局混乱，我们resize:none    |

##  vertical-align 垂直对齐

- 有宽度的块级元素居中对齐，是margin: 0 auto;
- 让文字居中对齐，是 text-align: center;

但是我们从来没有讲过有垂直居中的属性。

vertical-align 垂直对齐，它只针对于**行内元素**或者**行内块元素**，

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/xian.jpg" />

```css
vertical-align : baseline |top |middle |bottom 
```

设置或检索对象内容的垂直对其方式。

- 注意：

  vertical-align 不影响块级元素中的内容对齐，它只针对于**行内元素**或者**行内块元素**，

  特别是行内块元素， **通常用来控制图片/表单与文字的对齐**。

###  图片、表单和文字对齐

所以我们知道，我们可以通过vertical-align 控制图片和文字的垂直关系了。 默认的图片会和文字基线对齐。

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/基线对齐.jpg">

![1498467742995](H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/1498467742995.png)

### 去除图片底侧空白缝隙

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/35vertical.png">

- 原因：

  图片或者表单等行内块元素，他的底线会和父级盒子的基线对齐。

  就是图片底侧会有一个空白缝隙。

- 解决的方法就是：  

  - 给img vertical-align:middle | top| bottom等等。  让图片不要和基线对齐。<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/1633.png"  width="500"  style="border: 1px dashed #ccc;" />

    

  - 给img 添加 display：block; 转换为块级元素就不会存在问题了。<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/sina1.png" width="500" style="border: 1px dashed #ccc;"/>

##   溢出的文字省略号显示

###  white-space

- white-space设置或检索对象内文本显示方式。通常我们使用于强制一行显示内容 

~~~
white-space:normal ；默认处理方式

white-space:nowrap ；　强制在同一行内显示所有文本，直到文本结束或者遭遇br标签对象才换行。
~~~

###  text-overflow 文字溢出

- 设置或检索是否使用一个省略标记（...）标示对象内文本的溢出

~~~
text-overflow : clip ；不显示省略标记（...），而是简单的裁切 

text-overflow：ellipsis ； 当对象内文本溢出时显示省略标记（...）
~~~

**注意**：

一定要首先强制一行内显示，再次和overflow属性  搭配使用

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/dot.png">

###  总结三步曲

~~~css
  /*1. 先强制一行内显示文本*/
      white-space: nowrap;
  /*2. 超出的部分隐藏*/
      overflow: hidden;
  /*3. 文字用省略号替代超出的部分*/
      text-overflow: ellipsis;
~~~

##   CSS精灵技术（sprite) 重点

###  为什么需要精灵技术

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/sss.png" />

图所示为网页的请求原理图，当用户访问一个网站时，需要向服务器发送请求，网页上的每张图像都要经过一次请求才能展现给用户。

然而，一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接受和发送请求，这将大大降低页面的加载速度。

出现了CSS精灵技术（也称CSS Sprites、CSS雪碧）。

###  精灵技术讲解

CSS 精灵其实是将网页中的一些背景图像整合到一张大图中（精灵图），然而，各个网页元素通常只需要精灵图中不同位置的某个小图，要想精确定位到精灵图中的某个小图。

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/jds.png"  style="border: 1px dashed #ccc;" />

这样，当用户访问该页面时，只需向服务发送一次请求，网页中的背景图像即可全部展示出来。

我们需要使用CSS的

* background-image、
* background-repeat
* background-position属性进行背景定位，
* 其中最关键的是使用background-position 属性精确地定位。

###  精灵技术使用的核心总结

首先我们知道，css精灵技术主要针对于背景图片，插入的图片img 是不需要这个技术的。

1. 精确测量，每个小背景图片的大小和 位置。
2. 给盒子指定小背景图片时， 背景定位基本都是 负值。

### 制作精灵图(了解)

CSS 精灵其实是将网页中的一些背景图像整合到一张大图中（精灵图），那我们要做的，就是把小图拼合成一张大图。

大部分情况下，精灵图都是网页美工做。

```
我们精灵图上放的都是小的装饰性质的背景图片。 插入图片不能往上放。
我们可以横向摆放也可以纵向摆放，但是每个图片之间留有适当的空隙
在我们精灵图的最低端，留一片空隙，方便我们以后添加其他精灵图。
```

结束语：   小公司，背景图片很少的情况，没有必要使用精灵技术，维护成本太高。 如果是背景图片比较多，可以建议使用精灵技术。

### margin负值之美

#### 1). 负边距+定位：水平垂直居中

咱们前面讲过， 一个绝对定位的盒子， 利用  父级盒子的 50%，  然后 往左(上) 走 自己宽度的一半 ，可以实现盒子水平垂直居中。

#### 2). 压住盒子相邻边框 

<img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/margin.png" />



###  CSS三角形之美

~~~css
 div {

 	width: 0; 

    height: 0;
    line-height:0；
    font-size: 0;
	border-top: 10px solid red;

	border-right: 10px solid green;

	border-bottom: 10px solid blue;

	border-left: 10px solid #000; 

 }

~~~

一张图， 你就知道 css 三角是怎么来的了, 做法如下：

 <img src="H:/前端学习/百度云下载/【27】源码+课件+软件/01-03 前端开发基础/02-CSS资料/02-CSS资料/CSS-Day07/笔记/media/arr.png" />

1. 我们用css 边框可以模拟三角效果
2. 宽度高度为0
3. 我们4个边框都要写， 只保留需要的边框颜色，其余的不能省略，都改为 transparent 透明就好了
4. 为了照顾兼容性 低版本的浏览器，加上 font-size: 0;  line-height: 0;
