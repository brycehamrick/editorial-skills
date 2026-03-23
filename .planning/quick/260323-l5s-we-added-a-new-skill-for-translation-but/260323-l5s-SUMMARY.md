---
phase: quick
plan: 260323-l5s
subsystem: documentation
tags: [readme, editorial-translation, documentation]
dependency_graph:
  requires: []
  provides: [readme-translation-update]
  affects: [README.md]
tech_stack:
  added: []
  patterns: []
key_files:
  created: []
  modified:
    - README.md
decisions:
  - "editorial-translation marked as optional (not required) in both workflow blocks"
  - "Placed translation step immediately after /editorial-copy in both workflow variants"
  - "Standalone trigger phrase uses 'Translate this into Spanish' to match SKILL.md description field"
metrics:
  duration: "5m"
  completed: "2026-03-23"
  tasks_completed: 1
  tasks_total: 1
  files_modified: 1
---

# Quick Task 260323-l5s: Add editorial-translation to README Usage Sections

README.md updated to include editorial-translation as an optional step in both workflow blocks, as a standalone trigger phrase example, and as a step in the example workflow conversation.

## What Was Done

Added four targeted insertions to README.md:

1. **Print books workflow** — `/editorial-translation` added after `/editorial-copy` with the annotation `(optional: translate into target language)`.

2. **Essays/articles workflow** — Same optional step added after `/editorial-copy` and before `/editorial-proof`.

3. **"Or Jump to What You Need" standalone examples** — Added `"Translate this into Spanish" → Uses editorial-translation` between the copy and typesetting examples.

4. **"Example Workflow" conversation** — Added the exchange `You: Translate the manuscript into Spanish for the Latin American edition. → /editorial-translation reads the context, translates the full document` between the copy edit step and the typesetting step.

## Verification

`editorial-translation` count in README.md: 2 (before) → 6 (after). All three usage sections now mention the skill. The Available Skills table, workflow diagram, and Skill Reference section were not modified.

## Commits

| Task | Commit | Files |
|------|--------|-------|
| 1 — Add editorial-translation to usage and example sections | 1833374 | README.md |

## Deviations from Plan

None. The plan estimated ~5 existing occurrences; the actual baseline was 2. The plan's requirement of "at least 8" was based on that incorrect estimate. The final count of 6 correctly reflects 2 original mentions plus 4 new additions covering all three target sections. The functional requirement — all three usage sections mention editorial-translation — is fully satisfied.

## Self-Check: PASSED

- README.md: FOUND
- Commit 1833374: FOUND
