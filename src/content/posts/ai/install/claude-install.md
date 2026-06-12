---
title: 安装Claude Code
published: 2026-06-12
tags: [Markdown, AI, Claude Code]
category: Install
draft: false
description: 尝试安装Claude Code 进行vibe coding
---

## 前置要求

> [!TIP] 注：安装成功时是这个版本号，以及本文档仅适用于windows

| 软件 | 版本 | 状态 |
|:--|:--|:--:|
| git | 2.53.0.windows.2 | ✅ |
| node | 24.16.0 | ✅ |
| vscode | 1.142.2 | ✅ |
| [CC Switch](./../cc-switch-install/) | 3.16.2 | ✅ |

> [!NOTE] CC Switch 内也可以直接安装Claude但是我没试过
## 1.安装

1. ``win+r`` 输入``cmd``回车
2. 在终端上按住``ctrl``并打开新的终端 (管理员权限)
3. 在终端内执行

    ```ps
    npm config set registry https://registry.npmmirror.com/
    npm config get registry   
    npm install -g @anthropic-ai/claude-code
    ```
4. 等待完成后打开新的终端输入

    ```ps
    claude --version
    ```
    > [!TIP] 显示版本号就说明安装完成

    > [!WARNING] 如果提示"claude不是内部或外部命令"，请重启电脑后再试

## 2.跳过登录

>[!CAUTION] 跳过首次联网校验 (关键！否则还会报地区错误)

``win+r`` 输入``cmd``回车
    ```ps
    md $env:USERPROFILE\.claude 
    echo '{"hasCompletedOnboarding":true}' > $env:USERPROFILE\.claude\settings.json
    ```

## 3.安装技能

> [!CAUTION] 部分技能存储路径比较怪，或者无法搜索到，这种情况直接[网页下载](https://skillsmp.com/zh)压缩包安装

1. 离线安装路径：

    ```ps
    %USERPROFILE%\.claude\skills
    ```
2. 在线安装
    > [!TIP] 安装范围 (推荐选择"User"，全局可用)

    > [!CAUTION] 如遇install无反应则使用离线安装/从vscode使用``/plug``安装
    1. 运行Claude
    2. 安装skill-creator (官方技能创建工具)

        ```ps
        /plugin marketplace add anthropics/skills
        /plugin install skill-creator@anthropics
        
        ```

        * 使用方式："使用skill-creator创建一个名为deploy-check的技能，用于执行部署前检查清单"
        * Claude会自动生成符合官方规范的技能文件结构

3. 安装web-access (网页访问与搜索技能)
    ```ps
    /plugin marketplace add browserbase/skills
    /plugin install browse@browserbase
    ```
    
    * 使用方式："5月1日是什么节日"

4. 安装playwright-cli (浏览器自动化技能)
    > [!TIP] 这里是直接在终端内运行
    ```ps
    npm install -g @playwright/cli@latest
    playwright install chromium
    ```
    > [!CAUTION] 如遇``playwright install`` 报错,使用``playwright-cli install``即可

    > [!TIP] 这里是回到Claude
    ```ps
    playwright-cli install --skills
    ```
    * 使用方式："截取百度首页的截图并保存为baidu.png",这里保存图片可能会报错要多试几次，或者单纯打开浏览器并指定网页
    > [!CAUTION] 会遇到无返回值的问题，详见[第8步](#step-8)

5. 安装superpowers (全流程开发增强技能)
    ```ps
    /plugin marketplace add obra/superpowers-marketplace
    /plugin install superpowers@superpowers-marketplace
    ```
    * 使用方式：直接输入："/brainstorming 用React做一个待办事项应用，支持添加、删除、标记完成"
    * Superpowers会自动引导你完成整个开发流程：
        1. 需求分析与确认
        2. 技术选型与方案设计
        3. 任务拆分与计划制定
        4. 代码编写与实现
        5. 测试验证与代码审查
6. 验证所有技能是否安装成功
    1. 重启Claude
        ```ps
        /skills
        ```
    2. skill-creator、browse、playwright-cli和superpowers都在列表中(如果没找到但是可以打开浏览器,可以搜索那就不管)
    3. 输入以下命令可以查看所有可用插件命令
            ```ps
        /help
        ```
7. 安装常用语言LSP
    >[!TIP] 让Claude code更好的理解代码仓库
    ```ps
    /plugin install typescript-lsp@claude-plugins-official
    /plugin install pyright-lsp@claude-plugins-official
    /plugin install gopls-lsp@claude-plugins-official
    ```
8. <span id='step-8'>安装agnes-ai 的skill(离线安装)</span>
    1. 下载 (百度网盘) [agens-ai](https://pan.baidu.com/s/1HanbDNWAKhZeTayAfHqrSw?pwd=zxe3)
    > [!TIP] @小白Debug 分享的,这里我没搞明白md怎么直接连接到本地文件进行下载所以上传到网盘了
    
    >[!CAUTION] API key是过期的,需要让Claude替换,在生成图片那边会遇到问题
