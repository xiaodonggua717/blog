# Git及Github的使用教程

​																						**----Dgua**

------



[TOC]



## Git基本概念

### 什么是版本控制软件

版本控制软件是一个用来记录文件变化，以便将来查阅特定
版本修订情况的系统，因此有时也叫做“版本控制系统”分为

**本地版本控制软件**

使用软件来记录文件的不同版本，提高了工作效率，
降低了手动维护版本的出错率
缺点：

1. 单机运行，不支持多人协作开发
2.  版本数据库故障后，所有历史更新记录会丢失

**集中化的版本控制系统 如SVN**

特点：基于服务器、客户端的运行模式，服务器保存文件的所有更新记录，客户端只保留最新的文件版本

优点：联网运行，支持多人协作开发

缺点：

1. 不支持离线提交版本更新
2. 中心服务器崩溃后，所有人无法正常工作
3. 版本数据库故障后，所有历史更新记录会丢失  

**分布式版本控制系统 典型代表：Git**

特点：基于服务器、客户端的运行模式。服务器保存文件的所有更新版本，客户端是服务器的完整备份，并不是只保留文件的最新版本。

优点：

1. 联网运行，支持多人协作开发

2. 客户端断网后支持离线本地提交版本更新

3. 服务器故障或损坏后，可使用任何一个客户端的备份进行恢复

   

### Git的优势

Git 之所以快速和高效，主要依赖于它的如下两个特性：
① 直接记录快照，而非差异比较
② 近乎所有操作都是本地执行

传统的版本控制系统（例如 SVN）是基于差异的版本控制，它们存储的是一组基本文件和每个文件随时间逐步
累积的差异。

Git 快照是在原有文件版本的基础上重新生成一份新的文件，类似于备份。为了效率，如果文件没有修改，Git
不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

git的三个区域:工作区 暂存区 git仓库

对应的状态也是 已修改 已暂存 已提交

### Git的安装

在开始使用 Git 管理项目的版本之前，需要将它安装到计算机上。可以使用浏览器访问如下的网址，根据自己
的操作系统，选择下载对应的 Git 安装包：https://git-scm.com/downloads

![image-20210531160629579](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531160629579.png)

如果你右击桌面可以看到“Git GUI here” 和“Git Bash here“则说明安装已经成功

可以在cmd命令中输入 

```
git --version
```

来查看git的版本

![image-20210531160830512](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531160830512.png)

安装之后第一件事就要配置自己的用户名和邮箱地址

右击桌面 在弹出的选项中选择”Git Bash here“

通过

```
 git config --global user.name 
```

和 

```
git config --global user.email
```

 配置用户名和邮箱地址

![image-20210531120101332](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531120101332.png)

可以输入

```
 git config --list --global
```

 来查看所有的全局配置项 

## Git的基本操作

### 获取仓库的两种方式

1. 将本地目录转化为git仓库
2. 从其他服务器克隆一份git仓库

### 创建仓库

```
git init
```

 即将当前文件目录转化为git仓库

我们可以任意选择一个文件夹，在空白处右击选择”Git Bash here“ 就会弹出命令行

![image-20210531154411198](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531154411198.png)\

之后我们可以在文件夹中的隐藏项目中看到.git文件夹

![image-20210531154446686](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531154446686.png)

### 查看文件状态

查看文件处于什么状态 

```
git status
```

 它可以有一种精简方式来显示状态 

```
git status -s 
```

此状态下：

未被跟踪的文件前面有红色的??标记 ![image-20210531155223534](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531155223534.png)

新添加到暂存区将显示绿色的A  ![image-20210531155240613](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531155240613.png)

已经改动且添加到暂存区的文件显示绿色的M ![image-20210531155300958](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531155300958.png)

已经改动但未添加到暂存区的文件显示红色的M![image-20210531155250351](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531155250351.png)

比如我们新建一个test.txt文件

![image-20210531154619047](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531154619047.png)

### 跟踪新文件 

那么如何跟踪新文件呢?

使用

```
 git add  
```

如 git add test.txt 会把文件放入暂存区
![image-20210531154903870](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531154903870.png)

我们再使用git status可以看到 test.txt已经变成了 绿色的A

![image-20210531154824697](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531154824697.png)

面对很多数量的文件时我们可以使用

```
 git add .
```

来一次性将所有工作区中的文件全部追踪上并提交到暂存区。

### 提交文件

已经有一个文件等待被提交了 那么我们可以 使用 git commit 将所有暂存区的文件来进行提交  可以加上一个 -m 来写注释

 如 

