# Art-Of-Harness

一份关于 **DeepSeek Super-agent** 架构的技术报告，以单页静态网页形式呈现。

> 标题：《给 Agent 补一层操作系统》
> 副标题：DeepSeek Super-agent 技术报告 · 思想、业务流程与适用场景

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
├── index.html   # 全部内容：HTML + 内联 CSS + 内联 SVG 图表
├── README.md
└── LICENSE      # Apache License 2.0
```

页面内包含 4 张手写 SVG 图表：瓶颈换位、双层架构、事件流、消融实验对比。

## 免责声明

本报告为架构梳理与解读，**不代表 DeepSeek 官方立场**。文中实验数据均为团队自报，标注为初步参考；公开原型并非生产可用软件。

## License

[Apache License 2.0](LICENSE)
