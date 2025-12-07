# Geometric Operational Number System — Formalism v0.1

> A long-form specification unifying prime-factorized recursion, pointed n‑gons, CRT-style constraint solving, and Pythagorean metric certification on a tetra ⇄ sphere ⇄ cube atlas.

---

## 0. Motivation & Role
We seek a mechanistic, *operative* number system in which elements are small, addressable geometric programs (“digits”), arithmetic is composition of geometric operations, and solving proceeds by reconciling prime-factored constraints across multiple geometries with deterministic, integer-exact methods.

This document specifies the objects, operators, laws, normal forms, algorithms, and validation principles underpinning such a system.

---

## 1. Ambient Spaces and Charts
**1.1 Atlas.** We fix three mutually coupled spaces:
- **Tetra faces**: four planar faces of a regular tetrahedron \(T\).
- **Sphere**: unit two-sphere \(S^2\) centered at the origin \(O\).
- **Cube**: axis-aligned cube \(C=[-1,1]^3\), circumscribing \(S^2\).

**1.2 Orthogonal tripod.** Denote by \((X,Y,Z)\) the mutually orthogonal lines through \(O\) joining midpoints of opposite edges of \(T\). These act as global principal directions and supply a canonical right-handed frame.

**1.3 Charts and projections.** For each face \(f\):
- \(\Pi_{f\to S}\): radial map from face plane to \(S^2\) (great circle image).
- \(\Pi_{S\to C}\): radial map to the corresponding cube face (same normal as \(f\)).
- \(\Pi_{C\to f}\), \(\Pi_{S\to f}\) are the inverse charting maps restricted to their images.

All three charts share the same center \(O\); composition of these maps is well-defined wherever domains overlap.

---

## 2. Addresses and Prime Partitions
**2.1 Prime steps.** For each prime \(p\) we define a refinement operator \(S_p^{-1}\) acting on a chart cell to subdivide it into \(p\) congruent subcells along a designated local coordinate direction (chosen from \(X,Y,Z\) projected into the chart). Depth-\(k\) refinement is \(S_p^{-k}\).

**2.2 Address.** An **address** is a tuple
\[
 a := (\text{chart},\; \text{face\_id},\; w,\; u v,\; R) ,
\]
where:
- \(\text{chart}\in\{\text{face},\text{sphere},\text{cube}\}\),
- \(\text{face\_id}\in\{0,1,2,3\}\) selects a tetra face (redundant on \(S^2\)/\(C\) but retained for alignment),
- \(w\) is a **prime word**: a finite multiset or ordered list of pairs \((p,k)\) encoding refinement depths along the local basis axes,
- \(u v\in[0,1)^2\) denotes local coordinates within the current cell at depth \(w\),
- \(R\in SO(3)\) is the orientation induced from the tripod restricted to the chart (often implicit).

We write \(\text{cell}(a)\) for the geometric region corresponding to \(a\).

**2.3 Least-common refinement (LCR).** Given two addresses \(a_L,a_R\) possibly with different prime words and/or charts, their **LCR partition** is the minimal common refinement obtained by (i) transporting both to a common chart via \(\Pi\)-maps, (ii) taking componentwise \(\mathrm{lcm}\) on prime exponents, and (iii) aligning axes by the tripod.

---

## 3. Elementary Objects (Digits)
**3.1 Pointed n‑gon digit.** A digit is a quadruple
\[
 \pi_n = (a,\; n,\; w,\; \mathcal O)
\]
with:
- **Address** \(a\) as above.
- **Arity** \(n\in\mathbb N_{\ge 3}\): number of sides of a base polygon inscribed in \(\text{cell}(a)\) (in its chart), joined by straight segments to the apex \(O\) (point geometry). When \(n\to\infty\), the digit approaches a cone on the patch.
- **Weights** \(w\in\mathbb R^m\) (payload channels; e.g., mass, color, potential, small tensor coefficients).
- **Program** \(\mathcal O\): a right-associated word in operators \(\{S_p^{\pm1}, R_{\alpha}, T, \Pi_{*\to*}\}\), acting on the embedded polygon before apex-join.

