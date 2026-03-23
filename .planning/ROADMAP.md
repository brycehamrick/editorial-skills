# Roadmap

## Backlog

### Phase 999.1: editorial-translation skill (BACKLOG)

**Goal:** Build an `editorial-translation` skill for the editorial skills collection that translates nonfiction documents accurately into a target language while preserving intent, readability, and formatting. Primary use case is Spanish (to and from), but designed to work for any language pair.

**Context:**
- A reference implementation (`baoyu-translate`) lives in the repo root — useful for the chunking logic, audience/style options, and multi-mode workflow (quick/normal/refined), but is Chinese-centric and needs adaptation
- The skill should default to Spanish rather than Chinese, and generalize cleanly to any language
- Chunk threshold and chunk max words settings exist because long documents exceed context limits — chunking splits at markdown block boundaries and translates in parallel for consistency
- Consider using the installed `codex` skill (OpenAI Codex CLI) to perform the actual translation, passing content via temp files in `.tmp/` rather than stdin/stdout (5000-word chunks fit within codex's input capacity)
- Must follow all conventions in CLAUDE.md: frontmatter, context check, two-phase process, workflow position section, skill-creator use

**Requirements:** TBD
**Plans:** 0 plans

Plans:
- [ ] TBD (promote with /gsd:review-backlog when ready)
