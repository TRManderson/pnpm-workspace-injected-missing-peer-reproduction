# pnpm-workspace-injected-missing-peer-reproduction

This repo serves a a minimum reproduction of a pnpm issue around resolving peer dependencies when
using injected workspace packages


When an injected package from the workspace uses a `catalog:` constraint in its `peerDependencies`,
the `catalog:` contstraint is not then re-processed in the dependent package and is then listed as
an unmet peer when resolving peer dependencies as the literal version `catalog:` conflicts with the
resolved catalog version the package then pulls in as a direct dependency.

To reproduce, run `pnpm i --resolution-only`

```
$ pnpm i --resolution-only
Scope: all 3 workspace projects
Progress: resolved 3, reused 0, downloaded 0, added 0, done
 WARN  Issues with peer dependencies found
dependent-pkg
└─┬ pkg-with-catalog-peer 1.0.0
  └── ✕ unmet peer @types/node@catalog:: found 22.19.1
Done in 137ms using pnpm v10.22.0`
```