# Scash Explorer

![GitHub license](https://img.shields.io/github/license/team-exor/eiquidus?color=ffbd11)

Scash Explorer 是一个基于 [eIquidus](https://github.com/team-exor/eiquidus) 修改的开源区块浏览器，专为 **Scash** 区块链设计。

本项目在原版 eIquidus 的基础上进行了深度定制，核心增强了对 **Scash-DAP (Data Availability Protocol)** 的支持，使其能够直接解析和展示链上存储的数据。

## 🚀 主要特性

- **Scash-DAP 支持**: 
    - 自动识别并解析链上 DAP 协议数据。
    - 智能分类交易类型：**Inscription (刻字)** 与 **Transfer Message (转账留言)**。
    - 自动隐藏 DAP 协议地址和平台手续费地址，保持交易列表整洁。
    - 提供 "View Raw Data" 功能，查看原始交易输出和金额详情。
    - 独立展示平台手续费 (Platform Fee) 和 DAP 协议费用 (DAP Fee)。
- **基础浏览器功能**:
    - 区块、交易、地址详情查询。
    - 富豪榜 (Top 100)。
    - 网络状态监控（算力、难度、连接数）。
    - 市场数据集成。
    - 完整的 API 支持。

## 🛠 安装指南

### 先决条件

- **Node.js**: 推荐 v20.9.0 或更新版本。
- **MongoDB**: 推荐 v7.0.2 或更新版本。
- **Scash 节点**: 一个完全同步的 Scash 钱包守护进程，需开启 `txindex=1`。

### 1. 下载源码

```bash
git clone https://github.com/Forlingham/eiquidus.git
cd eiquidus
```

### 2. 安装依赖

```bash
npm install --only=prod
```

### 3. 配置

复制配置文件模板并进行修改：

```bash
cp settings.json.template settings.json
```

编辑 `settings.json`，重点配置以下部分：

- **dbsettings**: MongoDB 连接信息。
- **wallet**: Scash 节点 RPC 连接信息（host, port, user, password）。
- **scash_dap**: DAP 协议参数（默认已配置为 Scash 主网参数）。

### 4. 数据同步

在启动网站前，建议先手动同步数据：

```bash
# 同步区块
npm run sync-blocks

# 同步市场数据（可选）
npm run sync-markets

# 同步节点信息（可选）
npm run sync-peers
```

### 5. 启动浏览器

**测试模式**:
```bash
npm start
```

**生产模式 (使用 PM2)**:
```bash
npm run start-pm2
```

## 📜 常用命令

| 命令 | 描述 |
| :--- | :--- |
| `npm start` | 以前台模式启动浏览器（开发调试用） |
| `npm run start-pm2` | 使用 PM2 后台启动（生产环境推荐） |
| `npm run stop-pm2` | 停止 PM2 进程 |
| `npm run sync-blocks` | 手动同步区块数据 |
| `npm run reindex` | **警告**: 清空数据库并重新同步所有数据 |

## ❤️ 支持项目开发

如果你愿意支持本项目的持续开发与维护，欢迎捐助：

- **BTC**: `bc1qnvdrxs23t6ejuxjs6mswx7cez2rn80wrwjd0u8`
- **BNB**: `0xD4dB57B007Ad386C2fC4d7DD146f5977c039Fefc`
- **USDT (BEP-20)**: `0xD4dB57B007Ad386C2fC4d7DD146f5977c039Fefc`
- **SCASH**: `scash1qy48v7frkutlthqq7uqs8lk5fam24tghjdxqtf5`

你的支持将用于开源维护与基础设施建设，感谢你为 SCASH 社区的建设与创新助力。

## 📄 许可证

本项目遵循 [MIT License](LICENSE) 或原项目许可。
