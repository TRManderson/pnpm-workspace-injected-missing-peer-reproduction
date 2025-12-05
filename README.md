# pnpm-workspace-injected-missing-peer-reproduction

This repo serves a a minimum reproduction of a pnpm issue around resolving peer dependencies when
using injected workspace packages


When an injected package from the workspace uses a `catalog:` constraint in its `peerDependencies`,
the `catalog:` contstraint is not then re-processed in the dependent package and is then listed as
an unmet peer when resolving peer dependencies as the literal version `catalog:` conflicts with the
resolved catalog version the package then pulls in as a direct dependency.