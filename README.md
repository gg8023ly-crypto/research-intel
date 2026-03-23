# research-intel — 通用行业情报调研系统

> 多角色并行调研 · 严格质量审核 · 知识库自动沉淀

[English](#english) | 中文

---

## 功能介绍

`research-intel` 是一个运行在 OpenClaw 上的行业情报调研 Skill，专为需要系统性、高质量行业研究的场景设计。

### 核心特性

- **🤖 单模型即可运行** — 使用 OpenClaw 当前主模型，无需额外配置
- **👥 动态角色生成** — 根据调研主题自动分配 3-5 个专属研究角色，覆盖不同维度
- **⚡ 并行调研** — 多个研究 Agent 同时工作，大幅缩短调研时间
- **🔍 严格质量门控** — 5 维度评分（满分50），总分 ≥ 40 且单项 ≥ 7 才通过
- **📊 信源分级标注** — 一手/二手/三手信源严格区分，核心结论必须有一手数据支撑
- **💾 存储自动切换** — 有飞书 Token 用飞书多维表格，否则用本地 Markdown 文件
- **🔄 三种调研模式** — 完整调研 / 增量更新 / 快速问答，按需选择

### 适用场景

- 行业进入前的市场调研
- 竞争对手分析
- 政策法规跟踪
- 投资决策支持
- 定期行业动态更新
- 领导汇报材料准备

---

## 安装方法

### 方法1：git clone（推荐）

```bash
git clone https://github.com/gg8023ly-crypto/research-intel.git
cp -r research-intel ~/.openclaw/workspace/skills/research-intel
```

### 方法2：直接下载 SKILL.md

```bash
mkdir -p ~/.openclaw/workspace/skills/research-intel
curl -o ~/.openclaw/workspace/skills/research-intel/SKILL.md \
  https://raw.githubusercontent.com/gg8023ly-crypto/research-intel/main/SKILL.md
```

安装后重启 OpenClaw Gateway 使 Skill 生效：

```bash
openclaw gateway restart
```

---

## 使用方法

### 完整调研（模式A）

```
调研 AI芯片市场
帮我调研一下新能源汽车行业
深度调研 跨境电商政策
```

**流程**：
1. 系统分析主题，生成角色方案
2. 你确认角色方案
3. 多个研究 Agent 并行调研
4. 质量审核（不通过自动重跑，最多3轮）
5. 合并整合，生成最终报告
6. 自动归档到知识库

### 增量更新（模式B）

```
AI芯片市场最近有什么新变化
新能源汽车最新动态
跨境电商政策有什么更新
```

**流程**：读取历史记录 → 只搜最近14天 → 生成增量报告 → 更新知识库

### 快速问答（模式C）

```
比特币现在的监管政策是什么
特斯拉最新的市场份额是多少
```

**流程**：直接搜索回答 → 顺手归档到知识库

---

## 配置说明

在 OpenClaw 中设置环境变量（可选，不配置也能正常使用）：

```bash
# 指定调研使用的模型（默认用当前主模型）
RESEARCH_MODEL=gpt-4o

# 额外模型配置（可选，用于增强调研能力）
RESEARCH_API_KEY=sk-xxx
RESEARCH_API_BASE=https://api.openai.com/v1

# 飞书多维表格存储（可选，不配置则用本地文件）
RESEARCH_FEISHU_TOKEN=bascnXXXXXXXXXX

# 调研深度：quick / standard / deep（默认 standard）
RESEARCH_DEPTH=standard

# 输出语言：zh / en（默认 zh）
RESEARCH_LANG=zh
```

详细配置示例见 [config.example.md](./config.example.md)

---

## 输出示例

调研完成后，你会收到：

```
✅ 调研完成！

📊 质量评分：44/50
📁 报告路径：~/.openclaw/workspace/research-intel/ai-chip-market-20240315/output/report.md
💾 已归档到知识库

---
## 执行摘要

**核心结论1**：2024年全球AI芯片市场规模达到XXX亿美元，同比增长XX%...
**核心结论2**：英伟达市场份额持续领先，占据约XX%的数据中心GPU市场...
**核心结论3**：中国AI芯片国产替代进程加速，华为昇腾、寒武纪等...

## 关键数据
| 指标 | 数值 | 时间 | 信源 |
|------|------|------|------|
| 全球市场规模 | XXX亿美元 | 2024Q1 | IDC报告（二手） |
...
```

---

## 文件结构

调研结果保存在：

```
~/.openclaw/workspace/research-intel/
├── knowledge-base/
│   └── index.md              ← 所有调研记录索引
└── {topic-slug}/
    ├── config.md             ← 本次调研配置
    ├── brief.md              ← 主题简报
    ├── round-1/
    │   ├── agent-*.md        ← 各角色调研产出
    │   └── review.md         ← 质量审核报告
    ├── merged/
    │   └── draft-1.md        ← 合并草稿
    └── output/
        └── report.md         ← 最终报告 ⭐
```

---

## 常见问题

**Q: 调研需要多长时间？**
A: 取决于深度设置。quick 约5-10分钟，standard 约15-30分钟，deep 约30-60分钟。

**Q: 没有飞书账号可以用吗？**
A: 完全可以，不配置 `RESEARCH_FEISHU_TOKEN` 时自动使用本地 Markdown 文件存储。

**Q: 质量审核不通过怎么办？**
A: 系统会自动重跑（最多3轮）。3轮后仍不通过，会询问你是否接受当前质量。

**Q: 可以调研英文主题吗？**
A: 可以，设置 `RESEARCH_LANG=en` 即可获得英文报告。调研过程中会自动覆盖中英文信源。

---

## 版本历史

- **v1.0.0** (2024-03-15) — 初始版本

---

<a name="english"></a>

## English

`research-intel` is an industry intelligence research Skill for OpenClaw, designed for systematic, high-quality industry research.

### Quick Start

```bash
# Install
git clone https://github.com/gg8023ly-crypto/research-intel.git
cp -r research-intel ~/.openclaw/workspace/skills/research-intel
openclaw gateway restart

# Use
"Research AI chip market"
"What's new in EV industry recently"
```

### Key Features

- Dynamic role generation (3-5 research agents per topic)
- Parallel research with quality gating (score ≥ 40/50)
- Source classification: primary / secondary / tertiary
- Auto storage: Feishu Bitable or local Markdown
- Three modes: Full Research / Incremental Update / Quick Q&A

---

## License

MIT License — Free to use, modify, and distribute.

---

*Built for OpenClaw · Powered by multi-agent research workflows*
