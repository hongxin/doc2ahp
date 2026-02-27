# D1: Performance Benchmarks (RepoFlow)

**Source**: https://www.repoflow.io/blog/node-js-vs-deno-vs-bun-performance-benchmarks
**Fetched**: 2026-02-27
**Versions Tested**: Node 25.6.1 / Deno 2.6.9 / Bun 1.3.9

## HTTP GET Throughput (requests/second, p50)

| Runtime | Requests/sec |
|---------|-------------|
| Node 25.6.1 | 29,741.4 |
| Deno 2.6.9 | 32,632.4 |
| Bun 1.3.9 | 146,328.47 |

## JSON.parse 1KB (operations/second, p50)

| Runtime | Ops/sec |
|---------|---------|
| Node 25.6.1 | 1,665,362.13 |
| Deno 2.6.9 | 1,712,171.18 |
| Bun 1.3.9 | 3,401,606.41 |

## JSON.parse 100KB (operations/second, p50)

| Runtime | Ops/sec |
|---------|---------|
| Node 25.6.1 | 34,915.37 |
| Deno 2.6.9 | 35,113.55 |
| Bun 1.3.9 | 150,248.57 |

## JSON.stringify Small Object (operations/second, p50)

| Runtime | Ops/sec |
|---------|---------|
| Node 25.6.1 | 3,939,424.73 |
| Deno 2.6.9 | 4,269,231.94 |
| Bun 1.3.9 | 3,685,124.53 |

## JSON.stringify Medium Object (operations/second, p50)

| Runtime | Ops/sec |
|---------|---------|
| Node 25.6.1 | 81,640.03 |
| Deno 2.6.9 | 82,825.99 |
| Bun 1.3.9 | 134,715.97 |
