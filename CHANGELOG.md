# Changelog

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions follow
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Versions 1.0.0 and 1.1.0 were development iterations and were never published. 1.2.0 is
the first public release.

## [1.3.0] - 2026-08-28

Packaging and metadata only. No rule, reference file, or example changed.

### Changed

- Rewrote `LICENSE` as the verbatim MIT template with the three copyright lines stacked
  at the top. Three explanatory paragraphs sat between the copyright line and the
  permission grant, which stopped GitHub's detector from matching the template: the API
  reported `NOASSERTION` and the repo read as unlicensed to every license scanner. The
  derivation and both source links moved into the README.
- Shortened the frontmatter `description` from 307 characters to 180 and made it
  agent-neutral. It told the reader to apply the skill to prose "Claude drafts", which
  names the wrong vendor on the Codex, Cursor and OpenCode installs the README
  advertises. Anthropic caps the field at 200.
- Folded the useful half of `MERGE-NOTES.md` into a Merge decisions section in the
  README: the six source conflicts, which default won, and the two corrected defects in
  stop-slop's examples.

### Added

- A release asset, `slopslayer.zip`, built so its root folder is named `slopslayer` as
  Anthropic's packaging rules require. GitHub's own Download ZIP names the root
  `slopslayer-main`, which fails that check.

### Removed

- `MERGE-NOTES.md`. It shipped inside the skill telling the reader to install a skill
  named `deslop`, the pre-1.1.0 name, and to copy only `SKILL.md` and `references/`,
  dropping the `LICENSE` the MIT License requires. It also routed 11 rules to
  `references/phrases.md`, deleted in 1.2.0, and its rule counts and pointers had drifted
  from `SKILL.md`.
- `.github/settings.yml`. That path is the config file for the Probot Settings GitHub
  App, so installing that app would have made a documentation file authoritative over
  live repo settings, including `repository.name`. Four of its values had already drifted
  from the actual repo. GitHub stores the description and topics already.

The repo now tracks only what an agent needs plus the three files a reader needs:
`SKILL.md`, `references/`, `README.md`, `CHANGELOG.md`, `LICENSE`. Everything at the root
is either the skill or documentation of it, so the one-line clone install stays correct.

### Fixed

- The README claimed the skills CLI supports "about thirty" agents; it supports 73.
  Replaced with a link to the CLI's own list.

## [1.2.0] - 2026-08-27

### Changed

- Merged `references/phrases.md` into `references/language.md`, taking five reference
  files down to four. The two covered the same kind of rule, words and phrases to avoid,
  and always loaded together, so splitting them added a routing decision and saved
  nothing. The remaining split is by kind of rule and by when each is needed:
  `language.md` for word and phrase choice, `structures.md` for sentence and paragraph
  patterns, `mechanics.md` only when the output has markdown structure, `examples.md`
  only when calibrating.

### Added

- `LICENSE` carrying the copyright notices from both upstream projects, as the MIT
  License requires.
- `README.md`, `CHANGELOG.md`, `.gitignore`.

### Fixed

- Replaced a fabricated statistic in `references/examples.md`. Example 8 had attributed
  invented adoption figures to a named research firm. It now demonstrates the same
  transformation using evidence a writer would hold, which is the better lesson
  anyway: the fix for vague attribution is writing from what you know rather than finding
  a more impressive source.

## [1.1.0] - 2026-08

### Changed

- Renamed from `deslop` to `slopslayer`.
- Removed the 48-line quick-checks block from `SKILL.md`. It duplicated all four
  reference files. Replaced by an 11-rule list and a 3-question gate. `SKILL.md` went
  from 131 lines and roughly 1,900 tokens to 82 lines and roughly 1,230, a 35% cut.
- Right-sized the gate. Three pass-or-fail questions run on every pass; the full 42/60
  six-dimension rubric is now reserved for deliberate editing passes.
- Rewrote the frontmatter description to state always-on application explicitly and to
  include the new skill name as a trigger term.

### Added

- A Scope section. Prose only. The skill never rewrites code, structured data, direct
  quotations, or text inside quotation marks or code fences.
- A compile date and re-measurement cadence on the AI vocabulary list in
  `references/language.md`, since model vocabulary decays faster than any other content
  in the skill.

### Removed

- The non-standard `metadata:` block from `SKILL.md` frontmatter. Version history lives
  in this file and in git tags instead.

## [1.0.0] - 2026-08

### Added

- Initial merge of [stop-slop](https://github.com/hardikpandya/stop-slop) by Hardik
  Pandya and the [unslop](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop)
  skill from Cursor's pstack plugin by Lauren Tan.
- Everything unslop covers that stop-slop lacked: significance inflation, notability
  name-dropping, superficial -ing phrases, promotional language, vague attributions,
  formulaic challenges, AI vocabulary, copula avoidance, synonym cycling, false ranges,
  colon overuse, boldface overuse, inline-header lists, title case headings, decorative
  emoji, curly quotes, chatbot phrases, cutoff disclaimers, sycophantic tone, excessive
  hedging, generic conclusions, abstract metaphor nouns, concreteness, sentence density,
  and plain-word preference.
- unslop's positive voice section and self-audit step, neither of which stop-slop has.
  Skills that only ban things produce sterile prose, which is its own tell.
- Three before-and-after examples drawn from SaaS and finance prose, for in-domain
  calibration.
- A "domain terminology is not jargon" rule borrowed from
  [Stephen Turner's deslop](https://github.com/stephenturner/skill-deslop), without which
  the vocabulary rules strip precise financial terms.

### Fixed

- Two defects carried in stop-slop's own examples, where the corrected text violated the
  rules it was demonstrating. Example 4's rewrite used an em dash, banned by its rhythm
  table. Example 5's rewrite used a "not X, Y" contrast, banned by its binary-contrast
  table.

See the README's Merge decisions section for the six source conflicts and how each was
resolved.
