# Naive Nash

> What does the payoff space of a heads-up river poker spot look like around the Nash equilibrium,
> and how much does it cost to be away from it?

Independent, unsupervised study. Work in progress; nothing here is claimed to be new
(see [Status](#status)).

## Contents

1. [Status](#status)
2. [Key results](#key-results)
3. [Background](#background)
4. [The idea: bilinear payoffs and the exact local form](#the-idea)
5. [Case study 1: the clairvoyant game](#case-study-1-the-clairvoyant-game)
6. [Where the structure breaks](#where-the-structure-breaks)
7. [Next steps](#next-steps)
8. [Repository guide](#repository-guide)

## Status

- Scope: heads-up, zero-sum (constant-sum accounting), river only, known ranges, a few bet sizes,
  no card removal at first.
- Goal: a mathematical study of the payoff space and of how payoff and exploitability behave under
  deviations from equilibrium. It is not a solver, and it does not try to compete with CFR on speed.
- Novelty is **not** claimed. The ingredients (minimax, indifference, the Shapley-Snow structure,
  exploitability) are classical, and the literature search is not finished.

## Key results

_TODO: headline findings and one figure. So far (Part 1 and Part 2 below) only the clairvoyant game
is worked out._

## Background

_TODO: heads-up, river, bluff, bluff-catcher, nuts, air, Nash equilibrium. See
[docs/glossary.md](docs/glossary.md)._

## The idea

The payoff to player A is bilinear in the two players' mixed strategies,
$P(\sigma,\tau)=\sigma^\top M\tau$, so it is a weighted average of corner payoffs. Expanding around
a saddle point with full support gives an exact identity, with no truncation:

$$
P(\sigma^\star+\delta\sigma,\ \tau^\star+\delta\tau)=v+\delta\sigma^\top M\ \delta\tau .
$$

The matrix $D$ that represents this interaction term in tangent coordinates is the object of study:
its singular values, its kernel (non-uniqueness of the equilibrium) and its relation to the cost of
deviating. Unused strategies add first-order terms given by their regrets.

Full derivation: [docs/matrix_games.md](docs/matrix_games.md), Section 2.

## Case study 1: the clairvoyant game

The smallest interesting poker game: one player holds a bluff-catcher, the other holds the nuts or
air with equal probability. Solved by indifference, by the matrix formula and by calculus with a
boundary, then used as a hand-checkable laboratory for the local form: here $D=\tfrac{1+s}{2}$, a
wrong calling frequency costs first order in the size of the mistake with slopes $\tfrac s2$
(over-calling) and $\tfrac12$ (under-calling), and exploitability has a sharp minimum.

Write-up: [docs/clairvoyant_game.md](docs/clairvoyant_game.md). Code:
[notebooks/01_clairvoyant.ipynb](notebooks/01_clairvoyant.ipynb).

## Where the structure breaks

_TODO: when bilinearity holds, hidden assumptions (for example "always bet value"), raises, several
bet sizes, boundary equilibria, blockers._

## Next steps

_TODO. Planned order: the sequence form, then a continuous-range spot with hand strengths uniform on
[0,1] (closed form known), then a discretized N-hand spot where $D$ is a genuine matrix. A CFR
cross-check ([notebooks/02_cfr_baseline.ipynb](notebooks/02_cfr_baseline.ipynb)) is optional._

## Repository guide

| Path | Contents |
|---|---|
| `docs/matrix_games.md` | Matrix games, indifference, exploitability, the exact local form |
| `docs/clairvoyant_game.md` | The clairvoyant game and its sensitivity analysis |
| `docs/glossary.md` | Poker terms for readers without a poker background |
| `notebooks/` | Code: payoff matrices, verification, figures (one notebook per case study) |
| `figures/` | Images used in the documents |
