# Art-Of-Harness

**Art of Harness** 是一个无构建的静态站点，收录关于 Agent 架构、上下文工程与 Harness 设计的深度拆解。目前收录 1 篇：

> 标题：《给 Agent 补一层操作系统》
> 副标题：DeepSeek Super-agent 技术报告 · 思想、业务流程与适用场景

**在线预览：** <https://keayfun.github.io/Art-Of-Harness/>

## 这是什么

围绕《Super-agent 设计探索：迈向更自主的 Agent 系统》（DeepSeek Harness 团队，2026-10-31）做的架构梳理与解读，重点不在复述结论，而在拆解它背后的系统设计取舍：

- 瓶颈为什么从「模型能力」换位到「人的注意力」
- 把 Session 从产品概念降级为内部实现细节意味着什么
- Router / Worker 双层架构为什么要这样切
- 事件驱动的完整链路：Fast Path / Slow Path → Thread 归属 → 投机执行
- 消融实验数据与它的固有成本
- 四个准入条件、适用与不适用的场景
- 作者自己承认的四个未解难题

## 本地查看

无依赖、无构建，直接用浏览器打开即可：

```powershell
Start-Process index.html
```

或起一个静态服务器：

```powershell
python -m http.server 8000
# 然后访问 http://localhost:8000
```

## 项目结构

```
.
├── index.html                    # 导航首页（期刊索引风格）
├── pages/
│   └── deepseek-super-agent/
│       └── index.html            # 报告正文：HTML + 内联 CSS + 内联 SVG 图表
├── README.md
└── LICENSE                       # Apache License 2.0
```

报告页面内包含 4 张手写 SVG 图表：瓶颈换位、双层架构、事件流、消融实验对比。

## 新增一篇

站内每篇内容是一个独立目录，首页只做索引。新增分三步。

**1. 建页面目录**

```powershell
New-Item -ItemType Directory -Path "pages/<slug>" -Force
```

`<slug>` 用 kebab-case，例如 `deepseek-super-agent`。用目录而非单个 `xxx.html`，是为了让 URL 保持 `/pages/<slug>/` 的形态，日后要加配图、附件时也不用改地址。

**2. 在首页登记**

复制 `index.html` 中任意一个 `.entry` 块，改 `href`、编号、标题、摘要与标签：

```html
<a class="entry anim d3" href="pages/<slug>/">
  <div class="num">02</div>
  <div>
    <h3><span>标题</span></h3>
    <p class="sub">副标题</p>
    <p class="desc">一两句话说明这篇拆了什么。</p>
    <div class="tags">
      <span class="tag">标签</span>
    </div>
  </div>
  <div class="arrow">&rarr;</div>
</a>
```

同时把目录标题旁的「共 N 篇」改成实际数量。

**3. 子页面加返回入口**

在正文 `<div class="wrap">` 内的最前面放一个返回链接，目录层级深一层就多一个 `../`：

```html
<a class="back" href="../../">Art of Harness</a>
```

对应样式已定义在页面内，`::before` 会自动补一个左箭头。

### 约定

| 项目 | 约定 |
|---|---|
| 目录名 | kebab-case、语义化，如 `deepseek-super-agent` |
| 入口文件 | 固定 `index.html`，Pages 会自动作为目录首页 |
| 样式 | 内联在页面 `<style>` 中，单文件自包含，不引外部依赖 |
| 配色 | 复用 `--bg` / `--t1` / `--accent` 等 CSS 变量，保持全站一致 |
| 图表 | 手写内联 SVG，带 `<title>` 与 `<desc>` 便于无障碍读取 |

新增页面后直接 push 到 `main`，GitHub Pages 会在 1～2 分钟内自动发布。

## 免责声明

站内文章均为架构梳理与解读，**不代表 DeepSeek 官方立场**。文中实验数据为原作者团队自报，标注为初步参考；公开原型并非生产可用软件。

## License

[Apache License 2.0](LICENSE)
