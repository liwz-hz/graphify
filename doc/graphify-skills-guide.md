# graphify Skills 详细指南

本文档详细介绍 graphify 提供的各种 skill（斜杠命令），用通俗的语言解释每个命令的业务流程、应用场景和使用示例。

---

## 🎯 什么是 graphify？

graphify 是一个**知识图谱构建工具**，可以把你的代码库、文档、论文等变成一张可视化的关系网。

**想象一下**：
- 你刚接手一个陌生的项目，代码文件几百个，不知道从哪开始看
- 你读了很多技术论文，想整理它们之间的关系
- 你想快速理解一个开源项目的架构

graphify 能把这些杂乱的文件变成一张**关系地图**，告诉你：
- 核心概念是什么（God Nodes）
- 意想不到的关联在哪（Surprising Connections）
- 该从哪开始探索（Suggested Questions）

---

## 📚 核心 Skill：`/graphify`

### 一句话描述

把任何文件夹变成一张可导航的知识图谱，告诉你"什么连着什么"。

### 业务流程

```
用户输入: /graphify ./my-project

Step 1: 检测文件类型
├── 代码文件 (.py, .ts, .go...) → AST 自动提取
├── 文档文件 (.md, .txt) → AI 语义提取
├── 论文 PDF → 提取概念和引用
├── 图片 → 视觉理解内容
└── 视频 → Whisper 转录文字

Step 2: 提取实体和关系
├── AST 提取（免费、快速）
│   ├── 类、函数、变量
│   ├── 导入关系
│   ├── 继承关系
│   └── 调用关系
│
└── 语义提取（需要 AI）
    ├── 文档中的概念
    ├── 论文中的观点
    ├── 图片中的内容
    └── 跨文件的关联

Step 3: 构建图谱
├── 每个实体 → 一个节点
├── 每个关系 → 一条边
└── 节点带着置信度标签：
    ├── EXTRACTED（明确找到的）
    ├── INFERRED（推断出来的）
    └── AMBIGUOUS（不确定的）

Step 4: 社团检测
├── Leiden 算法自动分组
├── 相关的节点聚在一起
└── 形成"模块"、"子系统"

Step 5: 分析关键节点
├── God Nodes：连接最多的核心概念
├── Surprising Connections：跨模块的意外关联
└── Suggested Questions：图谱能回答的问题

Step 6: 生成输出
├── graph.html → 浏览器中打开的交互式图谱
├── GRAPH_REPORT.md → 审计报告
├── graph.json → 原始数据
└── obsidian/ → Obsidian 笔记库（可选）
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **新项目上手** | 先看图谱理解架构，再读代码 |
| **代码重构准备** | 找到高耦合模块，规划拆分策略 |
| **技术调研整理** | 论文 + 博客 + 笔记 → 一张关系图 |
| **知识库管理** | 个人笔记库 → 可查询的知识图谱 |

### 使用示例

```
# 基础用法：在当前目录构建图谱
/graphify .

# 指定目录
/graphify ./src

# 深度模式：提取更多推断关系
/graphify . --mode deep

# 增量更新：只处理变化的文件
/graphify . --update

# 只重新聚类（不重新提取）
/graphify . --cluster-only

# 跳过可视化（只要报告和 JSON）
/graphify . --no-viz

# 导出多种格式
/graphify . --svg --graphml
```

---

## 🔍 查询 Skill：`/graphify query`

### 一句话描述

在知识图谱中搜索，像问朋友一样提问："X 和 Y 有什么关系？"

### 业务流程

```
用户输入: /graphify query "authentication flow"

Step 1: 加载图谱
├── 读取 graphify-out/graph.json
└── 构建 NetworkX 内存图

Step 2: 找匹配节点
├── 搜索关键词 "authentication"
├── 找到标签匹配的节点
└── 取前 3 个作为起点

Step 3: 图遍历
├── BFS（默认）：广度优先，看周围一圈
│   └── 适合："这个概念连接到什么？"
│
└── DFS：深度优先，追一条链
    └── 适合："从 A 怎么到达 B？"

Step 4: 返回结果
├── 节点列表（按相关性排序）
├── 边列表（关系类型、置信度）
└── 来源位置（文件名、行号）
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **理解概念关系** | "认证流程涉及哪些模块？" |
| **追踪依赖链** | "这个函数被谁调用？" |
| **探索新领域** | "这个论文的核心观点是什么？" |

### 使用示例

