# Graph Report - distributed-ops-mcp-server  (2026-10-23)

## Corpus Check
- Large corpus: 500 files · ~680,437 words. Semantic extraction will be expensive (many Claude tokens). Consider running on a subfolder.

## Summary
- 10 nodes · 17 edges · 2 communities
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Distributed Infrastructure Ops Cockpit
- AI-driven Ops Cockpit MCP

## God Nodes (most connected - your core abstractions)
1. `Distributed Infrastructure Ops Cockpit & MCP Server - Case Study README` - 9 edges
2. `Unified multi-backend tool registry (hr_*, bot_*, infra_* namespaces)` - 6 edges
3. `AI-driven Ops Cockpit MCP Server` - 4 edges
4. `FastMCP server engine (stdio transport)` - 3 edges
5. `hr_* tools: Cloud PostgreSQL via pg8000` - 2 edges
6. `bot_* tools: remote VM SQLite over SSH (sqlite3 -readonly)` - 2 edges
7. `infra_* tools: containerized MongoDB via docker exec` - 2 edges
8. `Strict read-only security model (zero mutation guarantee)` - 2 edges
9. `Credential & secret scrubbing of query outputs before LLM transmission` - 2 edges
10. `Pydantic schema-validated tool definitions` - 2 edges

## Surprising Connections (you probably didn't know these)
- `Distributed Infrastructure Ops Cockpit & MCP Server - Case Study README` --references--> `FastMCP server engine (stdio transport)`  [EXTRACTED]
  README.md → README.md  _Bridges community 0 → community 1_

## Hyperedges (group relationships)
- **Ops Cockpit read-only access across PostgreSQL, SQLite and MongoDB backends** — distributed_ops_mcp_server_readme_fastmcp_stdio_engine, distributed_ops_mcp_server_readme_unified_tool_registry, distributed_ops_mcp_server_readme_hr_postgresql_backend, distributed_ops_mcp_server_readme_bot_sqlite_ssh_backend, distributed_ops_mcp_server_readme_infra_mongodb_backend, distributed_ops_mcp_server_readme_read_only_security_model [EXTRACTED 1.00]

## Communities (2 total, 0 thin omitted)

### Community 0 - "Distributed Infrastructure Ops Cockpit"
Cohesion: 0.60
Nodes (6): Distributed Infrastructure Ops Cockpit & MCP Server - Case Study README, bot_* tools: remote VM SQLite over SSH (sqlite3 -readonly), hr_* tools: Cloud PostgreSQL via pg8000, infra_* tools: containerized MongoDB via docker exec, Strict read-only security model (zero mutation guarantee), Unified multi-backend tool registry (hr_*, bot_*, infra_* namespaces)

### Community 1 - "AI-driven Ops Cockpit MCP"
Cohesion: 0.50
Nodes (4): FastMCP server engine (stdio transport), AI-driven Ops Cockpit MCP Server, Pydantic schema-validated tool definitions, Credential & secret scrubbing of query outputs before LLM transmission

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Distributed Infrastructure Ops Cockpit & MCP Server - Case Study README` connect `Distributed Infrastructure Ops Cockpit` to `AI-driven Ops Cockpit MCP`?**
  _High betweenness centrality (0.583) - this node is a cross-community bridge._
- **Why does `Unified multi-backend tool registry (hr_*, bot_*, infra_* namespaces)` connect `Distributed Infrastructure Ops Cockpit` to `AI-driven Ops Cockpit MCP`?**
  _High betweenness centrality (0.139) - this node is a cross-community bridge._
- **Why does `AI-driven Ops Cockpit MCP Server` connect `AI-driven Ops Cockpit MCP` to `Distributed Infrastructure Ops Cockpit`?**
  _High betweenness centrality (0.042) - this node is a cross-community bridge._