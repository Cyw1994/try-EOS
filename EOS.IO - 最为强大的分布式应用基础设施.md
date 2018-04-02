## EOS.IO - 最为强大的分布式应用基础设施

欢迎查看EOS.IO开源代码！EOS.IO提供给开发人员一个能够创建和部署具有高性能、横向可扩展的区块链基础架构，并在此之上进行分布式应用的开发。

源代码目前处于测试阶段但正在快速发展。也就是说，前期的开发者可以维护一个私有节点对网络进行验证亦或是开发一款分布式应用（智能合约）。

按照[Wiki](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public)中的描述测试网络正运行在`dawn-2.x`分叉，而`master`分叉将不再与公共的测试网络兼容。以下是通过`master`分叉来构建本地测试网络的操作说明。文档将在随后版本更新关于在`dawn-3.x`公共测试网络的下运行的说明。

### 支持的操作系统

EOS.IO现支持的操作系统如下：

1. Amazon 2017.09 and higher.  
2. Centos 7.  
3. Fedora 25 and higher (Fedora 27 recommended).  
4. Mint 18.  
5. Ubuntu 16.04 (Ubuntu 16.10 recommended).  
6. MacOS Darwin 10.12 and higher (MacOS 10.13.x recommended).  

## Resources 

1. [EOS.IO主页](https://eos.io)
2. [相关文档](https://eosio.github.io/eos/)
3. [博客](https://steemit.com/@eosio)
4. [社区电报群](https://t.me/EOSProject)
5. [开发者电报群](https://t.me/joinchat/EaEnSUPktgfoI-XPfMYtcQ)
6. [白皮书](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md)
7. [路线图](https://github.com/EOSIO/Documentation/blob/master/Roadmap.md)
8. [维基](https://github.com/EOSIO/eos/wiki)

## 目录

1. [入门手册](#入门手册)

2. [开发环境搭建](#setup)
   1. [脚本自动创建](#autobuild)
      1. [本地测试网络在Linux (Amazon, Centos, Fedora, Mint, & Ubuntu) 系统下的安装](#autoubuntulocal)
      2. [公共测试网络在(Amazon, Centos, Fedora, Mint, & Ubuntu) 体统下的安装](#autoubuntupublic)
      3. [MacOS系统下的本地测试网咯](#automaclocal)
      4. [MacOS系统下的公共测试网络](#automacpublic)

3. [创建EOS项目并运行节点](#runanode)
   1. [获取代码](#getcode)
   2. [由源代码创建](#build)
   3. [创建并启动单节点测试网络](#singlenode)
   4. [剩余步骤](#nextsteps)

4. [范例： Currency 智能合约演练](#smartcontracts)
   1. [智能合约范例](#smartcontractexample)
   2. [设置钱包并导入用户密钥](#walletimport)
   3. [为你的合约创建用户](#createaccounts)
   4. [将合约上传至区块链](#uploadsmartcontract)
   5. [向合约发送消息](#pushamessage)
   6. [查看合约余额](#readingcontract)

5. [执行本地测试网络](#localtestnet)

6. [将节点连接到公共测试网络](#publictestnet)

7. [Doxygen文档](#doxygen)

8. [通过Docker搭建EOS](#docker)

9. [手动安装各依赖项](#manualdep)
   1. [Amazon 2017.09或更高版本下的安装](#manualdepamazon)
   2. [Centos 7或更高版本下的安装](#manualdepcentos)
   3. [Fedora 25或更高版本下的安装](#manualdepfedora)
   4. [Mint 18下的安装](#manualdepubuntu)
   5. [Ubuntu 16下的安装](#manualdepubuntu)
   6. [MacOS Sierra 10.12或更高版本下的安装](#manualdepmacos)

   <a name="gettingstarted"></a>

## 入门手册

下面的介绍包括有软件的下载与安装、运行一个产生区块的简单测试网络、创建账户以及向区块链上传一个简单合约。

<a name="setup"></a>

## 开发环境

<a name="autobuild"></a>

#### 自动安装

支持的操作系统：

1. Amazon 2017.09 and higher.  
2. Centos 7.  
3. Fedora 25 and higher (Fedora 27 recommended).  
4. Mint 18.  
5. Ubuntu 16.04 (Ubuntu 16.10 recommended).  
6. MacOS Darwin 10.12 and higher (MacOS 10.13.x recommended).  

Amazon, Centos, Fedora, Mint, Ubuntu, & MacOS操作系统可通过自动构建脚本直接安装所有依赖项并搭建EOS环境。我们正努力在未来的新版本中支持更多的Linux/Unix发行版。

根据选择建立本地测试网络或是接入公共测试网络，跳转到下面的对应部分。按照指示克隆EOS源文件并运行位于根`eos`文件夹中的`eosio_build.sh`。

**⚠ 截至2018年2月, `master` 分叉承载了大量开发任务并现今已不再适合进行试验。⚠**

我们强烈建议您按照说明构建适用于[Linux](#autoubuntupublic) 或 [Mac OS X](#automacpublic)的公共测试网络。在我们重构`master`分支时，它已经支离破碎。本忠告会在`master`再次启用时移除，请耐心等候。

<a name="autoubuntulocal"></a>

#### 在Linux (Amazon, Centos, Fedora, Mint, & Ubuntu)下构建本地测试网络

克隆`eos`源文件并运行安装指令

```bash
git clone https://github.com/eosio/eos --recursive
cd eos
./eosio_build.sh
```

运行eosio_build.sh将把内容存放至`build`文件内。关键的执行文件（nodeos，cleos等）存放在`build/programs`文件内。

此外，可以针对您的构建可选择的运行一组测试来执行一些基本验证。

```bash
cd build
make test
```

为了便于合约开发，通过使用`make install`将目标内容安装至`user.local`文件夹。这一步在`build`文件夹目录执行。

若未在`build`文件夹目录下

```bash
cd build
```

执行`make install`

```bash
sudo make install
```

现在你可以进行下一步了—— [创建并启动单节点测试网络](#singlenode)

<a name="autoubuntupublic"></a>

#### 在Linux (Amazon, Centos, Fedora, Mint, & Ubuntu)下构建公共测试网络

`master`分叉将不再兼容`dawn-2.x`版本的公共测试网络。运行公共测试网络请参照[DAWN-2018-02-14/eos/README.md](https://github.com/EOSIO/eos/blob/DAWN-2018-02-14/README.md)

<a name="automaclocal"></a>

#### MacOS下创建本地测试网络

在运行安装指令前请确认你已安装/下载`XCode`。注意：如果系统未曾安装`homebrew`，安装指令会自动将其安装。了解[Homebrew Website](https://brew.sh)。

克隆`eos`源文件并运行安装指令

```bash
git clone https://github.com/eosio/eos --recursive
cd eos
./eosio_build.sh
```

运行eosio_build.sh将把内容存放至`build`文件内。关键的执行文件（nodeos，cleos等）存放在`build/programs`文件内。

此外，可以针对您的构建可选择的运行一组测试来执行一些基本验证。

```bash
cd build
make test
```

为了便于合约开发，通过使用`make install`将目标内容安装至`user.local`文件夹。这一步在`build`文件夹目录执行。

若未在`build`文件夹目录下

```bash
cd build
```

执行`make install`

```bash
sudo make install
```

现在你可以进行下一步了—— [创建并启动单节点测试网络](#singlenode)

<a name="automacpublic"></a>

#### MacOS下创建公共测试网络

`master`分叉将不再兼容`dawn-2.x`版本的公共测试网络。运行公共测试网络请参照[DAWN-2018-02-14/eos/README.md](https://github.com/EOSIO/eos/blob/DAWN-2018-02-14/README.md)

<a name="runanode"></a>

## 构建EOS并运行一个节点

<a name="getcode"></a>

获取源码

下载所有源码，EOS源文件或是部分子模块，最简单的方法是执行`git clone --recursive`：

```bash
git clone https://github.com/eosio/eos --recursive
```

如果使用repo而克隆指令中缺少`--recursive`标识，则可以通过在repo内运行以下命令来检索子模块：

```bash
git submodule update --init --recursive
```

<a name="build"></a>

### 通过源码构建

```bash
cd ~
git clone https://github.com/eosio/eos --recursive
mkdir -p ~/eos/build && cd ~/eos/build
cmake -DBINARYEN_BIN=~/binaryen/bin -DWASM_ROOT=~/wasm-compiler/llvm -
DOPENSSL_ROOT_DIR=/usr/local/opt/openssl -DOPENSSL_LIBRARIES=/usr/local/opt/openssl/lib ..
make -j$( nproc )
```

源代码构建同样支持。需要在编译器中覆盖clang的默认选项，请将这些标志添加到CMake命令中：

```
-DCMAKE_CXX_COMPILER=/path/to/c++ -DCMAKE_C_COMPILER=/path/to/cc
```

对于调试版本，添加`-DCMAKE_BUILD_TYPE=Debug`指令。其他常见的构建模型还有`Release` 和`RelWithDebInfo`。

在创建后运行测试插件，运行`test`目录下的`chain_test`程序。

EOS附带了大量的可执行程序，您可在`~/eos/build/programs`目录下找到。包括：

- nodeos - server-side blockchain node component
- cleos - command line interface to interact with the blockchain
- eosiowd - EOS wallet
- eosio-launcher - application for nodes network composing and deployment; [more on eosio-launcher](https://github.com/EOSIO/eos/blob/master/testnet.md)

<a name="singlenode"></a>

### 创建并启动单节点测试网络

成功创建项目后，`nodeos`二进制文件将出现在`build/programs/nodeos` 文件夹中。可以通过`build`文件夹内的`programs/nodeos/nodeos`直接运行`nodeos`。这里的指令假设条件是在`build`目录下执行。

默认的，`nodeos`将`etc/eosio/node_00`作为其配置文件。构建过程会在此文件夹内寻找默认的`genesis.json`文件。此外，可以通过 `--config-dir` 指令来指定配置文件夹并列出`nodeos`相关参数。如果您使用此选项，则需要手动将`genesis.json`文件复制到新选择的配置文件夹中。

`nodeos`需要正确的配置`config.ini`文件来确保执行有意义的工作。启动时，`nodeos`会在`config`文件中查找`config.ini`。如果配置文件不存在，则会创建一个默认的`config.ini`。若你还没有准备好`config.ini`文件，执行`nodeos`并立即使用<kbd>Ctrl-C</kbd>关闭。一个默认的配置（`config.ini`）将被创建在文件目录中。编辑该`config.ini`文件，根据你的需求加入或更新以下配置信息：

```
# Load the testnet genesis state, which creates some initial block producers with the default key
genesis-json = /path/to/eos/source/genesis.json
 # Enable production on a stale chain, since a single-node test chain is pretty much always stale
enable-stale-production = true
# Enable block production with the testnet producers
producer-name = eosio
# Load the block producer plugin, so you can produce blocks
plugin = eosio::producer_plugin
# Wallet plugin
plugin = eosio::wallet_api_plugin
# As well as API and HTTP plugins
plugin = eosio::chain_api_plugin
plugin = eosio::http_plugin
```

至此，`nodes`配置完毕，你将可以看到它的正常运行并开始产生新的区块。

当运行`nodeos`时，你应该会收到如下的日志信息。它意味着区块已成功创建。

```
1575001ms thread-0   chain_controller.cpp:235      _push_block          ] initm #1 @2017-09-04T04:26:15  | 0 trx, 0 pending, exectime_ms=0
1575001ms thread-0   producer_plugin.cpp:207       block_production_loo ] initm generated block #1 @ 2017-09-04T04:26:15 with 0 trxs  0 pending
1578001ms thread-0   chain_controller.cpp:235      _push_block          ] initc #2 @2017-09-04T04:26:18  | 0 trx, 0 pending, exectime_ms=0
1578001ms thread-0   producer_plugin.cpp:207       block_production_loo ] initc generated block #2 @ 2017-09-04T04:26:18 with 0 trxs  0 pending
...
```

默认情况，`nodeos`使用 `var/lib/eosio/node_00` 作为其数据目录（共享内存和日志信息均存放于此）。同样，你可以根据个人设定，通过使用 `--data-dir`命令来指定一个`nodeos`数据目录。

<a name="nextsteps"></a>

### 剩余步骤

更多的文档可以在[wiki](https://github.com/EOSIO/eos/wiki)上找到。维基主页上包括了上述程序、工具的详细相关文档，数据库模式以及API接口。维基同时包含了一个关于描述智能合约开发的章节，拥有一个简单的“货币”合约演练范例。

<a name="smartcontracts"></a>

## “货币”合约演练

EOS附带的智能合约范例可用于上传（至区块链）与执行来达到测试目的。接下来我们演示一下如何上传该“货币”合约并与其达成交互。

<a name="smartcontractexample"></a>

### 智能合约范例

首先，执行：

```bash
cd ~/eos/build/programs/nodeos/
./nodeos
```

<a name="walletimport"></a>

### 设置钱包并导入用户密钥

由于在`config.in`中配置了 `plugin = eosio::wallet_api_plugin` ，EOS钱包将作为`nodeos`程序的一部分运行。每份合约都需要一个关联账户，所以首先需要创建一个钱包。

```bash
cd ~/eos/build/programs/cleos/
./cleos wallet create # Outputs a password that you need to save to be able to lock/unlock the wallet
```

为了达到演练目的，导入`eosio`帐户的私钥，这是一个包含在`genesis.json`中的系统帐户，以便您能够根据现有帐户的权限发布API命令。下面引用的私钥在`config.ini`中能够找到并提供给您用于测试目的。

```
./cleos wallet import 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

<a name="createaccounts"></a>

### 为“货币”合约创立账户

首先，创建一些公钥/私钥对，在接下来的步骤中密钥对被分配为`owner_key`和`active_key`。

```bash
cd ~/eos/build/programs/cleos/
./cleos create key # owner_key
./cleos create key # active_key
```

按照上面输入得到两组公钥/私钥对作为输出

```
Private key: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Public key: EOSXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

**重点：**

保存好你的密钥对！

区分开`crate`与`create key`：`create`指令，其中`eosio`是授权创建货币帐户的帐户，而`PUBLIC_KEY_1`和`PUBLIC_KEY_2`是由`create key`命令生成的值。

```bash
./cleos create account eosio currency PUBLIC_KEY_1 PUBLIC_KEY_2
```

随后您应该返回一个JSON响应，并返回一个事务ID，确认它已成功执行。

继续，检查账户是否成功创建：

```bash
./cleos get account currency
```

如果正常运行，你将获得类似下面的返回值：

```json
{
  "account_name": "currency",
  "eos_balance": "0.0000 EOS",
  "staked_balance": "0.0001 EOS",
  "unstaking_balance": "0.0000 EOS",
  "last_unstaking_time": "2035-10-29T06:32:22",
...
```

此时，导入之前钱包创建的处于活跃状态的`private key`：

```bash
./cleos wallet import XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

<a name="uploadsmartcontract"></a>

### 将"货币"合约上传至区块链

上传之前，请先确认区块上并未有合约存在：

```bash
./cleos get code currency
code hash: 0000000000000000000000000000000000000000000000000000000000000000
```

通过之前为合约创建的账户，上传一个合约范例：

```bash
./cleos set contract currency ../../contracts/currency/currency.wast ../../contracts/currency/currency.abi
```

若收到一个含有`transaction_id`字段的JSON返回，那么恭喜你的智能合约已成功上传！

您也可以使用以下命令验证代码是否已设置：

```bash
./cleos get code currency
```

返回值大致如下：

```bash
code hash: 9b9db1a7940503a88535517049e64467a6e8f4e9e03af15e9968ec89dd794975
```

在使用“货币”合约前，你必须要分发你的“货币”：

```bash
./cleos push action currency issue '{"to":"currency","quantity":"1000.0000 CUR","memo":""}' --permission currency@active
```

接下来验证"货币”合约是否具有适当的初始余额：

```bash
./cleos get table currency currency account
{
  "rows": [{
     "currency": 1381319428,
     "balance": 10000000
     }
  ],
  "more": false
}
```

<a name="pushamessage"></a>

### 用“货币”合约实现资金转移

任何人都可以随时向任何合约发送任何消息，但部分请求可能缺少一些必要的许可信息，而遭到合约的拒绝接收。消息不再是“来自（from）”任何账户，而是“获得xx的许可下（with permission of）”，"xx"可以是一个或多个账户或者是权限等级（permission levels）。以下命令显示发送给“货币”合约的“转账”消息。

消息内容包括：`'{"from":"currency","to":"eosio","quantity":"20.0000 CUR","memo":"any string"}'`。从中我们可以看出，合约将资金从自身转移给其他人，这样的做法需要获得“货币”合约的许可：

```bash
./cleos push action currency transfer '{"from":"currency","to":"eosio","quantity":"20.0000 CUR","memo":"my first transfer"}' --permission currency@active
```

下面是一个泛化，显示`currency`账户仅被引用一次，以指定将`transfer`消息传递给哪个合约。

```bash
./cleos push action currency transfer '{"from":"${usera}","to":"${userb}","quantity":"20.0000 CUR","memo":""}' --permission ${usera}@active
```

作为交易成功提交的事务确认，您将收到包含`transaction_id` 字段的JSON输出。

<a name="readingcontract"></a>

### 读取范例“货币”合约余额

因此，首先检查前一个交易涉及的两个账户的状态：

```bash
./cleos get table eosio currency account
{
  "rows": [{
      "currency": 1381319428,
      "balance": 200000
       }
    ],
  "more": false
}
./cleos get table currency currency account
{
  "rows": [{
      "currency": 1381319428,
      "balance": 9800000
    }
  ],
  "more": false
}
```

和预期一样，接收账户`eosio`现在有`20 tokens`，而发送方较其最初的供应量少了`20 tokens`。

<a name="localtestnet"></a>

## 在本地测试网络中运行多个节点

你可以通过执行在`~/eos/build/programs/eosio-launcher` 目录下的`eosio-launcher`程序来运行测试网络。

出于测试目的，你将运行两个本地生产节点来彼此交互：

```bash
cd ~/eos/build
cp ../genesis.json ./
./programs/eosio-launcher/eosio-launcher -p2 --skip-signature
```

该指令会产生两个数据文件夹来对应每一个节点：`tn_data_00`和`tn_data_01`。

你会得到以下返回：

```bash
spawning child, programs/nodeos/nodeos --skip-transaction-signatures --data-dir tn_data_0
spawning child, programs/nodeos/nodeos --skip-transaction-signatures --data-dir tn_data_1
```

为了确认节点正常运行，执行以下`cleos`命令行：

```bash
~/eos/build/programs/cleos
./cleos -p 8888 get info
./cleos -p 8889 get info
```

对于每条命令，你应该获得带有区块链信息的JSON响应。

[这里](https://github.com/EOSIO/eos/blob/master/testnet.md)你了解更多关于`eosio-launcher`信息及其设置。

<a name="publictestnet"></a>

## 将节点连接到公共测试网络

想让本地节点连接至公共的测试网络，由`block.one`操作，提供了如下指令：

```bash
cd ~/eos/build/scripts
./start_npnode.sh
```

该命令将使用为名为`testnet_np`的实例提供的数据文件夹。

你应该能获得如下反馈：

```bash
Launched eosd.
See testnet_np/stderr.txt for eosd output.
Synching requires at least 8 minutes, depending on network conditions.
```

为了确认eosd操作以及同步：

```bash
tail -F testnet_np/stderr.txt
```

退出日志查看，使用Ctrl-C。在同步期间，您将看到类似于以下内容的日志消息：

```bash
3439731ms            chain_plugin.cpp:272          accept_block         ] Syncing Blockchain --- Got block: #200000 time: 2017-12-09T07:56:32 producer: initu
3454532ms            chain_plugin.cpp:272          accept_block         ] Syncing Blockchain --- Got block: #210000 time: 2017-12-09T13:29:52 producer: initc
```

当出现如下日志信息，则表明同步完成：

```bash
42467ms            net_plugin.cpp:1245           start_sync           ] Catching up with chain, our last req is 351734, theirs is 351962 peer ip-10-160-11-116:9876
42792ms            chain_controller.cpp:208      _push_block          ] initt #351947 @2017-12-12T22:59:44  | 0 trx, 0 pending, exectime_ms=0
42793ms            chain_controller.cpp:208      _push_block          ] inito #351948 @2017-12-12T22:59:46  | 0 trx, 0 pending, exectime_ms=0
42793ms            chain_controller.cpp:208      _push_block          ] initd #351949 @2017-12-12T22:59:48  | 0 trx, 0 pending, exectime_ms=0
```

此eosd实例在127.0.0.1:8888上侦听http请求，在端口9877的所有接口上侦听p2p请求，同时也包括的钱包插件。

<a name="doxygen"></a>

## Doxygen文档

您可以在Doxygen参考中找到更详细的API文档。

关于`master`分叉：https://eosio.github.io/eos/  

关于公共测试网络分叉： http://htmlpreview.github.io/?https://github.com/EOSIO/eos/blob/dawn-2.x/docs/index.html  

<a name="docker"></a>

## 通过Docker搭建EOS

您可以在[Docker Readme](https://github.com/EOSIO/eos/blob/master/Docker/README.md)中找到有关EOS Docker的最新信息。

<a name="manualdep"></a>

## 手动安装各依赖项

如果您更愿意手动构建依赖项，请按照以下步骤操作：

这个项目主要用C ++ 14编写，并使用CMake作为其构建系统。 推荐使用最新的Clang和最新版本的CMake。

依赖项：

- Clang 4.0.0
- CMake 3.5.1
- Boost 1.66
- OpenSSL
- LLVM 4.0
- [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)

<a name="manualdepamazon"></a>

### Amazon 2017.09或更高版本下的安装

安装开发工具包：

```bash
sudo yum update
sudo yum install git gcc72.x86_64 gcc72-c++.x86_64 autoconf automake libtool make bzip2 \
				 bzip2-devel.x86_64 openssl-devel.x86_64 gmp.x86_64 gmp-devel.x86_64 \
				 libstdc++72.x86_64 python36-devel.x86_64 libedit-devel.x86_64 \
				 ncurses-devel.x86_64 swig.x86_64 gettext-devel.x86_64
```

安装CMake 3.10.2：

```bash
cd ~
curl -L -O https://cmake.org/files/v3.10/cmake-3.10.2.tar.gz
tar xf cmake-3.10.2.tar.gz
rm -f cmake-3.10.2.tar.gz
ln -s cmake-3.10.2/ cmake
cd cmake
./bootstrap
make
sudo make install
```

安装Boost 1.66：

```bash
cd ~
curl -L https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.bz2 > boost_1.66.0.tar.bz2
tar xf boost_1.66.0.tar.bz2
echo "export BOOST_ROOT=$HOME/boost_1_66_0" >> ~/.bash_profile
source ~/.bash_profile
cd boost_1_66_0/
./bootstrap.sh "--prefix=$BOOST_ROOT"
./b2 install
```

安装[MongoDB (mongodb.org)](https://www.mongodb.com)：

```bash
mkdir ${HOME}/opt
cd ${HOME}/opt
curl -OL https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-amazon-3.6.3.tgz
tar xf mongodb-linux-x86_64-amazon-3.6.3.tgz
rm -f mongodb-linux-x86_64-amazon-3.6.3.tgz
ln -s ${HOME}/opt/mongodb-linux-x86_64-amazon-3.6.3/ ${HOME}/opt/mongodb
mkdir ${HOME}/opt/mongodb/data
mkdir ${HOME}/opt/mongodb/log
touch ${HOME}/opt/mongodb/log/mongod.log
		
tee > /dev/null ${HOME}/opt/mongodb/mongod.conf <<mongodconf
systemLog:
 destination: file
 path: ${HOME}/opt/mongodb/log/mongod.log
 logAppend: true
 logRotate: reopen
net:
 bindIp: 127.0.0.1,::1
 ipv6: true
storage:
 dbPath: ${HOME}/opt/mongodb/data
mongodconf

export PATH=${HOME}/opt/mongodb/bin:$PATH
mongod -f ${HOME}/opt/mongodb/mongod.conf
```

安装[mongo-cxx-driver (release/stable)](https://github.com/mongodb/mongo-cxx-driver)：

```bash
cd ~
curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.9.3/mongo-c-driver-1.9.3.tar.gz
tar xf mongo-c-driver-1.9.3.tar.gz
cd mongo-c-driver-1.9.3
./configure --enable-static --enable-ssl=openssl --disable-automatic-init-and-cleanup --prefix=/usr/local
make -j$( nproc )
sudo make install
git clone https://github.com/mongodb/mongo-cxx-driver.git --branch releases/stable --depth 1
cd mongo-cxx-driver/build
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..
sudo make -j$( nproc )
```

安装 [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)：

```bash
cd ~
git clone https://github.com/cryptonomex/secp256k1-zkp.git
cd secp256k1-zkp
./autogen.sh
./configure
make -j$( nproc )
sudo make install
```

默认情况下，LLVM和clang不包含WASM构建目标，因此您必须自己构建它：

```bash
mkdir  ~/wasm-compiler
cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd ..
mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
make -j$( nproc ) 
make install
```

至此，开发环境已搭建完毕。 现在可以开始 <a href="#runanode">构建EOS并运行一个节点了</a>。

<a name="manualdepcentos"></a>。

### Centos 7或更高版本下的安装

安装开发工具包：

- 在Centos上安装需要安装/启用[Centos SCL(Centos Software CollectionsRepository)](https://wiki.centos.org/AdditionalResources/Repositories/SCL):

```bash
sudo yum --enablerepo=extras install centos-release-scl
sudo yum update
sudo yum install -y devtoolset-7
scl enable devtoolset-7 bash
sudo yum install -y python33.x86_64
scl enable python33 bash
sudo yum install git autoconf automake libtool make bzip2 \
				 bzip2-devel.x86_64 openssl-devel.x86_64 gmp-devel.x86_64 \
				 ocaml.x86_64 doxygen libicu-devel.x86_64 python-devel.x86_64 \
				 gettext-devel.x86_64

```

安装CMake 3.10.2：

```bash
cd ~
curl -L -O https://cmake.org/files/v3.10/cmake-3.10.2.tar.gz
tar xf cmake-3.10.2.tar.gz
cd cmake-3.10.2
./bootstrap
make -j$( nproc )
sudo make install
```

安装 Boost 1.66：

```bash
cd ~
curl -L https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.bz2 > boost_1.66.0.tar.bz2
tar xf boost_1.66.0.tar.bz2
echo "export BOOST_ROOT=$HOME/boost_1_66_0" >> ~/.bash_profile
source ~/.bash_profile
cd boost_1_66_0/
./bootstrap.sh "--prefix=$BOOST_ROOT"
./b2 install
```

安装 [MongoDB (mongodb.org)](https://www.mongodb.com)：

```bash
mkdir ${HOME}/opt
cd ${HOME}/opt
curl -OL https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-amazon-3.6.3.tgz
tar xf mongodb-linux-x86_64-amazon-3.6.3.tgz
rm -f mongodb-linux-x86_64-amazon-3.6.3.tgz
ln -s ${HOME}/opt/mongodb-linux-x86_64-amazon-3.6.3/ ${HOME}/opt/mongodb
mkdir ${HOME}/opt/mongodb/data
mkdir ${HOME}/opt/mongodb/log
touch ${HOME}/opt/mongodb/log/mongod.log
		
tee > /dev/null ${HOME}/opt/mongodb/mongod.conf <<mongodconf
systemLog:
 destination: file
 path: ${HOME}/opt/mongodb/log/mongod.log
 logAppend: true
 logRotate: reopen
net:
 bindIp: 127.0.0.1,::1
 ipv6: true
storage:
 dbPath: ${HOME}/opt/mongodb/data
mongodconf

export PATH=${HOME}/opt/mongodb/bin:$PATH
mongod -f ${HOME}/opt/mongodb/mongod.conf
```

安装 [mongo-cxx-driver (release/stable)](https://github.com/mongodb/mongo-cxx-driver)：

```bash
cd ~
curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.9.3/mongo-c-driver-1.9.3.tar.gz
tar xf mongo-c-driver-1.9.3.tar.gz
cd mongo-c-driver-1.9.3
./configure --enable-static --enable-ssl=openssl --disable-automatic-init-and-cleanup --prefix=/usr/local
make -j$( nproc )
sudo make install
git clone https://github.com/mongodb/mongo-cxx-driver.git --branch releases/stable --depth 1
cd mongo-cxx-driver/build
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..
sudo make -j$( nproc )
```

安装[secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git):

```bash
cd ~
git clone https://github.com/cryptonomex/secp256k1-zkp.git
cd secp256k1-zkp
./autogen.sh
./configure
make -j$( nproc )
sudo make install
```

默认情况下，LLVM和clang不包含WASM构建目标，因此您必须自己构建它：

```bash
mkdir  ~/wasm-compiler
cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd ..
mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly 
-DLLVM_ENABLE_RTTI=1 -DCMAKE_BUILD_TYPE=Release ../
make -j$( nproc ) 
make install
```

至此，开发环境已搭建完毕。 现在可以开始 <a href="#runanode">构建EOS并运行一个节点了</a>。

<a name="manualdepfedora"></a>

### Fedora 25或更高版本下的安装

安装开发工具包：

```bash
sudo yum update
sudo yum install git gcc.x86_64 gcc-c++.x86_64 autoconf automake libtool make cmake.x86_64 \
				 bzip2-devel.x86_64 openssl-devel.x86_64 gmp-devel.x86_64 \
				 libstdc++-devel.x86_64 python3-devel.x86_64 libedit.x86_64 \
				 mongodb.x86_64 mongodb-server.x86_64 ncurses-devel.x86_64 \
				 swig.x86_64 gettext-devel.x86_64

```

安装 Boost 1.66：

```bash
cd ~
curl -L https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.bz2 > boost_1.66.0.tar.bz2
tar xf boost_1.66.0.tar.bz2
echo "export BOOST_ROOT=$HOME/boost_1_66_0" >> ~/.bash_profile
source ~/.bash_profile
cd boost_1_66_0/
./bootstrap.sh "--prefix=$BOOST_ROOT"
./b2 install
```

安装 [mongo-cxx-driver (release/stable)](https://github.com/mongodb/mongo-cxx-driver)：

```bash
cd ~
curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.9.3/mongo-c-driver-1.9.3.tar.gz
tar xf mongo-c-driver-1.9.3.tar.gz
cd mongo-c-driver-1.9.3
./configure --enable-static --enable-ssl=openssl --disable-automatic-init-and-cleanup --prefix=/usr/local
make -j$( nproc )
sudo make install
git clone https://github.com/mongodb/mongo-cxx-driver.git --branch releases/stable --depth 1
cd mongo-cxx-driver/build
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..
sudo make -j$( nproc )
```

安装 [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)：

```bash
cd ~
git clone https://github.com/cryptonomex/secp256k1-zkp.git
cd secp256k1-zkp
./autogen.sh
./configure
make -j$( nproc )
sudo make install
```

默认情况下，LLVM和clang不包含WASM构建目标，因此您必须自己构建它：

```bash
mkdir  ~/wasm-compiler
cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd ..
mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
make -j$( nproc ) install
```

至此，开发环境已搭建完毕。 现在可以开始 <a href="#runanode">构建EOS并运行一个节点了</a>。

<a name="manualdepubuntu"></a>

### Ubuntu 16.04 & Linux Mint 18下的安装

安装开发工具包：

```bash
sudo apt-get update
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
sudo apt-get install clang-4.0 lldb-4.0 libclang-4.0-dev cmake make \
                     libbz2-dev libssl-dev libgmp3-dev \
                     autotools-dev build-essential \
                     libbz2-dev libicu-dev python-dev \
                     autoconf libtool git mongodb
```

安装 Boost 1.66：

```bash
cd ~
wget -c 'https://sourceforge.net/projects/boost/files/boost/1.66.0/boost_1_66_0.tar.bz2/download' -O boost_1.66.0.tar.bz2
tar xjf boost_1.66.0.tar.bz2
cd boost_1_66_0/
echo "export BOOST_ROOT=$HOME/boost_1_66_0" >> ~/.bash_profile
source ~/.bash_profile
./bootstrap.sh "--prefix=$BOOST_ROOT"
./b2 install
source ~/.bash_profile
```

安装 [mongo-cxx-driver (release/stable)](https://github.com/mongodb/mongo-cxx-driver)：

```bash
cd ~
curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.9.3/mongo-c-driver-1.9.3.tar.gz
tar xf mongo-c-driver-1.9.3.tar.gz
cd mongo-c-driver-1.9.3
./configure --enable-static --enable-ssl=openssl --disable-automatic-init-and-cleanup --prefix=/usr/local
make -j$( nproc )
sudo make install
git clone https://github.com/mongodb/mongo-cxx-driver.git --branch releases/stable --depth 1
cd mongo-cxx-driver/build
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..
sudo make -j$( nproc )
```

安装 [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)：

```bash
cd ~
git clone https://github.com/cryptonomex/secp256k1-zkp.git
cd secp256k1-zkp
./autogen.sh
./configure
make
sudo make install
```

默认情况下，LLVM和clang不包含WASM构建目标，因此您必须自己构建它：

```bash
mkdir  ~/wasm-compiler
cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd ..
mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
make -j4 install
```

至此，开发环境已搭建完毕。 现在可以开始 <a href="#runanode">构建EOS并运行一个节点了</a>。

### MacOS Sierra 10.12或更高版本下的安装

macOS附加依赖项：

- Brew
- Newest XCode
- MongoDB C++ driver

将您的XCode升级到最新版本：

```bash
xcode-select --install
```

安装 homebrew：

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

安装依赖项：

```bash
brew update
brew install git automake libtool cmake boost openssl@1.0 llvm@4 gmp ninja gettext mongodb
brew link gettext --force
```

安装 [mongo-cxx-driver (release/stable)](https://github.com/mongodb/mongo-cxx-driver)：

```bash
cd ~
brew install --force pkgconfig
brew unlink pkgconfig && brew link --force pkgconfig
curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.9.3/mongo-c-driver-1.9.3.tar.gz
tar xf mongo-c-driver-1.9.3.tar.gz
rm -f mongo-c-driver-1.9.3.tar.gz
cd mongo-c-driver-1.9.3
./configure --enable-static --enable-ssl=darwin --disable-automatic-init-and-cleanup --prefix=/usr/local
make -j$( sysctl -in machdep.cpu.core_count )
sudo make install
cd ..
rm -rf mongo-c-driver-1.9.3

git clone https://github.com/mongodb/mongo-cxx-driver.git --branch releases/stable --depth 1
cd mongo-cxx-driver/build
cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local ..
make -j$( sysctl -in machdep.cpu.core_count )
sudo make install
cd ..
rm -rf mongo-cxx-driver
```

安装 [secp256k1-zkp (Cryptonomex branch)](https://github.com/cryptonomex/secp256k1-zkp.git)：

```bash
cd ~
git clone https://github.com/cryptonomex/secp256k1-zkp.git
cd secp256k1-zkp
./autogen.sh
./configure
make -j$( sysctl -in machdep.cpu.core_count )
sudo make install
```

为WASM构建LLVM和clang：

```bash
mkdir  ~/wasm-compiler
cd ~/wasm-compiler
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
cd llvm/tools
git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
cd ..
mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../
make -j$( sysctl -in machdep.cpu.core_count )
make install
```

至此，开发环境已搭建完毕。 现在可以开始 <a href="#runanode">构建EOS并运行一个节点了</a>。