**3.2 Collections.** A **numeral** is a finite multiset \(\mathbf N = \sum_i \pi_{n_i}\) (formal sum). All operations below extend pointwise and coalesce identical terms by idempotence rules.

---

## 4. Core Operators
We define three total operators on digits and numerals; they are the arithmetic of the system.

**4.1 Interference (join) \(\boldsymbol{\star}\).**
- On addresses: \(\text{cell}(a_1)\star\text{cell}(a_2)\) returns their **common subpartition** (intersection refined to LCR depth) as a disjoint union of subcells.
- On digits: \(\pi^{(1)}\star\pi^{(2)}\) overlays their payloads on the LCR subdivision with weight coalescence kernel \(\mathcal C(w_1,w_2)\) (default: vector addition or max).
- Laws: commutative, associative, idempotent (on identical \((a,n,\mathcal O)\)).

**4.2 Division (cut) \(\boldsymbol{\div}\).**
- On addresses: minimal separating partition of \(\text{cell}(a_1)\) by \(\text{cell}(a_2)\); returns the components of \(\text{cell}(a_1)\setminus \text{cell}(a_2)\) at LCR depth.
- On digits: restrict weights and programs to the remainder cells; anti-commutative at the set level.

**4.3 Composition (embed) \(\boldsymbol{\circ}\).**
- On addresses: chart transfer + refinement: \(a_1\circ a_2\) embeds the structure of \(a_2\) into \(a_1\) via chart maps and axis alignment.
- On digits: program composition \(\mathcal O_1\circ\mathcal O_2\); non-commutative, associative.

These three are closed on numerals and give a rig-like algebra when coupled with weight addition.

---

## 5. Adelic Residues and CRT Reconstruction
**5.1 Residues.** A **residue** on a cell is a triple \((p, k, r)\) interpreted as: “select subcell with index \(r\) at depth \(k\) under prime \(p\)” (indices taken in a fixed traversal order). A **residue set** is a finite family \(\mathcal R=\{(p_i,k_i,r_i)\}\) with pairwise coprime \(p_i\).

**5.2 Geometric CRT.** Given \(\mathcal R\) on a common address \(a\), the **CRT reconstruction** is the unique subcell at depth \(\prod_i p_i^{k_i}\) contained in all \(p_i\)-indexed selections. Operationally:
\[
 \text{CRT}(a,\mathcal R)\;=\; \bigstar_i S_{p_i}^{-k_i}(r_i) \quad\text{(computed at LCR depth).}
\]
If residues live on different charts, transfer via \(\circ\) to a common chart prior to \(\star\).

**5.3 Conflict and repair.** If \(\mathcal R\) is inconsistent, compute \(\operatorname{sep}(\mathcal R)\) by iteratively applying \(\div\) to isolate conflicting blocks; refine only those blocks and reattempt CRT.

---

## 6. Metric Structure and Pythagorean Valuation
**6.1 Axis valuations.** For a digit or numeral \(X\), define three axis-wise valuations \(V_X, V_Y, V_Z\) by integrating a chosen channel (or quadratic energy, e.g., recursion-Laplacian energy) along the projections onto axes \(X,Y,Z\) (pulled back to the chart).

**6.2 Pythagorean law.** The global valuation \(V\) satisfies
\[
 V^2(X)\;=\;V_X^2(X)+V_Y^2(X)+V_Z^2(X),
\]
by construction of the orthogonal tripod and axis-separable eigenmodes of the refinement operators. This identity is used as a metric certification after CRT recombination.

---

## 7. Positivity Layer (OPA)
**7.1 Positive arrays.** Internal fields are stored as positive measures on a compact abelian group \(G\) associated with the current chart cell (e.g., cyclic products modulo \(p^k\)).

