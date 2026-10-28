# 기여 안내

park285 소유 저장소 전체에 적용되는 PR 절차입니다. 저장소에 자체 `CONTRIBUTING.md`가 있으면 그 파일이 우선합니다. 빌드·테스트·게이트 같은 저장소별 요건은 각 저장소의 `README.md`와 `AGENTS.md`가 정본이며, 이 문서는 그것을 대신하지 않습니다.

## 언어

PR 제목, 본문, 커밋 메시지, 리뷰 코멘트는 한국어로 씁니다. 코드 식별자, 명령어, 경로, 오류 메시지 원문은 그대로 둡니다.

## 브랜치

- `main`에 직접 푸시하지 않습니다. 모든 변경은 브랜치와 PR을 거칩니다. 스택 저장소의 `main`은 ruleset이 PR·squash merge를 강제하고 삭제·non-fast-forward push를 막습니다. PR CI가 있는 저장소는 그 check(`fast-gate` 또는 `quality`)도 통과해야 합니다.
- 브랜치 이름은 `type/짧은-설명` 형식입니다. 예: `fix/pg-exporter-connlimit`, `chore/deps-bump-20261025`, `release/v12.0.1`.
- 게시된 커밋은 amend나 force-push 하지 않습니다. 리뷰 반영은 새 커밋으로 올립니다.

## 제목과 커밋 메시지

- 형식은 `type(scope): 무엇이 달라지는지 한 줄`입니다. `type`은 `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `ci`, `perf` 중 하나이고, `scope`는 바뀐 모듈이나 영역입니다.
- PR은 squash merge로 합치고 PR 제목이 머지 커밋 제목이 됩니다. PR 제목이 곧 `main` 이력이므로 제목만 읽고도 변경을 알 수 있게 씁니다.
- 하나의 PR은 하나의 목적만 다룹니다. 포맷팅, 이름 바꾸기, 무관한 정리는 섞지 않습니다.

## 본문

본문은 계정 공통 [PR 템플릿](pull_request_template.md)의 섹션(배경, 변경 내용, 리뷰 포인트, 검증, 영향과 롤백, 연관 작업)을 그 순서대로 따릅니다. 해당 없는 섹션은 지웁니다.

- 웹에서 PR을 열면 템플릿이 자동으로 채워집니다. 템플릿의 안내 주석은 게시된 본문에 표시되지 않으므로 지우지 않아도 됩니다.
- `gh pr create --body`나 `--body-file`은 템플릿을 채우지 않습니다. 섹션을 직접 쓰거나 원문을 가져와 시작합니다.

  ```sh
  gh api repos/park285/.github/contents/pull_request_template.md -H 'Accept: application/vnd.github.raw'
  ```

- 검증 섹션에는 실행한 명령과 결과를 적고, 실행하지 못한 검사는 이유와 함께 적습니다. 통과하지 않은 검사를 통과한 것처럼 쓰지 않습니다.
- 서브모듈 포인터를 바꿨다면 연관 작업 섹션에 저장소별 이전 SHA → 이후 SHA와 원격 게시 여부를 적습니다.

## 게시 전 확인

- 저장소가 정한 로컬 게이트(예: `pre-push-gate.sh`, `local-ci.sh`)를 통과한 뒤 푸시합니다. 어떤 게이트가 있는지는 각 저장소의 `README.md`와 `AGENTS.md`를 따릅니다.
- 시크릿, 토큰, 캡처 증거, 개인정보는 커밋하지 않습니다. 존재 여부와 위치만 적습니다.
- 다른 저장소와 짝을 이루는 PR이 있으면 양쪽 본문의 연관 작업 섹션에 서로를 적고 병합 순서를 밝힙니다.

## 머지

- squash merge로 합칩니다. 머지한 브랜치는 삭제합니다(코드 저장소는 자동 삭제가 켜져 있습니다).
- PR의 CI가 통과하고 리뷰 포인트에 적은 질문이 정리된 뒤 머지합니다.
- 머지 뒤 배포나 운영 반영이 필요하면 PR 본문의 영향과 롤백 섹션이 그 순서를 담고 있어야 합니다.

## 릴리스

버전 기준·검사 스크립트·배포 절차는 각 저장소의 `RELEASE_VERSIONING.md`(또는 release runbook)가 정본입니다. 이 절은 저장소가 따로 정하지 않은 공통 형식만 정합니다.

### 버전

- 루트 `VERSION`에 `v` 접두사 없는 `MAJOR.MINOR.PATCH`를 둡니다. 태그에는 `v`를 붙입니다.
- 지난 태그 이후 `type(scope)!:` 커밋이나 CHANGELOG의 breaking change 항목(기존 "파괴적 변경" 표기 포함)이 하나라도 있으면 MAJOR를 올립니다. 기능만 늘었으면 MINOR, 수정·보안·운영 안정화만 있으면 PATCH입니다.
- Go 모듈은 MAJOR를 올릴 때 module path의 `/vN`도 함께 바꿉니다.

### CHANGELOG와 릴리스 커밋

- 태그 전 변경은 `## 미출시` 아래에 적습니다.
- 릴리스 때는 `## 미출시` 제목을 남기고, 그 바로 아래에 `## vX.Y.Z - YYYY-MM-DD`를 넣어 기존 항목을 그 절로 옮깁니다.
- "발행 전", "태그 뒤 교체" 같은 준비 단계의 서술은 릴리스 절로 옮길 때 실제 결과로 고쳐 씁니다.
- 버전과 CHANGELOG를 바꾸는 커밋 제목은 `chore(release): vX.Y.Z 버전 올림과 CHANGELOG 구간 정리`로 씁니다. 저장소의 `check-release-version` 검사를 통과해야 합니다.
- 릴리스 커밋도 다른 변경과 같이 브랜치와 PR로 `main`에 반영합니다. 같은 PR에 담아도 됩니다.

