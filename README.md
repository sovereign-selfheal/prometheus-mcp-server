# prometheus-mcp-server

MCP server (FastMCP, `streamable-http` at `/mcp`) exposing PromQL queries against Thanos
Querier as MCP tools:

| Tool | Description |
|---|---|
| `query_prometheus` | Instant PromQL query |
| `query_prometheus_range` | Range query (default 30 min) with min/avg/max summary |

Used by the `triage-agent` demo to read error rates and latency from
`quarkus-buggy-app`, via the in-cluster Thanos Querier
(`https://thanos-querier.openshift-monitoring.svc:9091`).

## Build

```bash
podman build -t quay.io/sovereign-selfheal/prometheus-mcp-server:<tag> .
```

CI (`.github/workflows/build.yml`) runs on pull requests and pushes to `main` to verify
that this image builds (no push). Quay builds/pushes the tagged release image separately.

## Consumer

The Kubernetes manifest (`MCPServer` CR) and the pinned image digest live in the `gitops`
repo, `components/prometheus-mcp-server/`. This repo only owns the source and the build.
