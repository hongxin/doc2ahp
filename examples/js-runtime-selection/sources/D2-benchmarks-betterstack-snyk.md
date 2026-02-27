# D2: Performance & Feature Benchmarks (BetterStack & Snyk)

**Sources**:
- https://betterstack.com/community/guides/scaling-nodejs/nodejs-vs-deno-vs-bun/
- https://snyk.io/blog/javascript-runtime-compare-node-deno-bun/
**Fetched**: 2026-02-27

## HTTP Throughput — Express Framework (Average req/sec)

| Runtime | Avg req/sec | Ping | Query |
|---------|-------------|------|-------|
| Bun | 52,479.34 | 58,955.77 | 50,583.29 |
| Deno | 22,286.51 | 23,318.99 | 22,414.20 |
| Node.js | 13,254.55 | 16,821.80 | 16,250.99 |

## React SSR Throughput (Snyk data)

| Runtime | Requests/sec |
|---------|-------------|
| Bun | 68,000 |
| Deno | 29,000 |
| Node.js | 14,000 |

## SQLite Database Queries (Snyk data, queries/sec)

| Runtime | Queries/sec |
|---------|-------------|
| Bun | 81.37 |
| Deno | 43.50 |
| Node.js | 21.29 |

## Concurrent Connections — 10 concurrent (Snyk data, req/sec)

| Runtime | Requests/sec |
|---------|-------------|
| Bun | 110,000 |
| Deno | 67,000 |
| Node.js | 60,000 |

## Startup Time

| Runtime | Cold Start |
|---------|------------|
| Bun | ~5 ms |
| Node.js | ~25 ms |
| Deno | not specified (between Node and Bun) |

## Stack Overflow Questions (Dec 2024)

| Runtime | Tagged Questions |
|---------|----------------|
| Node.js | 475,028 |
| Deno | 1,105 |
| Bun | 264 |
