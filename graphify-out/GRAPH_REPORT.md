# Graph Report - .  (2026-04-14)

## Corpus Check
- 117 files · ~137,411 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 1390 nodes · 2135 edges · 63 communities detected
- Extraction: 88% EXTRACTED · 12% INFERRED · 0% AMBIGUOUS · INFERRED: 246 edges (avg confidence: 0.5)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- [[_COMMUNITY_Community 0|Community 0]]
- [[_COMMUNITY_Community 1|Community 1]]
- [[_COMMUNITY_Community 2|Community 2]]
- [[_COMMUNITY_Community 3|Community 3]]
- [[_COMMUNITY_Community 4|Community 4]]
- [[_COMMUNITY_Community 5|Community 5]]
- [[_COMMUNITY_Community 6|Community 6]]
- [[_COMMUNITY_Community 7|Community 7]]
- [[_COMMUNITY_Community 8|Community 8]]
- [[_COMMUNITY_Community 9|Community 9]]
- [[_COMMUNITY_Community 10|Community 10]]
- [[_COMMUNITY_Community 11|Community 11]]
- [[_COMMUNITY_Community 12|Community 12]]
- [[_COMMUNITY_Community 13|Community 13]]
- [[_COMMUNITY_Community 14|Community 14]]
- [[_COMMUNITY_Community 15|Community 15]]
- [[_COMMUNITY_Community 16|Community 16]]
- [[_COMMUNITY_Community 17|Community 17]]
- [[_COMMUNITY_Community 18|Community 18]]
- [[_COMMUNITY_Community 19|Community 19]]
- [[_COMMUNITY_Community 20|Community 20]]
- [[_COMMUNITY_Community 21|Community 21]]
- [[_COMMUNITY_Community 22|Community 22]]
- [[_COMMUNITY_Community 23|Community 23]]
- [[_COMMUNITY_Community 24|Community 24]]
- [[_COMMUNITY_Community 25|Community 25]]
- [[_COMMUNITY_Community 26|Community 26]]
- [[_COMMUNITY_Community 27|Community 27]]
- [[_COMMUNITY_Community 28|Community 28]]
- [[_COMMUNITY_Community 29|Community 29]]
- [[_COMMUNITY_Community 30|Community 30]]
- [[_COMMUNITY_Community 31|Community 31]]
- [[_COMMUNITY_Community 32|Community 32]]
- [[_COMMUNITY_Community 33|Community 33]]
- [[_COMMUNITY_Community 34|Community 34]]
- [[_COMMUNITY_Community 35|Community 35]]
- [[_COMMUNITY_Community 36|Community 36]]
- [[_COMMUNITY_Community 37|Community 37]]
- [[_COMMUNITY_Community 38|Community 38]]
- [[_COMMUNITY_Community 39|Community 39]]
- [[_COMMUNITY_Community 40|Community 40]]
- [[_COMMUNITY_Community 41|Community 41]]
- [[_COMMUNITY_Community 42|Community 42]]
- [[_COMMUNITY_Community 43|Community 43]]
- [[_COMMUNITY_Community 44|Community 44]]
- [[_COMMUNITY_Community 45|Community 45]]
- [[_COMMUNITY_Community 46|Community 46]]
- [[_COMMUNITY_Community 47|Community 47]]
- [[_COMMUNITY_Community 48|Community 48]]
- [[_COMMUNITY_Community 49|Community 49]]
- [[_COMMUNITY_Community 50|Community 50]]
- [[_COMMUNITY_Community 51|Community 51]]
- [[_COMMUNITY_Community 52|Community 52]]
- [[_COMMUNITY_Community 53|Community 53]]
- [[_COMMUNITY_Community 54|Community 54]]
- [[_COMMUNITY_Community 55|Community 55]]
- [[_COMMUNITY_Community 56|Community 56]]
- [[_COMMUNITY_Community 57|Community 57]]
- [[_COMMUNITY_Community 58|Community 58]]
- [[_COMMUNITY_Community 59|Community 59]]
- [[_COMMUNITY_Community 60|Community 60]]
- [[_COMMUNITY_Community 61|Community 61]]
- [[_COMMUNITY_Community 62|Community 62]]

## God Nodes (most connected - your core abstractions)
1. `Response` - 45 edges
2. `Request` - 42 edges
3. `_labels()` - 34 edges
4. `Cookies` - 27 edges
5. `Client` - 27 edges
6. `_make_id()` - 26 edges
7. `AsyncClient` - 26 edges
8. `HTTPTransport` - 22 edges
9. `TransportError` - 22 edges
10. `BaseTransport` - 21 edges

