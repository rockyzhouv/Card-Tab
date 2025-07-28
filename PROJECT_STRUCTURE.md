# 项目结构说明

## 📁 核心文件

### `workers.js`
- **作用**: Cloudflare Workers 主程序文件
- **功能**: 包含完整的 Web 应用逻辑，包括前端 HTML/CSS/JS 和后端 API
- **大小**: ~134KB，包含 4275 行代码
- **特点**: 单文件应用，无需构建步骤

### `wrangler.toml`
- **作用**: Cloudflare Workers 配置文件
- **功能**: 定义 Worker 名称、入口文件、KV 绑定、环境变量等
- **要求**: 必须与 Cloudflare Dashboard 中的 Worker 名称一致



## 📁 配置文件

### `.gitignore`
- **作用**: Git 忽略文件配置
- **内容**: 排除 node_modules、临时文件、敏感配置等



## 📁 文档文件

### `README.md`
- **作用**: 项目主要说明文档
- **内容**: 功能介绍、部署方法、演示站点等

### `DEPLOYMENT.md`
- **作用**: 详细部署指南
- **内容**: Git 自动构建部署配置、故障排除等

### `CHANGELOG.md`
- **作用**: 版本更新历史
- **内容**: 各版本的功能更新和修复记录

### `PROJECT_STRUCTURE.md`
- **作用**: 项目结构说明（本文件）
- **内容**: 各文件和目录的作用说明

## 📁 历史文件

### `history/`
- **作用**: 存放历史版本的代码
- **内容**: 不同日期的 workers.js 版本备份

## 📁 浏览器扩展

### `bookmarks-export-addons/`
- **作用**: 书签导出浏览器扩展
- **功能**: 帮助用户导出浏览器书签到 Card-Tab

### `bookmarks export script/`
- **作用**: 书签导出脚本
- **功能**: 独立的书签导出工具

## 📁 CI/CD 配置



## 🔧 部署相关

### 环境要求
- **Cloudflare Account**: 需要有效的 Cloudflare 账户
- **Wrangler CLI**: 可选，用于本地开发和手动部署

### 必需配置
1. **KV 存储**: 在 Cloudflare Dashboard 中创建名为 `CARD_ORDER` 的 KV 命名空间
2. **环境变量**: 在 Dashboard 中设置 `ADMIN_PASSWORD` 为 Secret
3. **Worker 名称**: 与 wrangler.toml 中的 name 字段一致

### 部署方式
1. **Git 自动构建**: 推荐，支持自动部署
2. **手动部署**: 使用 wrangler CLI 工具

## 📝 注意事项

1. **Worker 名称**: 必须与 Cloudflare Dashboard 中的名称一致
2. **KV 绑定**: 确保 KV 命名空间正确创建和绑定
3. **环境变量**: 敏感信息应设置为 Secret
4. **兼容性**: 使用 compatibility_date 确保功能兼容性
5. **构建**: 无需构建步骤，直接部署 workers.js 文件 