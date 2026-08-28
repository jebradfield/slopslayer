# slopslayer

Skill that removes AI writing patterns from prose and restores human voice.

It merges two existing skills: [stop-slop](https://github.com/hardikpandya/stop-slop) by
Hardik Pandya, which contributes the reference-file architecture and the scoring rubric,
and the [unslop](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop) skill
from Cursor's pstack plugin by Lauren Tan, which contributes the vocabulary and mechanics
rules and a positive voice section, which matters more than the rest of it. Skills that
only ban things produce sterile prose, which is its own tell.

Where the two sources contradict each other, slopslayer takes the version with a
diagnosis over the version with an absolute. stop-slop bans all adverbs; slopslayer says
an adverb propping up a weak verb means the verb is wrong. stop-slop bans passive voice
outright; slopslayer allows it when the actor is unknown or does not matter. The
[merge decisions](#merge-decisions) below list every place the two disagreed.

## Install

**Any agent, via the skills CLI**

```
npx skills add jebradfield/slopslayer -g
```

The `-g` flag installs to your user directory so the skill is available in every project.
Drop it to install into the current project only. The CLI detects which agents you have
and writes to the right path for each. See its
[supported agents](https://github.com/vercel-labs/skills#supported-agents) for the list.

**Claude Code, by hand**

```
git clone https://github.com/jebradfield/slopslayer.git ~/.claude/skills/slopslayer
```

Restart Claude Code. Run `/skills` and confirm `slopslayer` appears.

**claude.ai and Claude Desktop**

Download `slopslayer.zip` from the
[latest release](https://github.com/jebradfield/slopslayer/releases/latest). Then in
claude.ai open **Settings**, **Capabilities**, **Skills**, click **+**, choose
**Upload a skill**, and select the file. Turn on the toggle beside it.

Use the release zip, not the green **Code** button. Anthropic requires the zip's
root folder to be named exactly the same as the skill. GitHub's Download ZIP
names it `slopslayer-main`, which fails that check. The release zip is built
correctly, so nothing needs renaming.

**OpenCode**

```
git clone https://github.com/jebradfield/slopslayer.git ~/.config/opencode/skills/slopslayer
```

## Use

The skill triggers on any prose your agent drafts, edits, or reviews. Invoke it directly
with `/slopslayer` or by asking to deslop, unslop, or de-AI a draft.

It applies to prose only. It never rewrites code, structured data, direct quotations, or
text inside quotation marks or code fences.

## Structure

```
SKILL.md                  the skill, ~1,200 tokens
references/
  language.md             every word and phrase to avoid
  structures.md           sentence and paragraph patterns
  mechanics.md            punctuation and formatting
  examples.md             before and after transformations
README.md
CHANGELOG.md              version history
LICENSE
```

SKILL.md loads when the skill triggers. The reference files load only when a draft needs
the detail, so ordinary edits cost about 1,200 tokens rather than the full 6,000.

## Merge decisions

Six places where the two sources contradict each other, and which one won. Flip any of
them by editing the named file.

| Conflict | stop-slop | unslop | Default | Where |
|---|---|---|---|---|
| Adverbs | ban all `-ly` words | cut them, or fix the weak verb | **unslop** | `references/language.md` |
| Passive voice | ban outright | allow when the actor is unknown | **unslop** | `references/structures.md` |
| Rule of three | ban three-item lists | use the natural number | **unslop** | `references/structures.md` |
| Em dashes | replace with commas or periods | same, and ban the substitutes | **unslop** | `references/mechanics.md` |
| Bold-label lists | no rule | ban only the restating kind | **unslop** | `references/mechanics.md` |
| Voice | cut quotables | have opinions, let some mess in | **both** | `SKILL.md` |

The pattern is a diagnosis beating an absolute. A blanket no-adverb rule kills
"quarterly," "monthly," and "materially"; a blanket passive ban breaks technical and
regulatory writing where the actor is deliberately unnamed.

Two rules come from neither source: concreteness, added as a sixth scoring dimension, and
"domain terminology is not jargon," borrowed from
[Stephen Turner's deslop](https://github.com/stephenturner/skill-deslop), without which
the vocabulary rules strip precise domain terms.

Two defects in stop-slop's own examples are corrected here. Its example 4 used an em dash
in the "after" text, banned by its own rhythm table; its example 5 used a "not X, Y"
contrast, banned by its own binary-contrast table.

## Known gaps

Four things this skill does not do, listed so nobody is surprised:

- **No false-positive guard.** It has no list of what *not* to flag. Ordinary polish, a
  single "however," and curly quotes auto-inserted by Word will all read as evidence.
  [blader/humanizer](https://github.com/blader/humanizer) has the best version of this.
- **No preservation list.** Nothing instructs it to protect figures, honest hedges, or a
  deliberate rhythm.
- **No evidence boundary.** Nothing stops a rewrite from upgrading a hedge into a claim.
  That is a correctness problem in financial or technical writing, not a style one.
- **No detect mode.** It rewrites by default and cannot audit a draft without touching it.

## Maintenance

The AI vocabulary list in `references/language.md` is the most perishable content here.
Model vocabulary shifts every few releases: "delve" peaked in 2023 and had largely
disappeared by 2025. Re-measure against current model output roughly twice a year. The
habit is the target; the words are only this year's evidence of it.

## License

MIT. See [LICENSE](LICENSE).

This work derives from two MIT-licensed projects, and [LICENSE](LICENSE) carries both
copyright notices as the MIT License requires:

- [stop-slop](https://github.com/hardikpandya/stop-slop), copyright (c) 2025 Hardik Pandya
- [pstack](https://github.com/cursor/plugins) and its unslop skill, copyright (c) 2026
  Lauren Tan
