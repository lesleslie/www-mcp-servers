# WWW MCP Servers — Port Map

Authoritative port assignments for the `*-mcp` server fleet. The catalog `README.md` references these defaults; each server's `pyproject.toml` and/or `settings/<name>.yaml` is the runtime source of truth. When the values disagree, the **runtime source wins** and this map should be updated to match.

## Port allocation policy

- Default ports span **3032–3052** with intentional gaps.
- New servers pick the next free slot above the current maximum (currently **3052**, so the next server should use **3053** or higher).
- Gaps in the range (3033, 3035, 3036, 3041, 3049) are reserved for retired servers — please don't reuse them.

## Servers

Sorted by port. HTTP transport on the listed port unless noted.

| Server | Default Port | Source of truth | Role |
|---|---|---|---|
| [excalidraw-mcp](https://github.com/lesleslie/excalidraw-mcp) | 3032 | `excalidraw-mcp/pyproject.toml` (`mcp_http_port`) | Diagramming |
| [raindropio-mcp](https://github.com/lesleslie/raindropio-mcp) | 3034 | `raindropio-mcp/pyproject.toml` (`http_port`) | Bookmarks |
| [opera-cloud-mcp](https://github.com/lesleslie/opera-cloud-mcp) | 3037 | `opera-cloud-mcp/pyproject.toml` (`http_port`) | Hospitality PMS |
| [unifi-mcp](https://github.com/lesleslie/unifi-mcp) | 3038 | `unifi-mcp/pyproject.toml` (`http_port`) | Network operations |
| [mailgun-mcp](https://github.com/lesleslie/mailgun-mcp) | 3039 | `mailgun-mcp/pyproject.toml` (`http_port`) | Email operations |
| [graphics-mcp](https://github.com/lesleslie/graphics-mcp) | 3040 | `graphics-mcp/settings/graphics.yaml` (`http_port`) | Image operations |
| [porkbun-dns-mcp](https://github.com/lesleslie/porkbun-dns-mcp) | 3042 | `porkbun-dns-mcp/pyproject.toml` + `settings/porkbun-dns.yaml` | DNS management |
| [porkbun-domain-mcp](https://github.com/lesleslie/porkbun-domain-mcp) | 3043 | `porkbun-domain-mcp/pyproject.toml` + `settings/porkbun-domain.yaml` | Domain lifecycle |
| [neo4j-mcp](https://github.com/lesleslie/neo4j-mcp) | 3045 | `neo4j-mcp/settings/neo4j.yaml` (`http_port`) | Graph database |
| [synxis-crs-mcp](https://github.com/lesleslie/synxis-crs-mcp) | 3046 | `synxis-crs-mcp/pyproject.toml` + `settings/synxis-crs.yaml` | Reservations |
| [synxis-pms-mcp](https://github.com/lesleslie/synxis-pms-mcp) | 3047 | `synxis-pms-mcp/pyproject.toml` + `settings/synxis-pms.yaml` | Property operations |
| [langsmith-mcp](https://github.com/lesleslie/langsmith-mcp) | 3048 | `langsmith-mcp/pyproject.toml` + `settings/langsmith.yaml` | Observability |
| [css-mcp](https://github.com/lesleslie/css-mcp) | 3050 | `css-mcp/settings/css-mcp.yaml` (`http_port`) | CSS analysis |
| [penpot-api-mcp](https://github.com/lesleslie/penpot-api-mcp) | 3051 | `penpot-api-mcp/pyproject.toml` + `settings/penpot_api_mcp.yaml` | Design automation |
| [spline-mcp](https://github.com/lesleslie/spline-mcp) | 3052 | `spline-mcp/settings/spline.yaml` (`http_port`) | 3D scenes |

## Secondary ports

Some servers expose additional listeners beyond the MCP HTTP transport. Document them here so collisions don't surprise operators.

| Server | Secondary port | Purpose |
|---|---|---|
| excalidraw-mcp | 3060 | Canvas WebSocket server (`WEBSOCKET_PORT` env var). Renumbered 2026-08-31 to resolve the latent collision with `porkbun-dns-mcp`. |
| excalidraw-mcp | 3031 | TypeScript canvas server dev port (legacy; only used when running the Express server directly, not via the plugin). |

## Change log

- **2026-08-31** — `excalidraw-mcp` WebSocket canvas server renumbered 3042 → 3060 (collision with `porkbun-dns-mcp`).
- **2026-08-31** — `excalidraw-mcp` config key renamed `mcp_http_port` → `http_port` (and `mcp_http_host` → `http_host`) for ecosystem consistency.
- **2026-08-31** — `spline-mcp` renumbered 3048 → 3052 (collision with `langsmith-mcp`).
- **2026-08-31** — `excalidraw-mcp` corrected in `README.md` (3044 → 3032). The previous 3044 value did not match any source file.
- **2026-08-31** — `penpot-api-mcp` added (3051).
- **2026-08-31** — All `varies` placeholders replaced with concrete defaults sourced from each repo's config.

## Audit procedure

To detect future drift:

```bash
# For each server, grep its config for the declared port and compare to this map.
for s in /Users/les/Projects/*-mcp; do
  port=$(grep -hE '(http_port|mcp_http_port)\s*[=:]\s*[0-9]{4}' \
    "$s/pyproject.toml" "$s"/settings/*.yaml 2>/dev/null \
    | grep -oE '[0-9]{4}' | head -1)
  echo "$(basename "$s"): $port"
done
```

If any output disagrees with this map, the map is the source of truth to update — or vice versa, after investigation.
