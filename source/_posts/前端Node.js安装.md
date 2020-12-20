---
title: Node.js安装
categories:
	一起前端喵喵叫
date: 2019-07-29 20:55:47
notshow: true
---

# 下载安装

		地址：https://nodejs.org/zh-cn/
		下载好后有一个文件：node-v10.16.0-x64.msi
		双击一直下一步就可以了。

# 检查是否安装成功
	
		node -v 查看 node 版本
		npm -v 查看 npm 版本

		安装成功后在安装目录下会有一个node_modules 目录

# 环境配置

	此处的环境配置主要配置的是 npm 安装的全局模块所在的路径，以及缓存cache的路径，之所以要配置，是因为以后在执行类似：npm install express [-g] （后面的可选参数-g，g代表global全局安装的意思）的安装语句时，会将安装的模块安装到【C:\Users\用户名\AppData\Roaming\npm】路径中，占C盘空间。

　　例如：我希望将全模块所在路径和缓存路径放在我node.js安装的文件夹中，则在安装目录下创建两个文件夹【node_global】及【node_cache】



1、设置全局目录和缓存目录，创建完两个空文件夹之后，打开cmd命令窗口，输入

　　npm config set prefix "D:\MySoftInstallHome\node\node_global"

　　npm config set cache "D:\MySoftInstallHome\node\node_cache"


   重新配置：A、删除【 C:\Users\用户\.npmrc 】文件重新生成。如果 .npmrc 不在这个目录下，就 C 盘全局搜一下；B、直接修改编译 .npmrc 文件。

2、设置环境变量，“我的电脑”-右键-“属性”-“高级系统设置”-“高级”-“环境变量”
* 进入环境变量对话框，在【系统变量】下新建【NODE_PATH】,输入【D:\MySoftInstallHome\node\node_modules】
* 将【用户变量】下的【Path】修改为【D:\MySoftInstallHome\node\node_global】

   另附上地址：https://www.cnblogs.com/xinaixia/p/8279015.html

# 测试安装模块

+ npm install -g express-generator

安装 express 模块

+ 配置完后，安装个module测试下，我们就安装最常用的express模块，打开cmd窗口，输入如下命令进行模块的全局安装：

+ npm install express -g # -g是全局安装的意思

	会发现在	node_global 文件夹生成express 文件和express.cmd

+ 使用express创建一个工程，输入命令：express helloworld
+ 转到 helloworld 目录下，命令：cd helloworld
+ 装载 node 包管理器，执行命令：npm install
+ 启动 helloworld，输入命令：npm start，如下图，新创建的 helloworld 已经运行在3000端口上
+ 在浏览器中输入地址：http://localhost:3000/，如下图，访问我们的第一个node web 网页。　　　