### 태그

- 태그는 `main`에 반영된 커밋에 annotated tag로 만듭니다. squash merge 뒤에는 머지 커밋에 태그를 답니다.
  - 메시지 형식은 `vX.Y.Z: 이 릴리스를 한 줄로` 입니다.
  - 기존 태그는 옮기거나 다시 만들지 않습니다.
- 태그 push 때는 저장소 hook이 전체 gate를 실행합니다. 태그 대상 커밋을 checkout한 상태에서 `ALLOW_TAG_PUSH=1 git push origin vX.Y.Z`로 push합니다.

### 여러 저장소를 함께 내는 순서

공개 API를 바꾸는 라이브러리 릴리스는 소비자보다 먼저 냅니다.

1. shared-go → iris-client-go: 태그를 push하면 release workflow가 Release를 만듭니다. `docs/release-provenance.md`의 검증(checksum, provenance, SPDX, `gh release verify`)을 모두 통과해야 다음 단계로 갑니다.
2. 소비자: `GOWORK=off go mod tidy`로 go.sum을 갱신하고, 고정한 sibling SHA(예: `security.yml`)를 release SHA로 바꾼 뒤 gate를 다시 실행합니다.
3. Iris → iris-bridge → 봇·console → 메타 서브모듈 포인터. iris-bridge가 핀하는 Iris rev는 Iris PR이 squash 병합된 뒤의 `main` 커밋으로 올립니다. 브랜치 커밋은 `main`에 남지 않습니다.

### GitHub Release

- 제목은 태그와 같은 `vX.Y.Z`입니다.
- 본문은 계정 공통 [릴리스 템플릿](release_template.md)을 따릅니다. 아래 경우는 저장소 방식이 우선합니다.
  - shared-go·iris-client-go: workflow가 만듭니다.
  - hololive-bot: `scripts/publish-release.sh`가 만든 GitHub 생성 노트만 씁니다.
- Full Changelog와 생성 노트의 기준은 직전에 *게시된* Release입니다. 태그만 있고 Release가 없던 중간 버전의 변경도 빠지지 않게 하기 위해서입니다.
- APK 같은 산출물은 태그 커밋의 깨끗한 checkout에서 빌드합니다.
  - 서명자 검증 `PASS`와 checksum을 확인한 뒤 첨부합니다.
  - 같은 이름의 asset은 덮어쓰지 않습니다(`--clobber` 금지).
  - 첨부한 뒤 새 디렉터리에 다시 내려받아 checksum을 대조합니다.
- 서명 입력은 stack-secrets 파일을 그 자리에서 읽기만 하고, 값을 출력하거나 저장소·로그·asset에 복사하지 않습니다.