```
git commit -m "我修改了某某模块"
```

![image-20210531154945546](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531154945546.png)

如果这时候使用git status来检查文件情况,则显示没有东西可以提交(因为已经将可提交的文件提交完成)

![image-20210531161711731](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531161711731.png)

### 修改文件

那么如果我修改已经提交到暂存区的文件呢?

我们先修改test.txt 文件里面的内容  之后运行git status -s  我们可以看到一个红色的M

![image-20210531155054068](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531155054068.png)

即修改了文件但是还没有对其进行提交到暂存区,那么接着我们进行对已修改文件的暂存

这里又使用到了 git add

因为git add有三个功能:

- 可以用它开始跟踪新文件,
- 把已经跟踪且已经修改的文件放到暂存区
- 把冲突的文件标记为已解决状态 

git add test.txt 把已经修改的文件放在暂存区中 之后继续提交就可以

![image-20210531155204952](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531155204952.png)

### 撤销文件修改

假如我现在修改了之后将文件提交到了暂存区, 但是我突然后悔了怎么办呢？这里我们可以撤销文件修改

```
git checkout --文件名
```

比如我们此时test里面写入了一串数字 ‘1234’ 那么使用git checkout之后将会自动使用git仓库中的版本来替换掉目前的文件版本。

但是一旦撤销了修改，所有的修改都会消失且无法恢复，所以要小心使用这个命令。

### 取消暂存的文件

如果我已经将一批文件通过git add命令来存入了暂存区，但是我现在想要把其中某个文件从暂存区中拿出来应该怎么办呢？

我们可以使用git reset HEAD命令

```
git reset HEAD  文件名   //从暂存区中取出某个文件名

git reset HEAD .        //将暂存区中的文件全部移除
```

![image-20210531161443002](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531161443002.png)

我们可以看到test.txt的显示从绿色的M(已追踪)变成了红色的M(未追踪)

###  跳过暂存区

当然我们也可以直接将暂存区跳过 简化为工作区->Git仓库

```
git commit -a -m "描述"
```

直接将工作区里面的文件交到仓库中

![image-20210531161813610](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531161813610.png)

### 移除文件

如果我想要删除仓库中的文件 我有两种选择:

1. 将文件在工作区和仓库中全部移除,文件本身会被删除 

   ```
   git rm -f test.txt
   ```

   ![image-20210531163349513](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531163349513.png)

2. 只从仓库中移除文件而不删除文件本身

   ```
   git rm --cached test.txt
   ```



### 忽略文件

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 在这种情况下，我们可
以创建一个名为 .gitignore 的配置文件，列出要忽略的文件的匹配模式。

文件 .gitignore 的格式规范如下：

- 以**#**开头的都是注释
- 以**/**结尾的都是目录
- 以**/**开头的是防止递归
- 以**!**开头的表示取反

可以使用glob模式进行文件和文件夹的匹配

glob模式就是简化了的正则表达式:

所谓的 glob 模式是指简化了的正则表达式：

- 星号 * 匹配零个或多个任意字符
- **[abc]** 匹配任何一个列在方括号中的字符 （此案例匹配一个 a 或匹配一个 b 或匹配一个 c）
- 问号 **?** 只匹配一个任意字符
- 在方括号中使用**短划线**分隔两个字符， 表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配
  所有 0 到 9 的数字）
- 两个星号 ****** 表示匹配任意中间目录（比如 a/**/z 可以匹配 a/z 、 a/b/z 或 a/b/c/z 等）

使用.gitignore

<img src="C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531162347194.png" alt="image-20210531162347194" style="zoom:50%;" />

### 查看历史版本

可以使用

```
git log
//按时间先后顺序列出所有历史记录,最近的提交在最上面


git log -2 
// 只展示最新的2条提交历史,当然2可以换成别的数字,按需填写


git log --pretty = oneline
//将所提交历史信息在一行上展示


git log --pretty = format:"%h | %an | %ar | %s"
//自定义输出在一行上  %h是提交的简写哈希值 %an是作者名字 %ar是作者的修订日期 %s是提交说明
```

### 回退到指定的版本

<img src="C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531163221781.png" alt="image-20210531163221781" style="zoom: 67%;" />

## Github

### Github介绍

什么是开源:开源是指不仅提供程序还提供程序的源代码闭源是只提供程序，不提供源代码

开源并不意味着完全没有限制，为了限制使用者的使用范围和保护作者的权利，每个开源项目都应该遵守开源
许可协议（ Open Source License ）。

