# Audience and Style Presets

Reference tables for the `audience` and `style` settings in EXTEND.md and CLI flags.

## Audience Presets

Audience determines annotation depth and register — how much the translator explains domain jargon and cultural references, and what level of formality is appropriate.

| Value | Description | Effect |
|-------|-------------|--------|
| `general` | General readers (default) | Plain language, more translator's notes for jargon and cultural references |
| `technical` | Developers / engineers / domain experts | Less annotation on common technical terms; domain vocabulary used without apology |
| `academic` | Researchers / scholars | Formal register, precise terminology, citation-aware; minimal explanatory notes on established concepts |
| `business` | Business professionals | Business-friendly tone, explain technical concepts briefly, action-oriented framing |

Custom audience descriptions are also accepted, e.g., `--audience "Spanish-speaking readers interested in AI but without a technical background"`. The more specific the description, the better the translator can calibrate register and annotation depth.

## Style Presets

Style determines voice and sentence-level choices — independent of audience. A technical audience can receive an elegant-style translation; a general audience can receive a formal one.

**`elegant` is the default style for this skill**, chosen as more appropriate than `storytelling` for nonfiction books aimed at Spanish-language readers, where literary quality and careful word choice are highly valued.

| Value | Description | Effect |
|-------|-------------|--------|
| `storytelling` | Engaging narrative flow | Draws readers in, smooth transitions, vivid phrasing |
| `formal` | Professional, structured | Neutral tone, clear organization, no colloquialisms |
| `technical` | Precise, documentation-style | Concise, terminology-heavy, minimal embellishment |
| `literal` | Close to original structure | Minimal restructuring, preserves source sentence patterns |
| `academic` | Scholarly, rigorous | Formal register, complex clauses acceptable, citation-aware |
| `business` | Concise, results-focused | Action-oriented, executive-friendly, bullet-point mindset |
| `humorous` | Preserves and adapts humor | Witty, playful, recreates comedic effect in target language |
| `conversational` | Casual, spoken-like | Friendly, approachable, as if explaining to a friend |
| `elegant` | Literary, polished prose **(default)** | Aesthetically refined, rhythmic, carefully crafted word choices |

Custom style descriptions are also accepted, e.g., `--style "poetic and lyrical"` or `--style "warm but authoritative, like a trusted mentor"`.

## How Audience and Style Interact

Audience determines annotation depth and register. Style determines voice and sentence-level choices. They are independent — a technical audience can get an elegant-style translation, and a general audience can get a formal one.

**Examples:**

| Audience | Style | Result |
|----------|-------|--------|
| `general` | `elegant` | Polished literary prose with generous translator's notes; accessible to non-specialists |
| `technical` | `formal` | Clean, precise professional language; minimal annotations; assumes domain fluency |
| `academic` | `academic` | Formal scholarly register; complex sentences acceptable; terminologically exact |
| `business` | `conversational` | Casual, approachable tone; explains concepts briefly; skips deep annotations |

The default combination — `general` audience + `elegant` style — is appropriate for most nonfiction books translated for Spanish-language readers.
