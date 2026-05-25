# @significa/tsconfig

Significa's shared TypeScript configurations. Four variants, all strict, all `noEmit` (Biome handles syntax; tsc handles type-checking only).

## Install

```sh
pnpm add -D -E @significa/tsconfig typescript
```

## Variants

### `base` — neutral foundation

Strict mode, `target: ES2023`, `module: preserve`, `noEmit`, `verbatimModuleSyntax`, `erasableSyntaxOnly`. **No DOM lib, no JSX, no `allowImportingTsExtensions`.** Pick this only if your code is truly runtime-agnostic (rare). Most projects extend `react`, `astro`, or `node` directly.

```json
{
  "extends": "@significa/tsconfig/base",
  "include": ["src"]
}
```

### `react` — TanStack Start, Vite React

Extends `base`. Adds DOM lib, `jsx: react-jsx`, `allowImportingTsExtensions`.

```json
{
  "extends": "@significa/tsconfig/react",
  "include": ["src", "vite.config.ts"]
}
```

### `astro` — Astro projects

Extends `base`. Adds DOM lib, `jsx: preserve`, `allowImportingTsExtensions`. Pre-includes `${configDir}/.astro/types.d.ts` and `${configDir}/**/*`, excludes `dist`.

```json
{
  "extends": "@significa/tsconfig/astro",
  "compilerOptions": {
    "paths": { "@/*": ["./src/*"] }
  }
}
```

### `node` — Drizzle scripts, CLIs, tsx-run code, API-only services

Extends `base`. Swaps to `module: NodeNext` + `moduleResolution: NodeNext`, adds `types: ["node"]`. No DOM lib (the `base` default is fine for Node).

```json
{
  "extends": "@significa/tsconfig/node",
  "include": ["src", "scripts"]
}
```
