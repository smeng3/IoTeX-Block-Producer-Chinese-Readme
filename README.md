# IoTeX 全民节点竞选计划 — 如何部署


![MacDown logo](https://upload-images.jianshu.io/upload_images/15766012-4198f0aba2357a04.png)

###什么是IoTeX全民节点竞选？
IoTeX通过建立全民节点竞选机制，激励所有社区成员加入竞选和参与投票, 成为IoTeX生态的运营者，贡献者与利益共享者，共同维护IoTeX网络和推动社区发展。[原文链接](https://www.jianshu.com/p/5286298d3b27)

###为什么要竞选成为IoTeX全民节点？
IoTeX全民节点为网络的运营和生态的建设提供了宝贵的资源和服务，都将获得奖励。IoTeX预留了100亿通证供应总量中的12%进入IoTeX节点奖励池。 整个奖励池共由三部分组成，包括12亿IOTX通证、全部网络交易手续费(Gas)以及来自IoTeX基金会和社区的贡献/捐赠。[原文链接](https://www.jianshu.com/p/5286298d3b27)

##如何部署IoTeX节点？

###目录

&nbsp; [1. 安装运行环境](#1)

&nbsp; [2. 安装源文件](#2)

&nbsp; &nbsp; &nbsp; [2.1 下载代码](#2.1)

&nbsp; &nbsp; &nbsp; [2.2 使用 make 命令](#2.2)

&nbsp; &nbsp; &nbsp; [2.3 更新依赖(可选)](#2.3)

[3. 运行与测试](#3)

&nbsp; &nbsp; &nbsp; [3.1 Run Unit Tests (进行单元测试）](#3.1)

&nbsp; &nbsp; &nbsp; [3.2 Reboot (重启区块）](#3.2)

&nbsp; &nbsp; &nbsp; [3.3 Run (运行区块）](#3.3)

&nbsp; &nbsp; &nbsp; [3.4 Minicluster](#3.4)

&nbsp; &nbsp; &nbsp; [3.5 Deploy w/ Docker Image](#3.5)



	


<h2 id="1">1.安装运行环境</h2>


官方给出的环境指南里要求 Golang 在 1.11.5版本以上

| 环境语言  | 版本  | 描述 |
|:-------------:|:---------------:|:-------------:|
| Golang      | >= 1.11.5	 |The Go Programming Language |

[Golang](https://golang.org/dl/) 也叫做 Go语言, 是Google开发的一种静态强类型、编译型、并发型，并具有垃圾回收功能的编程语言。

在运行之前我们要安装go语言环境，这里也给出具体的安装流程:

 **Mac OS 操作系统** 可以点击 [这里](https://dl.google.com/go/go1.11.5.darwin-amd64.pkg) 下载安装

 **Win 操作系统** 可以点击   [这里] (https://dl.google.com/go/go1.11.5.windows-amd64.msi)下载安装

 **Linux 操作系统** 可以点击 [这里] (https://dl.google.com/go/go1.11.5.linux-amd64.tar.gz)下载安装

	具体安装流程也可参考go官网网站: https://golong.org

<h2 id="2">2.安装源文件</h2>

<h3 id="2.1">2.1下载代码</h3>

官方的代码文件由github托管保存，详情参阅: [https://github.com/iotexproject/iotex-core](https://github.com/iotexproject/iotex-core)

安装流程非常简单：

* 点开终端 ( Terminal)
* 输入如下命令

		mkdir -p ~/go/src/github.com/iotexproject
		cd ~/go/src/github.com/iotexproject
		git clone git@github.com:iotexproject/iotex-core.git
		cd iotex-core
**这里简单简单解释一下，mkdir 是新建一个文件夹，cd 命令是进入此文件夹，git clone 是将此文件下载**

下载完成后，这里我们要开始正式运行这个项目了



<h3 id="2.2">2.2 官方说明里指出，这个项目需要使用 `make` 命令 </h3>

如果您使用的跟我一样是 Mac OS 系统，请先下载安装 xcode 软件，并在安装时选择同时安装 Commend Line Tool

如已安装过或不记得是否有Commend Line Tool 

* 启动Xcode程序，打开Xcode菜单中的“Preferences...”菜单
* 点击到 Compontents 选项卡
* 点击“Command Line Tools”旁边的下载图标后等待下载，下载完毕并再进行安装
* 可以在 终端(Terminal）执行以下命令验证安装：
 			
		gcc --version
		whereis gcc
		whereis make

	正确安装后,部分返回结果如下：

		/user/bin/gcc	
		/user/bin/make


<h3 id="2.3">2.3 (可选)更新依赖 </h3>

如果需要更新依赖，可以自行安装 Go Dependency Management Tool :

**安装地址**：[https://github.com/golang/dep](https://github.com/golang/dep)

之后在 终端(Terminal）运行如下命令即可：

`dep ensure`

**注意**: 如果开发环境是 Ubuntu, 需要设置如下路径：
`LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$GOPATH/src/github.com/iotexproject/iotex-core/crypto/lib：$GOPATH/src/github.com/iotexproject/iotex-core/crypto/lib/blslib`


<h2 id="3">3.运行与测试</h2>


<h3 id="3.1">3.1 Run Unit Tests (进行单元测试） </h3>

在Terminal中，iotex-core 的文件夹下，输入并运行下方命令：

`make test`


<h3 id="3.2">3.2 Reboot (重启区块） </h3>

**官方说明里指出，可以从新的数据库中重启区块**

* 在终端(Terminal）里输入：

  `make reboot` 
  
* 观察到代码不断刷新，并有如下记录

		2018-08-28T09:54:02-07:00 |INFO| commit a block height=0 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:02-07:00 |INFO| Starting dispatcher iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:02-07:00 |INFO| Starting IotxConsensus scheme iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate scheme=STANDALONE
		2018-08-28T09:54:02-07:00 |INFO| start RPC server on 127.0.0.1:4689 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:02-07:00 |INFO| Starting Explorer JSON-RPC server on [::]:14004 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:03-07:00 |INFO| No peer exist to sync with. iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:03-07:00 |INFO| created a new block at="2018-08-28 09:54:03.210120086 -0700 PDT m=+1.047466065" iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:03-07:00 |INFO| created a new block height=1 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y length=1 networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:03-07:00 |INFO| commit a block height=1 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:04-07:00 |INFO| No peer exist to sync with. iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:04-07:00 |INFO| created a new block at="2018-08-28 09:54:04.213299491 -0700 PDT m=+2.050689454" iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:04-07:00 |INFO| created a new block height=2 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y length=1 networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T09:54:04-07:00 |INFO| commit a block height=2 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate


<h3 id="3.3">3.3 Run (运行区块） </h3>


**在已存在的数据库中重新启动区块链**

* 在终端(Terminal）里输入：
	`make run`
	
* 观察到代码不断刷新，并有如下记录

		2018-08-28T10:03:40-07:00 |INFO| Restarting blockchain blockchain height=3 factory height=3 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:40-07:00 |INFO| Starting dispatcher iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:40-07:00 |INFO| Starting IotxConsensus scheme iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate scheme=STANDALONE
		2018-08-28T10:03:40-07:00 |INFO| start RPC server on 127.0.0.1:4689 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:40-07:00 |INFO| Starting Explorer JSON-RPC server on [::]:14004 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:41-07:00 |INFO| created a new block at="2018-08-28 10:03:41.17804365 -0700 PDT m=+1.034361469" iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:41-07:00 |INFO| No peer exist to sync with. iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:41-07:00 |INFO| created a new block height=4 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y length=1 networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:41-07:00 |INFO| commit a block height=4 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:42-07:00 |INFO| No peer exist to sync with. iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:42-07:00 |INFO| created a new block at="2018-08-28 10:03:42.175542402 -0700 PDT m=+2.031857345" iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:42-07:00 |INFO| created a new block height=5 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y length=1 networkAddress=127.0.0.1:4689 nodeType=delegate
		2018-08-28T10:03:42-07:00 |INFO| commit a block height=5 iotexAddr=io1qyqsyqcy8uhx9jtdc2xp5wx7nxyq3xf4c3jmxknzkuej8y networkAddress=127.0.0.1:4689 nodeType=delegate


	**@注意事项**
	
	如提示 "error":"listen tcp :7788: bind: address already in use"：
   
   * control + z 退出当前运行界面
	
	* 可以运行如下命令，终止端口，重新运行

			lsof -i :778
			
		获得如下结果：
			
			COMMAND   PID     USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
			server  31014    user    5e   IPv6   0x1114edasfeasdf       0   TCP *:7788 (LISTEN)
		
		默默记录下 PID 的数值，如上结果为 31014, 则运行以下命令：
		
			sudo kill -9 31014


<h3 id="3.4">3.4 Minicluster </h3>

	
**官方说明中写道:** `make minicluster` runs a cluster of 4 delegate nodes with RollDPoS consensus scheme while actions are automatically injected to one of the nodes.

这里译为：

具体操作流程和上文相同

* 在终端(Terminal）里输入：
	`make minicluster `
	
* 观察到代码不断刷新，并有如下记录
		
		2018-10-18T14:23:18-07:00 |INFO| commit a block height=0
		2018-10-18T14:23:18-07:00 |INFO| Starting IotxConsensus scheme scheme=ROLLDPOS
		2018-10-18T14:23:18-07:00 |INFO| commit a block height=0
		2018-10-18T14:23:18-07:00 |INFO| Starting IotxConsensus scheme scheme=ROLLDPOS
		2018-10-18T14:23:18-07:00 |INFO| commit a block height=0
		2018-10-18T14:23:18-07:00 |INFO| Starting IotxConsensus scheme scheme=ROLLDPOS
		2018-10-18T14:23:18-07:00 |INFO| commit a block height=0
		2018-10-18T14:23:18-07:00 |INFO| Starting IotxConsensus scheme scheme=ROLLDPOS
		2018-10-18T14:23:18-07:00 |INFO| Starting Explorer JSON-RPC server on [::]:14004
		2018-10-18T14:23:18-07:00 |INFO| Starting dispatcher
		2018-10-18T14:23:18-07:00 |INFO| Starting Explorer JSON-RPC server on [::]:14006
		2018-10-18T14:23:18-07:00 |INFO| Starting dispatcher
		2018-10-18T14:23:18-07:00 |INFO| Starting Explorer JSON-RPC server on [::]:14005
		2018-10-18T14:23:18-07:00 |INFO| Starting dispatcher
		2018-10-18T14:23:18-07:00 |INFO| start RPC server on 127.0.0.1:4689
		2018-10-18T14:23:18-07:00 |INFO| start RPC server on 127.0.0.1:4691
		2018-10-18T14:23:18-07:00 |INFO| start RPC server on 127.0.0.1:4690
		2018-10-18T14:23:18-07:00 |INFO| Starting Explorer JSON-RPC server on [::]:14007
		2018-10-18T14:23:18-07:00 |INFO| Starting dispatcher
		2018-10-18T14:23:18-07:00 |INFO| start RPC server on 127.0.0.1:4692


<h3 id="3.5">3.5 Deploy w/ Docker Image </h3>

`make docker` 



