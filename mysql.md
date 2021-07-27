# 数据库与身份认证

## 数据库的基本概念

**什么是数据库**

数据库（database）是用来组织、存储和管理数据的仓库。

当今世界是一个充满着数据的互联网世界，充斥着大量的数据。数据的来源有很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、音乐、声音都是数据。

为了方便管理互联网世界中的数据，就有了数据库管理系统的概念（简称：数据库）。用户可以对数据库中的数据进行新增、查询、更新、删除等操作。

**常见的数据库及分类**

市面上的数据库有很多种，最常见的数据库有如下几个：

- MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise）
- Oracle 数据库（收费）
- SQL Server 数据库（收费）
- Mongodb 数据库（Community + Enterprise）

其中，MySQL、Oracle、SQL Server 属于**传统型数据库**（又叫做：关系型数据库 或 SQL 数据库），这三者的设计理念相同，用法比较类似。

而 Mongodb 属于**新型数据库**（又叫做：非关系型数据库 或 NoSQL 数据库），它在一定程度上弥补了传统型数据库的缺陷。

**数据组织结构**

在传统型数据库中，数据的组织结构分为数据库(database)、数据表(table)、数据行(row)、字段(field)这 4 大部分组成。

**实际开发中库、表、行、字段的关系**

- 在实际项目开发中，一般情况下，每个项目都对应独立的数据库。
- 不同的数据，要存储到数据库的不同表中，例如：用户数据存储到 users 表中，图书数据存储到 books 表中。
- 表中的行，代表每一条具体的数据。
- 每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这 3 个字段。

## 数据的使用

**创建数据库**

DataType 数据类型：

① int 整数

② varchar(len) 字符串

③ tinyint(1) 布尔值

字段的特殊标识：

① PK（Primary Key）主键、唯一标识

② NN（Not Null）值不允许为空

③ UQ（Unique）值唯一

④ AI（Auto Increment）值自动增长

### SQL

什么是 **SQL**

SQL（英文全称：Structured Query Language）是结构化查询语言，专门用来访问和处理数据库的编程语言。能够让我们**以编程的形式**，**操作数据库里面的数据**。



三个关键点：

①SQL 是一门数据库编程语言

②使用 SQL 语言编写出来的代码，叫做 SQL 语句

SQL 语言只能在关系型数据库中使用（例如 MySQL、Oracle、SQL Server）。非关系型数据库（例如 Mongodb）不支持 SQL 语言



### SQL语法

**增**

INSERT INTO 语句用于向数据表中插入新的数据行，语法格式如下：

```mysql
INSERT INTO table_name(列1，列2,...)VALUES(值1,值2,...)
```

```mysql
INSERT INTO user(name,password)VALUES('xiaodonggua','123456')
```

**删**

DELETE 语句用于删除表中的行。语法格式如下：

```mysql
DELETE FROM 表名称 WHERE 列名称 = 值
```

```mysql
DELETE FROM users WHERE id = 1  
```

**改**

Update 语句用于修改表中的数据,语法格式如下:

```mysql
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 旧值
```

```mysql
UPDATE users SET  password = '654321' WHERE name = 'xiaodonggua'
```

```mysql
UPDATE users SET  password = '654321' , id = 1 WHERE name = 'xiaodonggua'
```

**查**

SELECT 语句用于从表中查询数据。执行的结果被存储在一个结果表中（称为结果集）。语法格式如下

```js
SELECT * FROM 表名称
SELECT 列名称 FROM 表名称
```

**WHERE 子句**

WHERE 子句用于限定选择的标准。在 SELECT、UPDATE、DELETE 语句中，皆可使用 WHERE 子句来限定选择的标准。

下面的运算符可在 WHERE 子句中使用，用来限定选择的标准：

![image-20210607200447055](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210607200447055.png)

在某些版本的 SQL 中，操作符 <> 可以写为 != 

可以使用运算符和WHERE来选择满足特定条件的数据

```mysql
SELECT * FROM users where id>2
```

**AND和OR运算符**

AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来。

AND 表示必须同时满足多个条件，相当于 JavaScript 中的 && 运算符，例如 if (a !== 10 && a !== 20)

OR 表示只要满足任意一个条件即可，相当于 JavaScript 中的 || 运算符，例如 if(a !== 10 || a !== 20)

**ORDER BY子句**

ORDER BY 语句用于根据指定的列对结果集进行排序。

ORDER BY 语句默认按照升序对记录进行排序。

可以使用ASC/DESC 关键字来完成升序/降序。

示例：

```mysql
SELECT * FROM users ORDER BY status DESC;
```

同时 ORDER BY可以进行多重排序

对 users 表中的数据，先按照 status 字段进行降序排序，再按照 username 的字母顺序，进行升序排序，示例如下：

```mysql
SELECT * FROM users ORDER BY status DESC , username ASC
```

**COUNT(\*) 函数**

COUNT(*) 函数用于返回查询结果的总数据条数，语法格式如下：

```mysql
SELECT COUNT(*) FROM 表名
```

示例:

