# FrontierQA JS

TypeScript reporters for **Playwright** and **Jest**, plus the FrontierQA CLI wrapper — built for
[FrontierQA](https://frontierqa.dev), AI-native test reporting and failure triage.

**Status:** repository bootstrap. The first working release (`v0.1.0`) will print a terminal
summary and write a standardized `frontierqa-report.json` from real test runs.

## Packages

| Package | Registry | Purpose |
| --- | --- | --- |
| `@frontierqa/playwright` | npm | Playwright `Reporter` implementation |
| `@frontierqa/jest` | npm | Jest custom reporter |
| `@frontierqa/cli` | npm | `npx` entry point for local reports |

## Planned usage

```ts
// playwright.config.ts
export default defineConfig({
  reporter: [
    ['list'],
    ['@frontierqa/playwright', { output: 'frontierqa-report.json' }],
  ],
});
```

```js
// jest.config.js
module.exports = {
  reporters: ['default', ['@frontierqa/jest', { output: 'frontierqa-report.json' }]],
};
```

```bash
npx @frontierqa/cli report ./junit.xml --out frontierqa-report.json
```

Reports follow the workspace v1 contract (see `REASONIX.md`); secrets are redacted by default.

## Toolchain

- Node.js 24 LTS (`engines.node >= 22.0.0`; local dev on Node 25)
- pnpm workspace (`packages/*`)
- **tsdown** — dual ESM + CJS + `.d.ts`
- **Oxlint + Oxfmt**
- **Vitest**
- **@changesets/cli** for versioning and publishing

## Repository layout

```text
js/
├── packages/
│   ├── playwright/
│   ├── jest/
│   └── cli/
├── pnpm-workspace.yaml
└── .changeset/
```

## Development

```bash
pnpm install
pnpm -r build
pnpm -r test
pnpm -r lint
pnpm changeset          # record a version bump
pnpm changeset publish  # publish after CI is green
```

## License

MIT — see [LICENSE](LICENSE).

Copyright (c) 2026 FrontierQA.
