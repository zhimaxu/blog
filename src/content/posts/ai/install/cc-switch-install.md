---
title: 安装CC Switch
published: 2026-06-12
tags: [Markdown, AI, CC Switch]
category: Install
draft: false
---
## 1.下载

> [!IMPORTANT] 从[CC SWitch](https://github.com/farion1231/cc-switch/releases)下载对应安装包

> [!TIP] 注：[Github Proxy](https://github.akams.cn/) 代理加速

## 2.安装

> [!NOTE] 没什特殊的

## 3.配置

> [!NOTE] 本地<strong>ollama</strong>&&<strong>Agnes AI</strong>

### 3.1本地Ollama

1. 打开CC Switch右上角添加供应商
2. 下滑自定义供应商
   ![step 1](/public/assets/images/ai/install/cc-switch-step-1.png)
   ![step 2](/public/assets/images/ai/install/cc-switch-step-2.png)

3. 模型可以获取后再设置无需手动输入

### 3.2本地Agnes AI

> [!NOTE] 注：当前Agens AI是全球Top 10的AI实验室推出的全模态大模型，<strong>无限期免费</strong>，支持文本、图片、视频全模态，在多个权威评测榜单上跑分超过GPT 5.4和DeepSeek V4 Pro

1. [注册Agens AI 账号](https://agnes-ai.com/)
2. 点击右上角的"进入API平台"按钮，或 [直接访问](https://platform.agnes-ai.com/)
3. 使用邮箱、Google或GitHub账号快速注册登录（无需绑定银行卡）
4. 登录后，点击左侧导航栏的"API Keys"（API密钥）
5. 点击"创建新的密钥"按钮
6. 输入一个名称（如"Claude Code"），然后点击"创建"
7. 复制生成的API Key（以sk-开头），妥善保存，关闭窗口后可在操作处直接复制
8. 打开CC Switch右上角添加供应商
   ![step 3](/public/assets/images/ai/install/cc-switch-step-3.png)
   ![step 4](/public/assets/images/ai/install/cc-switch-step-4.png)

9. 模型可以获取后再设置无需手动输入

### 3.3 CC Switch 启动路由

1. 左上角设置
 ![step 5](/public/assets/images/ai/install/cc-switch-step-4.png)

#### 3.3.1 验证配置是否成功

1. ``win+r`` 输入``cmd`` 回车
2. 在终端内输入``claude``回车
3. 启动后输入一个简单的问题测试,例如："5月1日是什么节日"
4. 如果Claude Code 能够正常回复,说明配置成功！
5. 实用技巧1：不想一直确认权限可以：

    ```ps
    claude --dangerously-skip-permissions
    ```

    或者在配置json中添加
    
    ```json
    "skipDangerousModePermissionPrompt": true,
    ```
#### 4.异常问题处理
1. 访问异常：配置json中添加
    
    ```json
    "skipWebFetchPreflight": true,
    ```

    >[!IMPORTANT]因为Claude Code在访问网页前会调用 Anthropic 的服务来判断网页是否可以访问,这里直接给他权限读取全部的域名访问,就没有限制了
