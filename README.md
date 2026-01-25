# Hexo Theme MK

<div align="center">
  <img src="https://www.xudu.org/images/2026/01/theme-mk-cover.png" alt="Theme Preview" width="800">
  <br><br>
  
  [![Hexo](https://img.shields.io/badge/Hexo-%3E%3D%205.0-blue?logo=hexo)](https://hexo.io)
  [![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)
  [![Waline](https://img.shields.io/badge/Comment-Waline-brightgreen)](https://waline.js.org/)
  
  <p>一款移植自 WordPress 经典主题 mkBlog 的 Hexo 主题。</p>
  <p>清新、极简，拥有独特的“说说”碎碎念功能，并针对静态博客进行了极致的性能优化。</p>
  
  <p>
    <a href="#-演示预览">演示预览</a> •
    <a href="#-安装指南">安装指南</a> •
    <a href="#-配置文档">配置文档</a> •
    <a href="#-特色功能">特色功能</a>
  </p>
</div>

---

## ✨ 特性

Hexo-Theme-MK 不仅仅是简单的移植，更是一次从动态到静态的底层重构：

- 🎨 **经典复刻**：完美还原 mkBlog 的 UI 风格，支持 **列表 (List)** 与 **卡片 (Card)** 双模式切换。
- 💬 **说说/碎碎念**：类似朋友圈的时间轴动态展示，支持多彩气泡与独立单页。
- ⚡ **极致性能**：全站支持 **PJAX** 无刷新加载，集成代码压缩，访问速度飞快。
- 🔍 **本地搜索**：内置高效的 Local Search，秒级响应。
- 🛠 **实用工具箱**：内置在线二维码生成、随机密码、代码高亮转换等实用工具页面。
- 📺 **媒体聚合**：支持虎牙直播、在线壁纸等聚合页面（需配合 Cloudflare Workers）。
- 📊 **数据统计**：深度集成 **Waline** 评论系统，支持阅读量统计与评论管理。
- 📱 **全端适配**：完美适配 PC、平板与移动端，支持导航栏自动隐藏 (Headroom)。

---

## 👁 演示预览

- **在线演示**: [点击查看演示站点](https://www.xudu.org)
- **原版主题**: [mkBlog (WordPress)](https://mkblog.cn/)

---

## 📥 安装指南

### 1. 下载主题
在你的 Hexo 博客根目录下执行：

```bash
git clone https://github.com/xuduorg/hexo-theme-mk.git themes/hexo-theme-mk
```

### 2. 安装必要插件
本主题依赖 EJS 渲染引擎和搜索生成器，请务必安装：

```bash
npm install hexo-renderer-ejs --save
npm install hexo-generator-search --save
```

### 3. 启用主题
修改博客根目录的 `_config.yml` 文件：

```yaml
theme: hexo-theme-mk
```

---

## ⚙️ 核心配置

所有主题相关的配置均在 `themes/hexo-theme-mk/_config.yml` 中进行。

### 1. 基础设置
```yaml
# 主题色
theme_color: '#eb5055'

# 列表样式: 'list' (左图右文) 或 'card' (网格卡片)
list_style: 'card'

# PJAX 开关 (推荐开启)
pjax:
  enable: true

# 网站图标
favicon: /img/favicon.ico
```

### 2. 菜单配置
支持多级下拉菜单，配置结构如下：

```yaml
navbar:
  auto_hide: true
  logo: /img/logo.png
  
  menu:
    首页: /
    # 普通下拉菜单
    分类浏览: 
      url: javascript:;
      children:
        - 技术教程: /categories/tech/
        - 生活感悟: /categories/life/
    # 带父级链接的菜单
    归档:
      url: /archives/
      children:
        - 标签云: /tags/
    关于: /about/
```

### 3. 评论与统计 (Waline)
推荐使用 Waline，需提前在 Vercel 部署服务端。

```yaml
comments:
  enable: true
  type: 'waline'

waline:
  serverURL: 'https://你的Waline地址.vercel.app' 
  placeholder: '来都来了，说点什么吧...'
  visitor: true  # 开启阅读量统计
  avatar: 'mp'
  meta: ['nick', 'mail', 'link']
```

---

## 🎨 特色功能使用

### 1. 发布“说说” (碎碎念)
说说本质上是特定分类的文章。

1.  **创建说说页面**：`hexo new page "shuoshuo"`
2.  **设置页面 Layout**：编辑 `source/shuoshuo/index.md`，设置 `layout: page-shuoshuo`。
3.  **发布一条说说**：
    *   新建文章。
    *   Front-matter 中设置 `categories: [shuoshuo]` (分类名需与配置一致)。
    *   可选 `layout: shuoshuo` 以获得单页气泡样式。

### 2. 友情链接
1.  **创建页面**：`hexo new page "links"`，设置 `layout: page-links`。
2.  **添加数据**：在博客根目录创建 `source/_data/links.yml`，格式如下：

```yaml
- name: 孟坤博客
  url: https://mkblog.cn
  desc: 一个前端技术博客
  avatar: https://mkblog.cn/favicon.ico
```

### 3. 工具页面
主题内置了多个工具模板，通过 `layout` 字段调用：

| 页面功能 | Layout 名称 | 创建命令示例 |
| :--- | :--- | :--- |
| 在线二维码 | `page-qrcode` | `hexo new page qrcode` |
| 随机密码生成 | `page-password` | `hexo new page password` |
| 代码高亮转换 | `page-highlight` | `hexo new page code-highlight` |
| 全球直播聚合 | `page-webcams` | `hexo new page live` |

### 4. 文章短代码 (Tag Plugins)
在 Markdown 中直接使用，增强排版：

**按钮**
```markdown
{% btn https://github.com "GitHub" fa-github blue %}
```

**提示框**
```markdown
{% alert success %}
这是一个成功的提示消息。
{% endalert %}
```

**折叠内容**
```markdown
{% collapse "点击查看隐藏内容" %}
这里是隐藏的文字...
{% endcollapse %}
```

---

## 📝 文章 Front-matter 示例

```markdown
---
title: 我的新文章
date: 2023-10-27 12:00:00
tags: [Hexo, 教程]
categories: [技术]
thumbnail: /img/cover.jpg   # 卡片模式的封面图
article_from: reprint       # 标记为转载
article_auth: 原作者        # 转载来源作者
article_url: https://...    # 转载来源链接
---
```

---

## 🤝 贡献与反馈

欢迎提交 Issue 或 Pull Request。

*   **Bug 反馈**: 请提供复现步骤和截图。
*   **功能建议**: 欢迎提出新想法，帮助主题进化。

---

## 📜 许可证

本项目遵循 [MIT License](./LICENSE) 开源协议。

**致谢**: 本主题的原型设计与灵感来源于 [Meng Kun](https://mkblog.cn/) 开发的 WordPress 版 mkBlog 主题。
