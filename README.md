# Wedgwood Web Works MCP Servers

[![Code style: crackerjack](https://img.shields.io/badge/code%20style-crackerjack-000042)](https://github.com/lesleslie/crackerjack)
[![Runtime: oneiric](https://img.shields.io/badge/runtime-oneiric-6e5494)](https://github.com/lesleslie/oneiric)
[![Framework: FastMCP](https://img.shields.io/badge/framework-FastMCP-0ea5e9)](https://github.com/jlowin/fastmcp)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
[![Python: 3.13+](https://img.shields.io/badge/python-3.13%2B-green)](https://www.python.org/downloads/)

Catalog and operating map for the Wedgwood Web Works MCP server repositories.

**Status:** Internal Bodai ecosystem catalog

## Quick Links

- [Overview](#overview)
- [Architecture](#architecture)
- [MCP Servers](#mcp-servers)
- [Operating Model](#operating-model)
- [Common Commands](#common-commands)
- [Documentation Standards](#documentation-standards)
- [Security Notes](#security-notes)

## Quality & CI

Crackerjack is the standard quality-control and CI/CD gate across the MCP server repos. Individual repositories may still expose direct `pytest`, `ruff`, `pyright`, or `mypy` commands for targeted debugging, but repo-level validation should stay aligned with the Crackerjack workflow.

______________________________________________________________________

## Overview

This repository is the catalog for the `*-mcp` servers in the Wedgwood Web Works and Bodai ecosystem. It documents the shared stack, lists the active server repos, and provides a common operator orientation for local development and MCP client wiring.

The catalog is not itself an MCP server package. Use it as the index when deciding which integration server owns a capability, which port it normally binds to, and which repo README should hold detailed setup and tool documentation.

## Architecture

These servers use a layered architecture that keeps provider-specific code small and consistent:

- **FastMCP**: tool and route registration for the MCP protocol surface
- **mcp-common**: standard lifecycle CLI with `start`, `stop`, `restart`, `status`, and `health`
- **Oneiric**: shared runtime patterns, structured logging, snapshots, and health conventions
- **Pydantic**: typed request, response, and settings models
- **UV**: dependency management and local command execution

Typical server shape:

```text
<server>_mcp/
  cli.py        # mcp-common lifecycle CLI
  client.py     # provider API boundary, when needed
  config.py     # Pydantic settings and logging
  models.py     # typed domain models
  server.py     # FastMCP application factory
  tools/        # registered MCP tools
settings/
  <server>.yaml # committed defaults
tests/
```

## MCP Servers

| Server | Role | Default Port | Description |
|--------|------|--------------|-------------|
| [css-mcp](https://github.com/lesleslie/css-mcp) | CSS analysis | 3050 | CSS metrics, MDN docs, browser compatibility, and project analysis |
| [excalidraw-mcp](https://github.com/lesleslie/excalidraw-mcp) | Diagramming | 3044 | Real-time collaborative Excalidraw scene and WebSocket workflows |
| [graphics-mcp](https://github.com/lesleslie/graphics-mcp) | Image operations | 3040 | Raster image metadata, conversion, resizing, cropping, filters, and thumbnails |
| [langsmith-mcp](https://github.com/lesleslie/langsmith-mcp) | Observability | varies | LangSmith traces, prompts, datasets, experiments, and usage lookup |
| [mailgun-mcp](https://github.com/lesleslie/mailgun-mcp) | Email operations | varies | Mailgun email, domains, events, suppression lists, templates, and validation |
| [neo4j-mcp](https://github.com/lesleslie/neo4j-mcp) | Graph database | 3045 | Cypher, node, relationship, path, and schema operations |
| [opera-cloud-mcp](https://github.com/lesleslie/opera-cloud-mcp) | Hospitality PMS | varies | Oracle OPERA Cloud reservations, guests, rooms, operations, and financial data |
| [porkbun-dns-mcp](https://github.com/lesleslie/porkbun-dns-mcp) | DNS management | 3042 | Porkbun DNS record listing, creation, editing, and deletion |
| [porkbun-domain-mcp](https://github.com/lesleslie/porkbun-domain-mcp) | Domain lifecycle | 3043 | Porkbun domain inventory, metadata, auth codes, renewal, and pricing |
| [raindropio-mcp](https://github.com/lesleslie/raindropio-mcp) | Bookmarks | varies | Raindrop.io bookmark, collection, tag, batch, and filtering operations |
| [spline-mcp](https://github.com/lesleslie/spline-mcp) | 3D scenes | varies | Spline.design scene orchestration and asset workflows |
| [synxis-crs-mcp](https://github.com/lesleslie/synxis-crs-mcp) | Reservations | 3046 | SynXis CRS property search, availability, rates, and booking |
| [synxis-pms-mcp](https://github.com/lesleslie/synxis-pms-mcp) | Property operations | 3047 | SynXis PMS guest, room, check-in, check-out, and folio workflows |
| [unifi-mcp](https://github.com/lesleslie/unifi-mcp) | Network operations | varies | UniFi Network and Access controller management |

## Operating Model

The servers should feel interchangeable at the operational layer even when their provider APIs differ.

Expected common behavior:

- `uv sync --group dev` installs local development dependencies
- `uv run <server-name> start` starts the HTTP MCP server
- `uv run <server-name> health` returns local health metadata
- `settings/<server>.yaml` contains committed defaults
- environment variables override committed defaults
- provider credentials stay in environment variables, local `.env` files, or a secret manager
- `/health` and `/healthz` are available on HTTP-enabled servers that follow the current template

## Common Commands

Run these from an individual server repo:

```bash
uv sync --group dev
uv run <server-name> start
uv run <server-name> status
uv run <server-name> health
uv run pytest
uv run ruff check <package_name> tests
uv run ruff format <package_name> tests
```

Some repos use `pyright`; others use `mypy`. Follow the individual README and `pyproject.toml` for the authoritative type-check command.

## Documentation Standards

Each server README should include:

- badges for Crackerjack, Oneiric, FastMCP, UV, and Python
- a one-line purpose statement
- version and status
- quick links
- Quality & CI notes
- overview and capability bullets
- quick start with mock mode when available
- standard lifecycle CLI commands
- MCP client configuration example
- tool reference table
- configuration table
- project structure
- development commands
- security notes tailored to that provider

Keep catalog-level summaries here. Put detailed setup, provider-specific examples, and tool-level behavior in each server repo.

## Security Notes

- Never commit provider credentials, bearer tokens, customer data, or generated local `.env` files.
- Treat mutating tools as privileged operations, especially DNS, domain renewal, email sending, database mutation, reservation creation, and hospitality check-in/check-out workflows.
- Keep ports, hosts, provider URLs, tenant IDs, and account settings configurable.
- Scrub real domains, email addresses, hotel data, guest data, graph data, and local paths before sharing examples outside local development.

## Why WWW MCP Servers?

Most MCP servers in the wild are built directly on the MCP SDK, resulting in inconsistent patterns, missing production safeguards, and no standardized tooling. WWW MCP servers are built on the shared `mcp-common` foundation so each server gets the same operational model while keeping provider-specific logic isolated.

That gives the ecosystem:

- **Consistency**: unified CLI, configuration patterns, and health behavior
- **Production posture**: PID management, stale process recovery, graceful shutdown, and health persistence where supported
- **Security focus**: credential masking, input validation, and narrow provider boundaries
- **Maintainability**: improvements to shared lifecycle behavior can flow through the server fleet

---

**Wedgwood Web Works**
