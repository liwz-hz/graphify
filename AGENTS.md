# graphify

知识图谱构建工具，用于代码库、文档、论文、图片和视频。

## 关键提示：包名

**PyPI 包名是 `graphifyy`（双 y）。** `pip install graphify` 会安装一个无关的包。

```bash
pip install graphifyy
```

CLI 命令仍然是 `graphify`（单字）。

## 项目结构

单包 Python 库。每个流水线阶段是一个模块中的一个函数：

```
detect()  →  extract()  →  build_graph()  →  cluster()  →  analyze()  →  report()  →  export()
```

| 模块 | 函数 | 用途 |
|--------|----------|---------|
| `detect.py` | `detect()` | 收集文件，按扩展名过滤 |
| `extract.py` | `extract()` | AST（代码）+ 语义（文档/论文/图片）提取 |
| `build.py` | `build_from_json()` | 合并提取结果为 NetworkX 图 |
| `cluster.py` | `cluster()` | Leiden 社团检测 |
| `analyze.py` | `god_nodes()`, `surprising_connections()` | 找高连接度节点、跨社团边 |
| `report.py` | `generate()` | 输出 GRAPH_REPORT.md |
| `export.py` | `to_json()`, `to_html()`, `to_obsidian()` | 输出格式 |

模块间无共享状态。函数通过字典和 NetworkX 图通信。

## 开发命令

```bash
# 安装开发依赖
pip install -e ".[mcp,pdf,watch]"
pip install pytest

# 运行测试
pytest tests/ -q                    # 所有测试
pytest tests/test_extract.py -q     # 单文件测试
python -m pytest tests/ -q --tb=short  # CI 格式

# 验证 CLI 可用
graphify --help
graphify install
```

CI 在 Python 3.10 和 3.12 上运行。测试均为纯单元测试——无网络调用、无文件系统副作用（除 `tmp_path` 外）。

## 可选扩展

```bash
pip install "graphifyy[mcp]"       # MCP stdio 服务器
pip install "graphifyy[video]"     # Whisper 转录
pip install "graphifyy[office]"    # .docx/.xlsx 支持
pip install "graphifyy[all]"       # 所有可选依赖
```

## 提取数据格式

每个提取器返回：

```json
{
  "nodes": [{"id": "...", "label": "...", "source_file": "...", "source_location": "L42"}],
  "edges": [{"source": "...", "target": "...", "relation": "calls|imports|...", "confidence": "EXTRACTED|INFERRED|AMBIGUOUS"}]
}
```

`validate.py` 在 `build_from_json()` 使用前强制验证此格式。

## 新增语言支持

1. 在 `extract.py` 中添加 `extract_<lang>(path: Path) -> dict`
2. 在 `extract()` 分发逻辑和 `detect.py` 的 `CODE_EXTENSIONS` 中注册后缀
3. 在 `pyproject.toml` 中添加 tree-sitter 包
4. 在 `tests/fixtures/` 添加测试文件，在 `tests/test_languages.py` 添加测试

## 安全

所有外部输入通过 `security.py` 处理：
- URL：`validate_url()`（仅 http/https，阻止私有 IP）
- 图路径：`validate_graph_path()`（必须解析到 `graphify-out/` 内）
- 标签：`sanitize_label()`（去除控制字符，上限 256 字符）

## 支持的语言

23 种（通过 tree-sitter）：Python、JS、TS、Go、Rust、Java、C、C++、Ruby、C#、Kotlin、Scala、PHP、Swift、Lua、Zig、PowerShell、Elixir、Objective-C、Julia、Vue、Svelte、Dart。

## 输出目录

```
graphify-out/
├── graph.html       # 交互式可视化
├── GRAPH_REPORT.md  # 审计报告（关键节点、意外连接）
├── graph.json       # 原始图数据
├── cache/           # SHA256 提取缓存
└── transcripts/     # Whisper 转录文件
```

添加 `.graphifyignore`（gitignore 语法）可排除目录。

## graphify

This project has a graphify knowledge graph at graphify-out/.

Rules:
- Before answering architecture or codebase questions, read graphify-out/GRAPH_REPORT.md for god nodes and community structure
- If graphify-out/wiki/index.md exists, navigate it instead of reading raw files
- After modifying code files in this session, run `python3 -c "from graphify.watch import _rebuild_code; from pathlib import Path; _rebuild_code(Path('.'))"` to keep the graph current
