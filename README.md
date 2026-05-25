# code-quality

Significa's shared static-analysis configs.

## Packages

| Package | Description |
|---|---|
| [`@significa/biome-config`](./packages/biome-config) | Shared [Biome](https://biomejs.dev) v2 config. `pnpm add -D -E @significa/biome-config @biomejs/biome` |
| [`@significa/tsconfig`](./packages/tsconfig) | Shared TypeScript configs — `base`, `react`, `astro`, `node` variants. `pnpm add -D -E @significa/tsconfig typescript` |

The CI side (running Biome + tsc + Knip in GitHub Actions) is shipped by [`significa/actions`](https://github.com/significa/actions) — see its [`typescript-quality.yaml`](https://github.com/significa/actions/blob/main/.github/workflows/typescript-quality.yaml) reusable workflow. Knip configuration is per-project; see Knip's docs.

## Versioning

These packages stay in `0.x` indefinitely. **No semver guarantees** — minor bumps may change lint behavior or flip compiler options. Pin exactly (`pnpm add -E`) if you want reproducibility.

This matches the `@tsconfig/*` family pattern. We bump when Biome or TypeScript releases new versions or when we want a config change to roll out to all consumers.

## Releasing

Two packages, independent versioning. Tag scheme: `biome-config-v0.1.0` and `tsconfig-v0.1.0`.

```sh
# Bump biome-config (patch/minor/major)
pnpm release:biome-config patch
git push --follow-tags
# The publish workflow fires on the tag and publishes to npm with provenance.
```

Same flow for `tsconfig` via `pnpm release:tsconfig`. The tag prefix is baked into the script — `pnpm version` won't create plain `v0.1.0` tags.

Don't forget to update the package's `CHANGELOG.md` before bumping.

## License

MIT. See [LICENSE](./LICENSE).
