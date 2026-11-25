# The Riemann Hypothesis, read from its Lean proof

A reader's account of Levent Alpöge's formal proof, assembled from the statements read on [Riemann Statement a Day](https://riemannstatementaday.github.io/). Drafted by Claude (AI) and edited by the site's maintainers. It is not Alpöge's exposition and has not been refereed; where it and the Lean source disagree, the Lean source wins.

Last updated 2026-11-24. Live version: https://riemannstatementaday.github.io/#paper


## §1. Introduction

*Draft.*

In 2026 Levent Alpöge announced a formal proof of the Riemann Hypothesis in Lean, built on Mathlib. Its main theorem has the type of Mathlib's `RiemannHypothesis`, and the Lean kernel has checked every step. What a kernel check does not give is an account a mathematician can read. This paper is an attempt at one.

It is written from the outside in. Each section is assembled from statements of the reading blueprint ([chrisflav/riemann-blueprint](https://github.com/chrisflav/riemann-blueprint)) that have been read against the Lean source on this page, and it follows the order in which the formal proof uses them. A statement enters the paper only after someone has read it; each section lists the statements it draws on, and each of those links to its readings, including the concerns and the places readers got stuck.

The proof has the following overall shape, which the sections below fill in.

1. The Riemann Hypothesis follows from the non-vanishing of all Dirichlet $L$-functions on the half-plane $\mathrm{Re}\,s > 1/2$, by the functional equation (§2).
2. That non-vanishing follows from the existence of Galois representations attached to polarized automorphic representations of unitary type, together with a weak system of local parameters (§3).
3. Those Galois representations bound Tate–Shafarevich groups along a $2$-power cyclotomic tower. With theta lifts and the Siegel–Weil formula for families of definite unitary groups, the bound controls a weighted prime sum over short windows with square-root error, and Landau's theorem turns this into a zero-free half-plane (later sections, not yet written).

**Conventions.** $\chi$ is a Dirichlet character modulo $N \ge 1$, $\chi^*$ the primitive character inducing it, $L(\chi, s)$ its $L$-function, and $\zeta(s) = L(1, s)$ with $1$ the character modulo $1$. Lean names appear in `code` only to say where to look; the mathematics is meant to stand without them.

**Status.** This is a reader's account drafted by Claude (an AI) from the readings on this page and edited by the page's owner. It is not Alpöge's exposition, it has not been refereed, and sections marked *Draft* rest in part on readings no person has checked yet.


## §2. The statement, and its reduction to a half-plane

*Checked against the Lean.*

## What is proved

> **Theorem 2.1 (Riemann Hypothesis).** If $\zeta(s) = 0$, $s \ne 1$, and $s$ is not one of the trivial zeros $-2, -4, -6, \dots$, then $\mathrm{Re}\,s = 1/2$.

This is exactly Mathlib's definition [The Riemann Hypothesis](https://riemannstatementaday.github.io/#def-riemann-hypothesis), and the formal proof's main theorem has that type. Everything below proves it from a single statement about all Dirichlet $L$-functions.

> **Definition 2.2.** *Dirichlet $L$-functions do not vanish right of the critical line* if for every $N \ge 1$, every character $\chi$ modulo $N$, primitive or not, and every $s$ with $\mathrm{Re}\,s > 1/2$, we have $L(\chi, s) \ne 0$, except at the pole $\chi = 1$, $s = 1$.

See [Non-vanishing right of the critical line](https://riemannstatementaday.github.io/#def-nonvanishing-half-plane). The rest of the proof, from §3 on, is devoted to:

> **Theorem 2.3 (GRH, half-plane form).** Dirichlet $L$-functions do not vanish right of the critical line.

In the formal proof this theorem is closed: it is derived from statements that are themselves proved, and no hypothesis is left open at the top [GRH, half-plane form](https://riemannstatementaday.github.io/#thm-half-plane).

## From the half-plane to the critical line

Two classical facts do the rest.

*Primitive characters suffice.* If $\chi$ modulo $N$ is induced by $\chi^*$, then
$$L(\chi, s) = L(\chi^*, s) \prod_{p \mid N} \bigl(1 - \chi^*(p)\,p^{-s}\bigr),$$
and for $\mathrm{Re}\,s > 0$ each factor is nonzero, since $|\chi^*(p)\,p^{-s}| < 1$. So zeros of $L(\chi, s)$ with $\mathrm{Re}\,s > 0$ are zeros of $L(\chi^*, s)$ [Primitive characters suffice](https://riemannstatementaday.github.io/#thm-primitive-suffice).

*Reflection.* For primitive $\chi$ the completed $L$-function $\Lambda(\chi, s)$, which is $L(\chi, s)$ times a gamma factor $\Gamma_{\mathbb{R}}(s)$ or $\Gamma_{\mathbb{R}}(s+1)$ according to parity, satisfies a functional equation relating $\Lambda(\chi, s)$ to $\Lambda(\bar\chi, 1 - s)$, and the gamma factor does not vanish for $\mathrm{Re}\,s > 0$.

> **Corollary 2.4 (GRH for primitive characters).** If $\chi$ is primitive, every zero of $L(\chi, s)$ with $0 < \mathrm{Re}\,s < 1$ has $\mathrm{Re}\,s = 1/2$.

*Proof.* Let $L(\chi, s) = 0$ with $0 < \mathrm{Re}\,s < 1$. If $\mathrm{Re}\,s > 1/2$, Theorem 2.3 is contradicted. If $\mathrm{Re}\,s < 1/2$, the gamma factor is nonzero, so $\Lambda(\chi, s) = 0$; by the functional equation $\Lambda(\bar\chi, 1-s) = 0$, so $L(\bar\chi, 1 - s) = 0$ with $\mathrm{Re}(1-s) > 1/2$, and $\bar\chi$ is primitive, again contradicting Theorem 2.3. ∎ [GRH for primitive characters](https://riemannstatementaday.github.io/#thm-critical-line-primitive)

Combining the two facts gives the critical-strip form for every character, primitive or not [GRH, critical-strip form](https://riemannstatementaday.github.io/#thm-critical-line).

## Back to ζ

Taking $\chi = 1$ modulo $1$ in Theorem 2.3 gives $\zeta(s) \ne 0$ for $\mathrm{Re}\,s > 1/2$, $s \ne 1$ [Zeta does not vanish right of the line](https://riemannstatementaday.github.io/#lem-zeta-nonvanishing). For $\mathrm{Re}\,s < 1/2$ use the functional equation of $\zeta$ in the form
$$\zeta(s) = 2\,(2\pi)^{-(1-s)}\,\Gamma(1-s)\,\cos\!\bigl(\pi(1-s)/2\bigr)\,\zeta(1-s).$$
If $\zeta(s) = 0$ and $s$ is not a trivial zero, then $\Gamma(1-s)$ and the power of $2\pi$ are nonzero; the cosine vanishes only at $s = 0, -2, -4, \dots$, and $s = 0$ is not a zero because $\zeta(0) = -1/2$. So $\zeta(1-s) = 0$ with $\mathrm{Re}(1-s) > 1/2$, which is impossible. This proves Theorem 2.1 [The Riemann Hypothesis](https://riemannstatementaday.github.io/#thm-riemann-hypothesis).

This step of the formal proof uses only Mathlib: the argument is the textbook one, and all the depth lies in Theorem 2.3.

Drawn from: [def-riemann-hypothesis](https://riemannstatementaday.github.io/#def-riemann-hypothesis), [def-nonvanishing-half-plane](https://riemannstatementaday.github.io/#def-nonvanishing-half-plane), [def-zeros-on-line](https://riemannstatementaday.github.io/#def-zeros-on-line), [lem-zeta-nonvanishing](https://riemannstatementaday.github.io/#lem-zeta-nonvanishing), [thm-primitive-suffice](https://riemannstatementaday.github.io/#thm-primitive-suffice), [thm-critical-line-primitive](https://riemannstatementaday.github.io/#thm-critical-line-primitive), [thm-critical-line](https://riemannstatementaday.github.io/#thm-critical-line), [thm-half-plane](https://riemannstatementaday.github.io/#thm-half-plane), [thm-riemann-hypothesis](https://riemannstatementaday.github.io/#thm-riemann-hypothesis)


## §3. The outline: from Galois representations to the half-plane

*Draft.*

Theorem 2.3 is proved by a chain of reductions. This section states the links; later sections prove them.

## Two inputs

*Galois representations.* Let $E$ be a CM field, $l$ a prime and $\iota : \bar{\mathbb{Q}}_l \cong \mathbb{C}$. A *polarized pair* $(\pi, \chi)$ on $\mathrm{GL}_a(\mathbb{A}_E)$ is a regular algebraic cuspidal representation $\pi$ with a character $\chi$ such that $\pi^\vee \cong \pi^c \otimes (\chi \circ N)$, with the sign condition $\chi_v(-1) = (-1)^a$ at real places. *Polarized pairs have Galois representations* if each has a semisimple $r : G_E \to \mathrm{GL}_a(\bar{\mathbb{Q}}_l)$ with the expected Hodge–Tate weights and a weakened local–global compatibility [Galois representations of polarized representations](https://riemannstatementaday.github.io/#def-galois-reps-polarized). This is the theorem of Harris–Taylor, Shin, Chenevier–Harris, Barnet-Lamb–Gee–Geraghty–Taylor and Caraiani, in a weakened form.

*Local parameters.* For each $p$-adic field $F$, a *system of local parameters* assigns a Weil–Deligne representation to every irreducible smooth representation of $\mathrm{GL}_n(F)$. It is the local Artin map on characters, respects the Langlands classification and twists by $|\det|^s$, is fully compatible on *good* representations (characters and twists of depth-zero cuspidals), and on a depth-zero cuspidal built from a regular character $\theta$ of $\mathbb{F}_{g^n}^\times$ has the expected tame parameter [Local parameters](https://riemannstatementaday.github.io/#def-local-parameters). Such a system exists, by a direct construction [Local parameters exist](https://riemannstatementaday.github.io/#thm-local-parameters-exist).

This is much weaker than the local Langlands correspondence: other cuspidals get an arbitrary parameter of the right dimension [This is not the local Langlands correspondence](https://riemannstatementaday.github.io/#rem-local-parameters-weak). Since the Lean kernel accepted the whole proof with this weak notion, the formal proof never needs more. Whether every informal proof in the blueprint respects the same limit is still an open reading task.

## The chain

> **Theorem 3.1 (GRH from Galois representations).** If polarized pairs have Galois representations, Dirichlet $L$-functions do not vanish right of the critical line.

In the formal proof the hypothesis of Theorem 3.1 is itself proved, which is how Theorem 2.3 is closed [GRH from Galois representations](https://riemannstatementaday.github.io/#thm-grh-from-galois). The proof of Theorem 3.1 passes through three statements.

1. *A Tate–Shafarevich bound.* The Galois representations bound the total length of Tate–Shafarevich groups along a $2$-power cyclotomic tower, with exponent $401$ [The Tate–Shafarevich bound](https://riemannstatementaday.github.io/#def-sha-bound). Roughly: for primes $q \equiv 3 \bmod 8$ and $d \equiv 7 \bmod 16$ with $q \mid d + 1$, with $\log q$ and $\log d$ of size about $Y^{\varepsilon/5}$ and $Y^{\varepsilon/5}\log^2 Y$, and every odd $p \le Y^{\varepsilon/5}$ dividing $d + 1$, the sum of these lengths over levels $1 \le e < \lfloor x^{401} \rfloor$ is at most $e^{x^\varepsilon/2}$, for $\varepsilon < 1/52$ and $x \in [Y, Y^2]$.
2. *GRH from the bound* [GRH from the Tate–Shafarevich bound](https://riemannstatementaday.github.io/#thm-grh-from-sha-bound). Galois representations, local parameters and the Tate–Shafarevich bound together give Theorem 2.3. The published results this step also needs are derived inside the proof, not assumed.
3. *Families of definite unitary groups* [GRH from families of unitary groups](https://riemannstatementaday.github.io/#thm-grh-from-theta-integrals), [Zero-freeness from families](https://riemannstatementaday.github.io/#thm-zero-free-from-families). With theta lifts, periods and the Siegel–Weil formula for suitable families, the bound controls a weighted sum of the von Mangoldt function over windows $[Y, Y^{3/2}]$ with square-root error, giving zero-freeness for every primitive character, and then for all characters by §2.

**A gap in the account.** The formal version of step 3 also takes, as hypotheses, three results proved elsewhere in the argument: agreement of theta integrals, a local matching statement, and a covolume bound. The blueprint's statement of that step does not mention them. A reader of this section should know the chain runs through those chapters too; see the concern logged on [GRH from families of unitary groups](https://riemannstatementaday.github.io/#thm-grh-from-theta-integrals).

**Not yet read.** The exact local–global conditions in the Galois-representation hypothesis were not checked in the first reading (see the wall logged on [Galois representations of polarized representations](https://riemannstatementaday.github.io/#def-galois-reps-polarized)), so this section is a draft.

Drawn from: [thm-grh-from-galois](https://riemannstatementaday.github.io/#thm-grh-from-galois), [def-galois-reps-polarized](https://riemannstatementaday.github.io/#def-galois-reps-polarized), [def-local-parameters](https://riemannstatementaday.github.io/#def-local-parameters), [rem-local-parameters-weak](https://riemannstatementaday.github.io/#rem-local-parameters-weak), [thm-local-parameters-exist](https://riemannstatementaday.github.io/#thm-local-parameters-exist), [def-sha-bound](https://riemannstatementaday.github.io/#def-sha-bound), [thm-grh-from-sha-bound](https://riemannstatementaday.github.io/#thm-grh-from-sha-bound), [thm-grh-from-theta-integrals](https://riemannstatementaday.github.io/#thm-grh-from-theta-integrals), [thm-zero-free-from-families](https://riemannstatementaday.github.io/#thm-zero-free-from-families)


## §4. Sections still to be written

*Outline only.*

The remaining chapters of the blueprint will become sections here as their statements are read, in this order:

1. From prime sums to the zero-free half-plane: Landau's theorem and the short-window estimate.
2. Families of definite unitary groups: the family data and why a family exists.
3. Theta lifts, periods and the Siegel–Weil formula.
4. Heights and the covolume bound.
5. The Tate–Shafarevich bound, from the Galois representations.
6. Galois representations, in the weakened form the proof uses.
7. The published results the proof relies on, each with the form in which it is used.

To help, pick any statement from those chapters on the main page and [send a reading](https://riemannstatementaday.github.io/#send).
