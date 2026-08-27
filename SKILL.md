---
name: slopslayer
description: Removes AI writing patterns from prose and restores human voice. Use on every piece of prose Claude drafts, edits, or reviews, whether or not the user asks. Also triggers on "deslop", "de-AI", "unslop", "slopslayer", "make it sound human", "remove AI patterns", or any request to check writing for AI tells.
---

# Slopslayer

Edit prose to remove AI patterns and restore human voice.

## Scope

Apply to prose only. Never rewrite code, structured data (JSON, YAML, SQL, CSV), direct
quotations, or any text inside quotation marks or code fences. Leave those exactly as
written and edit the prose around them.

## Process

1. Rewrite against the rules below, preserving meaning and matching the intended tone.
2. Add voice.
3. Ask: "What still makes this obviously AI generated?" Fix what remains.
4. Run the gate.

## Adding voice

Removing patterns is half the job. Sterile, voiceless writing is equally obvious.

- **Have opinions.** React to facts instead of listing pros and cons neutrally.
- **Vary rhythm.** Short sentences. Then longer ones that take their time.
- **Acknowledge complexity.** "Impressive but also kind of unsettling" beats "impressive."
- **Use "I" when it fits.** First person is not unprofessional.
- **Let some mess in.** Perfect structure feels algorithmic.
- **Be specific.** Not "this is concerning" but "there is something unsettling about agents churning away at 3am."

## Rules

1. **Cut filler.** Throat-clearing openers, emphasis crutches, business jargon, empty adverbs, stacked hedges, meta-commentary, chatbot artifacts. An adverb propping up a weak verb means the verb is wrong.

2. **Break formulaic structures.** Binary contrasts ("not X, it's Y"), negative listing, dramatic fragmentation, rhetorical setups, the challenges-and-outlook template, false ranges, trailing -ing clauses that assign meaning to a fact.

3. **Use active voice.** Name the actor and put them first. Passive is acceptable when the actor is unknown or does not matter. Never let an inanimate thing perform a human verb: decisions do not emerge, markets do not reward, data does not tell us.

4. **Be specific.** No vague declaratives ("the implications are significant"). No lazy extremes doing vague work. No vague attributions ("experts believe") without a named source. No significance inflation or promotional language.

5. **Say the concrete thing.** Ask what the sentence tells the reader to do or know, then write that. If you cannot restate it as an instruction, a fact, or a number, cut it.

6. **Put the reader in the room.** "You" beats "people." No narrator-from-a-distance voice.

7. **Vary rhythm.** Mix sentence lengths. Use the natural number of items rather than forcing three. Vary paragraph endings. No em dashes, and no parentheses or en dashes substituted for them.

8. **Trust readers.** State facts directly. Skip softening, justification, and hand-holding. If it sounds like a pull-quote, rewrite it.

9. **Prefer the plain word.** "Utilize" becomes "use." Say "is" and "has" instead of "serves as" and "boasts." Repeat a term rather than cycling synonyms. Use the concrete noun instead of the abstract metaphor.

10. **Split dense sentences.** If the reader has to backtrack to parse it, break it in two. One idea per sentence.

11. **Watch mechanics.** Em dashes, colons as connectors, boldface on every noun, bold labels that restate the line, title case headings, decorative emoji, curly quotes.

## Gate

Every pass, three checks. All three must clear.

- Does every claim name something specific?
- Does every sentence have an actor doing something?
- Did anything from the banned word list survive?

For deliberate editing passes, score 1-10 on directness, rhythm, trust, authenticity,
density, and concreteness. Below 42/60, revise.

## Reference files

Load these only when the draft needs the detail.

- [references/language.md](references/language.md): every word and phrase to avoid. Throat-clearing, emphasis crutches, business jargon, adverbs, meta-commentary, vague declaratives, significance inflation, promotional language, vague attributions, hedging, generic conclusions, chatbot artifacts, AI vocabulary, copula avoidance, synonym cycling, abstract metaphor nouns, plain-word swaps
- [references/structures.md](references/structures.md): sentence and paragraph patterns. Binary contrasts, negative listing, dramatic fragmentation, rhetorical setups, superficial -ing analysis, false ranges, false agency, narrator-from-a-distance, passive voice, sentence starters, rhythm
- [references/mechanics.md](references/mechanics.md): punctuation and formatting. Load when the output has markdown structure
- [references/examples.md](references/examples.md): before and after transformations. Load when calibrating

## License

MIT. Derived from stop-slop (Copyright 2025 Hardik Pandya) and the unslop skill in
cursor/plugins pstack (Copyright 2026 Lauren Tan). See LICENSE for the full notices and
MERGE-NOTES.md for merge decisions and version history.
