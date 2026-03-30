# 部署完整指南

## 🎯 部署架构

```
GitHub Pages (前端HTML) ←→ Railway/Render (后端API) ←→ 飞书多维表格
        ↓                           ↓                      ↓
   团队访问界面                7x24小时运行            数据存储
        ↓
   飞书工作台集成
```

## 📋 部署步骤概览

1. **后端部署** → Railway/Render（免费）
2. **前端部署** → GitHub Pages（免费）
3. **飞书集成** → 添加到工作台

---

## 第一步：后端部署（Railway）

### 1.1 准备GitHub仓库

1. 在GitHub创建新仓库，例如：`delivery-management-system`
2. 上传以下文件结构：

```
delivery-management-system/
├── backend/
│   ├── src/
│   │   ├── main.py
│   │   └── graphs/
│   │       ├── graph.py
│   │       └── state.py
│   ├── config/
│   │   └── users.json
│   ├── requirements.txt
│   └── Procfile
├── frontend/
│   └── index.html
└── README.md
```

### 1.2 部署到Railway

1. 访问 https://railway.app
2. 使用GitHub账号登录
3. 点击 "New Project" → "Deploy from GitHub repo"
4. 选择您的仓库
5. 配置环境变量：
   - `COZE_WORKSPACE_PATH`: `/app`
   - `FEISHU_APP_ID`: 您的飞书应用ID
   - `FEISHU_APP_SECRET`: 您的飞书应用密钥

6. Railway会自动检测并部署
7. 部署完成后获得URL，例如：`https://delivery-system.railway.app`

---

## 第二步：前端部署（GitHub Pages）

### 2.1 启用GitHub Pages

1. 进入GitHub仓库
2. Settings → Pages
3. Source选择 `Deploy from a branch`
4. Branch选择 `main`，文件夹选择 `/ (root)`
5. 保存

### 2.2 获得访问地址

GitHub Pages会提供地址，例如：
`https://yourusername.github.io/delivery-management-system`

---

## 第三步：飞书集成

### 3.1 创建飞书应用

1. 访问 https://open.feishu.cn/app
2. 点击"创建企业自建应用"
3. 应用名称：配送管理系统
4. 应用描述：配送管理系统
5. 上传应用图标

### 3.2 配置应用主页

1. 进入应用 → 应用功能 → 网页
2. 配置桌面端主页：
   ```
   https://yourusername.github.io/delivery-management-system/frontend/index.html
   ```
3. 配置移动端主页（同上）

### 3.3 配置权限

1. 进入应用 → 权限管理
2. 搜索并开通以下权限：
   - `bitable:record:read` - 读取多维表格记录
   - `bitable:record:write` - 写入多维表格记录
   - `bitable:app:read` - 读取多维表格应用信息

### 3.4 发布应用

1. 进入应用 → 版本管理与发布
2. 点击"创建版本"
3. 填写版本号和描述
4. 点击"申请发布"
5. 管理员审核通过后即可使用

### 3.5 添加到工作台

1. 飞书管理后台 → 工作台
2. 点击"添加应用"
3. 搜索"配送管理系统"
4. 添加到工作台

---

## 第四步：配置前端

### 4.1 修改API地址

编辑 `frontend/index.html`，找到以下代码：

```javascript
// 第288行左右
const API_URL = 'https://delivery-system.railway.app';
```

改为您的Railway地址。

### 4.2 重新部署

提交代码到GitHub，GitHub Pages会自动更新。

---

## 📝 完整文件清单

### backend/requirements.txt

```txt
fastapi==0.104.1
uvicorn==0.24.0
pydantic==2.5.0
requests==2.31.0
python-multipart==0.0.6
lark-oapi==1.2.15
```

### backend/Procfile

```
web: python src/main.py -m http -p $PORT
```

### backend/src/main.py（核心代码）

已包含在项目中，包含：
- CORS支持
- 用户登录验证
- API接口
- 飞书多维表格集成

### frontend/index.html（完整HTML）

已包含登录功能和主界面。

---

## 🔧 环境变量配置

在Railway中设置以下环境变量：

| 变量名 | 说明 | 示例 |
|--------|------|------|
| `PORT` | 端口号 | 自动设置 |
| `COZE_WORKSPACE_PATH` | 工作目录 | `/app` |
| `FEISHU_APP_ID` | 飞书应用ID | cli_xxx |
| `FEISHU_APP_SECRET` | 飞书应用密钥 | xxx |

---

## 📊 飞书多维表格配置

### 表格结构

请确保飞书多维表格包含以下表格：

1. **客户订单表**
   - 客户姓名（文本）
   - 电话（文本）
   - 地址（文本）
   - 总餐数（数字）
   - 已吃餐数（数字）
   - 起送日期（日期）
   - 预计结束日期（日期）
   - 配送状态（单选）

2. **配送记录表**
   - 配送日期（日期）
   - 客户姓名（文本）
   - 配送数量（数字）
   - 是否已确认（复选框）

3. **公共假期表**
   - 日期（日期）
   - 说明（文本）

4. **客户暂停表**
   - 客户姓名（关联字段）
   - 开始日期（日期）
   - 结束日期（日期）

### 获取表格ID

1. 打开飞书多维表格
2. 点击右上角"..."
3. 选择"获取表格链接"
4. 从链接中提取：
   - `app_token`: 多维表格ID
   - `table_id`: 数据表ID

---

## 🎉 完成！

部署完成后：

1. ✅ 团队成员在飞书工作台找到"配送管理系统"
2. ✅ 点击打开，输入账号密码登录
3. ✅ 随时随地使用系统
4. ✅ 数据实时同步到飞书多维表格

---

## ❓ 常见问题

### Q1: Railway部署失败？
- 检查`requirements.txt`是否完整
- 检查`Procfile`格式是否正确
- 查看Railway日志排查错误

### Q2: 飞书应用无法打开？
- 检查GitHub Pages是否启用
- 检查URL是否正确
- 确认应用已发布

### Q3: API调用失败？
- 检查飞书权限是否开通
- 检查环境变量是否正确
- 查看后端日志

### Q4: 数据不同步？
- 检查飞书多维表格ID是否正确
- 检查API权限配置
- 确认字段名称匹配