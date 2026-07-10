# PRD Workflow State Templates

## Required state files

At the start of every PRD workflow, locate the target `PRD/` directory and read these files if they exist:

- `PRD_WORKFLOW_CHECKLIST.md`
- `PRD_DECISIONS.md`

Create only missing files. Never replace an existing state file wholesale. Read the current content, update the smallest relevant section, and preserve human edits.

Update both files immediately after each completed stage, user decision, changed assumption, or newly discovered blocker. Before asking any interview question, search `PRD_DECISIONS.md` and the source documents. Do not ask again when the answer is already explicit or can be safely inferred; record the source and confidence instead.

## `PRD_WORKFLOW_CHECKLIST.md`

```markdown
# PRD Workflow Checklist — <project>

## Workflow status

- Status: in_progress
- Current stage: 0. Intake and state setup
- Last updated: <ISO-8601 timestamp>
- Final approval: pending
- Execution requested: no

## Stage checklist

- [ ] 0. Intake and state setup
  - Result: pending
  - Evidence/output: `PRD_DECISIONS.md`
- [ ] 1. Build risk review — `foundation-build-risk-review`
  - Result: pending
  - Evidence/output: `00_BUILD_RISK_REVIEW.md`
- [ ] 2. Problem statement — `define-problem-statement`
  - Result: pending
  - Evidence/output: `00_PROBLEM_STATEMENT.md`
- [ ] 3. Hypothesis — `define-hypothesis`
  - Result: pending
  - Evidence/output: `00_HYPOTHESIS.md`
- [ ] 4. Main PRD — `show-me-the-prd`
  - Result: pending
  - Evidence/output: five-file PRD bundle
- [ ] 5. Adversarial review — `utility-pm-critic`
  - Result: pending
  - Evidence/output: `05_PRD_CRITIQUE.md`
- [ ] 6. Edge cases — `deliver-edge-cases`
  - Result: pending
  - Evidence/output: `06_EDGE_CASES.md`
- [ ] 7. Acceptance criteria — `deliver-acceptance-criteria`
  - Result: pending
  - Evidence/output: `07_ACCEPTANCE_CRITERIA.md`
- [ ] 8. Instrumentation — `measure-instrumentation-spec`
  - Result: pending
  - Evidence/output: `08_INSTRUMENTATION_SPEC.md`
- [ ] 9. Cross-document validation and human approval
  - Result: pending
  - Evidence/output: approval record below
- [ ] 10. Execution handoff — `goaljaby`
  - Result: not_requested
  - Evidence/output: `PLANS.md` and five companion files

## Quality gates

- [ ] No unresolved P0 findings
- [ ] Every P1 finding is fixed or explicitly accepted by the user
- [ ] No unexplained contradiction across problem, hypothesis, PRD, edge cases, acceptance criteria, and instrumentation
- [ ] Every `[NEEDS CLARIFICATION]` item is resolved, accepted as open, or assigned an owner
- [ ] Acceptance criteria cover the happy path, important failure paths, and relevant non-functional requirements
- [ ] Instrumentation maps to the hypothesis and success criteria
- [ ] Private data was not sent to an external service without approval

## Approval record

- Decision: pending
- Approved scope:
- Accepted open items:
- Approved by:
- Approved at:

## Blockers and next action

- Blockers: none
- Next action:
```

When a stage is completed or explicitly skipped, mark its checkbox `[x]` and set `Result` to `completed` or `skipped_by_user: <reason>`. A checkbox means the stage is resolved, not necessarily that an artifact was authored. Never mark a blocked or merely started stage complete.

## `PRD_DECISIONS.md`

```markdown
# PRD Decisions and Interview Notes — <project>

## Confirmed context

- Problem:
- Target user:
- Desired outcome:
- Current workaround:
- Scope boundary:

## Interview evidence

| ID | Question or evidence sought | Answer or source | Confidence | Used by stages |
|---|---|---|---|---|
| I-001 |  |  | confirmed / inferred / weak |  |

## Decisions

| ID | Decision | Rationale | Source | Status |
|---|---|---|---|---|
| D-001 |  |  | user / document / research | confirmed |

## Assumptions

| ID | Assumption | Risk if wrong | Validation | Status |
|---|---|---|---|---|
| A-001 |  |  |  | open |

## Open questions

| ID | Question | Why it matters | Owner | Needed before |
|---|---|---|---|---|
| Q-001 |  |  |  |  |

## Change log

| Timestamp | Change | Reason/source |
|---|---|---|
|  |  |  |
```

Record interview answers in the user's words when practical. Label agent inference as `inferred`, never as confirmed. When a decision changes, preserve the old entry as superseded and append the new decision plus a change-log row.
