<div align="center">

# Open Feach Robotics 기여 가이드

**누구에게나 닿는 로보틱스 — 함께 만듭니다.**

[English](CONTRIBUTING.md) · 📖 **한국어**

</div>

---

열린 로보틱스를 함께 만들어 주셔서 감사합니다. 이 문서는
[`open-feach`](https://github.com/open-feach)의 **모든 저장소**에 공통으로 적용됩니다.
저장소마다 세부 안내를 덧붙일 수는 있지만, 아래에 정리한 브랜치 전략·커밋 규칙·리뷰
절차는 조직 전체가 함께 따르는 기본 원칙입니다.

## 지원하는 ROS 2 배포판

아래 세 배포판을 지원하며, 각 배포판은 패키지 저장소마다 전용 브랜치로 오래 유지됩니다.

| 배포판 | 종류 | 브랜치 | 설명 |
|--------|------|--------|------|
| **Rolling** Ridley | rolling | `rolling` | 개발 브랜치. 새 작업은 모두 여기로 먼저 들어옵니다 |
| **Jazzy** Jalisco | LTS | `jazzy` | 백포트 대상 |
| **Lyrical** Luth | LTS | `lyrical` | 백포트 대상 |

> 지금 이 `open-feach/.github` 저장소는 ROS 패키지가 아니라 조직 공통 설정을 담는
> 저장소라서 기본 브랜치를 `main`으로 둡니다. 아래 브랜치 전략은 **패키지 저장소**를
> 기준으로 합니다.

## 브랜치 전략

ROS 2 코어, Nav2와 같은 방식을 씁니다.

```
              ┌────────────────────────────────────┐
  PR 머지 →   │  rolling  (기본 / 개발 브랜치)       │  → ROS 2 Rolling 대상
              └───────────────────┬────────────────┘
                                  │  cherry-pick / 백포트 (아래 방향으로만)
                      ┌───────────┴───────────┐
                      ▼                       ▼
                   jazzy                   lyrical
```

- **개발은 오직 `rolling`에서만 합니다.** 새 기능이든 수정이든 PR을 거쳐 이 브랜치에
  먼저 반영됩니다.
- **`jazzy`, `lyrical` 같은 distro 브랜치에는 백포트만 들어갑니다.** `rolling`에서
  cherry-pick으로 내려보내며, distro 브랜치에서 직접 개발하지 않습니다.
- **위로 거슬러 올리는 머지는 하지 않습니다.** 변경은 항상 `rolling`에서 distro
  방향으로만 흐릅니다.
- **distro 브랜치는 API/ABI 호환을 지킵니다.** 호환을 깨는 변경은 `rolling`에만
  넣을 수 있고, 이미 릴리즈된 distro로는 백포트하지 않습니다.

### 백포트 여부는 이렇게 판단합니다

- ✅ 버그 수정, 안전 관련 수정, 문서, 호환을 깨지 않는 개선 → 지원 distro로 백포트합니다.
- ❌ 공개 API를 바꾸는 새 기능이나 ABI를 깨는 변경 → `rolling`에만 넣습니다.
- 🤔 애매하면 일단 `rolling`에 PR을 열고 설명에 적어 주세요. 메인테이너가 라벨로
  정리해 드립니다.

## 기여 절차

1. 간단하지 않은 작업이라면 **먼저 이슈를 열어** 방향을 맞춰 주세요.
2. **`rolling`에서 브랜치를 따세요.** 이름은 내용이 드러나게 짓습니다: `feature/…`,
   `fix/…`, `docs/…`.
3. **`rolling`을 대상으로 PR을 올리세요.** PR 템플릿을 채우고, 한 PR에는 한 가지
   주제만 담아 주세요.
4. distro까지 반영해야 하는 수정이라면 PR에 **백포트 라벨**을 붙이세요.
   - `backport-jazzy`
   - `backport-lyrical`

   PR이 머지되면 해당 distro 브랜치로 백포트 PR이 자동으로(또는 메인테이너가)
   생성됩니다. cherry-pick 도중 충돌이 나면 직접 해결을 부탁드릴 수 있습니다.
5. **모든 커밋에 서명(sign-off)하고**([커밋에 서명하기](#커밋에-서명하기--dco) 참고)
   **CI를 통과시켜 주세요.** 필수 검사가 통과하고, 작성자가 아닌 메인테이너가 **1명
   이상 승인**해야 머지됩니다.

## 커밋에 서명하기 — DCO

ROS 2, Nav2와 마찬가지로 CLA 대신 [DCO(Developer Certificate of
Origin)](https://developercertificate.org/)를 사용합니다. 서명은 그 변경을 본인이
작성했거나 프로젝트 라이선스로 제출할 권한이 있음을 증명하는 것입니다.

**모든 커밋에는 커밋 작성자의 이름·이메일과 일치하는 `Signed-off-by` 줄이 있어야
합니다.** `-s` 옵션을 주면 git이 자동으로 붙여 줍니다.

```bash
git commit -s -m "fix(costmap): clamp inflation radius to map resolution"
```

그러면 아래와 같은 줄이 커밋에 추가됩니다.

```
Signed-off-by: Jane Doe <jane@example.com>
```

서명을 깜빡했다면 `git commit --amend -s`로 마지막 커밋을 고치거나,
`git rebase --signoff <기준-커밋>`으로 여러 커밋에 한 번에 서명할 수 있습니다. 공백
정리나 오타 수정 같은 사소한 변경에는 DCO 검사가 적용되지 않습니다.

## 라이선스

Open Feach의 프로젝트는 기본적으로 **Apache License 2.0**으로 배포되며, 기여하면 위
DCO에 따라 본인의 기여물이 Apache 2.0으로 라이선스되는 데 동의하는 것입니다.

**예외:** 프로젝트가 **Apache 2.0과 호환되지 않는** 외부 오픈소스를 활용하는 경우, 그
코드와 그것에 의존하는 구성 요소는 해당 외부 오픈소스의 라이선스를 따릅니다. 이런
경우에는 라이선스가 모호해지지 않도록 파일 헤더와 패키지 라이선스 메타데이터에 명확히
표기해 주세요.

## 커밋 메시지 — Conventional Commits

[Conventional Commits](https://www.conventionalcommits.org/) 규칙을 씁니다. 히스토리를
읽기 쉽게 만들고 변경 이력(changelog) 자동화에도 도움이 됩니다.

```
<type>(<scope, 선택>): <한 줄 요약>

<본문(선택) — 무엇을, 왜 바꿨는지. 어떻게는 코드가 말해 줍니다>

<푸터(선택) — 예: "Closes #123", "BREAKING CHANGE: …">
```

자주 쓰는 type: `feat`, `fix`, `docs`, `refactor`, `test`, `build`, `ci`, `chore`.

예시:

```
fix(costmap): clamp inflation radius to map resolution
feat(controller): add configurable goal tolerance
docs: explain rolling→distro backport flow
```

커밋 템플릿을 제공하니, 저장소를 클론한 뒤 한 번만 설정해 두세요.

```bash
git config commit.template .gitmessage
```

## 코드 스타일과 린터

ROS 2 스타일 가이드를 따르고 표준 도구로 이를 검사합니다. PR을 열기 전에 린터를 한 번
돌려 주세요.

- **C++ / Python 스타일**은 `ament_lint_common`이 검사합니다 (`ament_uncrustify`,
  `ament_cpplint`, `ament_flake8`, `ament_copyright` 등을 실행).
- `colcon test`로 테스트와 린트를 함께 돌리거나, 개별 패키지는 `ament_lint` 도구로
  따로 검사할 수 있습니다.
- 저장소에 `pre-commit` 설정이 있으면 `pre-commit install`로 설치해서 커밋마다 스타일이
  자동으로 검사되게 하세요.

CI가 이 린터들을 돌리므로, 통과하지 못한 PR은 머지되지 않습니다.

## 테스트

새 코드에는 테스트를 함께 넣고, 버그 수정에는 가능하면 회귀 테스트를 추가해 주세요.
`colcon test`로 전체 테스트를 돌려 통과를 확인한 뒤 리뷰를 요청하세요. 각 패키지는
[REP-2004(패키지 품질 등급)](https://www.ros.org/reps/rep-2004.html)에서 설명하는 품질
관행을 지향합니다.

## 패키지 버전 관리 (패키지 저장소)

릴리즈된 패키지에 영향을 주는 변경이라면 다음을 함께 갱신해 주세요.

1. **`package.xml`** — [semver](https://semver.org/)에 맞춰 `<version>`을 올립니다.
2. **`CHANGELOG.rst`** — 변경 항목을 추가합니다 (`catkin_prepare_release`로 자동화할
   수 있습니다).

## 행동 강령

기여에 참여하면 [행동 강령](CODE_OF_CONDUCT.md)을 지키는 데 동의하는 것으로 봅니다.
서로 존중하며 즐겁게 만들어 갑시다.

## 문의

- 💬 질문이나 아이디어는 저장소의 **Discussions**에 남겨 주세요.
- 🐛 버그와 구체적인 기능 제안은 **Issues**로 올려 주세요.
- 📬 팀에 직접 연락: **[openfeach@googlegroups.com](mailto:openfeach@googlegroups.com)**
