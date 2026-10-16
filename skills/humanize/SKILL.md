---
name: humanize
description: >
  Rewrite or generate English text so it reads as naturally human-written.
  Three auto-switching modes: academic mode for essays, assignments and
  coursework (citation-preserving for APA/MLA/Harvard, IELTS band 7-8
  vocabulary ceiling, word-count discipline), docs mode for README files
  and technical documentation (code blocks, commands and links untouched),
  and core mode for general prose. Use when asked to "humanize this",
  "rewrite naturally", "make this sound human", "make this less robotic",
  or when writing/editing/reviewing any document that must avoid
  AI-writing patterns. Preserves all facts, citations, quotes, code blocks,
  commands, and structure. Not for code or data.
metadata:
  version: "1.2.0"
  based-on: blader/humanizer (MIT) + harshaneel/humanize (MIT) + academic and docs adaptations
---

# Humanize — natural English writing, assignment-grade

Rewrite AI-sounding text so it reads like a person wrote it. Keep every fact,
citation, quote, and claim. Never invent anything.

## Modes at a glance

| Text type | Mode | Reference |
|---|---|---|
| Essay, assignment, coursework, citation | **academic mode** | [academic-mode](references/academic-mode.md) |
| README, docs/, guides, project reports, technical documentation | **docs mode** | section below |
| Blog posts, opinions, informal writing | core rules only | this file |

## Docs mode (README, documentation, project reports)

Activates when the text is project documentation: README, docs/ pages,
setup guides, architecture notes, deployment docs, status reports.

**Docs-specific rules (on top of core levers):**
- Keep neutral-plain register. Docs are allowed to be plain; plain is not
  the same as robotic. The patterns still apply (no "not X but Y", no
  forced triads, no decorative bold, no "It is important to note").
- Never touch: code blocks, inline code, commands, file paths, URLs,
  version numbers, config keys, YAML frontmatter, tables of data.
- Structure may stay list-heavy where readers scan (setup steps stay
  numbered steps). Do not flatten a genuinely scannable setup guide into
  prose. Flatten template decoration, not genuine structure.
- Facts, claims about behavior, and requirements are untouchable. Reword
  the sentences around them only.
- Headings stay descriptive and sentence-case; no emoji, no arrows, no
  decorative rules between sections.
- Reports written from evidence (test results, logs) keep every number and
  every outcome; reword only the narration around them.

## When academic mode activates

Turn academic rules ON (see [academic-mode](references/academic-mode.md)) when
the text or the request shows any of: essay, assignment, coursework, homework,
report, literature review, term paper, thesis statement, references,
citation, APA/MLA/Harvard, word count, professor, module, "for my class".

Academic mode changes register decisions but never disables the core
patterns. A formal register is not a license for robotic prose.

## Core workflow (always all four passes)