查询 users 表中 status 为 0 的总数据条数：

```mysql
SELECT COUNT (*) FROM users WHERE status = 0
```

**使用AS为列设置别名**

如果希望给查询出来的列名称设置别名，可以使用 AS 关键字，示例如下：

```mysql
SELECT COUNT (*) AS t FROM users WHERE status = 0
```

### 在项目中操作数据库

步骤:

- 安装操作 MySQL 数据库的第三方模块（mysql) 可以使用

  ```js
  npm install mysql
  ```

  

- 通过 mysql 模块连接到 MySQL 数据库

  ```js
  const db = mysql.createPool({
  	host: '127.0.0.1',
  	user: 'root',
  	password: 'admin123',
  	database: 'my_db_01',
  })
  ```

- 通过 mysql 模块执行 SQL 语句

**查询数据**

```js
const sqlStr = 'SELECT * FROM users'
db.query(sqlStr,(err,results) => {
	if (err) return console.log(err.message); 
	console.log(results);
	
})
```

**插入数据**

```js
const user ={
	id : 10,
	name : 'tk1',
	password : '12345',
	status : 0
}
const sqlStr = 'INSERT INTO users (id,name,password,status) VALUES (? ,?, ?, ?)'
db.query(sqlStr,[user.id,user.name,user.password,user.status],(err, results) => {
	if (err) return console.log(err.message); 
	if(results.affectedRows == 1) {
		console.log('123');
	}
})
```

如果数据对象的每个属性和和数据表的字段一一对应,则可以使用快捷方式

```js
const user ={
	id : 11,
	name : 'tk1',
	password : '12345',
	status : 0
}

const sqlStr = 'INSERT INTO users SET ?'
db.query(sqlStr,user,(err,results) => {
	if (err) return console.log(err.message); 
	if(results.affectedRows == 1) {
		console.log('123');
	}
})
```

**更新数据**

```js
const sqlStr = 'UPDATE users SET name=?  where id=?'
db.query(sqlStr,[user.name,user.id],(err,results) => {
	if (err) return console.log(err.message); 
	if(results.affectedRows == 1) {
		console.log('123');
	}
})
```

同理 如果数据对象的属性和数据表中字段一一对应,则可以使用快捷方式 

```js
const sqlStr = 'UPDATE users SET ?  where id=?'
db.query(sqlStr,[user,user.id],(err,results) => {
	if (err) return console.log(err.message); 
	if(results.affectedRows == 1) {
		console.log('123');
	}
})
```

**删除数据**

```js
 let id = 3;
const sqlStr = 'DELETE FROM users WHERE id=?'
db.query(sqlStr,id,(err,results) => {
	if (err) return console.log(err.message); 
	if(results.affectedRows == 1) {
		console.log('123');
	}
})
```

但是使用 DELETE 语句，会把真正的把数据从表中删除掉。为了保险起见，**推荐使用**标记删除的形式，来**模拟删除的动作**。

所谓的标记删除，就是在表中设置类似于 **status** 这样的**状态字段**，来**标记**当前这条数据是否被删除。

当用户执行了删除的动作时，我们并没有执行 DELETE 语句把数据删除掉，而是执行了 UPDATE 语句，将这条数据对应的 status 字段标记为删除即可。

# 身份认证

## Web开发模式

目前主流的 Web 开发模式有两种，分别是：

基于服务端渲染的传统 Web 开发模式

基于前后端分离的新型 Web 开发模式

### 服务端渲染的Web开发模式

服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要使用 Ajax 这样的技术额外请求页面的数据。代码示例如下

**服务端渲染的优缺点**

优点：

- **前端耗时少。**因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。尤其是移动端，更省电。
- 有利于SEO。因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信息，更有利于 SEO。

缺点：

- **占用服务器端资源。**即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。
- **不利于前后端分离，开发效率低。**使用服务器端渲染，则**无法进行分工合作**，尤其对于**前端复杂度高**的项目，不利于项目高效开发。





### 前后端分离的 Web开发模式

前后端分离的概念：前后端分离的开发模式，**依赖于** **Ajax** **技术的广泛应用**。简而言之，前后端分离的 Web 开发模式，就是**后端只负责提供** **API** **接口，前端使用** **Ajax** **调用接口**的开发模式。

优点：

- **开发体验好。**前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性。
-  **用户体验好。**Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
-  **减轻了服务器端的渲染压力。**因为页面最终是在每个用户的浏览器中生成的。

缺点：

 **不利于** **SEO****。**因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息。（解决方案：利用 Vue、React 等前端框架的 **SSR** （server side render）技术能够很好的解决 SEO 问题！）



## 身份认证

**身份认证**（Authentication）又称“身份验证”、“鉴权”，是指**通过一定的手段，完成对用户身份的确认**。

- 日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等。
- 在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的**手机验证码登录**、**邮箱密码登录**、**二维码登录**等

**不同开发模式下的身份认证**

①服务端渲染推荐使用 **Session** **认证机制**

② 前后端分离推荐使用 **JWT** **认证机制**

### Session认证机制



### JWT认证机制

