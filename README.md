# slopslayer

An agent skill that removes AI writing patterns from prose and restores human voice.

It merges two existing skills: [stop-slop](https://github.com/hardikpandya/stop-slop) by
Hardik Pandya, which contributes the reference-file architecture and the scoring rubric,
and the [unslop](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop) skill
from Cursor's pstack plugin by Lauren Tan, which contributes the vocabulary and mechanics
rules and a positive voice section, which matters more than the rest of it. Skills that only ban things
produce sterile prose, which is its own tell.

Where the two sources contradict each other, slopslayer takes the version with a
diagnosis over the version with an absolute. stop-slop bans all adverbs; slopslayer says
an adverb propping up a weak verb means the verb is wrong. stop-slop bans passive voice
outright; slopslayer allows it when the actor is unknown or does not matter.
Blanket bans damage technical and financial writing. Every one of these decisions is
documented in [MERGE-NOTES.md](MERGE-NOTES.md).

## Install

**Any agent, via the skills CLI**

```
npx skills add jebradfield/slopslayer -g
```

The `-g` flag installs to your user directory so the skill is available in every project.
Drop it to install into the current project only. The CLI detects which agents you have
and writes to the right path for each; it supports Claude Code, Codex, Cursor, OpenCode,
and about thirty others.

**Claude Code, by hand**

```
git clone https://github.com/jebradfield/slopslayer.git ~/.claude/skills/slopslayer
```

Restart Claude Code. Run `/skills` and confirm `slopslayer` appears.

**Claude Desktop or claude.ai**

Download the repository as a ZIP from the green Code button. In claude.ai, open
**Settings**, **Capabilities**, **Skills**, click **+**, choose **Upload a skill**, and
select the ZIP.

**OpenCode**

```
git clone https://github.com/jebradfield/slopslayer.git ~/.config/opencode/skills/slopslayer
```

## Use

The skill triggers on any prose Claude drafts, edits, or reviews. Invoke it directly with
`/slopslayer` or by asking to deslop, de-AI, or remove AI patterns from a draft.

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
MERGE-NOTES.md            merge decisions and source conflicts
CHANGELOG.md              version history
.github/settings.yml      repository description and topics, versioned
```

SKILL.md loads when the skill triggers. The reference files load only when a draft needs
the detail, so ordinary edits cost about 1,200 tokens rather than the full 6,000.

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

MIT. See [LICENSE](LICENSE), which carries the required copyright notices from both
upstream projects.
