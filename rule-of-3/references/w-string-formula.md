# Tripled-W formula

The widest Latin glyph at most font weights is the capital **W**. Stress-testing copy with W-strings surfaces wrap, overflow and alignment issues that English-only copy hides.

## Algorithm

For each text layer in the component instance:

1. `count` = length of the original string **including spaces**.
2. `w_count` = `(3 × count) + 2`. The `+2` is insurance against the few languages where average word length exceeds a 3× Latin-W estimate.
3. The replacement string is `w_count` capital W characters, with spaces re-inserted at the same proportional positions as the original. (Keeping spaces preserves the wrap behaviour the component would see with real multi-word copy.)

### Worked example

Original button label: `View All Transactions`

| Step | Value |
|------|-------|
| 1. Count characters incl. spaces | 21 |
| 2. `(3 × 21) + 2` | 65 |
| 3. Re-insert spaces proportionally — original spaces at index 4 and 8 (out of 21), i.e. at 19% and 38% of the way through. In a 65-char string that's roughly index 12 and 25. | `WWWWWWWWWWWW WWWWWWWWWWWWW WWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWWW` |

For shorter labels (under 6 characters), keep at least one space if the original had one — wrapping behaviour at very short lengths matters less than seeing the worst-case width.

## Edge cases

- **Empty / placeholder text** — skip the layer. Record it as "no copy to triple".
- **Numerals or symbols** — replace the whole string with W's; the goal is width, not semantic preservation.
- **Multi-line strings (already wrapped with `\n`)** — count and triple per line, keeping the line breaks. This tests how the component handles longer copy *and* manual breaks.
- **Hidden text layers** — skip. If a boolean prop reveals them later, the relevant variant in the curation step will cover it.

## Why W and why +2

- Capital W is the widest glyph in standard Latin typography at most weights.
- 3× is a pragmatic upper bound: most translations from English grow 20–80%; tripling buys headroom for languages with longer compounds (German, Finnish) and for future copy revisions.
- +2 is a small insurance buffer that costs almost nothing in design space but catches the cases where a designer's container was sized for "just enough".
