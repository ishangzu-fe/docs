# 公寓管理平台 Electron 客户端

## 大纲
	- 安装
	- Git 分支介绍
	- 版本介绍
	- 版本号规则
	- 开发
	- 打包
		- 打包过程
	- 发布
	- 项目结构
	- 热更新
	- 与子系统之间的通讯
	- 参考
		- Electron

- - - -

## 安装
1. 拉取项目：
`git clone git@192.168.0.192:isz-pc/electron-client.git`
2. 安装依赖：
`npm i`
安装前最好设置淘宝源：`npm config set registry https://registry.npm.taobao.org/`
3. 拉取发布项目
`git clone https://gitee.com/ishangzu-fe/clients.git ./publish`

需要注意的是，electron-builder 下载相关依赖会遇到网络问题，相关信息参见：https://github.com/electron-userland/electron-builder/issues/1859

- - - -

## Git 分支介绍
项目分支采用 Gitflow 模型：
- master: 主分支，仅包括发布的版本
- dev: 开发分支
- feature-…

- - - -

## 版本介绍
项目根据不同环境分为三个版本：
- 线上版本：正式环境
- 测试版本：测试和预发环境
- 开发版本：供中后台开发者使用

需要注意的是：
1. 测试版本只运行在测试和预发环境中使用
2. 打包时也需区分版本，在 config 中通过 env 变量来区分
3. 发布时也许区分版本，通过 publish 项目的分支来区分：
	- 线上版本 -> master
	- 测试版本 -> test
	- 开发版本 -> dev

- - - -

## 版本号规则
项目版本号分为主版本号和内容版本号，分别指项目版本和热更新包版本。
可以通过 package.json 中 version 和 meta.contentVersion 两个字段来指定各自的版本号。
目前主版本号采用 semver 版本规则，而内容版本号与主版本号相同，只是将点 ‘.’ 去掉。例如：主版本号为 2.1.14 ，则内容版本号为 2114。
测试版本可以通过内容版本来区分，一般提测时会指定内容版本为 21140，若有更新，递增末位数字，例如 21141, 21142…

- - - -

## 开发
启动使用以下命令：
`npm run dev`

- - - -

## 打包
打包使用以下命令：
`npm run pack <version> <contentVersion>`
选项：
	- version: 版本号
	- contentVersion: 内容版本号
版本号规则请参考上文内容。

需要注意的是：
	1. 请按照提示完成每项任务
	2. Windows 版本打包过程必须在 windows（或虚拟机）中执行

#### 打包过程
打包过程主要分为以下几个步骤：
	1. 检查版本参数
	2. 检查工作目录是否都已经提交
	3. 确认环境配置，包括当前分支和发布的版本类型
	4. 确认版本号
	5. 更改版本号
	6. webpack 打包
	7. 生成 asar 文件
	8. 生成 windows 可执行文件
	9. 生成 macOS 可执行文件和安装包
	10. 根据提示创建 exe 安装包

- - - -

## 发布
发布使用以下命令：
`npm run publish`
发布命令帮你将打好的包移至发布目录 publish 中，完成后需执行以下命令确认发布：
`git push`

#### 发布过程
发布过程做了以下几件事情：
1. 将新的安装包移至目录下的 publish 下
2. 根据用户输入生成新的更新记录并写入文件中
3. 更新版本文件（用于客户端下载页显示的版本号）
4. 提交内容并打上标签

注意：确认生成的更新记录以及版本文件无误后再同步到远程仓库

- - - -

## 项目结构
![](%E5%85%AC%E5%AF%93%E7%AE%A1%E7%90%86%E5%B9%B3%E5%8F%B0%20Electron%20%E5%AE%A2%E6%88%B7%E7%AB%AF/5A063FD3-C6FF-4070-BE89-3B81AE4AA0B3.png)
主要包含以下目录：
- assets
资源目录，包括图标图片字体等。
注意，webview 预加载脚本放在 assets 目录底下的 script 目录中。
- bin
脚本目录，包括打包发布等脚本，以及 webpack 的配置。
- master
项目入口，项目从这里开始执行，主要包括热更新的实现。
- proc-main
主线程逻辑目录。
其中 hooks 目录中，每个 js 文件对应相应的生命周期执行逻辑。
其中 modules 目录，是封装的一些功能模块。
- proc-renderer
渲染线程逻辑目录。
其中 windows 目录包含应用的界面代码，分为 Login、panel、platform。
	* Login 包含登录界面的代码。
	* Panel 包含关于面板的代码。
	* Platform 包含平台界面的代码。
