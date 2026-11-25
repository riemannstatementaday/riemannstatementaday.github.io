# How to read a statement

A reading compares one statement of the blueprint with the Lean declarations it links to, and says whether they match. It takes from twenty minutes to an afternoon.

1. **Pick one statement.** Today's statement is on the [front page](https://riemannstatementaday.github.io/); every statement is in the [index](https://riemannstatementaday.github.io/statements.md). One statement per reading.
2. **Open both sides.** The blueprint's wording (the "Statement in the blueprint" link) and the Lean declarations listed under it, in the [community mirror](https://github.com/leanprover-community/riemann-hypothesis). Note the commit you read.
3. **Compare.** Do the hypotheses, the conclusion and the quantities match? Does the Lean assume anything the prose doesn't mention? Is an informal "≍" a precise inequality in the code?
4. **Say what you found.**
   - *Checks out*: the two say the same thing.
   - *Mismatch or gap*: say exactly where they part.
   - *Honest wall*: say where you got stuck, so the next reader starts there.
   - *Exposition*: a plain-language account of the statement, for the paper.
5. **Name the declarations you read**, and say what you didn't check.
6. **If an AI helped, name the model and say what it did**, and what you checked yourself. At the least, open the Lean file and confirm the declarations it named exist and say what it claims.
7. **Send it** from the [Send a reading page](https://riemannstatementaday.github.io/#send), or open a [reading issue](https://github.com/riemannstatementaday/riemannstatementaday.github.io/issues/new?template=reading.yml) directly. It becomes a public GitHub issue; we re-read the statement and reply there with our verdict (Verified, Partial, Refuted or Unverified), then add it to the [reading log](https://riemannstatementaday.github.io/readings.md).

Good readings are short, specific and honest about what they don't cover. "I got stuck at `PropsB`" helps more than "looks fine".

## What the verdicts mean

- **Checked**: one reader found the statement and its proof sketch match the Lean.
- **Confirmed**: two different readers checked it, at least one without AI doing the reading.
- **Concern**: the latest reading found a mismatch or a gap.
- **Wall**: the latest reader got stuck, and says where.
- **Unreviewed by humans**: every reading so far was done by an AI.

For an example, see any reading in the [log](https://riemannstatementaday.github.io/readings.md); the first eighteen were done by Claude (AI) and say exactly which declarations were read.