## Surprising Connections (you probably didn't know these)
- `A .md file with enough paper signals should classify as PAPER.` --uses--> `FileType`  [INFERRED]
  tests/test_detect.py → graphify/detect.py
- `A plain .md file without paper signals should stay DOCUMENT.` --uses--> `FileType`  [INFERRED]
  tests/test_detect.py → graphify/detect.py
- `The real attention paper file should be classified as PAPER.` --uses--> `FileType`  [INFERRED]
  tests/test_detect.py → graphify/detect.py
- `Files matching .graphifyignore patterns are excluded from detect().` --uses--> `FileType`  [INFERRED]
  tests/test_detect.py → graphify/detect.py
- `No .graphifyignore is not an error.` --uses--> `FileType`  [INFERRED]
  tests/test_detect.py → graphify/detect.py

## Communities

### Community 0 - "Community 0"
Cohesion: 0.03
Nodes (84): Auth, BasicAuth, BearerAuth, DigestAuth, NetRCAuth, Authentication handlers. Auth objects are callables that modify a request before, Load credentials from ~/.netrc based on the request host., Base class for all authentication handlers. (+76 more)

### Community 1 - "Community 1"
Cohesion: 0.03
Nodes (52): _calls(), _labels(), Tests for language extractors: Java, C, C++, Ruby, C#, Kotlin, Scala, PHP, Swift, Methods on the same receiver type must share one canonical type node., Type node id should be scoped to directory, not file stem., _relations(), test_c_finds_functions(), test_c_finds_includes() (+44 more)

### Community 2 - "Community 2"
Cohesion: 0.04
Nodes (82): _check_tree_sitter_version(), _csharp_extra_walk(), extract(), extract_blade(), extract_c(), extract_cpp(), extract_csharp(), extract_dart() (+74 more)

### Community 3 - "Community 3"
Cohesion: 0.04
Nodes (56): classify_file(), convert_office_file(), count_words(), detect(), detect_incremental(), docx_to_markdown(), extract_pdf_text(), FileType (+48 more)

### Community 4 - "Community 4"
Cohesion: 0.05
Nodes (51): _agents_install(), _agents_uninstall(), _install(), Tests for graphify install --platform routing., Claude platform install writes CLAUDE.md; others do not., Installing twice does not duplicate the section., Installs into an existing AGENTS.md without overwriting other content., Uninstall keeps pre-existing content. (+43 more)

### Community 5 - "Community 5"
Cohesion: 0.07
Nodes (19): Base, Server, LinearAlgebra, add(), area(), Circle, Color, Config (+11 more)

### Community 6 - "Community 6"
Cohesion: 0.08
Nodes (39): _agents_install(), _agents_uninstall(), _antigravity_install(), _antigravity_uninstall(), _check_skill_version(), claude_install(), claude_uninstall(), _cursor_install() (+31 more)

### Community 7 - "Community 7"
Cohesion: 0.1
Nodes (33): _cross_community_surprises(), _cross_file_surprises(), _file_category(), god_nodes(), graph_diff(), _is_concept_node(), _is_file_node(), _node_community_map() (+25 more)

### Community 8 - "Community 8"
Cohesion: 0.07
Nodes (18): After merging multiple files, no internal edges should be dangling., Call-graph pass must produce INFERRED calls edges., AST-resolved call edges are deterministic and should be EXTRACTED/1.0., Same input always produces same output., run_analysis() calls compute_score() - must appear as a calls edge., Analyzer.process() calls run_analysis() - cross class→function calls edge., Same caller→callee pair must appear only once even if called multiple times., All edge sources must reference a known node (targets may be external imports). (+10 more)

### Community 9 - "Community 9"
Cohesion: 0.08
Nodes (13): CacheManager, createProcessor(), DataProcessor, Get-Data(), GraphifyDemo, IProcessor, Loggable, NetworkError (+5 more)

### Community 10 - "Community 10"
Cohesion: 0.07
Nodes (25): Tests for graphify/cache.py., Non-.md files are still hashed by their full content., _body_content correctly strips YAML frontmatter., _body_content returns content unchanged when no frontmatter present., Same file gives same hash on repeated calls., Different file contents give different hashes., Save then load returns the same result dict., After file content changes, load_cached returns None. (+17 more)

