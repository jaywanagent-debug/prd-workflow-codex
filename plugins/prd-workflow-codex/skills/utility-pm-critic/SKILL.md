---
name: utility-pm-critic
description: Run adversarial review on a PM artifact via the pm-critic sub-agent. Returns findings graded P0/P1/P2/P3 with a concrete fix suggestion per finding and a machine-readable status block. Use after producing a PRD, meeting recap, OKR set, persona, or any PM artifact you want stress-tested before it ships.
license: Apache-2.0
metadata:
  classification: utility
  version: "1.0.1"
  updated: 2026-06-10
  category: review
  frameworks: [triple-diamond]
  author: product-on-purpose
---
<!-- PM-Skills | https://github.com/product-on-purpose/pm-skills | Apache 2.0 -->
# PM Critic (Dispatch Skill)

This skill is a cross-client dispatch wrapper for the `pm-critic` sub-agent. It exists so that users on non-Claude clients can run adversarial review with the same intent as Claude Code users, without depending on native plugin sub-agent infrastructure.

Per master plan D11 (amended) + D30, sub-agents are a Claude Code plugin feature. Non-Claude clients (Codex CLI, Cursor, Windsurf, Copilot, Gemini CLI) cannot natively load `agents/pm-critic.md`. This skill bridges the gap.

## Bundled PRD Routing

This file is modified for the `prd-workflow-codex` bundle. Use the bundled `show-me-the-prd` as the PRD authoring standard and the bundled `deliver-edge-cases`, `deliver-acceptance-criteria`, and `measure-instrumentation-spec` as its hardening standards.

Do not bypass the bundled `goaljaby` for Codex `/goal` handoff. Skills not included in this bundle are optional suggestions, not runtime requirements.

## When to Use

- You want adversarial review of a PM artifact (PRD, OKR set, persona, lean canvas, meeting recap, interview synthesis, problem statement, hypothesis, edge case catalog, retrospective, etc.)
- You are running on a non-Claude AI client and the `pm-critic` sub-agent is not natively available
- You are running on Claude Code and prefer skill-invocation semantics over sub-agent semantics (e.g., for consistency across a multi-step workflow that mixes skills and sub-agent intents)

## When NOT to Use

- You want a structural lint / repo-level audit -> use `utility-pm-skill-auditor` (audits skills + repo state) instead
- You want to author a PRD (this skill only reviews) -> use the bundled `show-me-the-prd`
- You want code review -> use a code-review-specific tool (this skill is for PM artifacts)
- You want to enforce style rules like em-dash sweep -> that is `pm-release-conductor`'s G0 gate, not this skill

## Instructions

**Runtime detection step.** Determine which AI client is invoking this skill.

### If you are running in Claude Code with the pm-skills plugin installed

Invoke `@agent-pm-skills:pm-critic` on the target artifact. Pass the artifact path as argument (or the most recent artifact in session context if no argument is provided). Return the sub-agent's findings to the user. No further action needed from this skill - the sub-agent handles the review natively in its own context window.

### If you are running in any other AI client

Codex CLI, Cursor, Windsurf, Copilot, Gemini CLI, ChatGPT, or any other client without native pm-skills plugin sub-agent support:

1. Read the canonical sub-agent definition at `agents/pm-critic.md`
2. Execute the system prompt body in that file as your operating instructions for this turn
3. Read the target PM artifact specified by the user (path from `$ARGUMENTS`, or most recently produced artifact in session)
4. Read the canonical standards docs referenced by the pm-critic system prompt for the artifact type. For PRDs, use the bundled `skills/show-me-the-prd/SKILL.md` and the bundled hardening skills.
5. Produce findings graded P0/P1/P2/P3 with concrete fix suggestions, formatted per `references/TEMPLATE.md`
6. End the output with the layered structure per master plan D26:
   - Section (1): full human-readable findings (the P0/P1/P2/P3 report)
   - Section (2): `## Status Summary` in prose, summarizing what was found and what the user should do next
   - Section (3): `## Status` YAML block with machine-readable fields

## Output Format

See `references/TEMPLATE.md` for the canonical output structure (with the layered Status envelope per D26). See `references/EXAMPLE.md` for a worked example showing a real cross-client dispatch run against a PRD.

## Composition

- **Skills:** In this bundle, compose it with `define-problem-statement`, `define-hypothesis`, `show-me-the-prd`, `deliver-edge-cases`, `deliver-acceptance-criteria`, and `measure-instrumentation-spec`.
- **Sub-agents:** On Claude Code, this skill dispatches to `pm-critic` sub-agent. On non-Claude, this skill IS the inline execution; no further dispatch.
- **Workflows:** `pm-workflow-orchestrator` (shipped v2.24.0) can invoke this skill at quality-gate steps for cross-client compatibility.

## Cross-Client Notes

Upstream cross-client docs are not bundled in this local selected install. Treat this skill as the Codex-compatible inline path: read `agents/pm-critic.md`, read the relevant active skill or manual reference, then use `references/TEMPLATE.md` for output shape.

The "read and execute inline" pattern depends on the AI being able to:

1. Read a file path provided as a reference (most AI clients support this)
2. Treat that file's content as operating instructions for the current turn (most AI clients support this for SKILL.md-style instructions)
3. Read additional referenced standards docs at invocation time (all major AI clients support this)

If any of these are unreliable on a given client, that client cannot use this dispatch skill effectively.

## Reference Files

- Canonical sub-agent definition: [`agents/pm-critic.md`](../../agents/pm-critic.md)
- Output template: `references/TEMPLATE.md`
- Worked example: `references/EXAMPLE.md`
