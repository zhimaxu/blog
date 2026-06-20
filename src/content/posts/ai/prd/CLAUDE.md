# 智能客服系统 — 项目上下文

> 基于 Agnes AI 多模态模型（文本、图像、视频、语音），使用 Vue 3 + FastAPI 前后端分离架构，构建支持多租户 SaaS 化部署、多渠道接入、工单流转的企业级 AI 智能客服系统。

---

## 产品定位

面向中小企业的 AI 智能客服 SaaS 平台。帮助商家降低 60% 客服成本，提供 7×24 小时服务。

**北极星指标**：每日活跃对话数（Daily Active Conversations）

---

## 技术栈

| 层级 | 技术 |
|:--|:--|
| 前端 | Vue 3 + Vite + Element Plus + ECharts |
| 后端 | Python FastAPI + SQLAlchemy + Pydantic |
| 数据库 | MySQL 8.0（多租户隔离） |
| 向量数据库 | Qdrant（知识库语义检索） |
| 缓存 | Redis |
| 消息队列 | RabbitMQ + Celery |
| AI 模型 | Agnes AI（文本/图像/视频/语音，可动态配置） |
| 部署 | Docker + Docker Compose + Nginx |

---

## 核心架构（五层）

```
渠道层（网站/小程序/App/PC）
  → 前端层（Vue 3 SPA）
  → 后端层（FastAPI + WebSocket）
  → AI 服务层（Agnes AI 多模态模型）
  → 数据层（MySQL + Qdrant + Redis）
```

---

## MoSCoW 优先级

### ✅ Must Have（MVP 必须包含）

| 功能 | 验收标准 |
|------|---------|
| AI 自动问答 | 消息 3s 内返回 AI 回复，准确率 > 80% |
| 知识库管理 | 支持 Markdown/PDF 导入，100 篇文档检索 < 1s |
| 转人工 | 点击转人工后 10s 内有人工客服接入 |
| 客服工作台 | 支持至少 5 个并发会话，消息实时推送 |
| 数据分析 | 对话量、满意度、响应时长实时可查 |

### 🔶 Should Have（MVP 后可迭代）

图片/视频理解、工单系统、多租户管理、满意度评价、快捷回复

### 🔷 Could Have（有余力再做）

语音能力、OCR 识别、埋点分析、国际化、PC 客户端

### ❌ Won't Have

电话客服接入、视频通话、自研大模型

---

## 开发阶段

### Phase 1：后端骨架（2-3 天）
FastAPI + MySQL + Qdrant + Agnes AI 封装 + Docker Compose

### Phase 2：聊天核心（2-3 天）
POST /api/chat + 会话管理 + 多轮对话 + SSE 流式

### Phase 3：知识库管理（2-3 天）
文档导入 + 分块 + embedding + Qdrant 向量检索

### Phase 4：前端聊天（2-3 天）
Vue 3 聊天界面 + SSE/WebSocket + 文件上传

### Phase 5：客服工作台（3-4 天）
会话列表 + 聊天详情 + 主动接管 + 快捷回复

### Phase 6：数据分析（2-3 天）
对话统计 + 满意度 + 评分统计 + 效率统计

---

## 关键 API

| 方法 | 路径 | 说明 |
|:--|:--|:--|
| POST | `/api/chat` | 发送消息，返回 AI 回复 |
| WS | `/ws/chat/{id}` | WebSocket 实时通信 |
| POST | `/api/knowledge` | 导入/更新知识库 |
| POST | `/api/tools/convert` | 文件转 Markdown |
| GET | `/api/agent/sessions` | 获取会话列表 |
| POST | `/api/agent/sessions/:id/takeover` | 客服接管 |
| GET | `/api/agent/ratings` | 评分统计 |
| GET | `/api/agent/efficiency` | 效率统计 |
| POST | `/api/tickets` | 创建工单 |
| POST | `/api/admin/login` | 管理员登录 |

---

## 数据模型要点

- **20 张核心表**，按类别分 7 组（租户/权限/会话/工单/知识库/配置/统计）
- 所有业务表含 `tenant_id` 字段，多租户数据隔离
- 共享表模式（免费/标准）vs 独立数据库模式（专业/企业）
- Qdrant 存储知识库向量化文档，payload 含 tenant_id 隔离

---

## 非功能需求

- 消息响应 < 3s，P95 < 5s
- 支持并发 ≥ 1000 用户
- 系统可用性 ≥ 99.9%
- 租户数据严格隔离，JWT 鉴权
- 对话数据保留 90 天后归档，压缩文件保留 180 天

---

## 参考文档

- 详细 PRD：[ai-customer-service-v3.md](ai-customer-service-v3.md)
- 开发路线图：[vibe-coding-roadmap.md](vibe-coding-roadmap.md)
- 原型图：[product-prototype/](product-prototype/)
- SVG 图表：[svg/](svg/)
