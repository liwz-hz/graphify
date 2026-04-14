# OpenCode 安装 graphify 完整指南

本文档记录 graphify 在 OpenCode 平台的完整安装过程、组件分析及架构说明。

## 环境信息

| 项目 | 值 |
|------|-----|
| 操作系统 | Linux |
| Python | 3.12.3 (`/usr/bin/python3`) |
| OpenCode | `/usr/local/bin/opencode` |
| graphifyy 版本 | 0.4.12 |
| 安装位置 | `/home/lmm/.local/lib/python3.12/site-packages` |

---

## 一、安装步骤执行记录

### 步骤 1：安装 Python 包

```bash
pip3 install graphifyy --break-system-packages
```

**说明**：由于 PEP 668 保护机制，Ubuntu 系统默认禁止直接安装到系统 Python。使用 `--break-system-packages` 参数可绕过此限制。

**验证**：
```bash
python3 -c "import graphify; print('OK')"
# 输出: OK

pip3 show graphifyy
# 输出: Name: graphifyy, Version: 0.4.12
```

---

### 步骤 2：全局 skill 安装

```bash
python3 -m graphify install --platform opencode
```

**输出**：
```
skill installed  ->  /home/lmm/.config/opencode/skills/graphify/SKILL.md
```

**效果**：将 `SKILL.md` 复制到 OpenCode 全局 skills 目录，注册 `/graphify` 斜杠命令。

---

### 步骤 3：项目级完整安装

```bash
python3 -m graphify opencode install
```

**输出**：
```
graphify section written to /home/lmm/github_test/graphify/AGENTS.md
  .opencode/plugins/graphify.js  ->  tool.execute.before hook written
  opencode.json  ->  plugin registered
```

**效果**：三重配置
1. 更新项目 `AGENTS.md`，添加 graphify 使用指南
2. 创建 `.opencode/plugins/graphify.js` 插件
3. 注册插件到项目 `opencode.json`

---

## 二、组件架构详解

### 2.1 Skills 目录（全局）

**位置**：`~/.config/opencode/skills/graphify/SKILL.md`

**用途**：定义 `/graphify` 斜杠命令的行为。当用户输入 `/graphify <路径>` 时，OpenCode 自动加载此 skill 文件，指导 AI 执行完整的知识图谱构建流程。

**文件结构**：
```yaml
---
name: graphify
description: any input → knowledge graph → clustered communities → HTML + JSON + audit report
trigger: /graphify
---
```

**触发机制**：
- 用户输入 `/graphify` → OpenCode 检测到 trigger 匹配 → 加载 SKILL.md 内容 → AI 按步骤执行

**版本追踪**：`.graphify_version` 文件记录当前 skill 版本，便于后续升级检测。

---

### 2.2 Plugins 目录（项目级）

**位置**：`.opencode/plugins/graphify.js`

**用途**：实现 `tool.execute.before` 钩子，在每次执行 bash 命令前自动检测知识图谱是否存在，并注入提醒消息。

**核心代码**：
```javascript
export const GraphifyPlugin = async ({ directory }) => {
  return {
    "tool.execute.before": async (input, output) => {
      if (!existsSync(join(directory, "graphify-out", "graph.json"))) return;
      
      if (input.tool === "bash") {
        output.args.command =
          'echo "[graphify] Knowledge graph available..." && ' +
          output.args.command;
      }
    },
  };
};
```

**工作机制**：
1. OpenCode 启动时加载所有已注册的 plugin
2. 每次调用 bash 工具前，触发 `tool.execute.before` 事件
3. graphify 插件检测 `graphify-out/graph.json` 是否存在
4. 若存在，在 bash 命令前注入提醒消息
5. AI 看到提醒后，主动读取 `GRAPH_REPORT.md` 获取架构上下文

---

### 2.3 AGENTS.md（项目级）

**位置**：项目根目录 `AGENTS.md`

**用途**：提供持久化的项目级指令，告诉 AI 如何使用已构建的知识图谱。

**核心规则**（graphify 部分）：
```markdown
## graphify

This project has a graphify knowledge graph at graphify-out/.

Rules:
- Before answering architecture or codebase questions, read graphify-out/GRAPH_REPORT.md
- If graphify-out/wiki/index.md exists, navigate it instead of reading raw files
- After modifying code files, run rebuild command to keep the graph current
```

**与 skill 的区别**：
| 特性 | Skills (SKILL.md) | AGENTS.md |
|------|-------------------|-----------|
| 位置 | 全局 ~/.config/ | 项目根目录 |
| 触发方式 | 斜杠命令 `/graphify` | 每次会话自动加载 |
| 内容 | 构建流程的详细步骤 | 使用图谱的简短规则 |
| 作用阶段 | 执行时（主动） | 查询时（被动） |

---

### 2.4 opencode.json（项目级）

**位置**：项目根目录 `opencode.json`

**用途**：注册项目级插件，使 OpenCode 在启动时加载 `.opencode/plugins/graphify.js`。

**内容**：
```json
{
  "plugin": [
    ".opencode/plugins/graphify.js"
  ]
}
```

---

## 三、组件关系与协作流程

### 3.1 组件关系图