### Community 11 - "Community 11"
Cohesion: 0.11
Nodes (23): make_graph(), _make_simple_graph(), Tests for analyze.py., Code↔paper edge should score higher than code↔code edge., Helper: build a small nx.Graph from node/edge specs., Multi-file graph: should find cross-file edges between real entities., Concept nodes (empty source_file) must not appear in surprises., Single-file graph: should return cross-community edges, not empty list. (+15 more)

### Community 12 - "Community 12"
Cohesion: 0.11
Nodes (25): handle_delete(), handle_enrich(), handle_get(), handle_list(), handle_search(), handle_upload(), API module - exposes the document pipeline over HTTP. Thin layer over parser, va, Accept a list of file paths, run the full pipeline on each,     and return a sum (+17 more)

### Community 13 - "Community 13"
Cohesion: 0.12
Nodes (17): _call_pairs(), _confidences(), _labels(), Tests for multi-language AST extraction: JS/TS, Go, Rust., test_go_emits_calls(), test_go_finds_constructor(), test_go_finds_methods(), test_go_finds_struct() (+9 more)

### Community 14 - "Community 14"
Cohesion: 0.08
Nodes (25): Tests for graphify claude install / uninstall commands., claude_install also writes .claude/settings.json with PreToolUse hook., Running claude_install twice does not duplicate the PreToolUse hook., Creates CLAUDE.md when none exists., claude_uninstall removes the PreToolUse hook from settings.json., Written section includes the three rules., Appends to an existing CLAUDE.md without clobbering it., Running install twice does not duplicate the section. (+17 more)

### Community 15 - "Community 15"
Cohesion: 0.1
Nodes (24): attach_hyperedges(), _cypher_escape(), _html_script(), _html_styles(), _hyperedge_script(), prune_dangling_edges(), push_to_neo4j(), Store hyperedges in the graph's metadata dict. (+16 more)

### Community 16 - "Community 16"
Cohesion: 0.1
Nodes (6): _make_mock_response(), Tests for graphify/security.py - URL validation, safe fetch, path guards, label, test_safe_fetch_raises_on_non_2xx(), test_safe_fetch_returns_bytes(), test_safe_fetch_text_decodes_utf8(), test_safe_fetch_text_replaces_bad_bytes()

### Community 17 - "Community 17"
Cohesion: 0.09
Nodes (21): Tests for graphify.transcribe — video/audio transcription support., ImportError propagates when faster_whisper is not installed., Empty input returns empty list without error., transcribe_all() returns cached paths for already-transcribed files., transcribe_all() warns and skips files that fail to transcribe., Empty god_nodes returns fallback prompt., GRAPHIFY_WHISPER_PROMPT env var short-circuits LLM call., Returns a topic-based prompt from god node labels — no LLM call. (+13 more)

### Community 18 - "Community 18"
Cohesion: 0.16
Nodes (21): _detect_url_type(), _download_binary(), _fetch_arxiv(), _fetch_html(), _fetch_tweet(), _fetch_webpage(), _html_to_markdown(), ingest() (+13 more)

### Community 19 - "Community 19"
Cohesion: 0.18
Nodes (17): _make_graph(), Tests for serve.py - MCP graph query helpers (no mcp package required)., test_bfs_depth_1(), test_bfs_depth_2(), test_bfs_disconnected(), test_bfs_returns_edges(), test_communities_from_graph_basic(), test_communities_from_graph_isolated() (+9 more)

### Community 20 - "Community 20"
Cohesion: 0.17
Nodes (19): _make_graph(), Tests for graphify.wiki — Wikipedia-style article generation., God node with bad ID should not crash., Communities with more than 25 nodes show a truncation notice., test_article_navigation_footer(), test_community_article_has_audit_trail(), test_community_article_has_cross_links(), test_community_article_shows_cohesion() (+11 more)

### Community 21 - "Community 21"
Cohesion: 0.16
Nodes (17): build_graph(), cluster(), cohesion_score(), _partition(), Leiden community detection on NetworkX graphs. Splits oversized communities. Ret, Run a second Leiden pass on a community subgraph to split it further., Context manager to suppress stdout/stderr during library calls.      graspologic, Ratio of actual intra-community edges to maximum possible. (+9 more)

### Community 22 - "Community 22"
Cohesion: 0.16
Nodes (18): _body_content(), cache_dir(), cached_files(), check_semantic_cache(), clear_cache(), file_hash(), load_cached(), Strip YAML frontmatter from Markdown content, returning only the body. (+10 more)

