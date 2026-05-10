# Wedgwood Web Works MCP Servers

[![Code style: crackerjack](https://img.shields.io/badge/code%20style-crackerjack-000042)](https://github.com/lesleslie/crackerjack)
[![Runtime: oneiric](https://img.shields.io/badge/runtime-oneiric-6e5494)](https://github.com/lesleslie/oneiric)
[![Framework: FastMCP](https://img.shields.io/badge/framework-FastMCP-0ea5e9)](https://github.com/jlowin/fastmcp)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
[![Python: 3.13+](https://img.shields.io/badge/python-3.13%2B-green)](https://www.python.org/downloads/)

A collection of MCP servers built on the **Oneiric + mcp-common + FastMCP** stack.

This catalog covers the `*-mcp` repositories in the Wedgwood Web Works ecosystem. It does not attempt to list every sibling repo in the organization.

## Architecture

These servers use a layered architecture that eliminates boilerplate and provides production-grade reliability:

- **[FastMCP](https://github.com/jlowin/fastmcp)** - Tool/Resource decorators for clean API definitions
- **[mcp-common](https://github.com/lesleslie/mcp-common)** - Template Method Pattern with unified CLI (start/stop/restart/status/health), PID management, graceful shutdown, and security validation
- **[Oneiric](https://github.com/lesleslie/oneiric)** - Snapshot management, caching with TTL, and health probes

## MCP Servers

| Server | Description | GitHub |
|--------|-------------|--------|
| **css-mcp** | CSS analysis and documentation for the FastBlocks ecosystem | [github.com/lesleslie/css-mcp](https://github.com/lesleslie/css-mcp) |
| **excalidraw-mcp** | Real-time collaborative diagramming with WebSocket sync | [github.com/lesleslie/excalidraw-mcp](https://github.com/lesleslie/excalidraw-mcp) |
| **graphics-mcp** | Image manipulation via Pillow/pilkit | [github.com/lesleslie/graphics-mcp](https://github.com/lesleslie/graphics-mcp) |
| **langsmith-mcp** | LangSmith observability for traces, prompts, datasets, and experiments | [github.com/lesleslie/langsmith-mcp](https://github.com/lesleslie/langsmith-mcp) |
| **mailgun-mcp** | Full Mailgun API coverage - email, domains, events, suppression lists | [github.com/lesleslie/mailgun-mcp](https://github.com/lesleslie/mailgun-mcp) |
| **n8n-mcp** | n8n workflow automation integration | [github.com/lesleslie/n8n-mcp](https://github.com/lesleslie/n8n-mcp) |
| **neo4j-mcp** | Neo4j graph database integration | [github.com/lesleslie/neo4j-mcp](https://github.com/lesleslie/neo4j-mcp) |
| **opera-cloud-mcp** | Oracle Opera Cloud hospitality PMS integration | [github.com/lesleslie/opera-cloud-mcp](https://github.com/lesleslie/opera-cloud-mcp) |
| **porkbun-dns-mcp** | Porkbun DNS record management | [github.com/lesleslie/porkbun-dns-mcp](https://github.com/lesleslie/porkbun-dns-mcp) |
| **porkbun-domain-mcp** | Porkbun domain management | [github.com/lesleslie/porkbun-domain-mcp](https://github.com/lesleslie/porkbun-domain-mcp) |
| **raindropio-mcp** | Bookmark management with batch operations and filtering | [github.com/lesleslie/raindropio-mcp](https://github.com/lesleslie/raindropio-mcp) |
| **spline-mcp** | Spline.design 3D scene orchestration | [github.com/lesleslie/spline-mcp](https://github.com/lesleslie/spline-mcp) |
| **synxis-crs-mcp** | SynXis Central Reservation System integration | [github.com/lesleslie/synxis-crs-mcp](https://github.com/lesleslie/synxis-crs-mcp) |
| **synxis-pms-mcp** | SynXis Property Management System integration | [github.com/lesleslie/synxis-pms-mcp](https://github.com/lesleslie/synxis-pms-mcp) |
| **unifi-mcp** | UniFi Network and Access controller management | [github.com/lesleslie/unifi-mcp](https://github.com/lesleslie/unifi-mcp) |

## Why WWW MCP Servers?

Most MCP servers in the wild are built directly on the MCP SDK, resulting in inconsistent patterns, missing production safeguards, and no standardized tooling. Official servers from Anthropic are explicitly labeled as "reference implementations" for educational purposes, while community servers carry warnings that they are "untested and should be used at your own risk."

WWW MCP servers are different. Built on our shared **mcp-common** foundation, every server delivers:

- **Consistency** - Unified CLI, identical configuration patterns, and predictable behavior across all servers
- **Production-ready** - PID file management with stale recovery, graceful shutdown handling, health persistence, and comprehensive error handling
- **Security-first** - API key format validation, input sanitization, and automatic credential masking in logs
- **Maintained** - Active development with a single codebase (mcp-common) driving improvements across all servers

When you use a WWW MCP server, you're not getting a weekend project or a reference implementation—you're getting a dependable integration built on a battle-tested stack that's designed to run reliably in production environments.

---

**Wedgwood Web Works**