```
用户输入 "/graphify ."
        │
        ▼
┌─────────────────────────────────────────────────────────┐
│  Skills (全局)                                          │
│  ~/.config/opencode/skills/graphify/SKILL.md           │
│  • 定义完整的构建流程（9 个步骤）                        │
│  • 指导 AI 如何检测文件、提取、聚类、生成报告            │
└─────────────────────────────────────────────────────────┘
        │
        ▼ AI 执行构建流程
        │
┌─────────────────────────────────────────────────────────┐
│  输出: graphify-out/                                    │
│  ├── graph.json          (原始图谱数据)                 │
│  ├── GRAPH_REPORT.md     (审计报告)                     │
│  └── graph.html          (可视化)                       │
└─────────────────────────────────────────────────────────┘
        │
        ▼ 图谱已存在
        │
┌─────────────────────────────────────────────────────────┐
│  Plugin (项目级)                                        │
│  .opencode/plugins/graphify.js                         │
│  • tool.execute.before 钩子                            │
│  • 检测 graph.json 存在 → 注入提醒                      │
└─────────────────────────────────────────────────────────┘
        │
        ▼ 提醒消息注入到 bash 命令输出
        │
┌─────────────────────────────────────────────────────────┐
│  AGENTS.md (项目级)                                     │
│  • 持久化规则：读取 GRAPH_REPORT.md                     │
│  • AI 看到提醒后，遵循规则导航图谱                       │
└─────────────────────────────────────────────────────────┘
```

### 3.2 协作流程

| 阶段 | 触发方式 | 活跃组件 | 作用 |
|------|----------|----------|------|
| 构建 | `/graphify <路径>` | Skills | 执行完整的 9 步流程，生成图谱 |
| 导航 | 会话开始 | AGENTS.md | 提供使用图谱的规则 |
| 提醒 | bash 命令执行 | Plugin | 自动检测图谱存在，注入提醒 |
| 查询 | `/graphify query` | Skills | 执行查询流程（BFS/DFS） |

---

## 四、冲突分析

### 4.1 Skills 与 Plugin 的关系

**结论：互补，无冲突。**

- **Skills**：提供主动执行能力（构建图谱、查询图谱）
- **Plugin**：提供被动提醒能力（检测图谱存在，注入上下文）

两者职责不同，不会冲突。Plugin 只在图谱存在时注入提醒，不会干扰 Skills 的执行。

### 4.2 AGENTS.md 与 Plugin 的关系

**结论：协同，增强效果。**

- **Plugin**：负责"提醒"（告诉 AI 图谱可用）
- **AGENTS.md**：负责"指导"（告诉 AI 如何使用图谱）

Plugin 注入的提醒消息会引导 AI 查看 AGENTS.md 的规则，形成协同效应。

### 4.3 全局 Skills 与项目级 Plugin 的关系

**结论：层级设计，无冲突。**

```
全局配置 (~/.config/opencode/)
└── skills/graphify/SKILL.md  ← 所有项目共享的命令定义

项目配置 (项目根目录/)
├── .opencode/plugins/graphify.js  ← 项目特定的钩子
├── opencode.json                   ← 项目插件注册
└── AGENTS.md                       ← 项目特定的规则
```

全局 Skills 提供通用的 `/graphify` 命令行为，项目级配置提供特定项目的增强功能。

---

## 五、验证命令汇总

```bash
# 验证 Python 包
python3 -c "import graphify; print('OK')"
pip3 show graphifyy

# 验证 CLI
python3 -m graphify --help

# 验证全局 Skills
ls ~/.config/opencode/skills/graphify/
cat ~/.config/opencode/skills/graphify/.graphify_version

# 验证项目级 Plugin
ls .opencode/plugins/
cat .opencode/plugins/graphify.js

# 验证项目配置
cat opencode.json
cat AGENTS.md | grep -A10 "## graphify"
```

---

## 六、使用方式

### 6.1 构建图谱

在 OpenCode 会话中输入：
```
/graphify .
```

或在任意项目目录：
```
/graphify ./src
```

### 6.2 查询图谱

```
/graphify query "authentication flow"
/graphify path "AuthModule" "Database"
/graphify explain "UserModel"
```

### 6.3 自动导航

当图谱存在时，每次 bash 命令会自动收到提醒：
```
[graphify] Knowledge graph available. Read graphify-out/GRAPH_REPORT.md...
```

AI 会自动遵循 AGENTS.md 的规则，优先从图谱获取架构信息。

---

## 七、总结

| 组件 | 类型 | 位置 | 核心功能 |
|------|------|------|----------|
| SKILL.md | 全局 Skills | ~/.config/opencode/skills/ | 定义 `/graphify` 命令的完整流程 |
| graphify.js | 项目 Plugin | .opencode/plugins/ | bash 命令前的自动提醒钩子 |
| AGENTS.md | 项目规则 | 项目根目录 | 使用图谱的持久化指导 |
| opencode.json | 项目配置 | 项目根目录 | 注册项目级插件 |

三者协作形成完整的知识图谱体验：
- **Skills** → 构建/查询能力
- **Plugin** → 自动提醒能力
- **AGENTS.md** → 导航指导能力

无冲突，互为增强。

---

*文档生成时间：2026-04-14*
*graphify 版本：0.4.12*