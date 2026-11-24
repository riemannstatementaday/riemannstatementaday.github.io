# Riemann Statement a Day

A community reading log for the [reading blueprint](https://github.com/chrisflav/riemann-blueprint) of Levent Alpöge's Lean proof of the Riemann Hypothesis, and a human-readable paper that grows as its statements are read.

**Site:** https://riemannstatementaday.github.io/

Each day the site picks one statement. A reader reads it against the Lean source and sends what they found: it checks out, a mismatch or a gap, the place they got stuck, or a plain-language account for the paper. Every reading is logged, misses included. A verdict here says whether the blueprint's account matches the Lean source; it says nothing new about whether the proof is correct, which the Lean kernel already checks.

## Sending a reading

Use the **Send a reading** page on the site, or open a [reading issue](../../issues/new?template=reading.yml) directly. We re-read the statement, reply on the issue with our verdict (Verified, Partial, Refuted or Unverified) and add the reading to the log.

## How the site is kept

- `index.html` is the whole site. The list of statements is built from the blueprint and embedded in it (titles, ids and Lean declaration names only).
- `data/readings.json` is the reading log.
- `data/paper.json` is the paper, one entry per section, in proof order.

Only the maintainers change `data/`, by commit. Readings done by AI say so and name the model; many of the first readings were done by Claude (Anthropic) and carry an "Unreviewed by humans" stamp until a person reads the same statement.

## Credits

The statements, their labels and their links to Lean come from [chrisflav/riemann-blueprint](https://github.com/chrisflav/riemann-blueprint). The formal proof is Alpöge's ([alpo.ge/remark.pdf](https://alpo.ge/remark.pdf); community mirror [leanprover-community/riemann-hypothesis](https://github.com/leanprover-community/riemann-hypothesis)). Neither repository carries a license, so this site links to their text and quotes only titles and declaration names. This site is run by volunteers and is not affiliated with Alpöge, Anthropic, or the Lean and Mathlib maintainers.