- publish
发布目录，发布打包好的应用。
包含三个分支，对应三个版本：
	- master
	- test
	- dev
发布对应版本时，切记切换至对应的分支。

- - - -

## 热更新
热更新采用了最常见的方案，简单来说，就是检查版本，如果有更新就从远程拉取新版本覆盖旧版本。
所以，热更新主要分为三个步骤：
	1. 检查更新
	2. 下载更新
	3. 替换文件
代码在以下文件中：
	1. 检查和下载的逻辑代码：proc-main/modules/update.js
	2. 界面代码：proc-renderer/windows/login/components/update.vue
	3. 替换文件的逻辑代码：master/update-local.js
此外，我们生成的更新包目前被托管在[ishangzu-fe/clients - 码云](http://git.oschina.net/ishangzu-fe/clients)，其中除了更新包，还有每次上线打好的新版本（供下载使用）。并且还有一个包含更新记录的文件 update.js ，包含每次更新的版本号和更新记录等，检查更新就是通过它来实现的。

下面讲讲每个步骤具体是怎么做的：
1. 检查更新
首先会向码云请求包含更新记录的文件，获取到最新的版本号与本地的 package.json 中的 meta.contentVersion 字段进行比对，如果不同，就视为有新的版本，这样可以很容易实现版本的回退。
更新记录还包括一个 entry 字段，代表是否包含入口更新。什么是入口更新？项目代码打包时会生成两个 bundle，一个是 master.asar，一个是 app.asar，app.asar 包括应用的主要代码，master.asar 只包含 master 目录下的代码（包含更新替换步骤的代码），master.asar 就被视为项目的入口。
普通更新只会更新 app.asar 文件，如果我们把 entry 字段设为 true，则代表需要更新 master.asar。
2. 下载更新
下载更新只是从码云下载了一个压缩包并解压，存放于项目的 AppData 目录下（可以通过 app.getPath(‘appData’) 方法来获取每个系统下默认的应用数据目录）。
下载完成后，会将更新包的 MD5 值和更新记录中的 MD5 值进行比对，防止下载包损坏的现象。
如果下载成功，会立即重启应用。如果包含入口更新，会先执行更新包中包含的更新脚本文件，利用它来更新 master.asar 文件，完成后会立即重启应用。
3. 替换文件
替换文件发生在项目的一开始。打开的时候会检查应用的 AppData 目录下是否包含更新包，如果有会再比对版本号，如果更新包的版本号与本地版本号不同，就会视为有更新。
替换文件时可能会出现需要权限的问题，不同的系统，我们请求权限的方案是不同的。在 Windows 下，我们利用 cmd+vb 来请求管理员权限；在 MacOS 下，我们利用了第三方模块 sudo-prompt 来实现。

- - - -

## 与子系统之间的通信机制
与子系统之间的通信可以分为：
	1. 父 -> 子
	2. 子 -> 父
	3. WebSocket
其中父指的是客户端，子指的是包括 erp 在内的所有子系统。子系统在客户端存在的方式是 webview 标签。webview 标签是一个独立的渲染器进程，所以与 webview 标签通信就是进程间通讯的实现。webview 介绍参考：[<webview>标签 | Electron](https://electronjs.org/docs/api/webview-tag)

1. 父 -> 子
客户端向子系统发送信息有这几种方式：
	* Cookie
	* webview.send
	* url

- webview.send
webview.send 通过 ipc 的方式向 webview 页面发送消息，具体方法参考：[<webview>标签 | Electron](https://electronjs.org/docs/api/webview-tag#webviewsendchannel-arg1-arg2-)。
而 webview 页面进程需要监听客户端发送的消息，可以通过 ipcRenderer.on 方法来实现。
这是最佳实践。
- Cookie
Cookie 的方式不必说，electron 对 cookie 的读写有完全的控制权，具体方法参考：[Cookies | Electron](https://electronjs.org/docs/api/cookies)。
注意，这种方式并不是响应式的，即子系统必须去主动地查看 cookie 是否发生改变。
- url
Webview 的 src 属性接受一个 url 代表页面的地址，我们可以通过 url 查询字符串来传递信息。注意，这种方式会使子系统刷新。

2. 子 -> 父
子系统向客户端发送信息有这几种方式：
	1. 协议请求
	2. sendHost()

3. WebSocket 与 IPC 的方式实现类似，不再赘述。

- - - -

## 参考
- Electron
	- [文档  | Electron](https://electronjs.org/docs)



