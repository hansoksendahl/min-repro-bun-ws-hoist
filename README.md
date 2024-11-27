# Minimal Reproduction Monorepo

This Bun based monorepository is a minimal reproduction repository of the
hoisting issues that currently exist in Bun.

The issue [documented here](https://github.com/oven-sh/bun/issues/533) is that
hoisting breaks module boundaries. This can lead to unexpected build errors when
bundling, running code in CI/CD, or deploying.

Furthermore, the issue of implicit dependencies is not limited to packages
defined in the monorepo, they apply to third party dependencies as well.

## Repository Structure

- packages/
  - a/
  - b/ - has a dependencies on workspace package `a` and third party package
    `isOdd`.
  - c/ - has a 👻-dependencies on workspace package `a` and third party package
    `isOdd`.

## Resolution

Explicit dependencies are best for monorepo development and avoid some of the
issues discussed. I propose that `bun` provide a mechanism to avoid hoisting
dependencies to the top level.