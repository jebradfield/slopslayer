# Merge notes

Base: **stop-slop** by Hardik Pandya (MIT), SKILL.md plus `references/phrases.md`,
`references/structures.md`, `references/examples.md`.

Added: everything **unslop** (cursor/plugins, pstack) has that stop-slop lacks.

## Coverage

Every rule from both sources is present. Nothing was dropped and nothing was invented.

**From stop-slop, carried over intact:** 8 core rules (now 12 after additions), the
12-item quick-check list (now 34 across four groups), the 5-dimension scoring rubric (now
6), the reference-file architecture, and all content from phrases.md and structures.md
including the business-jargon table, the false-agency table, and the narrator-from-a-
distance table. Its 5 before-and-after examples are retained, 2 with corrections noted
below.

**From unslop, newly added (18 items stop-slop had no equivalent for):**

| unslop # | Rule | Where it landed |
|---|---|---|
| 1 | Significance inflation | phrases.md |
| 2 | Notability name-dropping | phrases.md |
| 3 | Superficial -ing phrases | structures.md |
| 4 | Promotional language | phrases.md |
| 5 | Vague attributions | phrases.md |
| 6 | Formulaic challenges | structures.md |
| 7 | AI vocabulary | language.md |
| 8 | Copula avoidance | language.md |
| 11 | Synonym cycling | language.md |
| 12 | False ranges | structures.md |
| 14 | Colon overuse | mechanics.md |
| 15 | Boldface overuse | mechanics.md |
| 16 | Inline-header lists | mechanics.md |
| 17 | Title case headings | mechanics.md |
| 18 | Decorative emojis | mechanics.md |
| 19 | Curly quotes | mechanics.md |
| 20 | Chatbot phrases | phrases.md |
| 21 | Cutoff disclaimers | phrases.md |
| 22 | Sycophantic tone | phrases.md |
| 24 | Excessive hedging | phrases.md |
| 25 | Generic conclusions | phrases.md |
| 26 | Abstract metaphor nouns | language.md |
| 27 | Say the concrete thing | SKILL.md core rule 5 |
| 28 | Shorten or split dense sentences | SKILL.md rule 11, structures.md |
| 31 | Prefer the plain word | SKILL.md rule 10, language.md |
| n/a | **Adding soul** section | SKILL.md, "Adding voice" |
| n/a | **Self-audit** step | SKILL.md, process step 4 |

The two unnumbered additions matter most. Stop-slop has no positive-voice section at all,
which is why it produces sterile output when its rules are applied as written. The self-audit step is
what makes the skill run a second pass instead of one lazy scan.

Two additions beyond the two sources, both flagged so they can be removed:

- **Concreteness** added as a sixth scoring dimension, threshold raised from 35/50 to
  42/60 to keep the same 70% bar.
- **"Domain terminology is not jargon"** in language.md, borrowed from Stephen Turner's
  deslop. Without it the vocabulary rules will strip precise finance terms.

## Conflicts and how I resolved them

Six places where the two sources disagree. Each default is marked. Flip any of them by
editing the named file.

### 1. Adverbs

- stop-slop: "Kill all adverbs. No -ly words." Absolute.
- unslop #30: "Cut adverbs, or use a stronger verb. An adverb propping up a weak verb
  means the verb is wrong."
- **Default: unslop.** The diagnosis is more useful than the ban, and an absolute
  no--ly rule kills "quarterly," "monthly," and "materially," which financial and
  technical prose require.
- Location: `references/language.md`, Adverbs section.

### 2. Passive voice

- stop-slop: "Every sentence needs a subject doing something. No passive constructions."
- unslop #29: "Passive is fine only when the actor is unknown or genuinely doesn't
  matter."
- **Default: unslop**, plus a methods-section carve-out. A blanket ban breaks technical
  and regulatory writing where the actor is irrelevant or deliberately unnamed.
- Location: `references/structures.md`, Passive voice section.

### 3. Rule of three

- stop-slop: "Three-item lists. Use two items or one."
- unslop #10: "Forcing ideas into groups of three. Use the natural number."
- **Default: unslop.** Some things come in threes. Banning the count rather than the
  forcing produces contorted lists.
- Location: `references/structures.md`, Rhythm patterns.

### 4. Em dashes

- stop-slop: "Remove. Use commas or periods."
- unslop #13: same, and also bans parentheses, en dashes, and hyphens-as-dashes as
  substitutes.
- **Default: unslop**, the stricter version. Trading an em dash for a parenthetical is
  the most common failed fix.
- Location: `references/mechanics.md`, Em dashes.

### 5. Bold-label lists

- stop-slop: no rule.
- unslop #16: bans the restating kind, explicitly permits a bold lead-in that ends in a
  period and is followed by new detail.
- **Default: unslop's nuanced version**, kept whole. The exception is the point.
- Location: `references/mechanics.md`, Inline-header lists.

### 6. Voice

- stop-slop rule 8: "Cut quotables. If it sounds like a pull-quote, rewrite it."
- unslop: "Have opinions. Let some mess in."
- **Both kept**, because they are compatible. Cut the manufactured aphorism; keep the
  real opinion. If they collide in practice, "cut quotables" is the one to relax.
- Location: SKILL.md, rule 9 and the Adding voice section.

## Defects corrected in the source

Stop-slop's `examples.md` violates its own rules twice. Both fixed in the merged file.

- **Example 4.** Its "after" text was `"Speed, quality, cost—pick two."` That is an em
  dash, banned by its own rhythm table. Rewritten as `"You can pick two of speed,
  quality, and cost."`
- **Example 5.** Its "after" text was `"The best teams optimize for learning, not
  productivity."` That is the "not X, Y" contrast banned by its own binary-contrast
  table. Rewritten as `"The best teams optimize for learning."`

Three examples added (6, 7, 8) covering the merged-in rules, drawn from SaaS and finance
prose so the skill has in-domain calibration.

## What neither source has

Listed as known gaps in the merged skill rather than as a criticism of either source.

- **A false-positive guard.** Neither file says what *not* to flag. Both will treat
  ordinary polish, a single "however," or auto-curled quotes from Word as evidence.
  blader/humanizer has the best version of this.
- **A preservation list.** Nothing tells the skill to protect figures, honest hedges,
  or a deliberate rhythm.
- **An evidence boundary.** Nothing prevents a rewrite from upgrading a hedge into a
  claim, which is a correctness problem in financial writing rather than a style one.
- **A detect mode.** Both rewrite by default. Neither can audit a draft and name patterns
  without touching it.

Adding those four is the obvious next version.

## Install

Claude Code, global:

```
mkdir -p ~/.claude/skills/deslop
cp -r SKILL.md references ~/.claude/skills/deslop/
```

Claude Desktop or claude.ai: zip this folder and upload it under Settings, Capabilities,
Skills, Upload skill.

If you rename the folder, rename the `name:` field in SKILL.md frontmatter to match.
The two must be identical.

---

Version history lives in [CHANGELOG.md](CHANGELOG.md). This file records the merge
rationale: what came from where, which conflicts existed, and how each was resolved.
