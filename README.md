<!-- solve-problem:6f0736e3-ba38-4277-8ef6-96ae4c1fde38 -->
# A factor-two approximation for asymmetric TSP

A [Tangle Solve problem](https://solve.tangle.tools/problems/6f0736e3-ba38-4277-8ef6-96ae4c1fde38).

## What is the problem?

**Asymmetric Traveling Salesman Problem (ATSP):** Given a complete directed graph on $n$ vertices with edge weights $c(i,j) \geq 0$ satisfying the **directed triangle inequality** $c(i,j) \leq c(i,k) + c(k,j)$, find a minimum-cost Hamiltonian cycle (a tour visiting every vertex exactly once). The goal: design a **polynomial-time 2-approximation**, i.e., an algorithm returning a tour of cost at most $2 \cdot \mathrm{OPT}$.

This is a 40+ year open problem (the symmetric version has the classic 1.5-approximation of Christofides; the asymmetric case is far harder). The precise target: deterministic or randomized polynomial time, guarantee $2$ (or $2+\varepsilon$ for any fixed $\varepsilon > 0$, which is considered equally interesting). Note the problem is in the *metric* setting; without the triangle inequality no finite approximation is possible (unless P=NP). Also note $2$ is a "psychological" barrier matching the natural LP integrality gap folklore — no matching hardness is known beyond $75/74$ (Karpinski–Lampis–Schmied, verify exact constant).

## Why does it matter?

ATSP models real routing where travel is asymmetric: one-way streets, flight schedules with fares, upstream/downstream river transport, and wind/terrain effects. A 2-approximation would match the guarantee of the classic double-tree/cycle-cover baseline in symmetric TSP intuition and likely require (or produce) a proof that the subtour-elimination LP relaxation has integrality gap at most ~2, resolving a major question in polyhedral combinatorics. Progress here feeds general techniques for metric-directed optimization (asymmetric k-center, directed Steiner variants).

## What's already known?

- **Cycle cover baseline (Frieze–Galbiati–Maffioli, 1982):** repeatedly patching cycle covers gives $\log_2 n$-approximation; later improved to $O(\log n / \log\log n)$ asymptotics.
- **Breakthrough — Svensson, Tarnawski, Végh (STOC 2018 / JACM):** first **constant-factor** approximation for metric ATSP, via local connectivity (LocalConnectivity) properties of the subtour LP and an algorithm for "node-weighted" ATSP. Constant was large (implicit, thousands).
- **Traub–Vygen (arXiv:1912.00670):** improved the constant to $22 + \varepsilon$ via a refined framework ("algorithmic patching", better reduction handling of irregular instances with vertex splitting). This 22+ε remains the best verified general bound.
- **Lower bounds:** the subtour LP for ATSP has integrality gap at least 2 (Charikar–Goemans–Karlin / others via graphic instances), so 2 is the natural ceiling for LP-based methods — no inapproximability beyond small constants is known.
- **Special cases:** node-weighted and graphical ATSP admit better constants (Svensson 2015 gave 8 for node-weighted; later improvements to ~3+ε, verify).

Approaches tried and stuck: pure cycle-cover patching cannot beat logarithmic; the STV framework's loss comes from "irregular" components and lower bounding arguments that multiply constants; reductions to node-weighted instances lose large factors.

## What would count as solving it?

A polynomial-time algorithm with proven worst-case guarantee:
- **Primary:** algorithm returning a tour of cost $\leq 2 \cdot \mathrm{OPT}$ (or $2+\varepsilon$) for all metric ATSP instances, with a correctness and ratio proof.
- **Equivalent-strength alternative:** prove the subtour LP integrality gap is at most 2 and give a matching efficient rounding (a pure gap bound without algorithm may be accepted as a major partial result).
- **Partial credit targets:** any constant below 22 (e.g., beating 10, matching 4), or 2-approximations for structured subclasses (graphical, shortest-path metrics of planar digraphs, etc.).

## How to start

1. Read **Traub–Vygen (1912.00670)** first — it contains a clean exposition of the STV framework, the standard "irregular instance" reduction, and an explicit accounting of where the constant blows up. Then **Svensson–Tarnawski–Végh (2018)** for the LocalConnectivity machinery.
2. Identify the loss terms: the constant is roughly a product of (a) the node-weighted ATSP approximation factor used on the reduced instance, (b) the vertex-splitting/patching loss, and (c) coefficients from the lower-bound function on components. Try to make these losses additive rather than multiplicative.
3. Study the known integrality-gap-2 lower-bound instances (e.g., graphic instances where the optimum is exactly twice the LP value) — any 2-approximation must be tight on these; check whether existing roundings are already tight there.
4. Main obstacle: no technique currently "sees" the gap between the LP optimum and true OPT beyond factor 2 in general; local-connectivity certificates are too weak. A new lower-bounding scheme or LP strengthening is the plausible route.

## Key references

- D. Svensson, J. Tarnawski, L. A. Végh, "A Constant-Factor Approximation Algorithm for the Asymmetric Traveling Salesman Problem", STOC 2018 / JACM. First constant-factor approximation for metric ATSP via local connectivity certificates of the subtour LP and a reduction to node-weighted instances. (verify journal details)
- L. Traub, J. Vygen, "An Improved Approximation Algorithm for ATSP", arXiv:1912.00670. Improves the constant to $22+\varepsilon$ by handling irregular instances via vertex splitting and better patching. https://arxiv.org/abs/1912.00670
- A. M. Frieze, G. Galbiati, F. Maffioli, "On the worst-case performance of some algorithms for the asymmetric traveling salesman problem", Networks 1982. The $\log_2 n$ cycle-cover patching baseline.
- O. Svensson, "Approximating ATSP by relaxing connectivity", FOCS 2015. 8-approximation (verify constant) for node-weighted ATSP — the key subroutine ancestor of the constant-factor result.
- A. Asadpour et al., "An $O(\log n/\log\log n)$-approximation algorithm for the asymmetric traveling salesman problem", SODA 2010. Thin-tree-based rounding; best pre-constant-factor bound via O(log n/log log n).

## Warnings

- "Metric" here means the **directed** triangle inequality; symmetric intuition (Christofides, double-tree = 2) does not transfer.
- The factor-2 integrality gap lower bounds mean the subtour LP alone cannot certify better than 2; do not aim for below 2 via that LP.
- Beware claimed constants in older papers — several early "constant-factor" claims in ATSP history were erroneous; the STV paper is the first fully verified constant.
- Beware folklore misattribution: the census phrase "constraint satisfaction" in the subfield label is spurious; this is purely approximation algorithms.

---
*`ALGO-000107` · unverified*

## Acceptance guidance

A polynomial-time algorithm with proven worst-case guarantee:
- **Primary:** algorithm returning a tour of cost $\leq 2 \cdot \mathrm{OPT}$ (or $2+\varepsilon$) for all metric ATSP instances, with a correctness and ratio proof.
- **Equivalent-strength alternative:** prove the subtour LP integrality gap is at most 2 and give a matching efficient rounding (a pure gap bound without algorithm may be accepted as a major partial result).
- **Partial credit targets:** any constant below 22 (e.g., beating 10, matching 4), or 2-approximations for structured subclasses (graphical, shortest-path metrics of planar digraphs, etc.).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/6f0736e3-ba38-4277-8ef6-96ae4c1fde38?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000107.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000107)
