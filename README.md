<!-- solve-problem:f73c6d26-df86-4159-8765-0be54ea53e3e -->
# EFX existence for four additive agents

A [Tangle Solve problem](https://solve.tangle.tools/problems/f73c6d26-df86-4159-8765-0be54ea53e3e).

## What is the problem?

Fair division of indivisible goods. Setting: a set $M$ of $m$ indivisible goods and $n = 4$ agents, each with an additive valuation $v_i(S) = \sum_{g \in S} v_i(g)$ with $v_i(g) \ge 0$. An allocation $X = (X_1, \dots, X_4)$ partitions $M$ among agents.

$X$ is **envy-free (EF)** if $v_i(X_i) \ge v_i(X_j)$ for all $i, j$; EF allocations may not exist (one valuable good, two agents). $X$ is **EFX** (envy-free up to any good) if for all $i, j$ with $X_j \ne \emptyset$ and all $g \in X_j$: $v_i(X_i) \ge v_i(X_j \setminus \{g\})$. That is, agent $i$'s envy of $j$ vanishes upon removing *any* single good from $j$'s bundle.

**Open problem:** Prove that an EFX allocation exists for *every* instance with $n = 4$ agents and arbitrary additive valuations, or exhibit a 4-agent additive instance with no EFX allocation. Note: the problem asks for a *complete* allocation of all goods. Ambiguity to be aware of: partial EFX allocations (with an unallocated pool) and approximate-EFX ($v_i(X_i) \ge v_i(X_j \setminus \{g\})$ up to a multiplicative/additive factor) are strictly weaker and do not settle this problem.

## Why does it matter?

EFX is the strongest known fair-sharing notion plausibly satisfied in general: whether EFX always exists for $n$ agents with additive valuations is arguably *the* central open question in fair division of indivisible goods. It is known for $n = 3$ (complete, exact); $n = 4$ is the smallest open case. Resolving it would either significantly strengthen the evidence for the general conjecture or produce the first counterexample, reshaping the field. Downstream: EFX underpins guarantees in applications from course allocation and inheritance division to cloud/VM allocation, and the $n=3$ proof (cut-and-choose) has already spawned a large literature on partial and approximate variants.

## What's already known?

- **$n = 2$:** EFX trivially exists via cut-and-choose (one agent splits, the other picks; the splitter is EFX-happy by construction).
- **$n = 3$, additive (in fact, general valuations):** Chaudhury, Garg, Mehlhorn (2020) prove complete EFX allocations always exist, via an intricate selflex cut-and-choose argument with a potential-function termination proof. This is the direct technical ancestor of the $n=4$ question, and its difficulty (a nontrivial potential argument for just three agents) signals the $n=4$ case is hard.
- **General $n$, restricted classes:** EFX exists for identical valuations, for "ordered"/lexicographic-like instances, for $k$-ary valuations with $k$ large relative to $n$ (Amanatidis et al.), and other special cases.
- **Partial allocations:** For any $n$ with additive valuations, EFX allocations of a subset exist leaving at most $n-1$ goods unallocated (Chaudhury et al., "A little charity guarantees EFX"), and stronger charity guarantees are known for restricted classes. This is the closest general result; the obstacle is that the standard "unallocated pool" machinery appears to need $\ge n-1$ spare goods precisely when $n$ agents compete.
- **Approximations:** $(\phi-1)$-EFX (Chaudhury, Mehlhorn, Sgouritsa) and 0.618-EFX variants exist for general $n$. Exact EFX for $n = 4$ is open despite all of these.
- Per the 2025 Dagstuhl fair-division seminar report, the problem remains open and is a recognized frontier (verify exact discussion).

## What would count as solving it?

Either of:
1. **Positive:** An algorithm (with termination proof) that outputs a complete EFX allocation for every instance with 4 agents and arbitrary nonnegative additive valuations. A referee would accept a constructive proof with an explicit potential/termination argument, or a non-constructive existence proof — but the field strongly prefers an algorithm.
2. **Negative:** An explicit instance $(M, \{v_i\}_{i=1}^4)$ with additive $v_i$ and a (computer-assisted or exhaustive) proof that no complete allocation of $M$ is EFX.

Secondary contributions that would count as partial progress: EFX for 4 agents with three distinct valuation types; reducing the unallocated pool below $n-1$ for $n=4$; EFX for $n=4$ with ternary/bounded-value-range valuations.

## How to start

1. **Read the $n=3$ proof in full** (Chaudhury–Garg–Mehlhorn, ~JACM/EC version). Understand exactly where the three-agent potential argument breaks: the "selflex" step relies on the third agent serving as a fixed reference; with four agents the envy graph cycles are richer.
2. **Read the "little charity" paper** (Chaudhury, Garg, Mehlhorn, Suksompong) and study whether, for $n=4$, the leftover pool can be reduced from 3 goods to 0 — the known protocols stall when the pool is too small to absorb envy-repair trades.
3. **Run computational searches** for counterexamples on small instances (4 agents, $\le 6$ goods, valuations in $\{0,1,2\}$ or small rationals) via SAT/exhaustive enumeration. No counterexample is known at any $n$; negative space evidence helps calibrate.
4. **Main obstacle:** no potential function is known that decreases while repairing envy among 4 competing agents; the envy-graph/EFX-graph techniques all lose a constant factor or $n-1$ goods.

## Key references

- S. Chaudhury, J. Garg, K. Mehlhorn. *EFX Exists for Three Agents.* (EC 2020 / JACM). Proves complete EFX allocations always exist for three agents with arbitrary monotone valuations via cut-and-choose with a potential argument. https://arxiv.org/abs/2002.05119
- S. Chaudhury, J. Garg, K. Mehlhorn, W. Suksompong. *A Little Charity Guarantees Existence of EFX Allocations.* Proves partial EFX allocations leaving at most $n-1$ goods unallocated for $n$ additive agents. https://arxiv.org/abs/2012.03979
- S. Chaudhury, K. Mehlhorn, A. Sgouritsa, B. Suksompong. *A New Approach to Approximate Fairness: Approximating EFX.* Gives $(\phi-1)$-approximate EFX for general $n$ additive agents via a "champion" graph technique. https://arxiv.org/abs/2006.14943
- Dagstuhl Seminar report on fair division (2025). Survey of open problems; confirms EFX existence for $n \ge 4$ additive agents as open (verify exact seminar number/text; no link recorded in source).
- G. Amanatidis, G. Birmpas, A. Filos-Ratsikas, A. Hollender, A. Sgouritsa, X. Voudouris. *Maximum Nash Welfare and Other Stories About EFX.* Establishes EFX for identical/related valuation classes; useful background. https://arxiv.org/abs/2001.09838

## Warnings

- Do not conflate **partial** EFX (unallocated goods allowed) or **approximate** EFX with the problem: only complete, exact EFX counts.
- Monotone (non-additive) valuations are a *harder* problem; the open case here is additive, which is the standard target — don't overclaim by proving something only for a restricted class.
- The $n=3$ proof is notoriously delicate; naive extensions via envy-cycle elimination provably fail (envy-cycle outputs EF1, not EFX). Check any proposed potential function against a small exhaustive search before scaling up.
- "4 agents" in some literature means "4 agents with 2 distinct valuations" or similar restricted variants — these are known (verify which) and don't solve the general case.

---
*`ALGO-000183` · unverified*

## Acceptance guidance

Either of:
1. **Positive:** An algorithm (with termination proof) that outputs a complete EFX allocation for every instance with 4 agents and arbitrary nonnegative additive valuations. A referee would accept a constructive proof with an explicit potential/termination argument, or a non-constructive existence proof — but the field strongly prefers an algorithm.
2. **Negative:** An explicit instance $(M, \{v_i\}_{i=1}^4)$ with additive $v_i$ and a (computer-assisted or exhaustive) proof that no complete allocation of $M$ is EFX.

Secondary contributions that would count as partial progress: EFX for 4 agents with three distinct valuation types; reducing the unallocated pool below $n-1$ for $n=4$; EFX for $n=4$ with ternary/bounded-value-range valuations.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/f73c6d26-df86-4159-8765-0be54ea53e3e?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000183.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000183)
