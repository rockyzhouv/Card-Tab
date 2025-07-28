# Card-Tab 书签卡片式管理，进入管理模式可以自由移动书签位置，添加和删除书签，支持自定义网站分类，支持切换暗色主题

> **Fork from**: [hmhm2022/Card-Tab](https://github.com/hmhm2022/Card-Tab) - 原项目地址

### [当前版本] - 2025.06.01
## ✨ 核心功能

### 🎨 界面设计
- **现代化视觉**：采用 Segoe UI 字体系统，米白色/深色双主题
- **卡片式布局**：美观的书签卡片，支持左侧装饰条和悬停效果
- **响应式设计**：完美适配桌面端和移动端设备
- **暗色主题**：一键切换，护眼舒适的夜间模式

### 🔍 搜索功能
- **多引擎搜索**：支持百度、必应、谷歌、DuckDuckGo
- **书签搜索**：快速搜索已保存的书签名称和网址
- **分类导航**：快捷按钮一键跳转到指定分类
- **智能高亮**：自动高亮当前可见分类

### 📚 书签管理
- **分类管理**：自定义分类，支持重命名和排序
- **卡片编辑**：修改名称、网址、描述和自定义图标
- **私密书签**：登录后可见的私密书签功能
- **拖拽排序**：直观的拖拽操作调整书签顺序

### 🔐 安全特性
- **JWT验证**：基于Token的身份验证机制
- **自动过期**：15分钟登录超时，保护隐私安全
- **自动备份**：KV存储保留最近10次数据备份
- **权限控制**：公开/私密书签分级管理

### 📱 用户体验
- **自定义图标**：支持图片URL链接，个性化书签外观
- **悬停提示**：鼠标悬停显示书签详细描述
- **返回顶部**：便捷的页面导航功能
- **加载动画**：流畅的交互反馈和视觉效果

📋 **查看完整更新历史**: [CHANGELOG.md](./CHANGELOG.md)

### 注意：如果你已经部署过第一版（20240902）导航，更新workes代码后将无法看到之前保存的书签，需重新添加书签，望知悉！

#### 2024.09.02 发布 （第一版很轻便，代码保留在history下）

#### 演示站点：  https://demo.usgk.dpdns.org   备用网址：https://demo.linuxdo.nyc.mn   密码：admin

#### 20250429 更新界面：
![1745910265848](https://github.com/user-attachments/assets/bce632fc-d61c-4efe-a74e-e416cab085b8)

#### 未登录界面
![image](https://github.com/user-attachments/assets/dd0cad75-11ce-4691-804f-b4dff5ae2cde)

#### 已登录界面（黑暗主题）
![image](https://github.com/user-attachments/assets/c18f0df4-8e00-45e6-84db-30f81b545d15)

#### 设置界面
![image](https://github.com/user-attachments/assets/dc91458a-840c-41f9-9e50-261471320f81)



# 部署方法：

## 🚀 快速部署（推荐）

### 方法一：Git 自动构建部署（推荐）
1. **Fork 本仓库**到你的 GitHub 账户
2. **登录 Cloudflare Dashboard**：https://dash.cloudflare.com
3. **创建新的 Worker**，选择 **Deploy** > **Connect to Git**
4. **连接 GitHub 仓库**，选择你的 Fork 仓库
5. **配置构建设置**：
   - Root directory: `/`
   - Build command: 留空
   - Install command: 留空
6. **在 Dashboard 中配置**：
   - 创建 KV 命名空间：`CARD_ORDER`
   - 设置环境变量：`ADMIN_PASSWORD` (Secret)
   - 绑定 KV 存储到 Worker
7. **部署完成**：推送到 `main` 分支即可自动部署

详细配置请参考：[DEPLOYMENT.md](./DEPLOYMENT.md)

### 方法二：手动部署
#### 五步即可完成部署：
#### 1. 登录 Cloudflare：  https://www.cloudflare.com  创建workers，复制 workers.js 的代码，然后部署
![image](https://github.com/user-attachments/assets/c067105b-91ee-43d5-90a9-806e5de5fe16)

#### 2. 新建一个名为CARD_ORDER的KV存储
![image](https://github.com/user-attachments/assets/706a7735-b47a-4f66-bdb4-827c38be692b)

#### 3. 添加环境变量，用于设置后台管理密码。变量名为ADMIN_PASSWORD，值your_password换成你自己的密码
![image](https://github.com/user-attachments/assets/532dcb8f-dc30-4ca9-aac9-21ef546bf367)

#### 4. 将workers的CARD_ORDER变量与新建的KV存储绑定，用于存储书签
![image](https://github.com/user-attachments/assets/9b166809-5b1e-451e-be99-253f6e60be54)

#### 5. 添加域名
![image](https://github.com/user-attachments/assets/4f23eab6-e94c-49b1-9198-3c8e05dffa8a)

## 此项目适合轻量使用，各位随意自行魔改，喜欢的话点一下小星星就行，谢谢！