Github 是全球最大的开源项目托管平台。因为只支持 Git 作为唯一的版本控制工具，故名 GitHub。

### Github账号注册

① 访问 Github 的官网首页 https://github.com/
② 点击“Sign up”按钮跳转到注册页面
③ 填写可用的用户名、邮箱、密码
④ 通过点击箭头的形式，将验证图片摆正
⑤ 点击“Create account”按钮注册新用户
⑥ 登录到第三步填写的邮箱中，点击激活链接，完成注册

### 创建远程仓库

创建仓库

![image-20210531165753332](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531165753332.png)

创建成功

![image-20210531165818208](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531165818208.png)

### 远程仓库的两种访问形式

 ### HTTPS

两个红框里的内容分别是你没有本地仓库的选择和有本地仓库的选择.

![image-20210531184548183](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531184548183.png)

我们已经创建了本地仓库,所以直接使用第二个红框里面的内容 即

```
git remote add origin 你的https方式显示的url
git branch -M main
git push -u origin main
```

之后会弹出如下的页面 填写账号密码(新版的git已经支持从浏览器登录了 如果你在github上登录了账号 那么就可以使用github账号一键登录 非常方便)

![image-20210531174009048](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531174009048.png)

在之后的过程中只需要使用命令git push即可将本地仓库推送到远程仓库中

![image-20210531181811889](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531181811889.png)

在实际操作中有可能会遇到以下的问题:

#### 报错1 

报错情况:

![image-20210531173907325](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531173907325.png)

这是因为这是服务器的SSL证书没有经过第三方机构的签署，所以报错。

解决办法是:

```
git config --global http.sslVerify "false"
```

![image-20210531173944229](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531173944229.png)

#### 报错2

如果在输入密码之后你的页面出现了

![image-20210531175059825](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531175059825.png)

这种报错则有可能是你的git版本过低 使用以下的命令更新一下即可

```
git update-git-for-windows
```

详细可见:[authentication - Logon failed, use ctrl+c to cancel basic credential prompt - Stack Overflow](https://stackoverflow.com/questions/64962533/logon-failed-use-ctrlc-to-cancel-basic-credential-prompt)

### SSH

SSH的作用:实现本地仓库和 Github 之间免登录的加密数据传输。

SSH key 的好处：免登录身份认证、数据加密传输

SSH key 由两部分组成，分别是

- id_rsa（私钥文件，存放于客户端的电脑中即可)
- id_rsa.pub（公钥文件，需要配置到 Github 中）

#### 生成SSH key

打开Git bash

粘贴如下的命令，并将 your_email@example.com 替换为注册 Github 账号时填写的邮箱：

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

连续敲击 3 次回车，即可在 C:\Users\用户名文件夹\.ssh 目录中生成 id_rsa 和 id_rsa.pub 两个文件

![image-20210531182156923](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531182156923.png)

![image-20210531182215935](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531182215935.png)

#### 配置SSH key

1. 打开id_rsa.pub
2. 在浏览器中登录 Github，点击头像 -> Settings -> SSH and GPG Keys -> New SSH key
3. 将 id_rsa.pub 文件中的内容，粘贴到 Key 对应的文本框中(可以用记事本方式打开)
4. 在 Title 文本框中任意填写一个名称，来标识这个 Key 从何而来

#### 检测是否配置成功

打开git bash

输入

```
 ssh -T git@github.com
```

之后有可能会让你确认是否连接 输入yes

如果你可以看到一个如下的提示消息则说明你已经成功配置了SSH key

![image-20210531183111465](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531183111465.png)

#### 基于SSH 将本地仓库上传到github

和https方式同理去你项目的初始页面寻找github提供给你的代码

![image-20210531184901881](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531184901881.png)

结果:

![image-20210531184850641](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531184850641.png)

此时刷新可以看到远程仓库里面已经发生了变化

![image-20210531184937441](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531184937441.png)

### 将远程仓库里面的代码克隆到本地

使用代码

```
git clone 远程仓库地址
```

远程仓库地址可以去github的仓库中进行寻找

![image-20210531185200414](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531185200414.png)

结果

![image-20210531185358976](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531185358976.png)

我们可以看到一个名为 project02(远程仓库名)的文件夹出现在了目录下面  ![image-20210531185513189](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531185513189.png)

## Git的分支

### 基础理念

#### 以往的问题

几乎所有的版本控制系统都以某种形式支持分支。 使用分支意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。 在很多版本控制系统中，这是一个略微低效的过程——常常需要完全创建一个源代码目录的副本。对于大项目来说，这样的过程会耗费很多时间。