0. **Density pre-check (light-edit guard).** Before rewriting, judge how
   much of the input is actually AI-flavored. If the text reads largely
   human already — varied rhythm, specific details, natural hedges — make
   the smallest edit that removes the few real tells, and say so ("light
   edit: three tells fixed"). Do not rewrite clean prose for the sake of
   rewriting. This skill's most common failure mode is over-correcting
   writing that was fine.

1. **Mark the tells.** Read the whole text once. Flag every pattern from
   [patterns](references/patterns.md), strongest first (patterns 1–5 justify
   an edit on one sighting; patterns marked *weak alone* need company).
   Look at paragraph shape, not just sentences: a contrast split across two
   sentences, three parallel examples, the same closer after every section.
2. **Draft the rewrite.** You may reorder, merge, split, and shorten dull
   parts. Keep every supported claim, every citation attached to its claim,
   every quotation verbatim. Do not add a fact, name, number, date, quote,
   or source that is not in the input. If a sentence needs a detail you do
   not have, write a simpler sentence instead.
3. **Self-audit.** Run [checklist](references/checklist.md) honestly. Fix
   what fails. The tells that most often survive a first rewrite: not-X-but-Y
   contrasts, one-line closers, forced triads, dashes, and bold labels.
4. **Write the final version.** Rewrite paragraphs around their main point
   rather than patching flagged phrases. Vary sentence length. Read it aloud
   in your head; if a sentence sounds like an announcement, it is a tell.

## The nine levers (apply in every rewrite)

### 1. Perplexity injection
Replace predictable vocabulary with the word a specific person would choose
here. One or two genuinely surprising but accurate word choices per
paragraph. A surprising word is not a rare word: "the delay cost us the
semester" beats "the temporal displacement adversely impacted academic
outcomes". In academic mode the surprise lives in precise verbs and concrete
nouns, not fancy adjectives.

### 2. Burstiness (sentence-length variance)
- At least one sentence of six words or fewer per 150 words of output.
- Never three consecutive sentences within five words of the same length.
- Academic target: sentence-length standard deviation above 40% of the mean.
- Long sentences are allowed only when the thought genuinely cannot be
  broken without losing the connection between its parts.

### 3. Hedge surgery
Delete the standard hedge set: "it is important to note that", "it is worth
mentioning", "generally speaking", "in many cases", "it could be argued
that" (when nothing is actually argued against). Replace with direct
assertion. Keep a hedge only when the source text is genuinely uncertain,
and then express it the way a careful student would: "the data suggest,
though the sample is small, that..."

### 4. Structural flattening
Structure comes from the content, not from a template. No bullet list plus
numbered sections plus "In conclusion" unless the assignment format demands
it. A paragraph is a topic move plus evidence plus what the writer makes of
it. No restating the topic sentence at the end of the paragraph.

### 5. Specificity insertion
Ground every abstract claim in what the input provides: numbers, named
examples, dates, sources. If the input is abstract, leave it abstract rather
than inventing specifics. Generic: "many studies have shown". Grounded:
"Chen's 2021 trial and the Okafor meta-analysis both found..." (only when
the input names them).

### 6. Voice and register
Follow the text type. In reflective or opinion pieces: first person is fine,
mild self-correction is fine ("or perhaps more accurately..."), mixed
feelings are fine. In analytical academic work: first person stays out,
perspective shows up through what the writer chooses to compare and
emphasize. Contractions: acceptable in informal text, sparing in academic
(avoid "don't" in a thesis-driven essay; "it's" is fine in a blog post).

### 7. Human transitions
Remove AI transition scaffolding: "Furthermore", "Moreover", "Additionally",
"In conclusion", "It is clear that". Replace with what actually connects the
two ideas: "The second problem is cost." / "That study, however, used a
sample of twelve." / "Which raises a harder question:" Often the best
transition is none; two sentences can sit next to each other.

### 8. Punctuation limits
- Em dash (—): maximum one per 300 words, and only if the input uses dashes.
  Replace with period, comma, or parentheses.
- Semicolon: remove in nearly all cases. Keep only in lists whose items
  contain commas ("Austin, TX; Denver, CO").
- Mid-sentence colon ("The problem: nobody tests this."): remove. A colon
  may appear only after a grammatically complete sentence introducing a
  list or quotation.
- Curly quotes: straighten, unless the assignment format requires otherwise.
- Ellipses and exclamation marks: rare in academic work; cut on sight.

### 9. RLHF voice strip
This is the highest-leverage lever. Remove the assistant fingerprint:
acknowledgment openers ("That's a great question"), offers ("Would you like
me to..."), helpful-summaries-of-what-you-just-said, unprompted balanced
tradeoffs ("While X has benefits, Y also has merits"), structured enumeration
when one flowing answer serves better, and hedged closers ("I hope this
helps"). The text should read like someone solving the problem, not like
someone serving a customer.

## Academic-mode quick rules (details in references/academic-mode.md)

- Citations are untouchable: an in-text citation stays exactly where the
  original put it, in exactly the original format (APA, MLA, or Harvard —
  preserve whichever appears). Never drop, move, or reformat a citation.
- Quotations in "..." are verbatim. Never edit inside quotation marks.
- The reference list is not prose. Never rewrite it.
- Thesis, topic sentences, and the evidence-to-analysis order survive.
- Word count: final output must land within ±10% of the input length unless
  the user specifies otherwise.
- Vocabulary ceiling: IELTS band 7–8. Prefer the precise word over the
  impressive word. Do not insert words a second-language student would not
  plausibly use ("perfunctory", "obfuscate", "recalcitrant"). Consistency
  with the writer's apparent level protects the writer.

## Banned vocabulary (replace on sight)

delve, tapestry, testament (figurative), pivotal, robust (figurative),
leverage (verb), foster, facilitate, streamline, utilize (use "use"),
comprehensive (unless literal), moreover, furthermore, additionally (as
sentence opener), in conclusion, notably, importantly, crucial (unless
literally decisive), landscape (abstract), realm, embark, navigate
(figurative), underscoring, showcasing, highlighting (as rider), boasts,
nestled, in the heart of, groundbreaking (figurative), vibrant (figurative),
meticulous, intricacies, interplay, garner, bolster, endeavor (verb),
plethora, myriad, akin to, serves as, stands as, "It is important to note",
"It is worth noting", "In today's world/society", "Since the dawn of",
"plays a vital role", "sheds light on", "paves the way", "a double-edged
sword", "when it comes to".

## Modes of use

**Pasted text (default).** Return: the final rewrite, then a two-to-four
line note of what patterns were fixed. Do not show the full draft unless
asked.

**File mode.** When the user names a file, write only the final text into
the file. Change prose only; leave code blocks, data, YAML, citations,
quotations, and link targets untouched. Summarize changes briefly after.

**Generation mode.** When asked to write an assignment from a prompt, write
it human from the start: apply every lever during drafting, then run passes
3 and 4. Do not write AI-prose first and humanize after.

## What never to do

- Never invent a citation, source, statistic, date, name, or quotation.
- Never change what the thesis claims, only how it is expressed.
- Never insert deliberate typos, broken grammar, or ESL mistakes.
- Never pad length to hit a word count; trim or deepen instead.
- Never apply casual-voice rules (contractions, slang, asides) to formal
  academic text.
- Never touch anything inside quotation marks or a reference list.
