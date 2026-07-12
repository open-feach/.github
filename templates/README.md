# CI templates

Starter workflows for Open Feach **ROS 2 package repositories**. They call the
organization's reusable workflow, [`.github/workflows/ros-ci.yml`](../.github/workflows/ros-ci.yml),
so the actual CI logic lives in one place for the whole org.

## Install into a package repo

Copy both files into the package repo's `.github/workflows/` directory:

| Template | Copy to | Trigger |
|----------|---------|---------|
| [`ci.yml`](ci.yml) | `.github/workflows/ci.yml` | push & pull_request on `rolling` / `jazzy` / `lyrical` |
| [`ci-nightly.yml`](ci-nightly.yml) | `.github/workflows/ci-nightly.yml` | weekly cron + manual dispatch |

Commit them on **every distro branch** (`rolling`, `jazzy`, `lyrical`) so push/PR
CI exists on each. `ci-nightly.yml` only needs to run from the default branch
(`rolling`) — see the note below.

## How it works

- **Per-branch (`ci.yml`)** — each distro branch is tested against **its own**
  distro. The distro is inferred from the branch name, so there is nothing to
  configure per repo. Override with `distros: '["rolling","jazzy"]'` only if a
  repo wants extra combinations.
- **Nightly (`ci-nightly.yml`)** — GitHub runs `schedule:` triggers **only on the
  default branch**, so a per-branch `on: schedule` would fire on `rolling` alone.
  Instead, one scheduled workflow sweeps every distro branch via a matrix and
  tests each against its matching distro.

## Maintaining CI centrally

Distro bumps, tool swaps, and engine changes happen once in
[`ros-ci.yml`](../.github/workflows/ros-ci.yml); package repos pick them up with
no change. The engine is [`industrial_ci`](https://github.com/ros-industrial/industrial_ci),
pinned to a commit SHA (bump it deliberately, never float on `@master`).
