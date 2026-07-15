---
name: prd-replan
description: Performs a plan-only Replan review for a PRD, architecture proposal, migration, security-sensitive change, or other high-risk plan. Use when the user says "리플랜", "리플랜으로 검토해줘", "replan this", or needs at least two viable options before approval.
---

# PRD Replan

## Purpose

Replan is a decision-quality review, not an execution command. It converts a high-risk plan into an explicit recommendation with alternatives, an ADR-lite, verification expectations, and a human approval gate.

## Rules

- Read the current plan and supporting facts before judging it. If `PRD_WORKFLOW_CHECKLIST.md` or `PRD_DECISIONS.md` exists, read it first.
- Preserve existing state files. Append a Replan Decision Record instead of replacing prior decisions.
- State 3–5 principles, the top decision drivers, and at least two viable options. Record why an option is rejected; do not silently omit it.
- Run `foundation-build-risk-review` and then `utility-pm-critic` sequentially. Resolve P0/P1 findings or explicitly record their owner and acceptance status.
- For security, migration, privacy, production, public API, significant cost, or cross-system work, include concrete unit, integration, end-to-end, and operational-observability verification.
- End every Replan result with `pending approval`.

## Required record

Use `references/replan-decision-record.md`. The record must include:

1. Scope and risk trigger
2. Principles and decision drivers
3. At least two options with bounded pros, cons, and invalidation rationale
4. ADR-lite: Decision, Drivers, Alternatives considered, Why chosen, Consequences, Follow-ups
5. Sequential-review findings and P0/P1 disposition
6. Required verification for high-risk work

## Stop boundary

Never use Replan to execute. Do not invoke `goaljaby`, create a `/goal` command, change code or configuration, write external systems, send messages, deploy, spend money, or delegate implementation.

After the user approves the recommendation, wait for a separate explicit request to prepare execution with `goaljaby` or to implement the approved plan.
