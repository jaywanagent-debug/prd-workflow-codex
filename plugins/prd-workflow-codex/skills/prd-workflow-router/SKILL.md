---
name: prd-workflow-router
description: Routes Korean or English PRD requests through the bundled build-risk, problem framing, hypothesis, interview, PRD generation, adversarial review, edge-case, acceptance-criteria, instrumentation, Replan, and execution-handoff skills. Use when the user says "PRD 만들자", "PRD 작성하자", "기획하자", "리플랜으로 검토해줘", "replan this", "기존 PRD 정리해줘", "PRD 만들고 실행까지", "make a PRD", or asks the agent to choose the complete PRD workflow automatically.
---

# PRD Workflow Router

## 목적

이 스킬은 환경별 전용 규칙을 제거한 공개용 PRD 라우터다. 플러그인에 포함된 전문 스킬을 순서대로 연결하고, PRD 작성·리플랜 검토·실제 구현을 분리한다. 위험 검토·문제와 가설·인터뷰·문서 체크·비판 검수·예외·완료 조건·측정 설계·승인 게이트를 사용자가 일일이 지정하지 않아도 기본 흐름에 포함한다.

## 기본 요청 계약

- 첫 PRD 질문 전에 `references/workflow-state-templates.md`를 읽고 대상 `PRD/` 폴더에서 `PRD_WORKFLOW_CHECKLIST.md`와 `PRD_DECISIONS.md`를 읽거나 생성한다. 단계·결정·가정·blocker가 바뀔 때마다 두 파일을 갱신한다.
- 인터뷰 질문 전에는 `PRD_DECISIONS.md`와 기존 자료를 먼저 검색한다. 확인된 답을 재사용하고 안전한 추론은 `inferred`로 기록하며, 미해결 gap만 질문한다.
- `PRD 만들자` / `PRD 작성하자` / `make a PRD` → 아래 전체 PRD 체인을 기본으로 실행한다.
- 사용자가 별도로 “인터뷰해”라고 말하지 않아도 부족한 정보만 gap interview로 확인한다. 입력이 충분하면 과잉 질문 없이 바로 문서를 만든다.
- 각 단계에 필요한 내용이 기존 입력에 이미 있으면 재질문하지 않고 정규화·검수만 한다.
- PRD 생성에는 5-file output, 비판 검수, edge cases, acceptance criteria, instrumentation spec, 최종 품질 체크를 기본 포함한다. 사용자가 별도로 체크리스트를 요청할 필요가 없다.
- 기존 기획·PRD·코드가 있으면 `show-me-the-prd`의 Enhancement Mode로 기존 의도를 보존하고 부족한 부분만 보강한다.
- `PRD 만들고 실행까지` / `PRD부터 구현까지` → PRD 생성과 검토를 먼저 끝낸 뒤, 사용자 승인 후 `goaljaby`로 실행 계획과 `/goal` 핸드오프를 준비한다.
- 이미 승인 가능한 PRD 폴더가 있고 “실행 준비”만 요청하면 `goaljaby`로 바로 간다.
- PRD만 요청한 경우 `goaljaby`, `/goal`, 코드 수정, 배포를 자동 시작하지 않는다.

## 라우팅

### 리플랜 — 계획 전용 합의 검토

`리플랜으로 검토해줘`, `리플랜 모드`, `replan this`처럼 명시했거나, 보안·인증·마이그레이션·개인정보·프로덕션 장애·공개 API 변경·상당한 비용·여러 시스템을 건드리는 계획이면 `prd-replan`을 먼저 사용한다.

1. 현재 계획, 관련 PRD, 코드 또는 운영 사실을 읽는다. PRD 상태 파일이 있으면 먼저 읽고 현재 내용을 보존한 채 필요한 기록만 추가한다.
2. `PRD_DECISIONS.md`에 Replan Decision Record를 append한다. 원칙 3~5개, 결정 요인, 실행 가능한 선택지 최소 2개, 각 선택지를 고르지 않은 이유를 포함한다.
3. Decision, Drivers, Alternatives considered, Why chosen, Consequences, Follow-ups 형식으로 ADR-lite를 만든다.
4. `foundation-build-risk-review`와 `utility-pm-critic`을 **순서대로** 실행해 P0/P1을 해결하거나 명시적으로 기록한다.
5. 고위험 계획이면 실패 시나리오, 단위·통합·E2E·운영 관측 검증 방법을 추가한다.
6. 결과는 항상 `pending approval`로 끝낸다.

