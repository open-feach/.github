<div align="center">

# Open Feach Robotics

**Organization-wide defaults & community health files.**

[![Contributing](https://img.shields.io/badge/contributing-guide-6f42c1?style=flat-square)](CONTRIBUTING.md)
[![Conventional Commits](https://img.shields.io/badge/commits-conventional-fe5196?style=flat-square)](https://www.conventionalcommits.org)
[![DCO](https://img.shields.io/badge/sign--off-DCO-1a73e8?style=flat-square)](CONTRIBUTING.md#sign-your-work--the-dco)

**English** · [한국어](README.ko.md)

</div>

---

The **`.github`** repository holds the conventions that shape every project across
[Open Feach Robotics](https://github.com/open-feach) — our public profile, contribution
rules, issue and pull-request templates, and shared CI. Whatever a repository doesn't
define for itself is inherited from here, so these defaults live in exactly one place.

> [!NOTE]
> This repository is organization infrastructure, not a ROS package, so its default branch
> is **`main`**. The `rolling` + distro-branch model described in the contribution guide
> applies to **package repositories**.

## What lives here

| Path | Purpose |
|------|---------|
| [`profile/`](profile/README.md) | The public organization profile shown at [github.com/open-feach](https://github.com/open-feach) |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Branch model, DCO sign-off, licensing, and commit & review conventions |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Contributor Covenant v2.1 |
| [`.github/workflows/ros-ci.yml`](.github/workflows/ros-ci.yml) | Reusable ROS 2 CI, called by every package repository |
| [`templates/`](templates/README.md) | Copy-in starter workflows that wire a package repo to the shared CI |
| [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | Default pull-request template |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | Bug-report and feature-request forms |
| [`.gitmessage`](.gitmessage) | Commit-message template (Conventional Commits + sign-off) |

Korean translations live beside each English file as `*.ko.md`.

---

<div align="center">
<sub><b>Open Feach Robotics</b> · robots for everyone</sub>
</div>
