# research-intel 配置示例

将以下配置添加到你的 OpenClaw 环境变量中。

## 最简配置（开箱即用）

无需任何配置，直接使用：

```
调研 AI芯片市场
```

系统会使用当前主模型 + 本地文件存储。

---

## 标准配置

```bash
# 调研深度（推荐 standard）
RESEARCH_DEPTH=standard

# 输出语言
RESEARCH_LANG=zh
```

---

## 飞书存储配置

如果你有飞书账号，可以将调研结果存入飞书多维表格，方便团队共享：

```bash
# 飞书多维表格 app_token
# 从飞书多维表格 URL 中获取：https://xxx.feishu.cn/base/{app_token}
RESEARCH_FEISHU_TOKEN=bascnXXXXXXXXXXXXXXXX
```

**飞书多维表格字段说明：**

系统会自动创建以下字段（如果不存在）：

| 字段名 | 类型 | 说明 |
|--------|------|------|
| 主题 | 文本 | 调研主题 |
| 领域标签 | 多选 | 行业/领域分类 |
| 调研时间 | 日期 | 完成时间 |
| 核心结论 | 文本 | 3-5条核心结论 |
| 关键数据 | 文本 | 重要数字和指标 |
| 信源质量 | 数字 | 质量评分（满分50） |
| 报告路径 | 文本 | 本地文件路径 |
| 下次复查日期 | 日期 | 建议复查时间 |

---

## 额外模型配置（可选）

如果你想使用特定模型进行调研（例如使用更强的模型）：

```bash
# 指定模型名称
RESEARCH_MODEL=gpt-4o

# 如果使用非默认 API 端点
RESEARCH_API_KEY=sk-your-api-key-here
RESEARCH_API_BASE=https://api.openai.com/v1
```

**支持的模型示例：**

```bash
# OpenAI
RESEARCH_MODEL=gpt-4o
RESEARCH_API_KEY=sk-xxx
RESEARCH_API_BASE=https://api.openai.com/v1

# Anthropic Claude（通过兼容端点）
RESEARCH_MODEL=claude-3-5-sonnet-20241022
RESEARCH_API_KEY=sk-ant-xxx
RESEARCH_API_BASE=https://api.anthropic.com/v1

# 本地 Ollama
RESEARCH_MODEL=llama3.1:70b
RESEARCH_API_BASE=http://localhost:11434/v1

# 中转站（如 usora）
RESEARCH_MODEL=gemini-3-pro-preview
RESEARCH_API_KEY=sk-xxx
RESEARCH_API_BASE=https://api.usora.net/v1
```

---

## 深度配置说明

| 深度 | 角色数 | 每角色关键词 | 最大轮次 | 适用场景 |
|------|--------|------------|---------|---------|
| `quick` | 2-3 | 3 | 1 | 快速了解，10分钟内 |
| `standard` | 3-4 | 5 | 2 | 日常调研，15-30分钟 |
| `deep` | 4-5 | 8 | 3 | 深度研究，30-60分钟 |

---

## 完整配置示例

```bash
# === research-intel 完整配置 ===

# 模型配置
RESEARCH_MODEL=gpt-4o
RESEARCH_API_KEY=sk-your-key
RESEARCH_API_BASE=https://api.openai.com/v1

# 存储配置
RESEARCH_FEISHU_TOKEN=bascnXXXXXXXXXXXXXXXX

# 调研参数
RESEARCH_DEPTH=standard
RESEARCH_LANG=zh
```

---

## 在 OpenClaw 中设置环境变量

编辑 OpenClaw 配置文件（通常在 `~/.openclaw/config.yaml`）：

```yaml
env:
  RESEARCH_DEPTH: standard
  RESEARCH_LANG: zh
  RESEARCH_FEISHU_TOKEN: "bascnXXXXXXXXXXXXXXXX"
```

或者在启动时通过 shell 设置：

```bash
export RESEARCH_DEPTH=deep
export RESEARCH_FEISHU_TOKEN=bascnXXXXXXXXXXXXXXXX
openclaw gateway start
```