### Community 23 - "Community 23"
Cohesion: 0.14
Nodes (17): _make_extraction(), Tests for confidence_score on edges., Edges lacking confidence_score get sensible defaults in to_json., Report summary line should include avg confidence for INFERRED edges., Surprising connections section shows confidence score next to INFERRED edges., Return a minimal extraction dict with one edge of each confidence type., EXTRACTED edges must have confidence_score == 1.0., INFERRED edges must have confidence_score between 0.0 and 1.0. (+9 more)

### Community 24 - "Community 24"
Cohesion: 0.14
Nodes (8): _make_report(), Tests for hyperedge support in graphify., Write graph.json then reload it - hyperedges must survive., test_hyperedges_roundtrip_via_json_file(), test_report_includes_hyperedge_node_list(), test_report_includes_hyperedges_section(), test_report_skips_hyperedges_section_when_empty(), test_report_skips_hyperedges_section_when_key_missing()

### Community 25 - "Community 25"
Cohesion: 0.12
Nodes (17): build_url_with_params(), flatten_queryparams(), is_known_encoding(), normalize_header_key(), obfuscate_sensitive_headers(), parse_content_type(), primitive_value_to_str(), Utility functions shared across the library. Small helpers that don't belong in (+9 more)

### Community 26 - "Community 26"
Cohesion: 0.18
Nodes (16): _make_extraction_with_semantic_edge(), _make_graph_with_semantic_edge(), _make_report_with_semantic_surprise(), _make_two_edge_graph(), Tests for semantically_similar_to edge support., Two nodes in separate files connected by a semantically_similar_to edge., Non-semantic edges must not get the [semantically similar] tag., Graph with one semantically_similar_to edge and one references edge, both cross- (+8 more)

### Community 27 - "Community 27"
Cohesion: 0.21
Nodes (16): delete_record(), _ensure_storage(), list_records(), load_index(), load_record(), Storage module - persists documents to disk and maintains the search index. All, Load the full document index from disk., Persist the index to disk. (+8 more)