**7.2 Gates and readout.** Computation uses positivity-preserving gates (convolution, subgroup averaging). Signs/phases are applied only at readout via characters \(\hat G\). Exact preservation of selected harmonics yields certified estimates; the remainder is bounded and absorbed as “invisible mass.”

---

## 8. Variable‑n Geometry and Fusion
**8.1 n‑fusion.** For two digits \(\pi_{n_1},\pi_{n_2}\), define arity fusion \(n_1\boxtimes n_2 = \mathrm{lcm}(n_1,n_2)\). Optionally store sector tags to retain anisotropy.

**8.2 Apex semantics.** The apex at \(O\) endows each digit with a distinguished normal direction (center→patch), enabling flux/transport operators aligned with chart normals.

---

## 9. Ratio Hierarchy Network (RHN)
**9.1 Graph.** An RHN is a DAG whose nodes are states \((a,\mathcal R,\mu)\) and edges are scale-option steps \((\Delta k, \text{transfer}, \text{twist})\):
- **Node**: address \(a\), hard ratio constraints \(\mathcal R\) as ideals/residues, and positive measure \(\mu\) for soft objectives.
- **Edge**: refine/coarsen certain primes \(\Delta k\), transfer between charts via Res/Norm/Hecke, optionally apply a twist (character label).

**9.2 Solver invariants.**
- **CRT gluing** on recombination frontiers (\(\star\)) at LCR depth.
- **Path independence** by functorial transfers (ascend–couple–descend).
- **Metric certification** via the Pythagorean valuation.

---

## 10. Normal Forms and Equality
**10.1 Operator normal form.** Push programs to a right-associated list; sort commuting factors; lift chart transfers outward when possible.

**10.2 Address coalescence.** Compute LCR of overlapping addresses; coalesce terms with identical \((a,n,\mathcal O)\) using idempotence.

**10.3 Depth discipline.** Fix a global depth cap \(D\); any numeral is canonically reduced by coarsening or refining to \(D\), then coalescing.

Confluence and termination give deterministic equality checks.

---

## 11. Algorithms (Reference)
**A1. Geometric CRT (per cell)**
1. Choose common chart; compute LCR depth \(K=\sum_i k_i\) per prime.
2. For each prime \(p\), select tile \(r_p\) at depth \(k_p\).
3. Return \(\bigstar_p S_p^{-k_p}(r_p)\), materialized at depth \(\prod p^{k_p}\).

**A2. RHN path exploration**
1. Initialize frontier with \((a_0,\mathcal R_0,\mu_0)\).
2. Expand via allowed edges (scheduler chooses primes and transfers).
3. On each recombination, compute CRT at LCR depth; apply metric check.
4. Prune branches violating constraints or metric; continue until fixed point or goal depth.

**A3. Pythagorean valuation**
1. Project numeral to axis-aligned eigenmodes along \(X,Y,Z\).
2. Compute valuations \(V_X,V_Y,V_Z\) as integrals/energies.
3. Verify \(V^2=V_X^2+V_Y^2+V_Z^2\) within chosen readout tolerance (exact on protected modes).

**A4. LCR transfer (face↔sphere↔cube)**
1. Lift both addresses to LCA in the fibration (often \(S^2\)).
2. Apply Res to fit into the common refinement; couple at LCA; apply Norm down to targets.
3. Record path to ensure path-independence (should cancel by construction).

---

## 12. Complexity & Parallelism
- Work factorizes per prime; merging is \(O(M)\) in the number of active primes and quasi-linear in depth per prime.
- Chart transfers are linear in block count at LCR.
- RHN path search is bounded by branching in the mixed-radix scheduler; pruning via metric/CRT checks keeps it polynomial in depth for fixed fanout.

---

## 13. Examples (Sketch)
**E1. Exact subdivision of a circular arc by 9**
- Activate prime 3 only; apply \(S_3^{-2}\); residues pick the 9-way split; CRT is trivial (single prime). No floating division occurs.

