# QWEN.md

This file provides guidance to Qwen Code when working with code in this repository.

## Repository Purpose

This is a **meta-project** - a documentation-only repository that catalogs Wedgwood Web Works MCP servers. There is no code to build, test, or lint here. The repository serves as a central index and reference point for the MCP server ecosystem.

## Related Repositories

The actual MCP servers and their shared foundations live in separate repositories:

| Repository | Purpose |
|------------|---------|
| **[mcp-common](https://github.com/lesleslie/mcp-common)** | Shared foundation for all WWW MCP servers (Template Method Pattern, unified CLI, PID management, graceful shutdown, security validation) |
| **[oneiric](https://github.com/lesleslie/oneiric)** | Runtime with snapshot management, caching with TTL, and health probes |
| **[crackerjack](https://github.com/lesleslie/crackerjack)** | Code quality and development platform (pytest, ruff, bandit, creosote) |

## MCP Servers Catalog

| Server | Description | Status |
|--------|-------------|--------|
| **excalidraw-mcp** | Real-time collaborative diagramming with WebSocket sync | Published |
| **mailgun-mcp** | Full Mailgun API coverage - email, domains, events, suppression lists | Published |
| **opera-cloud-mcp** | Oracle Opera Cloud hospitality PMS integration | Published |
| **porkbun-dns-mcp** | Porkbun DNS record management | In development |
| **porkbun-domain-mcp** | Porkbun domain management | In development |
| **raindropio-mcp** | Bookmark management with batch operations and filtering | Published |
| **synxis-crs-mcp** | Synxis Central Reservation System integration | In development |
| **synxis-pms-mcp** | Synxis Property Management System integration | In development |
| **unifi-mcp** | UniFi Network and Access controller management | Published |

## Architecture Stack

WWW MCP servers are built on a layered architecture:

```
┌─────────────────────────────────────────┐
│         FastMCP (Framework)             │  → Tool/Resource decorators for clean API definitions
├─────────────────────────────────────────┤
│         mcp-common (Foundation)         │  → Template Method Pattern, CLI, PID management, security
├─────────────────────────────────────────┤
│         Oneiric (Runtime)               │  → Snapshot management, caching, health probes
└─────────────────────────────────────────┘
```

## Updating This Repository

### Adding a New MCP Server

When a new server is added to the ecosystem:

1. Add an entry to the MCP Servers table in `README.md`
2. Include a GitHub link if published, or mark as "*(in development)*"
3. Keep descriptions concise (one line)
4. Update this QWEN.md if new patterns emerge

### Standard Badges

WWW MCP server repositories should include these badges in their README:
- `crackerjack` (code style)
- `oneiric` (runtime)
- `uv` (package manager)
- `Python 3.13+`
- `FastMCP` (framework) - for MCP server repos

## License

**BSD 3-Clause** - See `LICENSE` file for full terms.

## Git Workflow

This repository uses standard git workflow. Recent commits show:
- Checkpoint commits with quality scores (from crackerjack)
- Documentation updates for repository guidance

## Key Differentiators

WWW MCP servers prioritize:
- **Consistency** - Unified CLI, identical configuration patterns, predictable behavior
- **Production-ready** - PID file management, graceful shutdown, health persistence, comprehensive error handling
- **Security-first** - API key validation, input sanitization, credential masking in logs
- **Maintained** - Active development with shared codebase driving improvements across all servers
