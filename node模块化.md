# Node模块化

------

## 模块化的基本概念

**模块化**是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

编程领域中的模块化，就是**遵守固定的规则**，把一个大文件拆成独立并互相依赖的多个小模块。

把代码进行模块化拆分的好处：

- 提高了代码的复用性
- 提高了代码的可维护性
- 可以实现按需加载

### 模块化规范

**模块化规范**就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。

例如：

- 使用什么样的语法格式来引用模块
- 在模块中使用什么样的语法格式向外暴露成员

**模块化规范的好处**：大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。

## Node.js中的模块的分类

Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是：

- 内置模块（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
- 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
-  第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）

### 加载模块

```js
// 加载内置模块
const fs = require('fs')

//加载用户自定义模块
const custom = require('./custom.js')

//加载第三方模块
const moment = require('moment')
```

注意：

- 使用 require() 方法加载其它模块时，会执行被加载模块中的代码。
- 加载自定义模块时，不加.js后缀名也可以。
- 

### Node.js中的模块作用域

**模块作用域**:和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做**模块作用域**。防止了全局变量污染的问题。 



### **module** **对象**

在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息



### **module.exports** **对象**

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。

外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。

使用 require() 方法导入模块时，导入的结果，**永远以** **module.exports** **指向的对象为准**。



### exports 对象

由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 exports 对象。

官方文档中解释为:"exports is assigned the value of module.exports before the module is evaluated." 意思是：在模块被导出之前exports被赋值为module.exports。

默认情况下，exports 和 module.exports 指向同一个对象。最终共享的结果，还是以 module.exports 指向的对象为准。

值得注意的是，**你不能给exports赋值**，这很重要，很重要，很重要。

为了防止混乱，建议不要在同一个模块中同时使用 exports 和 module.exports



### 常错点

#### 1.module.export的重新指向问题

```js
//new.js中代码
module.exports.id=123;
module.exports={
	name:'123',
	sex:'man'
}
//引用文件中代码
const re = require('./new');
console.log(re);

// 输出结果为 { name: '123', sex: 'man' }

//假如将new.js中代码调换顺序如下
module.exports={
	name:'123',
	sex:'man'
}
module.exports.id=123;

//则输出结果为 { name: '123', sex: 'man', id: 123 }
```

#### 2.exports和module.exports混用时的情况

```js
exports.username = 'xiaodonggua';
module.exports.name = '123';
//输出的结果是{ username: 'xiaodonggua', name: '123' }
//一般情况下不会互相影响


exports.username = 'xiaodonggua';
module.exports = {
	name : 'tk'
}
//输出结果为 { name: 'tk' } 

module.exports.username = 'xiaodonggua';
exports = {
	name : 'tk',
	id : 717
}
//输出结果为 { username: 'xiaodonggua' }

exports = {
	name : 'tk',
	id : 717
}
module.exports = exports;
module.exports.username = 'xiaodonggua';
//输出结果为{ name: 'tk', id: 717, username: 'xiaodonggua' }
```



### Node.js中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。

CommonJS 规定：

①每个模块内部，module 变量代表当前模块。

②module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。

③加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块。

## npm与包

### 包

Node.js 中的第三方模块又叫做包。

就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。

不同于 Node.js 中的内置模块与自定义模块，包是由第三方个人或团队开发出来的，免费供所有人使用。

**注意**：Node.js 中的包都是免费且开源的，不需要付费即可免费下载使用。

可以从这个网站上https://www.npmjs.com/ 找到几乎所有你需要的包

**npm, Inc.** **公司**提供了一个包管理工具，我们可以使用这个包管理工具，从 https://registry.npmjs.org/ 服务器把需要的包下载到本地使用。

这个包管理工具的名字叫做 Node Package Manager（简称 npm 包管理工具），这个包管理工具随着 Node.js 的安装包一起被安装到了用户的电脑上。

大家可以在终端中执行 **npm -v** 命令，来查看自己电脑上所安装的 npm 包管理工具的版本号

### 包的分类

使用 npm 包管理工具下载的包，共分为两大类，分别是：

- 项目包
- 全局包



**1.** **项目包**

那些被安装到项目的 node_modules 目录中的包，都是项目包。

项目包又分为两类，分别是：

- 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
-  核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

用-D 来将其选择为开发依赖包

**2.** **全局包**

在执行 npm install 命令时，如果提供了 -g 参数，则会把包安装为全局包。

全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。

注意：

- 只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。
- 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可。

### i5ting_toc

i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下：

```
npm install -g i5ting_toc
i5ting_toc -f 要转化的md文件路径 -o
```

