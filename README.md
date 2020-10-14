# Introduction

* `目标：多人协作整理刷过题的代码和思路并作为未来的图书和开源项目`

* `使用工具 GitBook，Typora，git`

`gitbook是一个基于 Node.js 的命令行工具，支持 Markdown 和 AsciiDoc 两种语法格式，可以输出 HTML、PDF、eBook 等格式的电子书。html的电子书部署在服务器就相当于一个自己的博客网站。所以可以把 GitBook 定义为文档格式转换工具和网站部署工具。`
`Typora 是一款 Markdown 编辑器，排版漂亮，代码公式也可以快速插入`

`GitBook 又与 Markdown 和 Git 息息相关，因为只将它们结合起来使用，才能将它们的威力发挥到极致！因此，通常我们会选择合适的 Markdown 编辑工具以获得飞一般的写作体验；使用 GitBook 管理文档，预览、制作电子书；同时通过 Git 管理书籍内容的变更，并将其托管到云端（比如 GitHub、GitLab、码云，或者是自己搭建的 Git 服务器），实现多人协作。`

##  1.安装nvm进行nodejs版本管理

​	`nvm是nodejs的一个版本管理工具，下载地址为：`

```
`https://github.com/coreybutler/nvm-windows/releases`
```

`安装前先把原来安装的nodejs删除掉，在程序功能中删除即可`

`nodejs 是安装gitbook的必要环境，只有使用nvm下载稳定版的12.18.1可以避免踩坑，别问我为什么，最新版的根本不支持当前的gitbook，会在中途出现莫名的错误，下面是使用命令安装 nodejs 以及安装 gitbook的命令：`

```
#首先配置国内镜像方便快速下载nodejs
nvm node_mirror https://npm.taobao.org/mirrors/node/ 
nvm npm_mirror: https://npm.taobao.org/mirrors/npm/
#然后指定node版本进行安装
nvm install 12.18.1
#最后切换node版本
nvm use 12.18.1
#此时在命令行输入 node -v 查看node版本是否转换成功
```

##  2.安装cnpm下载gitbook工具

`因为源文件都在外网，所以使用cnpm下载国内的镜像最为便捷，以下为安装命令`

```
#node自带的包管理工具是npm
npm install -g cnpm --registry=https://registry.npm.taobao.org
#然后使用cnpm指定一个版本的gitbook进行安装
cnpm install -g gitbook@2.7.6
#不要问为什么不用最新的3.2.4版本，都是坑，然后安装gitbook-cli就是客户端，可以把你写的文档打包成网页方便大家一起浏览
cnpm install -g gitbook-cli
```

`至此gitbook 就安装完了，下面是gitbook进行文档创建和打包的代码`

```
#随意在自己喜欢的位置建立一个mybook目录,在此目录命令行进行初始化
gitbook init
```

`初始化之后会创建两个文件 SUMMARY.md和README.md 其中README.md就是这个项目的描述文件，SUMMARY才是核心，可以在其中用特殊的格式生成全书各个章节的目录，以及每一部分的空白文档。SUMMARY的书写格式如下`

```
# Summary
* [Introduction](README.md)
* [数组:Array](Array/README.md)
  * [Next Permutation Q31](Array/31_NextPermutation.md)
  * [Spiral Matrix Q54](Array/54_SpiralMatrix.md)
  * [Merge Intervals Q56](Array/56_MergeIntervals.md)
  * [Insert Interval Q57](Array/57_InsertInterval.md)
  * [Spiral Matrix II Q59](Array/59_SpiralMatrixII.md)
  * [Maximum Gap Q164](Array/164_MaximumGap.md)
  * [Rotate Array Q189](Array/189_RotateArray.md)
  * [Summary Ranges Q228](Array/228_SummaryRanges.md)
  * [Move Zeroes Q283](Array/283_MoveZeroes.md)
  * [Game of Life Q289](Array/289_GameOfLife.md)
```

`前两行是系统自动初始化添加的，可以理解为封面和摘要，后面是章节和每章的小节，这里*  []()组合分别填写章节名称和内容所在文件目录，可以说是全书的总纲。目前没有装插件除了md文件还不支持其他文件。下一步进行目录的生成和网站的部署`

```
#在SUMMARY完成编辑后保存并返回命令行，再次运行
gitbook init
#格式没有问题的情况下gitbook便会自动生成目录和里面的md文件
#然后进行 编译和服务器部署即可
gitbook build
gitbook serve
#服务器部署成功后便可从localhost:4000看到你当前笔记的样子了
```

##  3.安装Typora进行文本编辑

`不得不说，typora的界面简介，写出来的文本也是简介明了，没有一丝多余的功能，各级标题用#表示，章节用*表，简单的在文字周围加上符号就可以写出版式漂亮的文章`

```
https://www.typora.io/
#支持各种版本的电脑系统
```

##  4.最后就是同git的结合了

`不论何时何地，多少人协作，只要把自己写完的当前版本上传到云端，就能实时增加写作的内容。随时都能共同编辑这本未来的书。`

`复习一下git的使用，首先在码云或者github上注册自己的云端仓库。记住自己的账号密码。`

```
#首先去fork一下我的项目，就叫笔记
https://github.com/welblupen/notes
```

`然后去下载git工具，就可以将云端仓库的项目下载到本地，并多人协作编辑提交。`

```
#git 在这里下载 安装的时候一路确定就行
https://git-scm.com/downloads
```

`安装之后你可以在任何位置右键，就有gitbush  here的选项，进入最开始gitbook创建 mybook的目录，右键 进入git bush`

```
#首先配置自己本地仓库的用户名和邮箱
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
#如果是直接从远程克隆项目记住五个命令
#第一次从云端库克隆一份项目并在当前目录建立一个本地仓库并与云端关联
git clone https://github.com/welblupen/notes
#之后每次从云端下载并合并
git pull origin master
#自己写完文本之后把所写文档代码添加并提交到本地库
git add *
git commit -m "本次修改的内容"
#最后把本地仓库推送到云端库
git push origin master
#如果从零开始建立项目并推送到云端 需要先在项目目录建立本地库
git init "项目名"
#然后添加并提交所有代码到本地仓库
git add *
git commit -m "项目简单描述"
#然后连接git云端仓库
git remote add origin  git@github.com:welblupen/notes.git
#输入远程仓库的账号密码后 将本地库推送到远程仓库即可
git push -u origin master
```

`如果连接远程仓库访问被拒绝，则需要在自己电脑上生成ssh公钥`

```
https://blog.csdn.net/lw545034502/article/details/90696872
```

