# RecADWeekly — 电商广告生成式推荐与检索研究周报

本项目通过 Antigravity 定时自动化 Agent 持续追踪**电商广告与生成式推荐/检索（Generative Recommendation / Retrieval）**领域的最新论文与工业技术报告，聚焦**千万级 SKU、GR 召回 Top600 后接精排与竞价**场景下的核心问题：

- 召回排序一体化与多阶段级联编排
- 商业价值建模（bid、eCPM、广告收入、多目标优化）
- 解码优化（Lazy Decoder、宽 Beam Search、Trie、缓存与效率）
- 训推一致性
- 语义/商业 SID、Listwise 与偏好优化、长序列和长尾覆盖

## 目录结构

```text
.
├── README.md
├── covered-papers.json        # 跨期去重账本（记录已覆盖论文 ID、版本与核心发现）
├── agent/
│   ├── sidecar.json           # Antigravity 定时任务配置（已脱敏，本地部署需替换 <HOME>）
│   └── PROMPT.md              # Agent 完整执行规范与提示词
└── reports/
    ├── 2026-11-21.md          # 最新一期周报
    └── 2026-11-20.md
```

## 周报归档

| 期数日期 | 检索窗口 | 收录数量 | 报告链接 |
| :--- | :--- | :---: | :--- |
| 2026-11-21 | 2026-11-14 至 2026-11-21 | 7 篇 | [reports/2026-11-21.md](./reports/2026-11-21.md) |
| 2026-11-20 | 2026-11-13 至 2026-11-20 | 5 篇 | [reports/2026-11-20.md](./reports/2026-11-20.md) |

## Agent 定时设置与自动同步

- **运行频率**：每周一、周五 08:00（`Asia/Shanghai`），对应 cron `CRON_TZ=Asia/Shanghai 0 8 * * 1,5`
- **配置文件**：[agent/sidecar.json](./agent/sidecar.json) / [agent/PROMPT.md](./agent/PROMPT.md)
- **去重机制**：每次运行先读取 [covered-papers.json](./covered-papers.json) 与最近两期周报，无实质版本更新（`v2`/`v3`、新开源代码或新增关键实验）的已覆盖论文不会重复推荐。
- **自动同步**：每次生成周报后自动更新本 `README.md` 归档表与 `covered-papers.json`，并自动 `git commit && git push origin main` 同步至本仓库。
