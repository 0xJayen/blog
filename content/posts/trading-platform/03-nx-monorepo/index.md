---
title: 03. NX Monorepo
description: Setup NX for monorepo management along with PNPM workspaces.
date: "2025-03-08T01:41:45+06:00"
tags: ["devlog"]
categories: ["trading-platform"]
author: "Jayen"
---

To setup NX for monorepo management along with PNPM workspaces, the following files need to be
added:

```
trading-platform/
├── apps/
│   └── .gitkeep
├── nx.json
└── pnpm-workspace.yaml
```

`pnpm-workspace.yaml`

```yaml
packages:
    - apps/*
    - packages/*
onlyBuiltDependencies:
    - nx
```

`nx.json`

```json
{
    "$schema": "./node_modules/nx/schemas/nx-schema.json"
}
```

The only dependency needed so far is the `nx` package.

Instead of creating these files manually, the `nx init` command can be used to automate the creation
of the `nx.json` configuration file based on the PNPM Workspace configuration.

```bash
npx nx@latest init
```
