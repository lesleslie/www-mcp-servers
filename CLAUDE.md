# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **meta-project** - a documentation-only repository that lists Wedgwood Web Works MCP servers. There is no code to build, test, or lint here.

## Related Repositories

The actual MCP servers live in separate repositories:

- **[mcp-common](https://github.com/lesleslie/mcp-common)** - Shared foundation for all WWW MCP servers
- **[oneiric](https://github.com/lesleslie/oneiric)** - Runtime with snapshot management and caching
- **[crackerjack](https://github.com/lesleslie/crackerjack)** - Code quality and development platform

## Updating This Repository

The README.md is the primary artifact. When adding new MCP servers:

1. Add the server to the table in README.md
2. Include GitHub link if published, or mark as "*(in development)*"
3. Keep descriptions concise (one line)

## Standard Badges

WWW repositories should include these badges:
- crackerjack (code style)
- oneiric (runtime)
- uv (package manager)
- Python 3.13+

For repositories with MCP servers, also include:
- fastmcp (framework)

## License

BSD 3-Clause
