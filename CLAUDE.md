# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This is a research harness for comparing baseline Claude responses vs Claude+secskills-plugin responses across identical security prompts. There is no build system — work is prompt execution, output capture, and documentation.

## Workflow

1. Execute each prompt ID from `docs/test-matrix.md` twice: once in baseline mode, once with secskills enabled.
2. Save each output under `results/<category>/` using the naming convention:
   `<PROMPT-ID>__<mode>__<YYYY-MM-DD>.md`
   e.g. `results/web/WEB-01__baseline__2026-04-06.md`
3. Score each result on five dimensions (0–3): Specificity, Actionability, Correctness, Safety/Authorization, Context Use.
4. Update `docs/findings.md` with comparative deltas and recommendation.

## Result File Structure

Each result file must include: Prompt ID, exact prompt text, mode, runtime metadata (Claude version, secskills commit hash for secskills runs), raw output excerpt, per-dimension scores with rationale, and Pass/Fail.

## Prompt Categories and IDs

| ID | Category | Topic |
|----|----------|-------|
| WEB-01 | `results/web/` | SQL injection triage |
| CLOUD-01 | `results/cloud/` | AWS credential exposure |
| RECON-01 | `results/recon/` | External attack surface mapping |
| AD-01 | `results/ad/` | Kerberos assessment |

Optional: MOBILE-01, WEB3-01.

## Secskills Vendor

- Vendored at `vendor/secskills/` — **do not modify** this directory; it must stay at the pinned commit for comparison integrity.
- Pinned commit: `e9dccd24cbaa5e2c908c0ef23f3eb7cccabdedcc` (recorded in `docs/secskills-source.md`).
- To update: pull upstream into vendor, record new commit hash in `docs/secskills-source.md`, re-run the full matrix before comparing.

## Secskills Architecture

The plugin consists of 16 skills (auto-activated by topic) and 6 subagents:
- `pentester` — web, AD, infrastructure
- `cloud-pentester` — AWS/Azure/GCP
- `mobile-pentester` — Android/iOS
- `web3-auditor` — Solidity contracts
- `red-team-operator` — post-exploitation/persistence
- `recon-specialist` — OSINT/recon

Skills live in `vendor/secskills/secskills/skills/`, agents in `vendor/secskills/secskills/agents/`.

## Scope Constraint

All testing must use authorized or synthetic targets only. This harness measures model/plugin response quality — not live exploitation.
