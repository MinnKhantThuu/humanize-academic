# humanize-academic

**An agent skill that removes AI-writing tells from English text — with
dedicated modes for academic coursework and project documentation.**

Works in [Codex CLI](https://github.com/openai/codex), Claude Code, and any
agent that reads `SKILL.md` skill files.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Why this exists

Generic humanizers treat every text the same. But a university essay, a
README, and a blog post fail in different ways and need different
protection:

- An **essay** with `delve` and a uniform paragraph rhythm reads as
  ghostwritten. A citation moved off its claim reads as broken.
- A **README** with emoji headings and "not just X, but Y" reads as
  generated. Its code blocks and commands must survive editing untouched.
- A **student's essay** written in band-7 English suddenly containing
  band-9 vocabulary reads as someone else's work — even if no detector
  flags it.

`humanize-academic` switches modes automatically and protects what each
text type actually needs protected.

## What's different from other humanizer skills

| Capability | This skill | Generic humanizers |
|---|---|---|
| **Academic mode** — essays, coursework | yes, auto-activates | rare |
| **Citation-style awareness** — APA / MLA / Harvard in-text formats recognized and preserved byte-exact, attached to their claims, reference list never touched | yes | most treat citations as opaque tokens at best |
| **Docs mode** — README, technical docs | yes, auto-activates; code blocks, commands, paths, URLs, config keys, version numbers untouchable | rare |
| **ESL-safe vocabulary ceiling** — IELTS band 7–8; will not insert words that break consistency with the writer's demonstrated level | yes | no |
| **Word-count discipline** — output stays within ±10% of input (assignments have word counts) | yes | no |
| **Light-edit guard** — detects already-human text and refuses to over-correct | yes | no |
| Core pattern library | 26 patterns + 9 levers | varies |

Grounded in Wikipedia's
[Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
(via [blader/humanizer](https://github.com/blader/humanizer), MIT) and
2024–2026 detection research
(via [harshaneel/humanize](https://github.com/harshaneel/humanize), MIT).

## The three modes

| Text type | Mode | What gets protected |
|---|---|---|
| Essay, assignment, coursework, anything with citations | **academic** | citations (byte-exact, style-aware), quotations, thesis claims, word count ±10%, vocabulary-level consistency |
| README, docs/, guides, technical documentation, project reports | **docs** | code blocks, commands, file paths, URLs, config keys, version numbers, genuine list structure |
| Blog posts, opinions, informal prose | **core** | facts and claims |

## Installation

### Codex CLI

```bash
git clone https://github.com/homelander-mm/humanize-academic.git
mkdir -p ~/.codex/skills
cp -R humanize-academic/skills/humanize ~/.codex/skills/
```

Restart Codex. The skill auto-activates on "humanize this", essay/assignment
requests, and README/docs work.

### Claude Code

```bash
git clone https://github.com/homelander-mm/humanize-academic.git
mkdir -p ~/.claude/skills
cp -R humanize-academic/skills/humanize ~/.claude/skills/
```

### Any other agent

Copy `skills/humanize/` into whatever directory your agent reads skills
from, or paste `SKILL.md` contents into a project instruction file.

### Per-project install

Copy the `skills/humanize/` folder into the repo, then reference it from
the repo's `AGENTS.md`:

```markdown
## Writing
- When writing or editing English prose (docs, README, reports, essays),
  use the humanize skill at skills/humanize/SKILL.md.
```

## Usage

```text
Humanize this paragraph:
[paste text]

Humanize the prose in docs/DEPLOY.md        ← file mode; edits the file

Write a 500-word introduction about [topic]  ← generation mode; human
for my coursework                             from the first draft
```

The mode is chosen automatically from the text and the request. You can
force one: "humanize this in academic mode", "docs mode, don't touch the
install commands".

## Honest limits

Read this before relying on the skill:

- **This is not a detector-evasion tool.** It makes prose read human
  because AI-sounding prose is bad prose. Rule-based rewriting measurably
  lowers perplexity-based detector scores (ZeroGPT-class), but learned
  classifiers (GPTZero, Turnitin, Grammarly, Pangram) read an
  instruction-tuning fingerprint in the model's weights that surface
  editing cannot reach. No text-manipulation skill reliably beats those.
  Anyone claiming otherwise is selling something.
- **Substance is not style.** Humanized text can still carry
  AI-characteristic errors: confident hallucinations, missing lived
  detail, implausible specificity. The skill preserves what you give it;
  it cannot add the personal experience you don't supply.
- **Consistency is the real exposure.** In assessed academic work, the
  strongest signal is contrast with your other writing and in-class
  performance. The vocabulary ceiling reduces that contrast; it cannot
  erase it.
- **Use in line with your institution's rules.** This skill edits
  expression; it does not license submitting work that isn't yours under
  policies that require it to be. Check what your institution allows
  (editing assistance vs. authorship).

## Structure

```
skills/humanize/
├── SKILL.md                      # core rules, 9 levers, mode switching, banned vocabulary
└── references/
    ├── patterns.md               # the 26 AI-writing patterns with before/after examples
    ├── academic-mode.md          # citation handling, academic hedging, band ceiling
    └── checklist.md              # the 9-point self-audit run on every draft
```

## License

MIT. Pattern library adapted from
[blader/humanizer](https://github.com/blader/humanizer) (MIT) and
[harshaneel/humanize](https://github.com/harshaneel/humanize) (MIT); both
derived from Wikipedia's "Signs of AI writing" and the detection research
literature respectively.

## Acknowledgments

- [blader/humanizer](https://github.com/blader/humanizer) — the pattern
  catalog and the four-pass workflow
- [harshaneel/humanize](https://github.com/harshaneel/humanize) — the
  nine levers, the RLHF-fingerprint research grounding, and the honest
  benchmarking culture
- [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
  and WikiProject AI Cleanup — the original catalog