```
# 基础查询（BFS，广度优先）
/graphify query "how does authentication work"

# 深度查询（DFS，追踪一条路径）
/graphify query "how does request reach response" --dfs

# 限制输出长度
/graphify query "core modules" --budget 500
```

### 真实输出示例

查询 `"how does extract work"`：

```
Traversal: BFS | Start: [extract.py, build(), build_from_json()] | 35 nodes

NODE extract.py [src=graphify/extract.py community=39]
NODE build() [src=graphify/build.py community=39]
NODE build_from_json() [src=graphify/build.py community=39]
NODE test_extract.py [src=tests/test_extract.py community=8]

EDGE extract.py --contains--> build()
EDGE build() --calls--> build_from_json()
EDGE build_from_json() --uses--> extract()
```

---

## 🛤️ 路径 Skill：`/graphify path`

### 一句话描述

找两个概念之间的最短路径，告诉你"从 A 怎么走到 B"。

### 业务流程

```
用户输入: /graphify path "Client" "Transport"

Step 1: 匹配节点
├── 搜索 "Client" → 找最匹配的节点
├── 搜索 "Transport" → 找最匹配的节点
└── 如果找不到 → 报错退出

Step 2: 计算路径
├── NetworkX shortest_path()
├── 返回节点序列
└── 每步包含关系类型和置信度

Step 3: 解释路径
└── AI 用通俗语言解释每一步的含义
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **理解调用链** | "这个类怎么用到那个服务？" |
| **追踪数据流** | "请求怎么变成响应？" |
| **发现依赖路径** | "模块 A 依赖模块 B 吗？" |

### 使用示例

```
# 找两个概念的连接路径
/graphify path "Request" "Response"

# 找类和服务之间的路径
/graphify path "AuthController" "Database"

# 找概念到实现的路径
/graphify path "caching" "CacheService"
```

### 真实输出示例

查询 `path "Response" "Request"`：

```
Shortest path (2 hops):
  Response --uses--> [INFERRED]
  Auth --uses--> [INFERRED]
  → Request
```

解释：Response 和 Request 通过 Auth（认证机制）关联。认证处理器会修改 Request，然后可以检查 Response。

---

## 💡 解释 Skill：`/graphify explain`

### 一句话描述

详细解释一个节点，告诉你"这个东西是什么，连着什么"。

### 业务流程

```
用户输入: /graphify explain "Transformer"

Step 1: 匹配节点
├── 搜索标签中包含 "Transformer" 的节点
├── 取匹配度最高的
└── 如果多个匹配 → 列出候选

Step 2: 展示详情
├── 基本信息：ID、来源文件、类型、社团
├── 连接数：degree
└── 所有邻居节点

Step 3: 解释关系
└── AI 用通俗语言解释这个节点的作用和关联
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **理解核心概念** | "这个类是做什么的？" |
| **查看模块边界** | "这个函数依赖什么？" |
| **探索论文概念** | "这个术语在论文中的定义？" |

### 使用示例

```
# 解释一个类
/graphify explain "Response"

# 解释一个概念
/graphify explain "attention mechanism"

# 解释一个函数
/graphify explain "extract()"
```

### 真实输出示例

查询 `explain "Response"`：

```
Node: Response
  ID:        worked_httpx_raw_models_Response
  Source:    worked/httpx/raw/models.py
  Type:      code
  Community: 39
  Degree:    45

Connections (45):
  --> Auth [uses] [INFERRED]
  --> BasicAuth [uses] [INFERRED]
  --> BaseTransport [uses] [INFERRED]
  --> HTTPTransport [uses] [INFERRED]
  --> ConnectionPool [uses] [INFERRED]
  ...
```

---

## ➕ 添加 Skill：`/graphify add`

### 一句话描述

把网页、论文、推文添加到你的知识库，自动整理成笔记。

### 业务流程

```
用户输入: /graphify add https://arxiv.org/abs/1706.03762

Step 1: 检测 URL 类型
├── arXiv → 提取标题、摘要、作者
├── Twitter/X → 获取推文内容和作者
├── PDF → 直接下载
├── 图片 → 下载，等待视觉提取
└── 网页 → 转 Markdown

Step 2: 保存到 ./raw/
├── 创建 YAML frontmatter
├── 记录 source_url、author、contributor
└── 写入 .md 或 .pdf 文件

Step 3: 更新图谱
└── 自动运行增量提取，合并新内容
```

### 支持的 URL 类型

