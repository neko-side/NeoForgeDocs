# NeoForged 非官方中文文档

该仓库用于存储 NeoForge 文档的一个个人中文 fork. 同时包含 NeoGradle(NeoForge 的 Gradle 插件) 文档.

本文档基于 [Docusaurus 3](https://docusaurus.io)

## 贡献

你可以阅读 [contribution guidelines on the docs](https://docs.neoforged.net/contributing/).

如果你希望贡献该文档, fork 并 clone 此仓库.

本文档使用 Node.js 18. 可以手动安装或使用支持 `.node-version` 或 `.nvmrc` 的 Node 版本管理器. 对于大部分 Node 版本管理器, `install` 和/或 `use` 可用于安装正确的 Node.js 版本.

例如:

```bash
nvm install # 或 'nvs use'
```

你可以运行以下命令 如果你希望通过开发服务器在本地预览文档. 大部分的改变会立即生效而无需重启服务器.

```bash
npm install
npm run start
```

### 构建

如果你希望构建可以部署的静态文档, 运行以下命令:

```bash
npm run build
```

该命令会在 `build` 目录生成静态内容，可以被托管在任意内容托管服务.
