# 智能客服系统 Vibe Coding 准备流程

基于 [ai-customer-service-v3.md](ai-customer-service-v3.md) 的 MoSCoW 优先级，分阶段推进开发。

---

## 阶段规划

### Phase 1：后端骨架（2-3 天）

搭建 FastAPI + MySQL + Qdrant + Agnes AI 接入的基础设施。

**工作内容：**
- 初始化 FastAPI 项目结构
- 配置 MySQL 连接池、ORM（SQLAlchemy）
- 配置 Qdrant 客户端
- 封装 Agnes AI 多模型调用（文本/图像/视频/语音）
- 实现 AI 模型动态配置读取（从 MySQL `system_config` 表）
- 编写 Docker Compose 编排文件（MySQL + Qdrant + Redis + RabbitMQ）

**关键文件：**
- `backend/app/main.py` — FastAPI 入口
- `backend/app/core/config.py` — 配置管理
- `backend/app/core/database.py` — 数据库连接
- `backend/app/core/qdrant_client.py` — 向量数据库客户端
- `backend/app/services/agnes_ai.py` — Agnes AI 封装
- `docker-compose.yml` — 服务编排

---

### Phase 2：聊天核心（2-3 天）

打通「用户发消息 → AI 回复」的最小闭环。

**工作内容：**
- 实现 `POST /api/chat` 接口（SSE 流式输出）
- 实现会话管理（创建/获取/关闭会话）
- 实现多轮对话上下文管理（最近 N 轮消息）
- 实现消息持久化（MySQL `message` 表）
- 实现知识库检索路由（先查 Qdrant，再调 LLM）
- 编写单元测试

**关键 API：**
- `POST /api/chat` — 发送消息，返回 AI 回复（SSE 流式）
- `GET /api/session/{id}` — 获取会话详情
- `POST /api/session` — 创建新会话

---

### Phase 3：知识库管理（2-3 天）

实现文档导入和向量化检索。

**工作内容：**
- 实现 Markdown 文件导入接口
- 实现文档分块（chunk）逻辑
- 实现 embedding 调用（Agnes 图像模型也可用于 embedding）
- 实现 Qdrant 向量存储和检索
- 实现按分类/标签检索
- 实现文件转换工具（PDF/Word/Excel → Markdown）

**关键 API：**
- `POST /api/knowledge` — 导入/更新知识库
- `GET /api/knowledge` — 获取知识库列表
- `DELETE /api/knowledge/:id` — 删除知识库条目
- `POST /api/tools/convert` — 文件转 Markdown

---

### Phase 4：前端聊天界面（2-3 天）

实现用户侧的聊天交互界面。

**工作内容：**
- 初始化 Vue 3 + Vite + Element Plus 项目
- 实现聊天窗口组件（消息气泡、输入框、发送按钮）
- 实现 SSE/WebSocket 实时接收 AI 回复
- 实现图片/视频上传组件
- 实现转人工按钮
- 实现多语言切换（预留国际化接口）

**关键组件：**
- `ChatWindow.vue` — 聊天主界面
- `MessageBubble.vue` — 消息气泡
- `FileUpload.vue` — 文件上传组件
- `TransferToHuman.vue` — 转人工按钮

---

### Phase 5：转人工 + 客服工作台（3-4 天）

实现人工客服介入和后台管理界面。

**工作内容：**
- 实现 WebSocket 实时推送（新消息通知）
- 实现会话列表（左侧）+ 聊天详情（右侧）
- 实现客服主动接管功能
- 实现快捷回复功能
- 实现多会话并发（Tab 标签页）
- 实现用户信息面板（右侧边栏）

**关键 API：**
- `GET /api/agent/sessions` — 获取会话列表
- `POST /api/agent/sessions/:id/takeover` — 客服接管
- `WS /ws/chat/{sessionId}` — WebSocket 实时通信

---

### Phase 6：数据分析看板（2-3 天）

实现对话统计、满意度、效率统计。

**工作内容：**
- 实现对话统计接口（今日/本周/本月趋势）
- 实现常见问题 Top 10 统计
- 实现满意度评分统计
- 实现评分统计（日/周/月/季度/年，AI vs 人工对比）
- 实现效率统计（首响时间、平均响应时间、解决率）
- 前端数据可视化（ECharts / Chart.js）

**关键 API：**
- `GET /api/stats/chat` — 对话统计
- `GET /api/stats/satisfaction` — 满意度统计
- `GET /api/agent/ratings` — 评分统计
- `GET /api/agent/efficiency` — 效率统计

---

## 第二阶段：Should Have（MVP 后可迭代）

| 功能 | 说明 | 工作量 |
|:--|:--|:--|
| 图片/视频理解 | 调用 Agnes 图像/视频模型 | 1-2 天 |
| 工单系统 | 基础流转 + SLA 提醒 | 3-4 天 |
| 多租户（共享表） | tenant_id 隔离 | 2-3 天 |
| 满意度评价 | 对话后弹窗评分 | 1 天 |
| 快捷回复 | 预设话术管理 | 1-2 天 |

---

## 第三阶段：Could Have（有余力再做）

| 功能 | 说明 | 工作量 |
|:--|:--|:--|
| 语音能力 | ASR + TTS | 3-4 天 |
| OCR 识别 | 截图文字识别 | 2 天 |
| 埋点分析 | 用户行为追踪 | 2-3 天 |
| 国际化 | 中/英/日 | 2-3 天 |
| PC 客户端 | Electron 桌面版 | 5-7 天 |

---

## 开发顺序建议

```
Phase 1 (后端骨架)
    ↓
Phase 2 (聊天核心) ← 此时可演示：发消息 → AI 回复
    ↓
Phase 3 (知识库)   ← 此时可演示：导入文档 → AI 基于文档回答
    ↓
Phase 4 (前端聊天) ← 此时可演示：完整聊天界面
    ↓
Phase 5 (客服工作台) ← 此时可演示：转人工 + 客服介入
    ↓
Phase 6 (数据分析)   ← MVP 完成，可上线
    ↓
第二阶段：工单/多租户/满意度
    ↓
第三阶段：语音/OCR/国际化
```

---

## 技术栈总览

| 层级 | 技术 |
|:--|:--|
| 前端 | Vue 3 + Vite + Element Plus + ECharts |
| 后端 | Python FastAPI + SQLAlchemy + Pydantic |
| 数据库 | MySQL 8.0 |
| 向量数据库 | Qdrant |
| 缓存 | Redis |
| 消息队列 | RabbitMQ + Celery |
| AI 模型 | Agnes AI（文本/图像/视频/语音，可动态配置） |
| 部署 | Docker + Docker Compose + Nginx |
