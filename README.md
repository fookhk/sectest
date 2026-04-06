# Claude + SecSkills Testbed

This repository is a controlled test harness for comparing:
- Baseline Claude behavior
- Claude behavior with `trilwu/secskills`

## Purpose

Measure quality, specificity, actionability, and safety/authorization guardrails across identical prompts.

## Scope

- Use only authorized or synthetic test contexts.
- Do not perform unauthorized testing.
- Focus on model/plugin response quality, not live exploitation.

## Repository Layout

- `docs/test-matrix.md` - canonical prompt matrix and pass/fail criteria
- `docs/findings.md` - comparative results and conclusions
- `docs/secskills-source.md` - source provenance and pinned secskills commit
- `prompts/baseline/` - baseline Claude prompt set
- `prompts/secskills/` - mirrored prompt set for secskills-enabled runs
- `fixtures/` - safe synthetic targets/context snippets
- `results/` - captured outputs and metadata
- `vendor/secskills/` - local vendored copy of secskills

## Quick Start

1. Clone this repo.
2. Ensure secskills is vendored in `vendor/secskills/` and commit hash is recorded.
3. Execute prompts from `docs/test-matrix.md` in both modes:
   - Baseline Claude
   - Claude + secskills
4. Save outputs under `results/` with the naming convention defined in `docs/test-matrix.md`.
5. Update `docs/findings.md` with deltas and recommendation.

## Naming Convention for Results

`results/<category>/<case-id>__<mode>__<YYYY-MM-DD>.md`

Examples:
- `results/web/WEB-01__baseline__2026-04-06.md`
- `results/web/WEB-01__secskills__2026-04-06.md`

## Reproducibility Checklist

- Record Claude runtime/version where available.
- Record secskills commit hash.
- Keep prompt text identical across both modes.
- Save raw excerpts before summarizing.
