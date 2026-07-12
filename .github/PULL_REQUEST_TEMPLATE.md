<!--
Thanks for contributing to Open Feach! A few reminders:
- Open this PR against the `rolling` branch (development). Distro branches receive backports.
- Sign off every commit: `git commit -s`  (see CONTRIBUTING.md → Sign your work).
See the full guide: https://github.com/open-feach/.github/blob/main/CONTRIBUTING.md
-->

## Summary

<!-- What does this PR change, and why? Keep it focused on one topic. -->

## Related issue

<!-- e.g. "Closes #123". Non-trivial changes should reference an issue. -->

## Type of change

- [ ] 🐛 Bug fix (non-breaking)
- [ ] ✨ Feature (non-breaking)
- [ ] 💥 Breaking change (API/ABI) — **`rolling` only, not backported**
- [ ] 📝 Docs / chore / CI

## Backport

<!-- Bug/safety/doc fixes can be backported to supported distros. Breaking changes cannot. -->

- [ ] No backport needed
- [ ] Add label `backport-jazzy`
- [ ] Add label `backport-lyrical`

## Checklist

- [ ] Every commit is signed off (`Signed-off-by`, `git commit -s`)
- [ ] Follows [Conventional Commits](https://www.conventionalcommits.org/)
- [ ] Linters pass (`ament_lint_common` / `colcon test`)
- [ ] Tests added or updated, and passing
- [ ] Docs updated if behavior changed
- [ ] `package.xml` version and `CHANGELOG.rst` updated (if a released package changed)
