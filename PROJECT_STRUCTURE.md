# 项目结构说明

```
delivery-management-system/
│
├── backend/                    # 后端代码
│   ├── src/
│   │   └── main.py            # FastAPI主程序
│   ├── config/
│   │   └── users.json         # 用户配置文件
│   ├── requirements.txt        # Python依赖
│   ├── Procfile              # Railway启动文件
│   ├── railway.json          # Railway配置
│   └── .env.example          # 环境变量示例
│
├── frontend/                   # 前端代码
│   └── index.html            # HTML主文件
│
├── README.md                   # 项目说明
├── DEPLOYMENT.md              # 详细部署文档
├── QUICK_START.md             # 快速部署指南
└── .gitignore                 # Git忽略文件
```

## 文件说明

### 后端文件

| 文件 | 说明 | 是否必需 |
|------|------|----------|
| `main.py` | FastAPI应用主程序 | ✅ 必需 |
| `users.json` | 用户账号配置 | ✅ 必需 |
| `requirements.txt` | Python依赖列表 | ✅ 必需 |
| `Procfile` | Railway启动命令 | ✅ 必需 |
| `railway.json` | Railway部署配置 | 推荐 |
| `.env.example` | 环境变量示例 | 参考 |

### 前端文件

| 文件 | 说明 | 是否必需 |
|------|------|----------|
| `index.html` | 系统主界面 | ✅ 必需 |

### 文档文件

| 文件 | 说明 | 是否必需 |
|------|------|----------|
| `README.md` | 项目说明 | ✅ 必需 |
| `DEPLOYMENT.md` | 详细部署文档 | 推荐 |
| `QUICK_START.md` | 快速部署指南 | 推荐 |
| `.gitignore` | Git忽略配置 | 推荐 |

## 环境变量说明

| 变量名 | 说明 | 在哪里获取 |
|--------|------|-----------|
| `COZE_WORKSPACE_PATH` | 工作目录 | 固定值：`/app` |
| `FEISHU_APP_ID` | 飞书应用ID | 飞书开放平台 |
| `FEISHU_APP_SECRET` | 飞书应用密钥 | 飞书开放平台 |
| `BITABLE_APP_TOKEN` | 多维表格ID | 多维表格URL |
| `CUSTOMER_TABLE_ID` | 客户表ID | 多维表格URL |
| `DELIVERY_TABLE_ID` | 配送表ID | 多维表格URL |
| `HOLIDAY_TABLE_ID` | 假期表ID | 多维表格URL |
| `PAUSE_TABLE_ID` | 暂停表ID | 多维表格URL |

## 部署平台

| 组件 | 推荐平台 | 费用 | 说明 |
|------|---------|------|------|
| 前端 | GitHub Pages | 免费 | 自动部署，稳定可靠 |
| 后端 | Railway | 免费额度 | 简单易用，自动部署 |
| 后端 | Render | 免费 | 备选方案 |
| 后端 | PythonAnywhere | 免费 | 备选方案 |

## 技术栈

### 后端
- Python 3.8+
- FastAPI - Web框架
- Requests - HTTP客户端
- Pydantic - 数据验证

### 前端
- HTML5
- CSS3
- JavaScript (原生)

### 数据存储
- 飞书多维表格

### API
- RESTful API
- Token认证