| 类型 | 处理方式 | 输出格式 |
|------|----------|----------|
| **arXiv 论文** | API 获取元数据 | `.md`（标题 + 摘要）|
| **Twitter/X** | oEmbed API | `.md`（推文 + 作者）|
| **PDF** | 直接下载 | `.pdf` |
| **图片** | 直接下载 | `.png/.jpg` |
| **普通网页** | html2text | `.md` |

### 使用示例

```
# 基础用法：添加 URL
/graphify add https://arxiv.org/abs/1706.03762

# 标记作者
/graphify add https://blog.example.com/article --author "John Doe"

# 标记添加者
/graphify add https://twitter.com/user/status/123 --contributor "我"

# 指定保存目录
/graphify add https://example.com --dir ./my-notes
```

---

## 🔄 更新 Skill：`/graphify update`

### 一句话描述

只处理变化了的文件，快速更新图谱，不用重新处理所有内容。

### 业务流程

```
用户输入: /graphify update .

Step 1: 对比 manifest
├── 读取上次处理的文件列表
├── 对比当前文件列表
├── 找新增文件
├── 找修改文件（SHA256 对比）
└── 找删除文件

Step 2: 检查类型
├── 只有代码变化 → AST 提取（免费）
├── 有文档/图片变化 → 需要语义提取
└── 无变化 → 直接退出

Step 3: 增量提取
├── 只处理变化文件
├── 合入现有图谱
└── 删除文件 → 删除对应节点

Step 4: 重建图谱
└── 重新聚类、分析、生成报告
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **开发过程同步** | 写完代码，一键更新图谱 |
| **Git hook 集成** | 每次提交自动更新 |
| **CI/CD 集成** | 构建时保持图谱最新 |

### 使用示例

```
# 增量更新当前目录
/graphify update .

# 更新指定目录
/graphify update ./src

# CLI 命令（不需要 AI）
graphify update .
```

---

## 🧩 聚类 Skill：`/graphify cluster-only`

### 一句话描述

不重新提取，只重新分组，试试不同的聚类效果。

### 业务流程

```
用户输入: /graphify cluster-only .

Step 1: 加载现有图谱
├── 读取 graphify-out/graph.json
└── 跳过提取步骤

Step 2: 重新聚类
├── Leiden 算法
├── 可调整参数
└── 得到新的社团划分

Step 3: 重新分析
├── 重新计算 God Nodes
├── 重新找 Surprising Connections
└── 重新生成问题建议

Step 4: 更新输出
└── 更新报告和 JSON
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **调整分组效果** | 觉得社团划分不合理，重新试试 |
| **实验参数** | 测试不同的聚类配置 |
| **快速修复** | 社团划分出了问题，快速重做 |

### 使用示例

```
# 重新聚类当前目录
/graphify cluster-only .

# CLI 命令
graphify cluster-only ./my-project
```

---

## 👁️ 监控 Skill：`/graphify watch`

### 一句话描述

后台监控文件变化，自动更新图谱，边写代码边更新地图。

### 业务流程

```
用户输入: /graphify watch .

Step 1: 启动监控
├── 监听文件系统事件
├── 设置防抖时间（默认 3 秒）
└── 等待文件写入完成

Step 2: 检测变化
├── 代码变化 → 立即 AST 提取 + 重建
├── 文档变化 → 标记需要语义提取
└── 图片变化 → 标记需要视觉提取

Step 3: 自动处理
├── 代码 → 自动重建（无 LLM）
├── 文档 → 提示手动运行更新
└── 循环监控

Step 4: 持续运行
└── Ctrl+C 停止
```

### 应用场景

| 场景 | 说明 |
|------|------|
| **实时开发** | 写代码时保持图谱同步 |
| **AI 协作** | 多 Agent 写代码，自动追踪变化 |
| **长期项目** | 持续维护知识库 |

### 使用示例

```
# 监控当前目录
/graphify watch .

# 调整防抖时间（等文件写完）
/graphify watch . --debounce 5

# CLI 命令（后台终端运行）
python3 -m graphify.watch . --debounce 3
```

---

## 🔧 CLI 安装 Skill：`graphify install`

### 一句话描述

把 graphify 的 skill 文件复制到你的 AI 工具配置目录，让 `/graphify` 命令可用。

### 业务流程

