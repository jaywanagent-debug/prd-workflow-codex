# PRD Workflow for Codex

`PRD 만들자`라는 한 문장에서 시작해 빌드 위험, 문제와 가설, 인터뷰, 5개 PRD 문서, 비판 검수, 예외·완료 조건, 측정 설계, 승인 후 실행 계획까지 연결하는 Codex 플러그인 번들입니다.

워크플로 시작 시 `PRD_WORKFLOW_CHECKLIST.md`와 `PRD_DECISIONS.md`를 만들거나 이어서 사용합니다. 모든 전문 스킬이 같은 인터뷰 답변과 결정 기록을 재사용하므로 이미 답한 질문을 반복하지 않고, 단계별 완료·보류·승인 상태를 체크박스로 추적합니다.

## 포함된 스킬

- `prd-workflow-router` — 환경별 전용 규칙을 제거한 공개용 전체 PRD 라우터입니다.
- `foundation-build-risk-review` — 시작 전에 가장 큰 실패 가정과 빌드 여부를 검토합니다.
- `define-problem-statement` — 사용자 문제, 영향, 성공 기준과 제약을 정리합니다.
- `define-hypothesis` — 해결 가정을 반증 가능한 가설과 목표 수치로 만듭니다.
- `show-me-the-prd` — 부족한 정보만 인터뷰하고 5개 PRD 문서를 생성합니다.
- `utility-pm-critic` — PRD를 P0/P1/P2/P3로 비판 검수합니다.
- `deliver-edge-cases` — 오류·경계·동시성·복구 경로를 정리합니다.
- `deliver-acceptance-criteria` — 완료 조건을 Given/When/Then으로 만듭니다.
- `measure-instrumentation-spec` — 측정 이벤트, 속성, 개인정보와 QA 체크를 설계합니다.
- `goaljaby` — 승인된 PRD를 검증·복구·진척 문서와 Codex `/goal` 핸드오프로 변환합니다.

## 기본 동작

- `PRD 만들자` → 위험 검토 → 문제·가설 → 인터뷰형 5-file PRD → 비판 검수 → 예외·완료 조건 → 측정 설계 → 최종 승인
- `기존 PRD 정리해줘` → 기존 의도를 보존하는 Enhancement Mode
- `PRD 만들고 실행까지` → PRD 승인 후 실행 문서 6종과 `/goal` 핸드오프
- PRD만 요청하면 구현, `/goal`, 배포는 자동으로 시작하지 않습니다.

## 자동 운영 파일

- `PRD_WORKFLOW_CHECKLIST.md` — 전체 단계, 품질 게이트, blocker, 승인과 다음 작업을 추적합니다.
- `PRD_DECISIONS.md` — 인터뷰 답변, 근거, 확정 결정, 추론, 가정, 미결정 질문과 변경 이력을 보존합니다.

기존 파일이 있으면 통째로 교체하지 않고 현재 상태를 읽어 필요한 항목만 갱신합니다.

이 저장소는 직접 링크 설치용으로만 배포하며 별도의 공개 플러그인 디렉터리나 큐레이션 목록에는 등록하지 않습니다.

## 설치

GitHub에 게시한 뒤 저장소를 marketplace로 추가하고 플러그인을 설치합니다.

```bash
codex plugin marketplace add jaywanagent-debug/prd-workflow-codex --ref main
codex plugin add prd-workflow-codex@prd-workflows
```

로컬에서 먼저 시험하려면 저장소 루트에서 다음을 실행합니다.

```bash
codex plugin marketplace add .
codex plugin add prd-workflow-codex@prd-workflows
```

## 사용 예시

- `PRD 만들자. 직원용 운영 가이드 구조를 다시 설계하고 싶어.`
- `이 PRD는 기존 의도를 유지하면서 불필요한 내용만 정리해줘.`
- `이 PRD 검토하고 실행 준비 문서까지 만들어줘.`

## 공개용 정리 내용

- 개인 홈과 환경별 로컬 절대경로 제거
- 특정 담당자 호칭과 회사 내부 전용 승인 문구 제거
- 마케팅·QA·법무 등 이 PRD 체인과 무관한 내부 스킬 의존성 제거
- 비공개 문서와 고객 데이터의 외부 전송 금지 원칙 유지
- GPTaku MIT 라이선스와 Product on Purpose Apache-2.0 저작권·수정 고지 보존

## 라이선스

이 번들의 신규 라우터와 패키징 변경은 MIT License로 배포됩니다. `show-me-the-prd`와 `goaljaby`는 MIT, Product on Purpose 기반 7개 PM 스킬과 `pm-critic`은 Apache-2.0 조건을 따릅니다. 자세한 내용은 [THIRD_PARTY_NOTICES.md](./THIRD_PARTY_NOTICES.md)와 [LICENSES/Apache-2.0.txt](./LICENSES/Apache-2.0.txt)를 확인하세요.
