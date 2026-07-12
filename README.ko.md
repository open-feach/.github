<div align="center">

# Open Feach Robotics

**조직 전체 기본값과 커뮤니티 상태 파일.**

[![Contributing](https://img.shields.io/badge/contributing-guide-6f42c1?style=flat-square)](CONTRIBUTING.ko.md)
[![Conventional Commits](https://img.shields.io/badge/commits-conventional-fe5196?style=flat-square)](https://www.conventionalcommits.org)
[![DCO](https://img.shields.io/badge/sign--off-DCO-1a73e8?style=flat-square)](CONTRIBUTING.ko.md)

[English](README.md) · **한국어**

</div>

---

**`.github`** 저장소는 [Open Feach Robotics](https://github.com/open-feach)의 모든 프로젝트를
관통하는 공통 규약을 담습니다 — 공개 프로필, 기여 규칙, 이슈·PR 템플릿, 그리고 공유 CI까지.
각 저장소가 스스로 정의하지 않은 것은 모두 이곳에서 상속되므로, 이 기본값들은 오직 한 곳에만
존재합니다.

> [!NOTE]
> 이 저장소는 ROS 패키지가 아니라 조직 인프라이므로 기본 브랜치를 **`main`**으로 둡니다.
> 기여 가이드에 설명된 `rolling` + distro 브랜치 모델은 **패키지 저장소**에 적용됩니다.

## 구성

| 경로 | 용도 |
|------|------|
| [`profile/`](profile/README.md) | [github.com/open-feach](https://github.com/open-feach)에 노출되는 공개 조직 프로필 |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | 브랜치 모델, DCO 서명, 라이선스, 커밋·리뷰 규약 |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Contributor Covenant v2.1 |
| [`.github/workflows/ros-ci.yml`](.github/workflows/ros-ci.yml) | 모든 패키지 저장소가 호출하는 재사용 ROS 2 CI |
| [`templates/`](templates/README.md) | 패키지 저장소를 공유 CI에 연결하는 복사용 스타터 워크플로 |
| [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | 기본 PR 템플릿 |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | 버그 신고·기능 제안 폼 |
| [`.gitmessage`](.gitmessage) | 커밋 메시지 템플릿 (Conventional Commits + 서명) |

한국어판은 각 영어 파일 옆에 `*.ko.md`로 함께 있습니다.

---

<div align="center">
<sub><b>Open Feach Robotics</b> · 모두를 위한 로봇</sub>
</div>
