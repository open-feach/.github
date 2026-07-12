<div align="center">

# Contributing to Open Feach Robotics

**Robotics within reach — built together.**

📖 **English** · [한국어](CONTRIBUTING.ko.md)

</div>

---

Thanks for helping build open robotics! This guide applies to **every repository** in the
[`open-feach`](https://github.com/open-feach) organization. Individual repositories may add
their own notes, but the branch model, commit style, and review flow below are the shared
default across the org.

## Supported ROS 2 distributions

We target these distributions. Each has its own long-lived branch in every package repo:

| Distro | Type | Branch | Notes |
|--------|------|--------|-------|
| **Rolling** Ridley | rolling | `rolling` | Development branch — all new work lands here first |
| **Jazzy** Jalisco | LTS | `jazzy` | Backport target |
| **Lyrical** Luth | LTS | `lyrical` | Backport target |

> The `open-feach/.github` repository (this one) is org infrastructure, not a ROS package,
> so it keeps `main` as its default branch. The model below applies to **package repositories**.

## Branch model

We follow the same model as ROS 2 core and Nav2.

```
             ┌────────────────────────────────────┐
  PRs land → │  rolling  (default / development)   │  → targets ROS 2 Rolling
             └───────────────────┬────────────────┘
                                 │  cherry-pick / backport (downward only)
                     ┌───────────┴───────────┐
                     ▼                       ▼
                  jazzy                   lyrical
```

- **`rolling` is the one and only development branch.** All new features and fixes are
  merged here first via pull request.
- **Distro branches (`jazzy`, `lyrical`) receive backports** of applicable fixes, cherry-picked
  down from `rolling`. Never develop directly on a distro branch.
- **No upward merges.** Changes flow `rolling` → distro, never the reverse.
- **Distro branches stay API/ABI stable.** Breaking changes are allowed on `rolling` only.
  We do **not** backport changes that break API/ABI on a released distro.

### How to decide what to backport

- ✅ Bug fixes, safety fixes, docs, and non-breaking improvements → backport to supported distros.
- ❌ New features that change public API, or anything breaking ABI → `rolling` only.
- 🤔 Unsure? Open the PR against `rolling` and ask in the description; a maintainer will label it.

## Contribution flow

1. **Open an issue first** for anything non-trivial, so we can agree on the approach.
2. **Branch from `rolling`.** Use a descriptive name: `feature/…`, `fix/…`, `docs/…`.
3. **Open a pull request against `rolling`.** Fill in the PR template and keep the PR focused.
4. **Request a backport** by adding a label to the PR when the fix should reach a distro:
   - `backport-jazzy`
   - `backport-lyrical`

   After the PR merges, a backport PR is opened automatically (or by a maintainer) against
   that distro branch. If the cherry-pick conflicts, you may be asked to resolve it.
5. **Sign off every commit** (see [Sign your work](#sign-your-work--the-dco)), and **keep CI
   green.** A PR merges only after required checks pass and at least one maintainer who did
   **not** author it approves.

## Sign your work — the DCO

Like ROS 2 and Nav2, we use the [Developer Certificate of Origin](https://developercertificate.org/)
(DCO) instead of a CLA. Signing off certifies that you wrote the change, or otherwise have
the right to submit it under the project license.

**Every commit must carry a `Signed-off-by` line** whose name and email match the commit
author. Git adds it for you with `-s`:

```bash
git commit -s -m "fix(costmap): clamp inflation radius to map resolution"
```

This appends, for example:

```
Signed-off-by: Jane Doe <jane@example.com>
```

Forgot to sign off? Amend the last commit with `git commit --amend -s`, or re-sign a range
with `git rebase --signoff <base>`. The DCO check is not enforced on trivial changes
(whitespace, typo fixes).

## Licensing

Open Feach projects are released under the **Apache License 2.0** by default, and by
contributing you agree that your contributions are licensed under Apache 2.0, per the terms
of the DCO above.

**Exception:** when a project incorporates third-party open-source code whose license is
**not compatible with Apache 2.0**, that code — and the component that depends on it —
follows the upstream license instead. Document any such case clearly (in the file header and
the package's license metadata) so the licensing stays unambiguous.

## Commit messages — Conventional Commits

We use [Conventional Commits](https://www.conventionalcommits.org/). This keeps history
readable and lets us automate changelogs.

```
<type>(<optional scope>): <short summary>

<optional body — what & why, not how>

<optional footer — e.g. "Closes #123", "BREAKING CHANGE: …">
```

Common types: `feat`, `fix`, `docs`, `refactor`, `test`, `build`, `ci`, `chore`.

Examples:

```
fix(costmap): clamp inflation radius to map resolution
feat(controller): add configurable goal tolerance
docs: explain rolling→distro backport flow
```

A commit template is provided — enable it once per clone:

```bash
git config commit.template .gitmessage
```

## Code style and linters

We follow the ROS 2 style guides and enforce them with the standard tooling, so please run
the linters before opening a PR:

- **C++ / Python style** is enforced by `ament_lint_common` (which runs `ament_uncrustify`,
  `ament_cpplint`, `ament_flake8`, `ament_copyright`, and friends).
- Run everything the tests run with `colcon test`, or lint a single package with
  `ament_lint` tools directly.
- Where a repo provides a `pre-commit` config, install it (`pre-commit install`) so style is
  checked on every commit.

CI runs these linters; a PR that fails them will not merge.

## Tests

New code should come with tests, and bug fixes should add a regression test where practical.
Run the suite with `colcon test` and make sure it passes before requesting review. Packages
aim for the quality practices described in
[REP-2004 (Package Quality Categories)](https://www.ros.org/reps/rep-2004.html).

## Package versioning (package repos)

When a change affects a released package, update:

1. **`package.xml`** — bump `<version>` following [semver](https://semver.org/).
2. **`CHANGELOG.rst`** — add an entry (`catkin_prepare_release` automates this).

## Code of conduct

By participating you agree to uphold our [Code of Conduct](CODE_OF_CONDUCT.md). Be kind;
robotics is hard enough without hostility.

## Questions

- 💬 Use the repository's **Discussions** for questions and ideas.
- 🐛 Use **Issues** for bugs and concrete feature requests.
- 📬 Reach the team at **[openfeach@googlegroups.com](mailto:openfeach@googlegroups.com)**.