### Community 28 - "Community 28"
Cohesion: 0.17
Nodes (13): _communities_from_graph(), _filter_blank_stdin(), _find_node(), _load_graph(), Return node IDs whose label or ID matches the search term (diacritic-insensitive, Filter blank lines from stdin before MCP reads it.      Some MCP clients (Claude, Start the MCP server. Requires pip install mcp., Reconstruct community dict from community property stored on nodes. (+5 more)

### Community 29 - "Community 29"
Cohesion: 0.23
Nodes (14): _make_git_repo(), Tests for hooks.py - git hook install/uninstall., test_install_appends_to_existing_hook(), test_install_creates_hook(), test_install_creates_post_checkout_hook(), test_install_idempotent(), test_install_is_executable(), test_install_post_checkout_is_executable() (+6 more)

### Community 30 - "Community 30"
Cohesion: 0.17
Nodes (13): _build_opener(), _NoFileRedirectHandler, Fetch *url* and return decoded text (UTF-8, replacing bad bytes).      Wraps saf, Resolve *path* and verify it stays inside *base*.      *base* defaults to the `g, Strip control characters and cap length.      Safe for embedding in JSON data (i, Raise ValueError if *url* is not http or https, or targets a private/internal IP, Redirect handler that re-validates every redirect target.      Prevents open-red, Fetch *url* and return raw bytes.      Protections applied:     - URL scheme val (+5 more)

### Community 31 - "Community 31"
Cohesion: 0.26
Nodes (14): make_graph(), test_to_cypher_contains_merge_statements(), test_to_cypher_creates_file(), test_to_graphml_creates_file(), test_to_graphml_has_community_attribute(), test_to_graphml_valid_xml(), test_to_html_contains_legend_with_labels(), test_to_html_contains_nodes_and_edges() (+6 more)

### Community 32 - "Community 32"
Cohesion: 0.29
Nodes (13): _make_graph(), Tests for graphify/benchmark.py., test_print_benchmark_no_crash(), test_query_bfs_expands_neighbors(), test_query_returns_positive_for_matching_question(), test_query_returns_zero_for_no_match(), test_run_benchmark_corpus_tokens_proportional(), test_run_benchmark_error_on_empty_graph() (+5 more)

### Community 33 - "Community 33"
Cohesion: 0.21
Nodes (13): build_whisper_prompt(), download_audio(), _get_whisper(), _get_yt_dlp(), is_url(), _model_name(), Transcribe a video/audio file or URL to a .txt transcript.      If video_path is, Transcribe a list of video/audio files or URLs, return paths to transcript .txt (+5 more)

### Community 34 - "Community 34"
Cohesion: 0.2
Nodes (13): batch_parse(), parse_and_save(), parse_file(), parse_json(), parse_markdown(), parse_plaintext(), Parser module - reads raw input documents and converts them into a structured fo, Read a file from disk and return a structured document. (+5 more)

### Community 35 - "Community 35"
Cohesion: 0.2
Nodes (13): enrich_document(), extract_keywords(), find_cross_references(), normalize_text(), process_and_save(), Processor module - transforms validated documents into enriched records ready fo, Lowercase, strip extra whitespace, remove control characters., Pull non-stopword tokens from text, deduplicated. (+5 more)

### Community 36 - "Community 36"
Cohesion: 0.22
Nodes (12): _git_root(), install(), _install_hook(), Walk up to find .git directory., Install a single git hook, appending if an existing hook is present., Remove graphify section from a git hook using start/end markers., Install graphify post-commit and post-checkout hooks in the nearest git repo., Remove graphify post-commit and post-checkout hooks. (+4 more)

### Community 37 - "Community 37"
Cohesion: 0.23
Nodes (9): make_graph(), Clustering should not emit ANSI escape codes or other output.      graspologic's, Same as above but for stderr — ANSI codes can go to either stream., test_cluster_covers_all_nodes(), test_cluster_does_not_write_to_stderr(), test_cluster_does_not_write_to_stdout(), test_cluster_returns_dict(), test_cohesion_score_range() (+1 more)

### Community 38 - "Community 38"
Cohesion: 0.26
Nodes (12): End-to-end pipeline test: detect → extract → build → cluster → analyze → report, Second run on unchanged corpus should produce identical node/edge counts., Run the full pipeline on the fixtures directory. Returns a dict of outputs., run_pipeline(), test_pipeline_all_nodes_have_community(), test_pipeline_detection_finds_code_and_docs(), test_pipeline_extraction_confidence_labels(), test_pipeline_graph_has_edges() (+4 more)

### Community 39 - "Community 39"
Cohesion: 0.21
Nodes (9): build(), build_from_json(), Build a NetworkX graph from an extraction dict.      directed=True produces a Di, Merge multiple extraction results into one graph., Merge multiple extraction results into one graph.      directed=True produces a, assert_valid(), Validate an extraction JSON dict against the graphify schema.     Returns a list, Raise ValueError with all errors if extraction is invalid. (+1 more)

### Community 40 - "Community 40"
Cohesion: 0.27
Nodes (11): Tests for rationale/docstring extraction in extract.py., # NOTE: must run before compile() or linker will fail, Trivial docstrings under 20 chars should not become rationale nodes., test_class_docstring_extracted(), test_function_docstring_extracted(), test_module_docstring_extracted(), test_rationale_comment_extracted(), test_rationale_confidence_is_extracted() (+3 more)

### Community 41 - "Community 41"
Cohesion: 0.17
Nodes (0): 

### Community 42 - "Community 42"
Cohesion: 0.38
Nodes (9): make_inputs(), test_report_contains_ambiguous_section(), test_report_contains_communities(), test_report_contains_corpus_check(), test_report_contains_god_nodes(), test_report_contains_header(), test_report_contains_surprising_connections(), test_report_shows_raw_cohesion_scores() (+1 more)

### Community 43 - "Community 43"
Cohesion: 0.2
Nodes (1): Tests for watch.py - file watcher helpers (no watchdog required).

### Community 44 - "Community 44"
Cohesion: 0.2
Nodes (1): Tests for graphify.ingest.save_query_result

### Community 45 - "Community 45"
Cohesion: 0.24
Nodes (1): ApiClient

### Community 46 - "Community 46"
Cohesion: 0.36
Nodes (8): _community_article(), _cross_community_links(), _god_node_article(), _index_md(), Return (community_label, edge_count) pairs for cross-community connections, sort, Generate a Wikipedia-style wiki from the graph.      Writes:       - index.md, _safe_filename(), to_wiki()

### Community 47 - "Community 47"
Cohesion: 0.28
Nodes (8): _estimate_tokens(), print_benchmark(), _query_subgraph_tokens(), Token-reduction benchmark - measures how much context graphify saves vs naive fu, Print a human-readable benchmark report., Run BFS from best-matching nodes and return estimated tokens in the subgraph con, Measure token reduction: corpus tokens vs graphify query tokens.      Args:, run_benchmark()

### Community 48 - "Community 48"
Cohesion: 0.39
Nodes (5): Analyzer, compute_score(), normalize(), Fixture: functions and methods that call each other - for call-graph extraction, run_analysis()

### Community 49 - "Community 49"
Cohesion: 0.36
Nodes (7): _has_non_code(), _notify_only(), Watch watch_path for new or modified files and auto-update the graph.      For c, Re-run AST extraction + build + cluster + report for code files. No LLM needed., Write a flag file and print a notification (fallback for non-code-only corpora)., _rebuild_code(), watch()

### Community 50 - "Community 50"
Cohesion: 0.43
Nodes (6): load_extraction(), test_ambiguous_edge_preserved(), test_build_from_json_edge_count(), test_build_from_json_node_count(), test_edges_have_confidence(), test_nodes_have_label()

### Community 51 - "Community 51"
Cohesion: 0.43
Nodes (6): EventServiceProvider, NotifyAdmins, OrderPlaced, SendWelcomeEmail, ShipOrder, UserRegistered

### Community 52 - "Community 52"
Cohesion: 0.47
Nodes (2): build_graph(), Graph

### Community 53 - "Community 53"
Cohesion: 0.33
Nodes (5): Animal, -initWithName, -speak, Dog, -fetch

### Community 54 - "Community 54"
Cohesion: 0.47
Nodes (4): AppServiceProvider, CashierGateway, PaymentGateway, StripeGateway

### Community 55 - "Community 55"
Cohesion: 0.6
Nodes (2): RateLimiter, Throttle

### Community 56 - "Community 56"
Cohesion: 0.6
Nodes (2): ColorResolver, DefaultPalette

### Community 57 - "Community 57"
Cohesion: 0.5
Nodes (3): MyApp.Accounts.User, create(), validate()

### Community 58 - "Community 58"
Cohesion: 0.67
Nodes (3): generate(), Mirrors export.safe_name so community hub filenames and report wikilinks always, _safe_community_name()

### Community 59 - "Community 59"
Cohesion: 0.5
Nodes (1): Transformer

### Community 60 - "Community 60"
Cohesion: 0.67
Nodes (1): graphify - extract · build · cluster · analyze · report.

### Community 61 - "Community 61"
Cohesion: 1.0
Nodes (0): 

### Community 62 - "Community 62"
Cohesion: 1.0
Nodes (0): 

## Knowledge Gaps
- **327 isolated node(s):** `Mirrors export.safe_name so community hub filenames and report wikilinks always`, `Store hyperedges in the graph's metadata dict.`, `Remove edges whose source or target node is not in the node set.      Returns th`, `Escape a string for safe embedding in a Cypher single-quoted literal.`, `Generate an interactive vis.js HTML visualization of the graph.      Features: n` (+322 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **Thin community `Community 61`** (1 nodes): `manifest.py`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.
- **Thin community `Community 62`** (1 nodes): `__init__.py`
  Too small to be a meaningful cluster - may be noise or needs more connections extracted.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `ValidationError` connect `Community 12` to `Community 0`?**
  _High betweenness centrality (0.005) - this node is a cross-community bridge._
- **Why does `Cookies` connect `Community 0` to `Community 25`?**
  _High betweenness centrality (0.005) - this node is a cross-community bridge._
- **Are the 39 inferred relationships involving `Response` (e.g. with `Auth` and `BasicAuth`) actually correct?**
  _`Response` has 39 INFERRED edges - model-reasoned connections that need verification._
- **Are the 39 inferred relationships involving `Request` (e.g. with `Auth` and `BasicAuth`) actually correct?**
  _`Request` has 39 INFERRED edges - model-reasoned connections that need verification._
- **Are the 19 inferred relationships involving `Cookies` (e.g. with `Utility functions shared across the library. Small helpers that don't belong in` and `Convert a primitive value to its string representation.`) actually correct?**
  _`Cookies` has 19 INFERRED edges - model-reasoned connections that need verification._
- **Are the 12 inferred relationships involving `Client` (e.g. with `Request` and `Response`) actually correct?**
  _`Client` has 12 INFERRED edges - model-reasoned connections that need verification._
- **What connects `Mirrors export.safe_name so community hub filenames and report wikilinks always`, `Store hyperedges in the graph's metadata dict.`, `Remove edges whose source or target node is not in the node set.      Returns th` to the rest of the system?**
  _327 weakly-connected nodes found - possible documentation gaps or missing edges._