**E2. Two scale paths, triadic vs. quinary**
- Run two branches with \(S_3\) and \(S_5\) refinements; recombine via LCR with exponents \((k_3,k_5)\); CRT picks the unique subcell; metric valuation certifies.

**E3. Ratio-preserving mesh**
- Encode edge-length and area ratios as residue ideals; RHN explores refinements; recombine at goal depth with Pythagorean check; produce canonical numeral.

---

## 14. Interoperability (Linear World)
- **Valuations** map numerals to reals/complex by integrating channels or reading protected harmonics.
- **Projections** yield classical UVs, lengths, areas from addresses; rotations are read as sums of adelic angles.
- **Export**: mesh/texture/field backends via the cube-face chart for rasterization, or via \(S^2\) for geodesic outputs.

---

## 15. Axioms & Laws (Summary)
1. **Closure**: \(\star,\div,\circ\) closed on numerals.
2. **\(\star\) rig**: commutative, associative, idempotent; distributes over address unions.
3. **\(\circ\)**: associative; respects chart maps; functorial with transfers (Res/Norm/Hecke).
4. **CRT determinism**: residue families reconstruct unique subcells at finite depth.
5. **Pythagorean valuation**: axis-wise valuations are orthogonal; global norm squares sum.
6. **Confluence**: normal form reduction terminates and is unique at fixed depth cap.

---

## 16. Minimal API (Pseudo)
```text
// core types
type prime_word = list<{p:int, k:int, axis: {X|Y|Z}}>
struct addr { chart: {face|sphere|cube}; face_id: int; w: prime_word; uv: (float,float); R: SO3 }
struct digit { a: addr; n: int; w: vec[m]; O: list<op> }

// ops
digit interfere(digit x, digit y)   // ⋆
digit divide(digit x, digit y)      // ÷
digit compose(digit x, digit y)     // ∘
addr  lcr(addr a, addr b)
addr  transfer(addr a, chart t)      // Res/Norm/Hecke under the hood

// residues & CRT
struct residue { p:int; k:int; r:int }
addr  crt(addr a, list<residue> R)   // returns unique subcell at depth ∏p^k

// valuations
vec3  axis_vals(numeral X)           // (V_X, V_Y, V_Z)
float norm_val(numeral X)            // V, s.t. V^2 = sum of squares

// RHN
struct rhn_node { a:addr; R: list<residue>; mu: opa }
struct rhn_edge { delta_k: map<p,int>; transfer: map; twist: char }
num    solve(rhn_node start, goals)
```

---

## 17. Validation Checklist
- **Integer exactness**: circle/arc splits by \(n\) implemented via prime refinement only.
- **Path independence**: transfers along any two chart paths agree (up to canonical normal form).
- **CRT determinism**: repeated CRT with permuted residue order yields identical address.
- **Pythagorean certification**: \(V^2=V_X^2+V_Y^2+V_Z^2\) holds exactly on protected modes, within bound on others.
- **Confluence**: numerals normalize to a unique representation at depth cap.

---

## 18. Outlook & Extensions
- Higher polytope atlases (octa/icosa) with compatible tripod choices.
- Stochastic operators in \(\mathcal O\) with martingale positivity in OPA.
- Learning layer: differentiable valuations and residue selection with integer guards.
- Hardware mapping: prime-parallel kernels; FWHT/NTT backends on \(G\).

---

### Glossary
- **Digit**: pointed \(n\)-gon with address, weights, and program.
- **Numeral**: finite sum of digits.
- **Address**: charted cell identified by a prime word and local coordinates.
- **LCR**: least-common refinement of two addresses/partitions.
- **Residue**: (prime, depth, tile index) selector.
- **CRT**: Chinese remainder reconstruction by \(\star\) after prime-wise selection.
- **OPA**: positivity-first measure layer with character readouts.
- **RHN**: ratio hierarchy network; DAG over addresses with ratio constraints and scalings.
- **Tripod**: the three orthogonal directions induced by opposite-edge midpoints of the tetra.

---

*End of v0.1*