```
用户输入: graphify install --platform opencode

Step 1: 检测平台
├── claude → ~/.claude/skills/
├── opencode → ~/.config/opencode/skills/
├── cursor → .cursor/rules/
├── codex → .agents/skills/
└── 其他平台类似

Step 2: 复制 skill 文件
├── 读取内置的 skill.md / skill-opencode.md
├── 写入目标目录
└── 添加版本标记

Step 3: 注册配置
├── Claude → 写入 CLAUDE.md
├── OpenCode → 写入 AGENTS.md + 插件
├── Gemini → 写入 GEMINI.md + hook
└── Cursor → 写入 .cursor/rules/

Step 4: 配置 hooks（部分平台）
├── PreToolUse hook → 检测图谱存在时提醒
├── tool.execute.before → OpenCode 插件
└── git hooks → 提交后自动重建
```

### 支持的平台

| 平台 | 安装命令 | 配置写入 |
|------|----------|----------|
| **Claude Code** | `graphify install` | CLAUDE.md + PreToolUse hook |
| **OpenCode** | `graphify install --platform opencode` | AGENTS.md + plugin |
| **Codex** | `graphify install --platform codex` | AGENTS.md + hooks.json |
| **Cursor** | `graphify install --platform cursor` | .cursor/rules/graphify.mdc |
| **Gemini CLI** | `graphify install --platform gemini` | GEMINI.md + BeforeTool hook |
| **Aider** | `graphify install --platform aider` | AGENTS.md |
| **GitHub Copilot** | `graphify install --platform copilot` | ~/.copilot/skills/ |

### 使用示例

```
# 默认安装（Claude Code）
graphify install

# 安装到 OpenCode
graphify install --platform opencode

# 安装到 Cursor
graphify install --platform cursor

# 安装到 Gemini CLI
graphify install --platform gemini
```

---

## 🗺️ 技能协作流程图

### `/graphify` 9 步流水线

```
┌──────────────────────────────────────────────────────────────────────┐
│ Step 1: 安装检查                                                      │
│ 确保 graphifyy 包已安装，写 Python 解释器路径                          │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 2: 文件检测                                                      │
│ detect() → 分类文件类型，计算词数，跳过敏感文件                        │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 2.5: 视频转录（如有）                                            │
│ Whisper 转录 → 生成文本，当作文档处理                                  │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 3A: AST 提取（代码）                                             │
│ tree-sitter → 提取类、函数、导入、调用                                 │
│ 免费、快速、确定性                                                    │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 3B: 语义提取（文档/图片）                                        │
│ AI subagents → 提取概念、关系、设计意图                                │
│ 需要 tokens，可缓存                                                   │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 3C: 合并结果                                                     │
│ AST + 语义 → 去重 → 最终提取数据                                       │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 4: 构建图谱                                                      │
│ build_from_json() → NetworkX 图                                       │
│ cluster() → Leiden 社团检测                                           │
│ god_nodes() / surprising_connections() → 分析                         │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 5: 标注社团                                                      │
│ AI 为每个社团起一个人类可读的名字                                      │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 6: 生成输出                                                      │
│ to_html() → graph.html                                                │
│ to_obsidian() → obsidian vault（可选）                                │
└──────────────────────────────────────────────────────────────────────┘
                                  ↓
┌──────────────────────────────────────────────────────────────────────┐
│ Step 7-9: 导出 + 清理                                                 │
│ Neo4j / SVG / GraphML（可选）                                         │
│ 保存 manifest + cost，清理临时文件                                    │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🎓 最佳实践

### 什么时候用 `/graphify`？

| 文件规模 | 建议 |
|----------|------|
| **< 50 文件** | 图谱价值有限，直接读代码更快 |
| **50-200 文件** | 推荐，图谱能帮你快速定位 |
| **> 200 文件** | 先选关键子目录，避免处理太多 |

### 什么时候用 `--mode deep`？

- 你需要更丰富的关系推断
- 你在做深度代码分析
- 你愿意消耗更多 tokens

### 什么时候用 `--update`？

- 你刚改了几个文件
- 你不想等完整构建
- 你在持续开发中

### 什么时候用 `watch`？

- 你在长时间编码
- 多个 Agent 同时工作
- 你想让图谱始终最新

---

## 📌 总结

graphify 的核心理念：

> **把杂乱的文件变成一张可查询的关系地图，让你不再迷失在代码海洋里。**

每个 skill 的本质：

| Skill | 本质 |
|-------|------|
| `/graphify` | 构建 → 地图生成 |
| `/graphify query` | 搜索 → 地图导航 |
| `/graphify path` | 路径 → 路线规划 |
| `/graphify explain` | 解释 → 地点详情 |
| `/graphify add` | 添加 → 扩充地图 |
| `/graphify update` | 更新 → 地图维护 |
| `/graphify watch` | 监控 → 自动更新 |

---

*文档生成时间：2026-04-14*