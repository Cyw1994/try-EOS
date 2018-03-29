## EOS.IO - 最为强大的分布式应用基础设施

欢迎查看EOS.IO开源代码！EOS.IO提供给开发人员一个能够创建和部署具有高性能、横向可扩展的区块链基础架构，并在此之上进行分布式应用的开发。

源代码目前处于测试阶段但正在快速发展。也就是说，前期的开发者可以维护一个私有节点对网络进行验证亦或是开发一款分布式应用（智能合约）。

按照[Wiki](https://github.com/EOSIO/eos/wiki/Testnet%3A%20Public)中的描述测试网络正运行在`dawn-2.x`分叉，而`master`分叉将不在于公共的测试网络兼容。以下是通过`master`分叉来构建本地测试网络的操作说明。文档将在随后版本更新关于在`dawn-3.x`公共测试网络的下运行的说明。

### 支持的操作系统

EOS.IO现支持的操作系统如下：

1. Amazon 2017.09 and higher.  
2. Centos 7.  
3. Fedora 25 and higher (Fedora 27 recommended).  
4. Mint 18.  
5. Ubuntu 16.04 (Ubuntu 16.10 recommended).  
6. MacOS Darwin 10.12 and higher (MacOS 10.13.x recommended).  

## Resources

1. [EOS.IO 主页](https://eos.io)
2. [Documentation 文档](https://eosio.github.io/eos/)
3. [Blog 博客](https://steemit.com/@eosio)
4. [Community Telegram Group 社区电报群组](https://t.me/EOSProject)
5. [Developer Telegram Group 开发者电报群组](https://t.me/joinchat/EaEnSUPktgfoI-XPfMYtcQ)
6. [White Paper 白皮书](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md)
7. [Roadmap](https://github.com/EOSIO/Documentation/blob/master/Roadmap.md)
8. [Wiki](https://github.com/EOSIO/eos/wiki)

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
   3. [测试网络下创造并发布一个单节点](#singlenode)
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
8. [通过Docker部署EOS](#docker)
9. [手动安装各依赖项](#manualdep)
   1. [Amazon 2017.09或更高版本的安装](#manualdepamazon)
   2. [Centos 7或更高版本的安装](#manualdepcentos)
   3. [Fedora 25或更高版本的安装](#manualdepfedora)
   4. [Mint 18的安装](#manualdepubuntu)
   5. [Ubuntu 16的安装](#manualdepubuntu)
   6. [MacOS Sierra 10.12或更高版本的安装](#manualdepmacos)

## 入门手册