#### 分支的作用

在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发。

在进行提交操作时，Git 会保存一个提交对象（commit object）。 知道了 Git 保存数据的方式，我们可以很自然的想到——该提交对象会包含一个指向暂存内容快照的指针。 但不仅仅是这样，该提交对象还包含了作者的姓名和邮箱、提交时输入的信息以及指向它的父对象的指针。 首次提交产生的提交对象没有父对象，普通提交操作产生的提交对象有一个父对象， 而由多个分支合并产生的提交对象有多个父对象。

打个比方就是:你在学前端，另一个平行世界的你去学后端，结果有一天两个平行宇宙合并了，那么合并之后的你既会前端又会后端。

#### 功能分支

在初始化本地git仓库时，git就已经帮我们创建了一个main的主分支，它的作用就是用来保存和记录整个项目已经完成的功能代码。因此不允许程序员直接在main上进行代码的修改（因为风险比较高，如果哪个憨憨一不小心删了整个项目就GG了）

基于此 我们有了功能分支的概念：功能分支是专门用来开发新功能的分支，它是临时从main主分支上分叉出来的，当新功能开发且测试完毕后，最终需要合并到main主分支。



### 查看分支列表

```
git branch
```

![image-20210531191231759](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531191231759.png)

分支名字前面的*号表示当前所处的分支。

### 创建新分支

首先我们要创建新的分支出来

```
git branch 分支名字
```

![image-20210531191609225](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531191609225.png)

### 切换分支

为了工作我们要切换到对应的分支去

```
git checkout 要切换的分支名
```

![image-20210531192103746](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531192103746.png)

### 分支的快速创建和切换

那么有没有更快的办法呢，当然有

```
git checkout -b 分支名
```

![image-20210531192231202](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531192231202.png)

创建一个新的分支并自动切换过去，它其实是 git branch 和git checkout的简写

### 合并分支

在不同分支上完成了工作，接下来就需要合并到主分支上

第一步 切换到主分支

```
git checkout main
```

第二步 运行git merge命令 将所选分支合并

```
git merge 指定分支
```

![image-20210531192708497](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531192708497.png)

### 删除分支

合并之后之前的分支可以删掉了，需要我们先切换到主分支上，这时我们可以使用

```
git branch -d 分支名称
```

![image-20210531193103887](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531193103887.png)

这样我们就删除了想要删掉的分支

### 遇到冲突时

如果在两个不同的分支中，对同一个文件进行了不同的修改，Git 就没法干净的合并它们。 此时，我们需要打开
这些包含冲突的文件然后手动解决冲突。

### 将本地分支推送到远程仓库

```
git push -u 远程仓库名 分支名：远程分支名（即你想在远程仓库中新建的分支名 可不加）
```

![image-20210531194452765](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531194452765.png)

实际中远程仓库名经常会是origin 

第一次带 -u  之后就可以不用了

 ### 查看远程仓库中的所有分支列表

```
git remote show 远程仓库名称
```

![image-20210531195105110](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531195105110.png)

### 跟踪分支

跟踪分支指的是 从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下：

<img src="C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210531195212469.png" alt="image-20210531195212469" style="zoom: 80%;" />

### 拉取远程分支的最新代码

可以使用 

```
git pull
```

### 删除远程仓库中的分支

```
git push 远程仓库名 --delete 远程分支
```

示例：

```
git push origin --delete xiaodonggua
```

参考资料:[Git - Book (git-scm.com)](https://git-scm.com/book/en/v2)



问题!:

当我在github远程仓库中添加了一个新的readme之后 突然发现push操作报错了

![image-20210612173036908](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210612173036908.png)

**问题原因**：远程库与本地库不一致造成的，在hint中也有提示把远程库同步到本地库就可以了。

**解决办法**：使用命令行：

```bash
git pull --rebase 
```

该命令的意思是把远程库中的***\*更新合并\****到（**pull=fetch+merge**）本地库中，**–-rebase**的作用是取消掉本地库中刚刚的commit，并把他们**接到**更新后的版本库之中。



1. 发生问题时候的状态：

![image-20210612173428122](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210612173428122.png)

2. 执行 git pull -–rebase origin master 操作，意为先取消commit记录，并且把它们临时保存为补丁(patch)(这些补丁放到”.git/rebase”目录中)，之后同步远程库到本地，最后合并补丁到本地库之中。

![image-20210612173438755](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20210612173438755.png)

3. 最后把本地库push到远程库当中，使本地与远程仓库保持一致。

