# 🚀 快速部署指南

## 📋 部署前准备

### 1. 获取飞书多维表格ID

1. 打开您的飞书多维表格
2. 点击右上角 `...` → `获取表格链接`
3. 从链接中提取以下ID：
   ```
   例如链接：https://xxx.feishu.cn/base/XXXXXX?table=tblYYYYYY
   
   BITABLE_APP_TOKEN = XXXXXX (base/后面的部分)
   CUSTOMER_TABLE_ID = tblYYYYYY (table=后面的部分)
   ```

### 2. 创建飞书应用

1. 访问 https://open.feishu.cn/app
2. 点击"创建企业自建应用"
3. 应用名称：配送管理系统
4. 应用类型：企业自建应用
5. 创建完成后获取：
   - App ID
   - App Secret

### 3. 配置应用权限

在飞书应用管理页面：

1. 进入"权限管理"
2. 搜索并开通：
   - `bitable:record:read` - 读取记录
   - `bitable:record:write` - 写入记录
   - `bitable:app:read` - 读取应用信息

---

## 🎯 第一步：部署后端（Railway）

### 1.1 创建GitHub仓库

```bash
# 1. 在GitHub创建新仓库
# 仓库名：delivery-management-system

# 2. 克隆仓库到本地
git clone https://github.com/你的用户名/delivery-management-system.git
cd delivery-management-system

# 3. 复制项目文件到仓库
# 复制 backend/ 和 frontend/ 文件夹
# 复制 README.md, .gitignore, DEPLOYMENT.md

# 4. 提交代码
git add .
git commit -m "初始化项目"
git push origin main
```

### 1.2 部署到Railway

1. 访问 https://railway.app
2. 使用GitHub账号登录
3. 点击 `New Project` → `Deploy from GitHub repo`
4. 选择您的仓库 `delivery-management-system`
5. 设置根目录为 `/backend`
6. 配置环境变量：
   ```
   COZE_WORKSPACE_PATH=/app
   FEISHU_APP_ID=cli_xxxxxxxxxx
   FEISHU_APP_SECRET=xxxxxxxx
   BITABLE_APP_TOKEN=xxxxxxxx
   CUSTOMER_TABLE_ID=tblxxxxxx
   DELIVERY_TABLE_ID=tblxxxxxx
   HOLIDAY_TABLE_ID=tblxxxxxx
   PAUSE_TABLE_ID=tblxxxxxx
   ```
7. 点击 `Deploy`
8. 等待部署完成，获得URL：
   ```
   https://delivery-management-system-production.up.railway.app
   ```

### 1.3 测试API

访问：`https://你的域名.railway.app/health`

应该返回：
```json
{"status":"ok","message":"Service is running"}
```

---

## 🎨 第二步：部署前端（GitHub Pages）

### 2.1 修改API地址

编辑 `frontend/index.html`，找到第288行：

```javascript
const DEFAULT_API_URL = 'https://your-app.railway.app';
```

改为您的Railway地址：

```javascript
const DEFAULT_API_URL = 'https://delivery-management-system-production.up.railway.app';
```

### 2.2 启用GitHub Pages

1. 进入GitHub仓库
2. `Settings` → `Pages`
3. Source选择 `Deploy from a branch`
4. Branch选择 `main`，文件夹选择 `/(root)`
5. 点击 `Save`

### 2.3 获得访问地址

GitHub Pages会提供地址：
```
https://你的用户名.github.io/delivery-management-system/frontend/
```

---

## 📱 第三步：集成到飞书

### 3.1 配置应用主页

1. 进入飞书应用管理
2. 进入"应用功能" → "网页"
3. 配置桌面端主页：
   ```
   https://你的用户名.github.io/delivery-management-system/frontend/
   ```
4. 配置移动端主页（同上）

### 3.2 发布应用

1. 进入"版本管理与发布"
2. 点击"创建版本"
3. 填写版本号：`1.0.0`
4. 填写版本描述：`初始化版本`
5. 点击"申请发布"

### 3.3 添加到工作台

1. 飞书管理后台 → 工作台
2. 点击"添加应用"
3. 搜索"配送管理系统"
4. 添加到工作台

---

## ✅ 部署完成！

### 测试流程

1. 在飞书工作台找到"配送管理系统"
2. 点击打开
3. 输入账号密码：
   - 用户名：`admin`
   - 密码：`admin123`
4. 登录成功后即可使用

### 团队成员使用

团队成员在飞书工作台找到应用，使用分配的账号密码登录即可。

---

## ❓ 常见问题

### Q1: Railway部署失败？

检查：
- `backend/requirements.txt` 是否存在
- `backend/Procfile` 格式是否正确
- 环境变量是否配置完整

查看Railway日志：
1. 进入项目 → `Deployments`
2. 点击最新部署
3. 查看 `Build Logs` 和 `Deploy Logs`

### Q2: 飞书应用无法打开？

检查：
- GitHub Pages是否已启用
- URL是否正确（注意结尾的 `/frontend/`）
- 应用是否已发布

### Q3: API调用失败？

检查：
- Railway应用是否正常运行
- 飞书应用权限是否已开通
- 环境变量是否正确

### Q4: 数据不同步？

检查：
- 多维表格ID是否正确
- 表格字段名称是否匹配
- 飞书应用是否有权限访问表格

---

## 📝 修改账号密码

编辑 `backend/config/users.json`：

```json
{
  "users": [
    {
      "username": "新用户名",
      "password": "新密码",
      "role": "管理员"
    }
  ]
}
```

提交代码后Railway会自动重新部署。

---

## 🔧 后续维护

### 更新代码

```bash
git add .
git commit -m "更新说明"
git push origin main
```

Railway和GitHub Pages会自动更新。

### 查看日志

Railway控制台 → 项目 → `Deployments` → 点击部署 → `Logs`

---

**恭喜！您的配送管理系统已成功部署！** 🎉