### 规范的包结构

一个规范的包，它的组成结构，必须符合以下 3 点要求：

- 包必须以单独的目录而存在
- 包的顶级目录下要必须包含 package.json 这个包管理配置文件
- package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口。

### 开发属于自己的包

 **初始化包的基本结构**

①新建 tools 文件夹，作为包的根目录

②在 tools 文件夹中，新建如下三个文件：

- package.json （包管理配置文件）
- index.js     （包的入口文件）
- README.md （包的说明文档）

初始化 package.json文件:

```js
{
	"name": "dgua-tools",       //包的名称 是唯一的 不可重复 命名前要去npm官网查询是否有相同名称
	"version": "1.0.0",         //版本号 初始为1.0.0                     
	"main": "index.js",         //入口文件标注
	"description": "提供了格式化时间,HtmlEscape的功能",   //描述
	"keywords": ["dgua"],        //检索关键字
	"license": "ISC"            //开源许可协议 npm官方推荐为ISC
}
```

了解更多关于开源许可协议可以去[七种开源许可证_countofdane的博客-CSDN博客](https://blog.csdn.net/countofdane/article/details/82380892)查看

**在** **index.js** **中定义格式化时间的方法**

```js
//包的入口文件

//定义格式化时间的函数
function dataFormat(dataStr){
	const dt = new Date(dataStr)
	const y= dt.getFullYear();
	const m = padZero (dt.getMonth()+1);
	const d = padZero(dt.getDate())
	const hh = padZero(dt.getHours())
	const mm =padZero(dt.getMinutes())
	const ss =padZero( dt.getSeconds())
	return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}

function padZero (n){
	return n>9?n:'0'+n;
}

module.exports = {
	dataFormat
}
```

**编写包的说明文档**

包根目录中的 README.md 文件，是包的使用说明文档。通过它，我们可以事先把包的使用说明，以 markdown 的格式写出来，方便用户参考。

README 文件中具体写什么内容，没有强制性的要求；只要能够清晰地把包的作用、用法、注意事项等描述清楚即可。

我们所创建的这个包的 README.md 文档中，会包含以下 6 项内容：

安装方式、导入方式、格式化时间、转义 HTML 中的特殊字符、还原 HTML 中的特殊字符、开源协议

如下

```
## 安装
​```
npm install dgua-tools
​```

## 导入
​```js
const dgua = require('dgua-tools')
​```

## 格式化时间
​```js
//调用dataformat
const time =tk.dateFormat(new Date())
console.log(time);
​```

## 开源协议
ISC
```

### 发布自己的包

首先我们要注册一个npm账号

**1.** **注册** **npm** **账号**

- 访问 https://www.npmjs.com/ 网站，点击 sign up 按钮，进入注册用户界面
- 填写账号相关的信息：Full Name、Public Email、Username、Password
- 点击 Create an Account 按钮，注册账号
- 登录邮箱，点击验证链接，进行账号的验证

**2.** **登录** **npm** **账号**

npm 账号注册完成后，可以在终端中执行 npm login 命令，依次输入用户名、密码、邮箱后，即可登录成功。

注意：在运行 npm login 命令之前，必须先把下包的服务器地址切换为 npm 的官方服务器。否则会导致发布包失败！

**3.** **把包发布到** **npm** **上**

将终端切换到包的根目录之后，运行 npm publish 命令，即可将包发布到 npm 上（注意：包名不能雷同）。

**4.** **删除已发布的包**

运行 npm unpublish 包名 --force 命令，即可从 npm 删除已发布的包。

注意：

- npm unpublish 命令只能删除 72 小时以内发布的包
- npm unpublish 删除的包，在 24 小时内不允许重复发布
- 发布包的时候要慎重，尽量不要往 npm 上发布没有意义的包！

## 模块的加载机制

### 优先从缓存中加载

**模块在第一次加载后会被缓存**。 这也意味着多次调用 require() 不会导致模块的代码被执行多次。

注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。

### 内置模块的加载机制

内置模块是由 Node.js 官方提供的模块，内置模块的加载优先级最高。

例如，require('fs') 始终返回内置的 fs 模块，即使在 node_modules 目录下有名字也叫做 fs的包。

### 自定义模块的加载机制

使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。

同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：

1. 按照确切的文件名进行加载
2. 补全 .js 扩展名进行加载
3. 补全 .json 扩展名进行加载
4. 补全 .node 扩展名进行加载
5. 加载失败，终端报错

### 第三方模块的加载机制

如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。

如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。

### 目录作为模块

当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式：

①在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口

②如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件。

③如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'

