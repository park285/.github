<!--
GitHub Release 본문 템플릿입니다. 제목은 태그와 같은 `vX.Y.Z`로 씁니다.
저장소 규칙이 본문 형식을 따로 정하면 그 규칙이 우선합니다.
- shared-go·iris-client-go: tag workflow가 Release와 asset을 만듭니다. 손으로 만들거나 고치지 않습니다.
- hololive-bot: `scripts/publish-release.sh`가 만든 GitHub 생성 노트만 씁니다.
해당 없는 섹션은 지웁니다. 안내 주석은 게시된 본문에 표시되지 않습니다.
-->

## 변경 사항

<!-- CHANGELOG `## vX.Y.Z - YYYY-MM-DD` 절의 요약입니다. 파괴적 변경은 "(파괴적)"으로 표시하고 맨 위에 둡니다. 전체 목록은 태그 기준 CHANGELOG 링크로 둡니다.
예: 전체 목록은 [CHANGELOG vX.Y.Z](https://github.com/park285/<repo>/blob/vX.Y.Z/CHANGELOG.md)에 있습니다. -->

## 호환성과 배포 순서

<!-- 다른 저장소나 운영 상태와 맞춰야 하는 것만 적습니다.
- 짝 릴리스: 함께 배포해야 하는 저장소와 버전(예: Iris vX ↔ IrisBridge vY, ABI 43)
- 선행 조건: inbox 배수, ingress quiesce, migration 순서, env 추가·퇴역
- 구버전 비호환: 이 릴리스와 섞이면 동작하지 않는 이전 버전 -->

## 산출물

<!-- 첨부 파일이 있을 때만 씁니다(APK 등).
- 설치·사용할 파일 이름과 용도, 설치 파일이 아닌 첨부(mapping 등)
- 식별 정보: package·versionName·versionCode 등
- 서명자 유지 여부와 업데이트 설치 가능 여부 -->

## 출처와 무결성

<!-- 산출물이 있는 Release에 씁니다.
- Source revision: `<40자 SHA>`
- Release signer SHA-256: `<digest>` — 검증 PASS
- <파일> SHA-256: `<digest>`
- 첨부한 `SHA256SUMS`로 대조하는 방법, 비밀·세션 원문이 들어 있지 않다는 확인 -->

**Full Changelog**: https://github.com/park285/<repo>/compare/<직전 게시 Release 태그>...vX.Y.Z
