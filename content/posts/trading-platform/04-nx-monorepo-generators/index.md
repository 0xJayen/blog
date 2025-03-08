---
title: 04. NX Monorepo Generators
description: Using NX Generators to scaffold monorepo projects.
date: "2025-03-08T13:41:20+06:00"
tags: ["devlog"]
categories: ["trading-platform"]
author: "Jayen"
---

NX comes with a bunch of [plugins](https://nx.dev/plugin-registry) and within them abilities to
generate project boilerplate code. I wanted to use [NestJS](https://nestjs.com/) and
[Next.js](https://nextjs.org/) as my main frameworks for this project, I installed the following NX
plugins and used their generators to generate the following applications and libraries.

-   [@nx/nest](https://nx.dev/nx-api/nest)
-   [@nx/next](https://nx.dev/nx-api/next)
-   [@nx/js](https://nx.dev/nx-api/js)

I then ran the following commands to generate 6 separate applications and 2 libraries to start
things off.

```bash
npx nx g @nx/nest:app apps/gateway --strict
npx nx g @nx/nest:app apps/users-service --strict
npx nx g @nx/nest:app apps/coins-service --strict
npx nx g @nx/nest:app apps/trades-service --strict
```

```bash
npx nx g @nx/next:app apps/site
npx nx g @nx/next:app apps/admin
```

```bash
npx nx g @nx/js:lib packages/sdk
npx nx g @nx/js:lib packages/service-contracts
```

NX's generators for NestJS and Next.js lets you choose between using a test-runner for each project
and I opted to go with [Jest](https://jestjs.io/) for the NestJS projects and
[Playwright](https://playwright.dev/) for the Next.js ones.

With the following commands, I was able to generate the following files:

```
trading-platform/
├── apps/
│   ├── gateway/
│   ├── gateway-e2e/
│   ├── users-service/
│   ├── users-service-e2e/
│   ├── coins-service/
│   ├── coins-service-e2e/
│   ├── trades-service/
│   ├── trades-service-e2e/
│   ├── site/
│   ├── site-e2e/
│   ├── admin/
│   └── admin-e2e/
└── packages/
    ├── sdk/
    └── service-contracts/
```

That's a lot of boilerplate code that I just generated and to be honest, it's kind of overwhelming.
When you just use the generator commands the original framework authors provide, you get a much more
minimal boilerplate code which is way easier to reason about as it doesn't have all this complex
configuration and setup steps.

I've been using [Turborepo](https://turbo.build/repo/docs) for managing my monorepos for a while
but, this time I wanted to give NX a shot. I must say, NX's concept of using these generators and
out-of-the-box boilerplate code might be overwhelming at first, but it takes a huge load off my
shoulders of having to configure everything manually all by myself.

Anyways, there was one more thing I still had to do, which was upgrading all the packages to their
latest version from the `package.json` file. There's a nice little CLI that lets you do this in a
single command.

```bash
npx npm-check-updates --upgrade --removeRange
```

**CAUTION**: This will upgrade every package to their latest available version without checking for
compatibility. Use this carefully and test that the upgrade doesn't break your existing
applications.