리플랜은 검토만 한다. 이 단계에서는 `goaljaby`, `/goal`, 코드·설정·데이터 수정, 외부 발신, 배포를 실행하지 않는다. 승인 뒤 사용자가 별도로 “실행 준비” 또는 “goaljaby로 넘겨줘”라고 요청한 경우에만 기존 실행 전환 흐름으로 들어간다.

### 전체 PRD 체인

1. **시작 전 위험 검토 — `foundation-build-risk-review`**
   만들 가치와 가장 큰 실패 가정을 빠르게 확인한다. 학습·내부 실습 목적이면 시장성 대신 범위와 명확성만 본다.
2. **문제 정리 — `define-problem-statement`**
   사용자, 문제, 영향, 성공 기준, 제약, 열린 질문을 정리한다.
3. **가설 정리 — `define-hypothesis`**
   해결 가정을 반증 가능한 문장, 목표 수치, 검증 방법으로 바꾼다.
4. **본 PRD — `show-me-the-prd`**
   부족한 정보만 인터뷰하고 5-file PRD bundle을 만든다.
5. **비판 검수 — `utility-pm-critic`**
   PRD를 P0/P1/P2/P3로 공격적으로 검수한다. P0/P1은 수정한 뒤 한 번 재검수하고, 남으면 사용자 결정으로 넘긴다.
6. **예외 조건 — `deliver-edge-cases`**
   입력 경계, 오류 상태, 동시성, 외부 연동 실패, 복구 경로를 문서화한다.
7. **완료 조건 — `deliver-acceptance-criteria`**
   happy path, edge case, error state, non-functional requirement를 Given/When/Then으로 만든다.
8. **측정 설계 — `measure-instrumentation-spec`**
   이벤트, 속성, 발화 조건, 개인정보 처리, QA 검증 체크리스트를 만든다.
9. **최종 검토 게이트**
   문서 간 모순과 `[NEEDS CLARIFICATION]` 잔존 여부를 점검하고 사용자에게 승인·수정·보류를 요청한다.
10. **실행 전환 — `goaljaby`**
    사용자가 실행까지 요청했고 PRD를 승인한 경우에만 6개 실행 문서와 복사용 `/goal` 명령을 준비한다.

사용자가 “바로 PRD부터”라고 명시한 경우에만 1~3단계를 생략할 수 있다. 그래도 5~9단계의 품질 검수는 기본 유지한다.

### 권장 산출물

- `PRD_WORKFLOW_CHECKLIST.md`
- `PRD_DECISIONS.md`
- `00_BUILD_RISK_REVIEW.md`
- `00_PROBLEM_STATEMENT.md`
- `00_HYPOTHESIS.md`
- `show-me-the-prd`의 5-file PRD bundle
- `05_PRD_CRITIQUE.md`
- `06_EDGE_CASES.md`
- `07_ACCEPTANCE_CRITERIA.md`
- `08_INSTRUMENTATION_SPEC.md`
- 실행 승인 시 `goaljaby`의 6개 실행 문서

### 기존 PRD 개선

1. 기존 문서와 관련 자료를 먼저 읽는다.
2. 1~8단계 기준으로 존재하는 산출물과 누락된 산출물을 표시한다.
3. 유지할 결정과 변경할 결정을 구분한다.
4. 모순·누락·불필요한 내용을 제시하고 필요한 항목만 확인한다.
5. 승인된 범위만 수정하고 전체 체인의 문서 간 일관성을 다시 검사한다.

### PRD에서 실행 준비까지

1. PRD가 검토 가능한 상태인지 확인한다.
2. 실행까지 요청됐더라도 PRD 승인 전에는 `goaljaby`를 시작하지 않는다.
3. 승인 후 `goaljaby`가 `VALIDATION.md`, `RECOVERY.md`, `PLAN.md`, `PROGRESS.md`, `goal-command.md`, `PLANS.md`를 만든다.
4. 생성 결과를 사용자에게 검토받는다.
5. 실제 `/goal` 실행은 사용자가 복사 실행하거나 명시적으로 승인한 뒤에만 진행한다.

## 안전 경계

- 외부 전송, 게시, 유료 서비스 사용, 프로덕션 변경은 별도 승인 없이 실행하지 않는다.
- 비공개 문서나 고객 데이터를 외부 리서치 서비스에 전송하지 않는다.
- 기존 파일을 수정할 때는 먼저 현재 상태를 읽고 필요한 차이만 반영한다.
- 요청이 PRD 작성까지만인지 실행 준비까지인지 모호하면 PRD 작성과 검토까지만 진행한다.

## 참조

모든 PRD workflow 시작 시 `references/workflow-state-templates.md`를 먼저 읽는다.
