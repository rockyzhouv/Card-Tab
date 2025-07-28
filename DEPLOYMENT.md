# Cloudflare Workers 部署指南

## 项目配置要求

根据 [Cloudflare Workers 构建故障排除文档](https://developers.cloudflare.com/workers/ci-cd/builds/troubleshoot/#workers-name-requirement)，项目已配置以下必要文件：

### 1. wrangler.toml 配置
- ✅ `name = "card-tab"` - Worker名称配置
- ✅ `main = "workers.js"` - 入口文件配置
- ✅ `compatibility_date` - 兼容性日期设置
- ✅ KV存储绑定配置
- ✅ 环境变量配置
- ✅ 多环境部署配置



## 部署前准备

### 1. 创建 KV 存储
在 Cloudflare Dashboard 中创建 KV 命名空间：

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com)
2. 进入 **Workers & Pages**
3. 选择 **KV** 标签页
4. 点击 **Create a namespace**
5. 输入名称：`CARD_ORDER`
6. 复制生成的 KV ID

### 2. 配置 KV 存储和环境变量
**注意**：这些配置在 Cloudflare Dashboard 中设置，不需要修改 wrangler.toml 文件。

在 Cloudflare Dashboard 中：
1. 创建 KV 命名空间：`CARD_ORDER`
2. 设置环境变量：`ADMIN_PASSWORD` (Secret)
3. 绑定 KV 存储到 Worker



## Git 自动构建部署配置

### 1. 连接 Git 仓库
1. 在 Cloudflare Dashboard 中创建新的 Worker
2. 选择 **Deploy** > **Connect to Git**
3. 选择 GitHub 或 GitLab
4. 授权访问你的仓库
5. 选择 `Card-Tab` 仓库

### 2. 配置构建设置
在 **Settings** > **Build** > **Build Configuration** 中：

- **Root directory**: `/` (项目根目录)
- **Build command**: 留空（无需构建步骤）
- **Output directory**: 留空
- **Install command**: 留空（无需安装依赖）

### 3. 配置环境变量和 KV 绑定
在 **Settings** > **Variables** 中：
- 添加 `ADMIN_PASSWORD` 作为 Secret 环境变量

在 **Settings** > **KV Namespace Bindings** 中：
- 绑定 `CARD_ORDER` 到创建的 KV 命名空间

### 4. 配置 API Token
1. 在 **Account Home** > **API Tokens** 中创建新 Token
2. 权限：**Workers Scripts:Edit**
3. 在构建配置中选择该 Token

## 部署流程

### 自动部署
- 推送到 `main` 分支 → 自动部署到生产环境
- 推送到其他分支 → 创建预览部署

### 手动部署
```bash
# 使用 wrangler CLI 部署
wrangler deploy

# 部署到生产环境
wrangler deploy --env production

# 部署到测试环境
wrangler deploy --env staging
```

## 故障排除

### 常见错误及解决方案

1. **Worker 名称不匹配**
   ```
   ✘ [ERROR] The name in your wrangler.toml file must match the name of your Worker
   ```
   - 确保 Cloudflare Dashboard 中的 Worker 名称与 `wrangler.toml` 中的 `name` 字段一致

2. **缺少 wrangler.toml**
   ```
   ✘ [ERROR] Missing entry-point
   ```
   - 确保 `wrangler.toml` 文件在项目根目录

3. **账户 ID 错误**
   ```
   Could not route to /client/v4/accounts/<Account ID>/workers/services/<Worker name>
   ```
   - 移除 `wrangler.toml` 中的 `account_id` 字段，让系统自动检测

4. **API Token 过期**
   ```
   Failed: The build token selected for this build has been deleted or rolled
   ```
   - 创建新的 API Token 并更新构建配置

5. **构建超时**
   ```
   Build was timed out
   ```
   - 构建时间超过20分钟限制，检查构建配置

## 验证部署

部署成功后，访问以下URL验证：
- 生产环境：`https://card-tab.your-subdomain.workers.dev`
- 测试环境：`https://card-tab-staging.your-subdomain.workers.dev`

## 注意事项

1. **安全性**：确保 `ADMIN_PASSWORD` 设置为 Secret 环境变量
2. **KV 存储**：确保 KV 命名空间正确创建和绑定
3. **权限**：确保 API Token 具有足够的权限
4. **分支策略**：建议使用 `main` 分支作为生产环境，其他分支用于测试

## 支持

如遇到问题，请参考：
- [Cloudflare Workers 文档](https://developers.cloudflare.com/workers/)
- [构建故障排除指南](https://developers.cloudflare.com/workers/ci-cd/builds/troubleshoot/)
- [Cloudflare Developers Discord](https://discord.gg/cloudflaredev) 