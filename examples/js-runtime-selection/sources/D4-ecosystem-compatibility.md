# D4: Ecosystem & Compatibility Data

**Sources**:
- https://dev.to/pockit_tools/deno-2-vs-nodejs-vs-bun-in-2026-the-complete-javascript-runtime-comparison-1elm
- https://dev.to/jsgurujobs/bun-vs-deno-vs-nodejs-in-2026-benchmarks-code-and-real-numbers-2l9d
- https://pullflow.com/blog/deno-vs-bun-2025/
- npm registry, JSR registry
**Fetched**: 2026-02-27

## npm Ecosystem Size

- npm registry: ~3.1 million packages (as of 2025-2026)
- Weekly downloads: billions (npm is the world's largest software registry)

## Runtime Compatibility with npm

| Runtime | npm Compatibility | Notes |
|---------|------------------|-------|
| Node.js | 100% | npm is built for Node.js |
| Bun | ~95% | Most popular packages work; edge cases in native addons |
| Deno | ~90% | Deno 2.0 added `npm:` specifier; some Node APIs still incomplete |

## Package Management Speed (1,847 dependencies monorepo)

| Tool | Install Time |
|------|-------------|
| npm install | 28 minutes |
| pnpm install | 4 minutes |
| bun install | 47 seconds |

## TypeScript Support

| Runtime | TypeScript | Notes |
|---------|-----------|-------|
| Node.js | Via --strip-types (v22.6+) or ts-node | Native type stripping added recently; no type checking |
| Deno | Native, first-class | Built-in TS compiler, type checking included |
| Bun | Native, first-class | Built-in transpiler, fastest TS execution |

## Security Model

| Runtime | Security Approach |
|---------|-------------------|
| Node.js | Unrestricted by default; experimental --permission flag |
| Deno | Permissions-based sandbox by default (--allow-net, --allow-read, etc.) |
| Bun | Unrestricted by default (like Node.js) |

## Built-in Tooling

| Feature | Node.js | Deno | Bun |
|---------|---------|------|-----|
| Package manager | npm (separate) | Built-in (+ JSR) | Built-in (bun install) |
| Test runner | node:test (v18+) | deno test | bun test |
| Bundler | None (use webpack/vite) | deno bundle (deprecated) | bun build |
| Linter | None (use eslint) | deno lint | None |
| Formatter | None (use prettier) | deno fmt | None |

## Development Governance

| Metric | Node.js | Deno | Bun |
|--------|---------|------|-----|
| Governance | OpenJS Foundation, open | Deno Land Inc. (VC-backed) | Oven (VC-backed) |
| Core team ownership | Community-driven | 28% community | 92% core team |
| Review turnaround | Varies | 100% review coverage | 6m 53s median |
