# eIquidus

![GitHub release (latest by date)](https://img.shields.io/github/v/release/team-exor/eiquidus?color=ffbd11&label=version)
![GitHub Release Date](https://img.shields.io/github/release-date/team-exor/eiquidus)
![GitHub last commit](https://img.shields.io/github/last-commit/team-exor/eiquidus)
<img src="public/img/screenshots/platform-windows macos linux-lightgrey.svg" />
![GitHub](https://img.shields.io/github/license/team-exor/eiquidus?color=ffbd11)

eIquidus 使用 Node.js 和 MongoDB 编写，是最稳定、安全、可定制且功能丰富的开源区块浏览器，支持几乎所有实现某种形式 [Bitcoin RPC API 协议](https://developer.bitcoin.org/reference/rpc/index.html) 的山寨币（不支持 EVM 区块链，如 ETH、BNB 等）。eIquidus 最初是为 [Exor 区块链](https://github.com/team-exor/exor) 构建的，现已发展成为一个功能齐全的浏览器，其核心重点是稳定性和安全性。这里包含了 [原始 iquidus 浏览器](https://github.com/iquidus/explorer) 的所有功能，以及来自其他 iquidus 分支的许多新想法，还有专门为 eIquidus 开发的大量自定义更改和错误修复。

![主页](public/img/screenshots/homepage-1-103-0.png)

### 众筹计划

Exor 接受定向捐赠，以众筹区块浏览器和其他 Exor 相关项目的各种功能和改进请求。[浏览未资助任务列表](https://exor.io/tasklist/hide-completed/hide-funded/show-unfunded/) 并将 Exor 币发送到正确的资助地址，以帮助实现您希望看到的任务的资助目标。一旦达到资助目标，Exor 开发人员将尽快开始任务工作，并将其作为首要任务直到完成。如果您是软件开发人员，并希望通过完成资助任务来换取 EXOR 报酬，请使用下面的 [开发者联系方式](#developer-contact) 链接与我们联系。

**新功能：** 已添加初步插件支持。帮助支持第一个自动快照创建插件提案。更多信息：[https://exor.io/task/181/b371d98f6217f2f533b3a0c9fedce7b200571c4f/](https://exor.io/task/181/b371d98f6217f2f533b3a0c9fedce7b200571c4f/)

### 高级支持

本项目中的所有代码均开源，并在 BSD-3-Clause 许可下免费提供。如果您在为您的代币设置浏览器时需要帮助，或者有兴趣聘请开发人员为您的浏览器进行自定义更改，您可以使用下面的 [开发者联系方式](#developer-contact) 链接联系开发人员。

### 开发者联系方式

欢迎使用以下选项之一联系开发人员：

<div align="center">
<a href="https://discord.gg/dSuGm3y"><img src="https://img.shields.io/badge/Discord-Joe%20%5BTeam%20Exor%5D-blue?style=for-the-badge&logo=Discord" /></a>&nbsp;
<a href="https://t.me/joeuhren"><img src="https://img.shields.io/badge/Telegram-joeuhren-blue?style=for-the-badge&logo=Telegram" /></a>
</div>

目录
------------------

- [功能特性](#features)
- [实时演示](#see-it-in-action)
- [安装](#installation)
  - [预安装](#pre-install)
    - [Node.js](#nodejs)
    - [MongoDB](#mongodb)
  - [数据库设置](#database-setup)
  - [下载源代码](#download-source-code)
  - [安装 Node 模块](#install-node-modules)
  - [配置浏览器设置](#configure-explorer-settings)
- [启动/停止浏览器](#startstop-the-explorer)
  - [启动浏览器（用于测试）](#start-explorer-use-for-testing)
  - [停止浏览器（用于测试）](#stop-explorer-use-for-testing)
  - [使用 PM2 启动浏览器（推荐用于生产环境）](#start-explorer-using-pm2-recommended-for-production)
  - [使用 PM2 启动浏览器并查看日志](#start-explorer-using-pm2-and-log-viewer)
  - [使用 PM2 停止浏览器（推荐用于生产环境）](#stop-explorer-using-pm2-recommended-for-production)
  - [使用 PM2 重载浏览器（推荐用于生产环境）](#reload-explorer-using-pm2-recommended-for-production)
  - [使用 Forever 启动浏览器（备选生产环境选项）](#start-explorer-using-forever-alternate-production-option)
  - [使用 Forever 停止浏览器（备选生产环境选项）](#stop-explorer-using-forever-alternate-production-option)
  - [使用 Forever 重载浏览器（备选生产环境选项）](#reload-explorer-using-forever-alternate-production-option)
- [同步数据库与区块链](#syncing-databases-with-the-blockchain)
  - [手动同步数据库命令](#commands-for-manually-syncing-databases)
  - [Crontab 示例](#sample-crontab)
- [钱包设置](#wallet-settings)
- [在 80 端口运行 Express Web 服务器](#run-express-webserver-on-port-80)
  - [使用 Setcap 安全地授予用户权限](#use-setcap-to-safely-grant-user-permissions)
  - [使用另一个 Web 服务器作为反向代理](#use-another-webserver-as-a-reverse-proxy)
- [TLS/SSL 支持](#tlsssl-support)
  - [先决条件](#prerequisites)
  - [手动将 TLS/SSL 证书链接到浏览器](#manually-link-tlsssl-certificates-to-the-explorer)
  - [使用 Nginx 作为反向代理](#use-nginx-as-a-reverse-proxy)
- [CORS 支持](#cors-support)
  - [什么是 CORS？](#what-is-cors)
  - [如何从使用 CORS 中获益？](#how-to-benefit-from-using-cors)
- [实用脚本](#useful-scripts)
  - [更新浏览器脚本](#update-explorer-script)
  - [备份数据库脚本](#backup-database-script)
  - [恢复数据库脚本](#restore-database-script)
  - [删除数据库脚本](#delete-database-script)
  - [基准测试脚本](#benchmark-script)
- [已知问题](#known-issues)
- [捐赠 / 支持我们](#donations--support-us)
- [特别感谢](#special-thanks)
- [许可证](#license)

### 功能特性

- 使用以下脚本和技术构建：
  - Node.js（推荐 v20.9.0 或更新版本）
  - MongoDB（推荐 v7.0.2 或更新版本）
  - jQuery v3.7.1
  - Bootstrap v5.1.3
  - DataTables v1.13.6
  - Font Awesome v6.4.2
  - Luxon v3.4.3
  - Chart.js v4.4.7
    - chartjs-plugin-crosshair v2.0.5
      - 具有工作同步功能的分支版本：([https://github.com/joeuhren/chartjs-plugin-crosshair](https://github.com/joeuhren/chartjs-plugin-crosshair))
      - 原始版本：([https://github.com/abelheinsbroek/chartjs-plugin-crosshair](https://github.com/abelheinsbroek/chartjs-plugin-crosshair))
    - chartjs-chart-financial v0.1.1 ([https://github.com/chartjs/chartjs-chart-financial](https://github.com/chartjs/chartjs-chart-financial))
    - chartjs-adapter-luxon v1.3.1 ([https://github.com/chartjs/chartjs-adapter-luxon](https://github.com/chartjs/chartjs-adapter-luxon))
    - chartjs-plugin-annotation v3.1.0 ([https://github.com/chartjs/chartjs-plugin-annotation](https://github.com/chartjs/chartjs-plugin-annotation))
  - OverlayScrollbars v2.3.2
  - flag-icons v6.11.1 ([https://github.com/lipis/flag-icons](https://github.com/lipis/flag-icons))
  - Intl.js（使用 v4.8.0 polyfill 服务，仅在浏览器尚不支持 ECMAScript 国际化 API 时下载）
- 平台独立（经测试可在 Windows、MacOS 和 Linux 上运行） **注意：** 本指南中的大多数说明都是针对 Linux 编写的，使用其他操作系统时可能需要进行修改
- 移动端友好
- 多线程区块同步
- Sass 支持
- 页面/功能：
  - **主页/浏览器：** 显示最新的区块链交易
  - **主节点：** 显示网络上已知处于活动状态的所有主节点的当前列表。*\*仅适用于主节点币*
  - **大额变动：** 显示大于特定可配置金额的最新区块链交易
  - **网络：** 显示过去 24 小时内连接到 coind 钱包的对等节点列表，以及可用于更轻松地将您自己的钱包连接到网络的有用 addnode 数据
  - **前 100 名：** 显示前 100 个最富有的钱包地址，基于所有接收交易总和接收硬币总数最高的前 100 个钱包地址，以及财富分布的表格和饼图细分。此外还支持从前 100 名列表中省略销毁的硬币
  - **市场：** 显示许多与交易所相关的指标，包括市场摘要、24 小时图表、最近的买/卖单和最新的交易历史。能够直接与交易所 API 和/或来自 [https://www.coingecko.com/en/api](https://www.coingecko.com/en/api) 的 coingecko API 集成，以获取当前市场价格并转换为美元。支持以下 8 个加密货币交易所：
    - [AltMarkets](https://altmarkets.io)
    - [Dex-Trade](https://dex-trade.com)
    - [Dexomy](https://dexomy.com)
    - [FreiExchange](https://freiexchange.com)/[FreiXLite](https://freixlite.com) *\*由于缺乏 OHLCV API 数据，不支持图表*
    - [NonKyc](https://nonkyc.io)
    - [Poloniex](https://poloniex.com)
    - [Xeggex](https://xeggex.com)
    - [Yobit](https://yobit.net) *\*由于缺乏 OHLCV API 数据，不支持图表*
  - **API：** 可用的公共 API 列表，可用于从网络检索信息，而无需本地钱包。支持以下公共 API：
    - **RPC API 调用**（从 coind 返回数据）
      - **getdifficulty：** 返回当前难度
      - **getconnectioncount：** 返回区块浏览器与其他节点的连接数
      - **getblockcount：** 返回当前区块索引
      - **getblockhash：** 返回特定索引处的区块哈希
      - **getblock：** 返回有关具有给定哈希的区块的信息
      - **getrawtransaction：** 返回给定交易 ID 的原始交易表示
      - **getnetworkhashps：** 返回当前网络哈希率
      - **getvotelist：** 返回当前投票列表
      - **getmasternodecount：** 返回网络上主节点的总数 *\*仅适用于主节点币*
    - **扩展 API 调用**（从本地索引返回数据）
      - **getmoneysupply：** 返回当前货币供应量
      - **getdistribution：** 返回财富分布统计数据
      - **getaddress：** 返回给定地址的信息
      - **getaddresstxs：** 返回钱包地址从特定偏移量开始的交易
      - **gettx：** 返回给定交易哈希的信息
      - **getbalance：** 返回给定地址的当前余额
      - **getlasttxs：** 返回大于特定硬币数量的交易，从特定偏移量开始
      - **getcurrentprice：** 返回最后已知的交易所价格
      - **getbasicstats：** 返回有关硬币的基本统计信息，包括：区块计数、流通供应量、美元价格、默认市场价格和主节点数量 *\*主节点数量仅适用于主节点币*
      - **getsummary：** 返回硬币数据的摘要，包括：难度、混合难度、流通供应量、哈希率、默认市场价格、美元价格、网络连接计数、区块计数、在线主节点计数和离线主节点计数 *\*主节点计数仅适用于主节点币*
      - **getnetworkpeers：** 返回过去 24 小时内连接到浏览器节点的网络对等节点列表
      - **getmasternodelist：** 返回网络上主节点的完整列表 *\*仅适用于主节点币*
      - **getmasternoderewards：** 返回特定地址在特定区块高度之后到达的主节点奖励交易列表 *\*仅适用于主节点币*
      - **getmasternoderewardstotal：** 返回特定地址在特定区块高度之后到达的主节点奖励中赚取的硬币总数 *\*仅适用于主节点币*
  - **认领地址：** 允许任何人使用其本地钱包中的 **签名消息** 功能为其拥有的钱包地址设置自定义显示名称。包括 *敏感词* 过滤支持。
  - **孤块：** 显示孤块列表，并带有指向下一个和上一个“好”区块的链接
  - **区块信息：** 显示区块摘要和特定区块高度的交易列表，以及可选的多算法硬币哈希算法和提取/挖掘区块的钱包地址可选列表
  - **交易信息：** 显示交易摘要、可选的 OP_RETURN 值、提取/挖掘 coinbase 交易的钱包地址可选列表、特定交易的输入地址和输出地址列表
  - **地址信息：** 显示钱包地址摘要（余额、总发送、总接收、二维码）和特定钱包地址的最新交易列表
- 从 26 个内置主题中进行选择，并具有可调整的设置（如浅色和深色选项）以自定义浏览器的外观和感觉：
  - **Exor** *\*专为 eIquidus 制作的默认主题*
  - **Cerulean** ([预览](https://bootswatch.com/cerulean/))
  - **Cosmo** ([预览](https://bootswatch.com/cosmo/))
  - **Cyborg** ([预览](https://bootswatch.com/cyborg/))
  - **Darkly** ([预览](https://bootswatch.com/darkly/))
  - **Flatly** ([预览](https://bootswatch.com/flatly/))
  - **Journal** ([预览](https://bootswatch.com/journal/))
  - **Litera** ([预览](https://bootswatch.com/litera/))
  - **Lumen** ([预览](https://bootswatch.com/lumen/))
  - **Lux** ([预览](https://bootswatch.com/lux/))
  - **Materia** ([预览](https://bootswatch.com/materia/))
  - **Minty** ([预览](https://bootswatch.com/minty/))
  - **Morph** ([预览](https://bootswatch.com/morph/))
  - **Pulse** ([预览](https://bootswatch.com/pulse/))
  - **Quartz** ([预览](https://bootswatch.com/quartz/))
  - **Sandstone** ([预览](https://bootswatch.com/sandstone/))
  - **Simplex** ([预览](https://bootswatch.com/simplex/))
  - **Sketchy** ([预览](https://bootswatch.com/sketchy/))
  - **Slate** ([预览](https://bootswatch.com/slate/))
  - **Solar** ([预览](https://bootswatch.com/solar/))
  - **Spacelab** ([预览](https://bootswatch.com/spacelab/))
  - **Superhero** ([预览](https://bootswatch.com/superhero/))
  - **United** ([预览](https://bootswatch.com/united/))
  - **Vapor** ([预览](https://bootswatch.com/vapor/))
  - **Yeti** ([预览](https://bootswatch.com/yeti/))
  - **Zephyr** ([预览](https://bootswatch.com/zephyr/))
- 每个页面顶部的可自定义面板，显示以下信息：
  - **网络：** 显示当前网络哈希率 *\*仅适用于 POW 币*
  - **难度：** 显示当前工作量证明和/或权益证明难度
  - **主节点：** 显示在线和无法访问的主节点数量 *\*仅适用于主节点币*
  - **硬币供应量：** 显示当前流通硬币供应量值
  - **价格：** 显示当前市场价格（使用默认市场对测量的值）
  - **美元价格：** 显示当前市场价格（以美元测量的值）
  - **市值：** 显示当前市值（使用默认市场对测量的值）
  - **美元市值：** 显示当前市值（以美元测量的值）
  - **Logo：** 显示您的硬币 Logo 图像
- 可配置的网络图表，可独立显示在任何页面的标题中
  - **哈希率图表：** 列出过去若干区块或小时内估计的网络每秒哈希数的折线图 *\*需要完全同步后才会开始收集网络数据*
  - **难度图表：** 列出过去若干区块或小时内区块难度的折线图 *\*需要完全同步后才会开始收集网络数据*
- 根据需要在浏览器页脚添加任意数量的自定义社交链接。用于链接到 github、twitter、coinmarketcap 或任何其他社交媒体或外部链接。
- 自定义 rpc/api 命令支持，增加了区块链兼容性。支持的命令：
  - **getnetworkhashps：** 返回估计的网络每秒哈希数
  - **getmininginfo：** 返回包含挖矿相关信息的 json 对象
  - **getdifficulty：** 返回工作量证明难度作为最小难度的倍数
  - **getconnectioncount：** 返回与其他节点的连接数
  - **getblockcount：** 返回最长区块链中的区块数
  - **getblockhash：** 返回提供的最佳区块链高度处的区块哈希
  - **getblock：** 返回包含有关区块信息的对象
  - **getrawtransaction：** 返回原始交易数据
  - **getinfo：** 返回包含各种状态信息的对象
  - **getblockchaininfo：** 返回包含有关区块链处理的各种状态信息的对象
  - **getpeerinfo：** 返回有关每个连接的网络节点的数据，作为对象的 json 数组
  - **gettxoutsetinfo：** 返回有关未花费交易输出集的统计信息的对象
  - **getvotelist：** 返回有关当前投票列表详细信息的对象
  - **getmasternodecount：** 返回包含网络上主节点总数的 json 对象
  - **getmasternodelist：** 返回包含网络上所有主节点状态信息的 json 数组
  - **verifymessage：** 验证签名消息。必须接受以下参数：
    - **address：** 用于签名的钱包地址
    - **signature：** 签名者提供的 base 64 编码签名
    - **message：** 被签名的消息
- 对以下自定义区块链功能的额外支持：
  - 比特币 P2PK 交易
    - 比特币 rpc/api 命令：
      - **getdescriptorinfo：** 接受描述符作为输入并返回包含更详细信息的对象，包括其计算的校验和
      - **deriveaddresses：** 接受输出描述符作为输入并返回包含一个或多个 P2PKH 地址的数组
  - Heavycoin 民主投票和奖励支持
    - **奖励页面：** 显示奖励/投票信息
    - Heavycoin rpc/api 命令：
      - **getmaxmoney：** 返回总共将产生的硬币数量
      - **getmaxvote：** 返回当前投票阶段允许的最大投票数
      - **getvote：** 返回当前区块奖励投票设置
      - **getphase：** 返回当前投票阶段名称
      - **getreward：** 返回当前区块奖励
      - **getsupply：** 返回当前货币供应量
      - **getnextrewardestimate：** 根据去中心化投票的当前状态返回下一个区块奖励的估计值
      - **getnextrewardwhenstr：** 返回描述直到票数统计和计算下一个区块奖励还有多长时间的字符串
    - Heavycoin 公共 API：
      - **getmaxmoney：** 返回最大可能的货币供应量
      - **getmaxvote：** 返回当前投票阶段允许的最大投票数
      - **getvote：** 返回当前区块奖励投票设置
      - **getphase：** 返回当前投票阶段
      - **getreward：** 返回当前区块奖励，该奖励已在前一轮区块奖励投票中民主决定
      - **getsupply：** 返回当前货币供应量
      - **getnextrewardestimate：** 根据去中心化投票的当前状态返回下一个区块奖励的估计值
      - **getnextrewardwhenstr：** 返回描述直到票数统计和计算下一个区块奖励还有多长时间的字符串
  - Zcash/zk-SNARKs 私有交易支持

### 实时演示

-  https://explorer.exor.io/

### 安装

#### 预安装

在使用浏览器之前，必须安装以下先决条件：

- [Node.js](https://nodejs.org/en/)（推荐 v20.9.0 或更新版本）
- [MongoDB](https://www.mongodb.com/)（推荐 v7.0.2 或更新版本）
- [Git](https://git-scm.com/downloads)（推荐 v2.36.0 或更新版本）
- 一个完全同步的 *coind* 钱包守护进程，支持 [Bitcoin RPC API 协议](https://developer.bitcoin.org/reference/rpc/index.html)。**注意：** 在大多数情况下，区块链必须在启用 `txindex` 功能的情况下同步，以便访问所有交易。有关更多详细信息，请参阅 [钱包设置](#wallet-settings) 部分。

##### Node.js

安装 Node.js 的推荐方法是使用 Node 版本管理器 (NVM)：

```
sudo apt update
sudo apt install curl
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
source ~/.profile
nvm install --lts
```

在上面的最后一个命令中使用 `--lts` 选项将安装最新 LTS 版本的 Node.js。如果您想安装特定版本，可以使用以下命令：

```
nvm install 20.9.0
```

如果需要，可以使用 NVM 同时安装多个版本的 Node.js。使用以下语法轻松将当前 Node.js 版本更改为另一个已安装版本：

```
nvm use 18.14.2
```

##### MongoDB

建议遵循官方 mongo 网站上的安装说明，因为它们会更频繁地更新，并针对许多不同的操作系统提供具体说明：[https://www.mongodb.com/docs/manual/administration/install-community/](https://www.mongodb.com/docs/manual/administration/install-community/)。

以下是在 Ubunutu 22.04 上安装最新 v7.x 版本 MongoDB 的说明（一次运行一行）：

```
sudo apt-get install gnupg curl
curl -fsSL https://pgp.mongodb.com/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

安装 MongoDB 后，建议运行以下命令启动数据库服务器并将其添加为服务，以确保重启后自动启动：

```
sudo systemctl start mongod
sudo systemctl enable mongod.service
```

#### 数据库设置

打开 MongoDB cli（旧版 mongo shell `mongo` 在 MongoDB v5.0 中已弃用，在 MongoDB v6.0 中已删除。新安装现在必须使用 `mongosh`）：

```
mongosh
```

选择数据库：

**注意：** `explorerdb` 是您将存储本地浏览器数据的数据库名称。您可以将其更改为任何您想要的名称，但必须确保在 `settings.json` 文件中为 `dbsettings.database` 设置相同的名称。

```
use explorerdb
```

创建一个具有读/写访问权限的新用户：

```
db.createUser( { user: "eiquidus", pwd: "Nd^p2d77ceBX!L", roles: [ "readWrite" ] } )
```

退出 mongo shell：

```
exit
```

#### 下载源代码

```
git clone https://github.com/team-exor/eiquidus explorer
```

#### 安装 Node 模块

```
cd explorer && npm install --only=prod
```

#### 配置浏览器设置

```
cp ./settings.json.template ./settings.json
```

*在 settings.json 中进行必要的更改*

**注意：** 您可以通过将自己的 javascript 代码添加到 `public/js/custom.js` 文件并将 css 规则添加到 `public/css/custom.scss` 文件来进一步自定义站点。向 `custom.js` 和 `custom.scss` 添加更改是自定义站点的首选方法，而不会影响将来接收浏览器代码更新的能力。

### 启动/停止浏览器

#### 启动浏览器（用于测试）

您可以在终端窗口中启动浏览器，该窗口将输出所有警告和错误消息，使用以下命令之一（请确保在 explorer 目录中运行）：

```
npm start
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/npm run prestart && /path/to/node --stack-size=10000 ./bin/cluster
```

**注意：** mongod 必须正在运行才能启动浏览器。

浏览器默认为集群模式，即为每个 cpu 核心分叉一个进程实例，从而提高性能和稳定性。负载均衡会自动处理，任何因某种原因死亡的实例都将自动重启。如果需要，可以使用以下命令启动单个实例：

```
npm run start-instance
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/npm run prestart && /path/to/node --stack-size=10000 ./bin/cluster 1
```

#### 停止浏览器（用于测试）

要停止使用 `npm start` 运行的浏览器，您可以在运行浏览器的终端中使用组合键 `CTRL+C` 结束进程，或者从另一个终端使用以下命令之一（请确保在 explorer 目录中运行）：

```
npm stop
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/node ./scripts/stop_explorer.js
```

#### 使用 PM2 启动浏览器（推荐用于生产环境）

[PM2](https://www.npmjs.com/package/pm2) 是 Node.js 应用程序的进程管理器，具有内置的负载均衡器，允许您始终保持浏览器处于活动状态并运行，即使它崩溃也是如此。一旦您配置好浏览器以在生产环境中正常工作，建议使用 PM2 来启动和停止浏览器，而不是 `npm start` 和 `npm stop`，以保持浏览器持续运行，而无需始终保持终端窗口打开。

您可以使用以下终端命令之一使用 PM2 启动浏览器（请确保在 explorer 目录中运行）：

```
npm run start-pm2
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/npm run prestart "pm2" && /path/to/pm2 start ./bin/instance -i 0 -n explorer -p "./tmp/pm2.pid" --node-args="--stack-size=10000"
```

**注意：** 使用以下命令查找 PM2 的安装路径（仅限 Linux）：

```
which pm2
```

#### 使用 PM2 启动浏览器并查看日志

或者，您可以使用 PM2 启动浏览器并自动打开日志查看器，这将允许您查看所有出现的警告和错误消息，使用以下终端命令之一（请确保在 explorer 目录中运行）：

```
npm run start-pm2-debug
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/npm run prestart "pm2" && /path/to/pm2 start ./bin/instance -i 0 -n explorer -p "./tmp/pm2.pid" --node-args="--stack-size=10000" && /path/to/pm2 logs
```

#### 使用 PM2 停止浏览器（推荐用于生产环境）

要在通过 PM2 运行时停止浏览器，您可以使用以下终端命令之一（请确保在 explorer 目录中运行）：

```
npm run stop-pm2
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/pm2 stop explorer
```

#### 使用 PM2 重载浏览器（推荐用于生产环境）

当通过 PM2 运行时，可以在单个命令中停止并重启浏览器，这在更新浏览器代码后通常是必要的。使用以下终端命令之一重载浏览器（请确保在 explorer 目录中运行）：

**注意：** 假设浏览器可以访问 2 个或更多 cpu，则此重载将以零停机时间的方式完成，同时执行重启。如果您只有一个 cpu，则在执行重启时浏览器将无法访问几秒钟。

```
npm run reload-pm2
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/pm2 reload explorer
```

#### 使用 Forever 启动浏览器（备选生产环境选项）

[Forever](https://www.npmjs.com/package/forever) 是 PM2 的替代方案，它是另一个有用的 Node.js 模块，用于始终保持浏览器处于活动状态并运行，即使浏览器崩溃或停止也是如此。一旦您配置好浏览器以在生产环境中正常工作，forever 可以作为 PM2 的替代方案来启动和停止浏览器，而不是 `npm start` 和 `npm stop`，以保持浏览器持续运行，而无需始终保持终端窗口打开。

您可以使用以下终端命令之一使用 forever 启动浏览器（请确保在 explorer 目录中运行）：

```
npm run start-forever
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/npm run prestart "forever"
```

**注意：** 使用以下命令查找 forever 的安装路径（仅限 Linux）：

```
which forever
```

#### 使用 Forever 停止浏览器（备选生产环境选项）

要在通过 forever 运行时停止浏览器，您可以使用以下终端命令之一（请确保在 explorer 目录中运行）：

```
npm run stop-forever
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/forever stop "explorer"
```

#### 使用 Forever 重载浏览器（备选生产环境选项）

当通过 forever 运行时，可以在单个命令中停止并重启浏览器，这在更新浏览器代码后通常是必要的。使用以下终端命令之一重载浏览器（请确保在 explorer 目录中运行）：

**注意：** 在执行重启时，浏览器将无法访问几秒钟。

```
npm run reload-forever
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/forever restart "explorer"
```

### 同步数据库与区块链

sync.js（位于 scripts/ 中）用于更新本地数据库。必须从 explorer 根目录调用此脚本。

```
用法: /path/to/node scripts/sync.js [mode]

模式: (必填)
update           从上次同步更新索引到当前区块
check            检查索引是否有（并添加）任何丢失的交易/地址
                 可选参数：开始检查的区块号
reindex          清除索引然后从创世区块重新同步到当前区块
reindex-rich     清除并重新创建富豪榜数据
reindex-txcount  重新扫描并扁平化 tx 计数以加快访问速度
reindex-last     重新扫描并扁平化最后区块索引值以加快访问速度
market           更新市场摘要、订单簿、交易历史 + 图表
peers            根据本地钱包连接更新对等节点信息
masternodes      更新网络上活动主节点的列表

注意:
- 'current block' 是脚本执行时最新创建的区块。
- market + peers 数据库仅支持（并默认为）reindex 模式。
- 如果 check 模式发现丢失数据（除了自上次同步以来的新数据），
  这可能意味着 settings.json 中的 sync.update_timeout 设置得太低。
```

*建议使用下面的手动命令进行区块链、市场、对等节点和主节点的初始同步，以确保没有同步问题。当您确定一切都正确同步后，您应该按照下面的指示将必要的脚本安装到 crontab 中，间隔 1 分钟以上*

#### 手动同步数据库命令

浏览器包含许多 npm 脚本，便于同步各种浏览器数据库。以下脚本是用于将浏览器与区块链同步的主要命令：

- `npm run sync-blocks`：连接到钱包守护进程以将区块/交易拉入浏览器，从创世区块开始到当前区块。重复调用此命令将记住上次下载的区块，以允许连续同步新区块。
- `npm run sync-markets`：连接到 `settings.json` 文件中定义的各种交易所 api，以提供市场相关数据，如市场摘要、订单簿、交易历史和图表。
- `npm run sync-peers`：连接到钱包守护进程并拉入有关已连接节点的数据。
- `npm run sync-masternodes`：连接到钱包守护进程并拉入网络上活动主节点的列表。*\*仅适用于主节点币*

还包含少量有用的脚本，以帮助解决您在使用浏览器时可能遇到的各种问题：

- `npm run check-blocks`：通过与钱包守护进程进行比较来重新检查所有以前同步的区块，以查找并添加任何丢失的交易/地址。可选参数：开始检查的区块号。示例：`npm run check-blocks 1000` 将从区块 1000 开始检查。:warning: **警告：** 这可能需要很长时间，具体取决于区块链的长度，除非绝对必要，否则通常不建议这样做。此外，在检查丢失数据时，您将无法将新区块同步到浏览器中，直到检查命令完成。如果您通过此检查确实发现了丢失的交易（除了自上次同步以来的新数据），这可能意味着 `settings.json` 中的 `sync.update_timeout` 设置得太低。
- `npm run reindex`：删除所有区块、交易和地址，并从创世区块重新同步到当前区块。:warning: **警告：** 这将清除浏览器中所有与区块链相关的数据。建议在继续此命令之前 [备份浏览器数据库](#backup-database-script)。
- `npm run reindex-rich`：清除并重新创建前 100 名持币者页面的富豪榜数据。很少需要，但对于调试或如果您确定富豪榜数据因某种原因不正确时可能很有用。
- `npm run reindex-txcount`：通过重新计算 mongo 数据库中存储的 tx 来重新计算存储在 `stats.txes` 中的交易计数。很少需要，但对于调试或如果您注意到主交易列表显示的条目数错误时可能很有用。如果此值因某种原因有偏差，您将无法在主交易列表中翻回到第 1 个区块。
- `npm run reindex-last`：在 mongo 数据库中查找最后一个交易，并将 `stats.last` 值重置为最新的区块索引。很少需要，但对于调试可能很有用。`stats.last` 值用于记住上次同步停止的区块，以便从下一个区块恢复同步。

另请参阅 [实用脚本](#useful-scripts) 部分以获取更多有用的脚本。

#### Crontab 示例

*Crontab 示例；每分钟更新索引，每 2 分钟更新市场数据，每 5 分钟更新对等节点和主节点*

使用 npm 脚本的更简单的 crontab 语法，但根据权限和 nodejs 的安装方式，可能无法在某些系统上运行：

```
*/1 * * * * cd /path/to/explorer && npm run sync-blocks > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && npm run sync-markets > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && npm run sync-peers > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && npm run sync-masternodes > /dev/null 2>&1
```

或者，通过直接调用 sync 脚本来运行 crontab，如果无法从 crontab 运行 npm 脚本，这种方法应该更有效：

```
*/1 * * * * cd /path/to/explorer && /path/to/node scripts/sync.js update > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && /path/to/node scripts/sync.js market > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && /path/to/node scripts/sync.js peers > /dev/null 2>&1
*/5 * * * * cd /path/to/explorer && /path/to/node scripts/sync.js masternodes > /dev/null 2>&1
```

### 钱包设置

连接到 eIquidus 的钱包必须使用以下标志运行：

```
-daemon -txindex
```

您可以使用以下语法调用您的 coin 守护进程：

```
coind -daemon -txindex
```

或者，您可以将设置添加到您的 coins 配置文件中（推荐）：

```
daemon=1
txindex=1
```

### 在 80 端口运行 Express Web 服务器

典型的 Web 服务器绑定到端口 80 以通过 http 协议提供网页，但默认情况下 Express Web 服务器无法执行此操作，除非授予它 root 权限，出于安全原因不建议这样做。相反，有两种推荐的解决方法来实现相同的最终结果：

**注意：** 请务必允许端口 80 通过您可能配置的任何防火墙，否则可能无法远程访问浏览器网站。

#### 使用 Setcap 安全地授予用户权限

**注意：** 此选项仅适用于 Linux 用户

1. 您可以使用 `setcap` 命令更改 `node` 二进制文件的功能，以专门允许 Express Web 服务器绑定到小于 1024 的端口（此一次性命令需要 root 权限）：

```
sudo setcap cap_net_bind_service=+ep `readlink -f \`which node\``
```

2. 打开 `settings.json` 文件并将 `webserver.port` 设置更改为 80。保存更改并重新启动浏览器。

现在您应该能够通过 IP 地址或域名浏览浏览器，而无需再指定 3001 端口。

#### 使用另一个 Web 服务器作为反向代理

**注意：** 以下说明仅适用于 Linux 用户，但在任何操作系统上安装和配置另一个 Web 服务器应该是可能的

设置另一个可以绑定到端口 80 并将所有传入流量转发到 eIquidus node.js 应用程序的 Web 服务器涉及几个步骤。可以使用任何商业 Web 服务器创建反向代理，但在这种情况下，将使用 Nginx 作为示例：

1. 使用以下终端命令安装 Nginx：

```
sudo apt-get install nginx
```

2. 删除默认配置文件：

```
sudo rm /etc/nginx/sites-enabled/default
```

3. 在 `/etc/nginx/sites-available/` 中创建一个名为 `node` 的新文件，并使用 nano 文本编辑器打开它：

```
sudo nano /etc/nginx/sites-available/node
```

4. 将以下代码粘贴到文件中，并确保将 `example.com` 更改为您的域名或 IP 地址，并将 `proxy_pass` 行上的端口 `3001` 更改为您在 `settings.json` 文件中为 `webserver.port` 设置配置的端口号。编辑完成后，按 CTRL+X，然后按 Y（是保存），然后按 ENTER 完成保存对配置文件的更改：

```
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_set_header   X-Forwarded-For $remote_addr;
        proxy_set_header   Host $http_host;
        proxy_pass         "http://127.0.0.1:3001";
    }
}
```

5. 为刚刚创建的 Nginx 配置文件创建一个新的符号链接，并将其链接到 `/etc/nginx/sites-enabled` 目录：

```
sudo ln -s /etc/nginx/sites-available/node /etc/nginx/sites-enabled/node
```

6. 重新启动 Nginx 以应用配置更改：

```
sudo service nginx restart
```

7. Nginx 现在将所有传入请求转发到 eIquidus，重新启动浏览器后，应该可以通过 http://example.com 浏览它，而无需再使用 http://example.com:3001 端口。

### TLS/SSL 支持

类似于 [绑定到端口 80 的问题](#run-express-webserver-on-port-80)，典型的 Web 服务器绑定到端口 443 以通过 https 协议提供网页，但默认情况下 Express Web 服务器无法执行此操作，除非授予它 root 权限，出于安全原因不建议这样做。相反，有两种推荐的解决方法来实现相同的最终结果：[手动将 TLS/SSL 证书链接到浏览器](#manually-link-tlsssl-certificates-to-the-explorer) 或 [使用 Nginx 作为反向代理](#use-nginx-as-a-reverse-proxy)。

**注意：** 请务必允许端口 443 通过您可能配置的任何防火墙，否则可能无法远程访问浏览器网站。

#### 先决条件

**注意：** 以下说明仅适用于 Linux 用户，但在任何操作系统上安装和配置 certbot 应该是可能的

在生成 TLS/SSL 证书之前，必须完成几个常见步骤：

1. 安装 snapd：

```
sudo apt install snapd
```

2. 确保 snapd 是最新的：

```
sudo snap install core; sudo snap refresh core
```

3. 安装 certbot（有关不同操作系统和配置的完整安装说明，请参见此处：[https://certbot.eff.org/instructions](https://certbot.eff.org/instructions)）：

```
sudo snap install --classic certbot
```

4. 准备 certbot 命令：

```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

#### 手动将 TLS/SSL 证书链接到浏览器

**注意：** 以下说明仅适用于 Linux 用户，但在任何操作系统上安装和配置 certbot 应该是可能的

按照以下步骤配置 Express Web 服务器以使用 TLS/SSL：

1. 如果您尚未这样做，请运行 [使用 Setcap 安全地授予用户权限说明](#use-setcap-to-safely-grant-user-permissions) 中的 `setcap` 命令，这将允许 node.js 绑定到端口 443 而无需 root 权限。

2. 通过 certbot 生成有效 TLS/SSL 证书有不同的选项。如果您在端口 80 上运行浏览器，则可以在步骤 2A) 上运行命令，否则如果浏览器在除 80 以外的任何端口号上运行，请在步骤 2B) 上运行命令。此步骤很重要，因为 certbot 将定期自动续订您的 TLS/SSL 证书，如果选择了错误的选项，它将无法续订：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A. 当浏览器已使用端口 80 时，使用 Webroot 方法。请务必将 webroot-path 更改为 explorer/public 目录的绝对路径：

**注意：** 浏览器必须正在运行才能使此命令正常工作：

```
sudo certbot certonly --webroot --webroot-path /path/to/explorer/public
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;B. 当浏览器尚未占用端口 80 时，使用 Standalone 方法：

```
sudo certbot certonly --standalone
```

Certbot 将询问几个简单的问题，并为您的域生成必要的 TLS/SSL 证书文件。它还将安装必要的文件，以便在证书即将过期时自动续订，因此您无需执行任何特殊操作即可使其保持最新状态。

3. 生成 TLS/SSL 证书后，您需要使用以下命令授予非 root 用户权限：

```
sudo chmod -R 755 /etc/letsencrypt/live/
sudo chmod -R 755 /etc/letsencrypt/archive/
```

4. 最后一步是在浏览器的 `settings.json` 文件中启用 TLS，并指定刚刚生成的 3 个主要证书文件的路径。示例：

```
  "webserver": {
    "port": 80,
    "tls": {
      "enabled": true,
      "port": 443,
      "cert_file": "/etc/letsencrypt/live/example.com/cert.pem",
      "chain_file": "/etc/letsencrypt/live/example.com/chain.pem",
      "key_file": "/etc/letsencrypt/live/example.com/privkey.pem"
    },
    "cors": {
      "enabled": false,
      "corsorigin": "*"
    }
  },
```

确保 `webserver.tls.enabled` = true，并通过将 `example.com` 更改为您刚刚为其生成 TLS/SSL 证书的域名，指定 `webserver.tls.cert_file`、`webserver.tls.chain_file` 和 `webserver.tls.key_file` 文件的确切路径。

5. 如果一切顺利，您现在应该能够启动浏览器并使用安全的 https 连接（如 [https://example.com](https://example.com)）浏览它。

#### 使用 Nginx 作为反向代理

**注意：** 以下说明仅适用于 Linux 用户，但在任何操作系统上安装和配置 certbot 和 nginx 应该是可能的

1. 如果您尚未这样做，请先完成 [使用另一个 Web 服务器作为反向代理说明](#use-another-webserver-as-a-reverse-proxy)，然后继续执行下面的步骤 #2。

2. 通过 certbot 生成新的 TLS/SSL 证书，这将自动编辑您的 Nginx 配置文件并同时启用 https：

```
sudo certbot --nginx
```

Certbot 将询问几个简单的问题，并为您的域生成必要的 TLS/SSL 证书文件并将其链接到 Nginx。它还将安装必要的文件，以便在证书即将过期时自动续订，因此您无需执行任何特殊操作即可使其保持最新状态。

3. 如果一切顺利，您现在应该能够启动浏览器并使用安全的 https 连接（如 [https://example.com](https://example.com)）浏览它。

### CORS 支持

eIquidus 具有基本的 CORS 支持，这对于防止其他站点使用公共 API 很有用，同时仍允许特定的白名单网站访问。

#### 什么是 CORS？

*CORS 描述摘自 [MaxCDN One](https://www.maxcdn.com/one/visual-glossary/cors/)*

>为了防止网站相互篡改，Web 浏览器实施了一种称为同源策略的安全措施。同源策略允许资源（如 JavaScript）与来自同一域的资源交互，但不允许与来自不同域的资源交互。这通过防止滥用（例如运行读取安全网站上密码字段的脚本）来为用户提供安全性。

>在需要跨域脚本的情况下，CORS 允许 Web 开发人员绕过同源策略。CORS 添加 HTTP 标头，指示 Web 浏览器如何使用和管理跨域内容。然后，浏览器根据其安全配置允许或拒绝访问内容。

#### 如何从使用 CORS 中获益？

您必须首先通过编辑 settings.json 文件并将 `webserver.cors.enabled` 的值设置为 true 来在 eIquidus 中设置 CORS。

```
  "webserver": {
    "cors": {
      "enabled": true,
```

`webserver.cors.corsorigin` 设置默认为 "\*"，允许来自任何来源的所有请求。将此设置保持为 "\*" 可能会导致滥用，因此不建议这样做。因此，您应该将 `webserver.cors.corsorigin` 设置更改为您控制的外部来源，如下例所示：

```
  "webserver": {
    "cors": {
      "enabled": true,
      "corsorigin": "http://example.com"
```

上面的示例将允许从 eIquidus 共享资源以用于来自 example.com 域的所有数据请求，而来自任何其他域的所有请求将按正常情况被拒绝。

以下是使用 [jQuery](https://jquery.com) 的简单 javascript 调用示例，可以在您的 example.com 网站上使用它来从 eIquidus 返回当前区块计数：

```
jQuery(document).ready(function($) {
  $.ajax({
    type: "GET",
    url: "http://your-eiquidus-url/api/getblockcount",
    cache: false
  }).done(function (data) {
    alert(data);
  });
});
```

### 实用脚本

#### 更新浏览器脚本

自动下载并安装最新的浏览器源代码，更新过时的依赖项并使用单个命令重载浏览器。此更新脚本可以在浏览器处于活动运行状态时安全运行，以防止需要手动关闭来进行更新，但请注意，在更新浏览器时，网站可能无法访问几秒钟或更长时间。

**注意：** 只有通过从 git 克隆源代码安装的浏览器安装才能自动更新。请务必遵循 [快速安装说明](#quick-install-instructions) 来设置浏览器以最佳地使用此更新脚本。

使用以下命令更新浏览器：

```
npm run update-explorer
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/node ./scripts/update_explorer.js
```

**注意：** 更新脚本还支持几个可选参数。

如果您只想更新浏览器代码，而不检查过时的依赖项，请使用以下命令：

```
npm run update-explorer "explorer-only"
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/node ./scripts/update_explorer.js "explorer-only"
```

如果您只想升级过时的依赖项，而不检查浏览器代码更新，请使用以下命令：

```
npm run update-explorer "dependencies-only"
```

或（适用于 crontab）：

```
cd /path/to/explorer && /path/to/node ./scripts/update_explorer.js "dependencies-only"
```

#### 备份数据库脚本

对 eIquidus mongo 数据库或单个集合进行完整备份并保存到压缩文件。内置锁定机制可防止在备份过程中更新或更改数据。可以在浏览器处于活动运行状态和/或关闭时安全地创建备份。

参数：
1. 备份路径或文件名（可选）
2. 集合名称（可选） **注意：** 此参数对于备份单个数据库集合（如 `claimaddresses` 或插件相关集合）很有用，以后可以将其恢复到现有数据库中，而不会影响任何其他数据库集合。

支持以下备份方案：

**备份数据库（未指定文件名）**

`npm run create-backup`：默认备份到 explorer/backups 目录，文件名为当前日期，格式为 yyyy-MMM-dd.bak

**备份数据库（指定部分文件名）**

`npm run create-backup test`：默认备份 explorer/backups 目录，文件名为 test.bak

**备份数据库（指定完整文件名）**

`npm run create-backup today.bak`：默认备份 explorer/backups 目录，文件名为 today.bak

**备份数据库（指定带部分文件名的完整路径）**

`npm run create-backup /usr/local/bin/abc`：备份 /usr/local/bin 目录，文件名为 abc.bak

**备份数据库（指定完整路径和文件名）**

`npm run create-backup ~/new.bak`：备份用户主目录，文件名为 new.bak

**备份数据库（同时指定文件名和集合）**

`npm run create-backup test claimaddresses`：默认仅备份 `claimaddresses` 集合到 explorer/backups 目录，文件名为 test.bak

**备份数据库（未指定文件名，且仅备份单个集合）**

`npm run create-backup "" masternodes`：默认仅备份 `masternodes` 集合到 explorer/backups 目录，文件名为当前日期，格式为 yyyy-MMM-dd.bak 

#### 恢复数据库脚本

恢复以前保存的 eIquidus mongo 数据库备份。:warning: **警告：** 除非指定了单个集合名称，否则这将完全覆盖您现有的 eIquidus mongo 数据库，因此请务必在继续之前进行完整备份。内置锁定机制可防止在恢复备份时更新或更改数据。可以在浏览器处于活动运行状态和/或关闭时安全地恢复备份。

**注意：** 较旧的 v1.x eIquidus 数据库备份被压缩为 tar.gz 文件。这些较旧的 tar.gz 备份仍然可以恢复，但您必须专门添加 .tar.gz 后缀。示例：`npm run restore-backup /path/to/old_backup.tar.gz`

参数：
1. 备份路径或文件名（可选）
2. 集合名称（可选） **注意：** 此参数对于恢复单个数据库集合（如 `claimaddresses` 或插件相关集合）很有用，而不会影响任何其他数据库集合。此选项可用于单个集合备份或完整数据库备份，并且仅恢复指定的集合。

支持以下恢复方案：

**恢复数据库（指定部分文件名）**

`npm run restore-backup old`：恢复 explorer/scripts/backups/old.bak 文件

**恢复数据库（指定完整文件名）**

`npm run restore-backup working.bak`：恢复 explorer/scripts/backups/working.bak 文件

**恢复数据库（指定带部分文件名的完整路径）**

`npm run restore-backup /home/explorer/backup`：恢复 /home/explorer/backup.bak 文件

**恢复数据库（指定完整路径和文件名）**

`npm run restore-backup ~/archive.bak`：恢复 ~/archive.bak 文件

**恢复数据库（同时指定文件名和集合）**

`npm run restore-backup test claimaddresses`：仅从 explorer/scripts/backups/test.bak 文件恢复 `claimaddresses` 集合

#### 删除数据库脚本

擦除 eIquidus mongo 数据库以重新开始。:warning: **警告：** 这将完全销毁您现有 eIquidus mongo 数据库中的所有数据，因此请务必在继续之前进行完整备份。内置锁定机制可防止在删除数据库时更新或更改数据。删除数据库的过程可以在浏览器处于活动运行状态和/或关闭时执行。

使用以下命令删除 mongo 数据库：

`npm run delete-database`

#### 基准测试脚本

此脚本更多是供开发人员使用的调试工具，允许您将一定数量的区块（默认为 5000 个区块）同步到单独的 mongodb 数据库，并输出同步的总 tx 和地址记录以及完成所需的总时间。settings.json 文件中有一个 `benchmark` 部分，可用于配置各种基准测试选项。

可以使用以下命令启动基准测试脚本：

`npm run benchmark`

### 已知问题

**错误：bind EACCES ...**

当您尝试在低于 1024 的端口号上运行浏览器时，可能会出现此错误。此问题有几种解决方案，在 [在 80 端口运行 Express Web 服务器](#run-express-webserver-on-port-80) 部分中有更详细的解释。

**错误：Callback was already called**

此错误通常意味着浏览器与钱包守护进程之间存在某种连接问题。导致此错误的最常见错误是在 settings.json 中配置了钱包的 P2P 端口号而不是 RPC 端口号。如果您的钱包未设置为接受 RPC 连接，也可能会发生这种情况。

**警告：Accessing non-existent property 'padLevels' of module exports inside circular dependency**

当前使用 `forever` 模块启动或停止浏览器时会显示此警告。好消息是，尽管显示此警告可能会令人困惑，但可以安全地忽略它。这是 `forever` 的一个根深蒂固的问题，目前正在 [此处](https://github.com/foreversd/forever/issues/1077) 积极讨论。长话短说，`forever` 依赖于许多过时的依赖项，这些依赖项需要重写代码的某些部分，到目前为止尚未正式解决。`Forever` 仍然作为选项包含在内，供习惯使用它的人使用，尽管我们建议使用 `pm2` 来运行您的生产浏览器，因为它更现代，可以做 `forever` 能做的一切，甚至更多。

### 捐赠 / 支持我们

eIquidus 区块浏览器由 [Exor 开发团队](https://exor.io/#section-team) 为广大加密社区的利益不懈努力为您带来。如果您喜欢我们的工作，请考虑支持我们继续开发此项目以及许多其他很酷的加密项目，您可以在我们的 [github 页面](https://github.com/team-exor) 上找到这些项目。

您可以通过以下选项之一支持我们：

1. 购买并持有 EXOR。购买和交易我们的 EXOR 币有助于刺激市场价格，这使我们能够聘请更多开发人员并在未来继续发布高质量的产品。我们在以下交易所上市：
    - [FreiXLite](https://freixlite.com/market/EXOR/LTC)
    - [Dexomy](https://dexomy.com/exchange/dashboard?coin_pair=EXOR_USDT)
2. 参与我们的 [众筹计划](https://exor.io/tasklist/hide-completed/hide-funded/show-unfunded/)，方法是发送一些加密货币来帮助资助您最希望看到的任务，或者 [提交新的自定义任务请求](https://exor.io/add-new-task/)，详细说明您希望为任何 Exor 相关项目开发的功能或改进。
3. 考虑通过向我们发送一些加密货币来进行小额捐赠：
    - **BTC:** [15zQAQFB9KR35nPWEJEKvmytUF6fg2zvdP](https://www.blockchain.com/btc/address/15zQAQFB9KR35nPWEJEKvmytUF6fg2zvdP)
    - **ETH:** [0x1E4163EE9721bCA934D9e40C792360A901a59E02](https://etherscan.io/address/0x1E4163EE9721bCA934D9e40C792360A901a59E02) **注意：** 可用于 USDT 或 ETH 网络上的任何其他代币
    - **BNB:** [0x1E4163EE9721bCA934D9e40C792360A901a59E02](https://bscscan.com/address/0x1E4163EE9721bCA934D9e40C792360A901a59E02) **注意：** 可用于 USDT 或 BNB 网络上的任何其他代币
    - **EXOR:** [EYYW8Nvz5aJz33M3JNHXG2FEHWUsntozrd](https://explorer.exor.io/address/EYYW8Nvz5aJz33M3JNHXG2FEHWUsntozrd)
4. 您是软件开发人员吗？考虑利用我们的 [众筹计划](https://exor.io/tasklist/hide-completed/)，通过提交开放赏金任务的代码改进来获得 EXOR 报酬，帮助使区块浏览器和其他 Exor 相关项目变得更好。

### 特别感谢

- **[Luke Williams (aka iquidus)](https://github.com/iquidus):** 创建了原始的 [Iquidus 浏览器](https://github.com/iquidus/explorer)
- **[Alan Rudolf (aka suprnurd)](https://github.com/suprnurd):** 提供了在 [Ciquidus 浏览器](https://github.com/suprnurd/ciquidus) 中发现的自定义更改
- **[Tim Garrity (aka uaktags)](https://github.com/uaktags):** 为 Iquidus 浏览器做出了许多贡献，以及来自 [uaktags 浏览器](https://github.com/uaktags/explorer) 的自定义功能
- **[TheHolyRoger](https://github.com/TheHolyRoger):** 为 Iquidus 浏览器继续工作并做出贡献
- **[Karzo](https://github.com/KarzoGitHub):** 帮助进行批量写入区块同步代码更改
- 所有其他以某种方式帮助塑造 Iquidus 浏览器的 Iquidus 贡献者

### 许可证

Copyright (c) 2019-2025, The Exor Community<br />
Copyright (c) 2017, The Chaincoin Community<br />
Copyright (c) 2015, Iquidus Technology<br />
Copyright (c) 2015, Luke Williams<br />
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

* Neither the name of Iquidus Technology nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
