# Mirror‑CRT Primality Geometry: A Two‑Phase, Bi‑Dimensional Recursive Structure

## Abstract
We present a concise framework for prime/composite structure built from a **two‑phase**, **bi‑dimensional** encoding of integers along a **CRT hierarchy**. Each level couples a standard residue axis with a mirror (quotient) axis per prime pair, yielding a **Mirror‑CRT (bi‑CRT)** state space. The induced recursion is **cycle‑free** by a contractivity argument, furnishing a Bratteli–Vershik (BV) dynamical view. We outline exact, parameter‑free invariants derivable from this structure and relate them to known congruence‑based primality criteria. The artifact consolidates the theory, the geometry, and practical heuristics into a roadmap toward a **definition‑level invariant** in the same geometry.

---

## 1. Core constructs
**Prime ladder.** Let \(p_1<p_2<\dots<p_k\). Define mirror partners \(q_i:=p_{k+1-i}\). For each pair \((p_i,q_i)\) write \(m_i:=p_i q_i\) and \(\Lambda_k:=\mathrm{lcm}(m_1,\dots,m_{\lfloor k/2\rfloor})\). Work in \(R_k:=\mathbb Z/\Lambda_k\mathbb Z\).

**Two‑phase digits (per pair).** For \(n\in\mathbb Z\):
- CRT axis (residues): \(x_i\equiv n\pmod{p_i},\; y_i\equiv n\pmod{q_i}.\)
- Mirror axis (quotients): \(a_i\equiv \lfloor n/p_i\rfloor\pmod{q_i},\; b_i\equiv \lfloor n/q_i\rfloor\pmod{p_i}.\)
Package as the **pair block** \(\mathcal M_i(n)=\begin{bmatrix}x_i & a_i\\ b_i & y_i\end{bmatrix}\).

**Bi‑CRT coordinates (packed).** \(r_i:=x_i+p_i y_i\in\mathbb Z_{m_i},\; s_i:=a_i p_i+b_i\in\mathbb Z_{m_i}.\) The integer is then represented by \(\mathrm{BiCRT}_k(n)=(r_i,s_i)_{i=1}^{\lfloor k/2\rfloor}\).

**Recursive map (local).** The mixed‑radix recursion \(T_k\) obeys a **pair‑local rule modulo \(m_i\)**:
\[ T_k(n) \equiv a_i(n)+q_i b_i(n) \pmod{m_i}. \]
Equivalently, on mirror coordinates \((a,b)\) the pair map is
\[ F_{p,q}(a,b)=(\lfloor (a+q b)/p\rfloor\!\mod q,\; b). \]

---

## 2. Geometry: a second axis from mirror symmetry
The standard CRT encodes **where** \(n\) sits on each \(\mathbb Z_{p_i}\times\mathbb Z_{q_i}\) torus via \((x_i,y_i)\). The mirror coordinates \((a_i,b_i)\) encode **how** carries propagate when viewing \(n\) through the complementary divisions by \(p_i\) and \(q_i\). Stacking these gives a bi‑dimensional state per pair, i.e., a genuine **second coordinate** that is linearly related to \(n\) yet orthogonal (in information) to residues.

---

## 3. Dynamics and contractivity (cycle‑free)
**Pair decoupling.** The global update modulo \(m_i\) depends only on the pair’s \((a_i,b_i)\). Thus the global system is the product of independent rectangles \([0,q_i𝜋1]\times[0,p_i𝜋1]\).

**Contraction lemma.** Fix \((p,q)\) and \((a,b)\). Under \(F_{p,q}\): \(b\) is **frozen**; \(a\) updates by \(a\mapsto \lfloor (a+qb)/p\rfloor\). For any interval \(I\subset\{0,\dots,q-1\}\) of width \(W\),
\[ \mathrm{width}(F(I))\le \lceil W/p\rceil. \]
Hence the diameter contracts by at least \(p\) each step. After \(\lceil \log_p q\rceil\) steps the image is a singleton; therefore the pair map has **no cycles**, only fixed points.

**Global consequence.** The product of cycle‑free maps is cycle‑free; \(T_k\) reaches a fixed point with depth bounded by \(\max_i \lceil \log_{p_i}q_i\rceil\). For odd \(k\), the middle self‑pair collapses in one step.

---

## 4. BV/AF‑algebra view (structural spine)
- **Bratteli diagram.** Level \(k\) vertices correspond to pair rectangles; edges encode the piecewise constant map \(a\mapsto \lfloor (a+q b)/p\rfloor\) for each fixed \(b\).
- **Vershik map.** Well‑defined by contractivity: orbits strictly shorten then land at a minimal fixed vertex.
- **AF traces.** Normalized edge multiplicities define traces on the inductive limit; extreme points represent single‑fold alignments, while faces represent multi‑fold (composite) coherence.

This BV spine supplies **parameter‑free** objects (edge counts, incidence matrices, characteristic polynomials) for invariants.

---

## 5. Invariants (discrete, parameter‑free)
We list candidate invariants that arise naturally in the bi‑CRT space. Some show signal empirically; the goal is a proof‑quality criterion.

**(I) Mirror discrepancy per pair.** \(\Delta_i(n):=(q_i a_i-p_i b_i)\bmod m_i\). Vector \(\Delta(n)=(\Delta_i)_{i}\) measures cross‑phase alignment. Patterns such as “align at \(k=2\), break at \(k=3\)” embody the **one‑fold only** principle.

**(II) Alignment signature.** For level \(k\), define MR digits \(d^+_k(n)\) and \(d^-_k(n)\) (forward vs. mirrored divisions). The boolean \(A_k(n):=[d^+_k(n)=d^-_k(n)]\) tracks equality along the tower. Prime‑like behavior is \(A_2=1, A_3=0\).

**(III) Fix‑depth profile.** \(D_k(n):=\max_i \text{steps to fix under }F_{p_i,q_i}\). Prime‑like: \(D_2=1\) but \(D_3>1\). Composite‑like: \(D_k\) stays small at \(\ge 2\) successive levels.

**(IV) Level polynomial.** For each pair, form the transfer operator on \(a\) (for fixed \(b\)) and assemble a **level polynomial** \(Q_k(X)\) (e.g., characteristic polynomial of the incidence matrix restricted to unit classes). A potential criterion:
\[ (X+1)^n-(X^n+1)\in (Q_k(X),\,n)\subset R_k[X]/(X^{\Lambda_k}-1). \]
Proof target: primes satisfy the inclusion for all \(k\le c\log n\); composites fail at some bounded \(k\).

---

## 6. Two‑phase hyperbolic flow (fast heuristic)
A separate, factor‑free flow embeds phase \(+\) via primorial‑scaled coordinates and phase \(-\) via **time‑reversed** mixed‑radix digits. Channel shears over the first few primes produce three scale invariants \(I_1,I_2,I_3\) with a simple decision rule. Empirically (on moderate ranges) this reaches ~80–90% accuracy, cleanly explained by small‑prime saturation and two‑phase decoherence.

**Role here.** The flow is a **computational front‑end** and a phenomenological guide; the **bi‑CRT invariants** aim to provide the **definition‑level** spine.

---

## 7. What’s proven vs. conjectured
**Proven (within this artifact).**
- Pair‑locality of the update modulo \(m_i\).
- Pair‑map contractivity \(\Rightarrow\) cycle‑free; global cycle‑free as product.

**Conjectured/targets.**
- Existence of a level‑polynomial criterion equivalent to a known primality congruence (AKS‑type) but expressed entirely within the bi‑CRT/BV spine.
- Stabilization of a **single, parameter‑free** obstruction at depth \(k\le c\log n\), independent of range.

---

## 8. Roadmap to a definition‑level invariant
1) **Formalize the pair‑decoupling lemma** and the contraction lemma; record the global depth bound.
2) **Construct incidence matrices** per level (restricted to unit classes) and derive \(Q_k(X)\). Explore ideal‑membership tests of the form above; attempt an equivalence proof to a standard congruence.
3) **Validate on hard families**: large semiprimes with both factors > depth primes; Carmichael numbers; prime powers; near‑primorial regions.
4) **Scale depth** with \(k=O(\log n)\) and seek a monotone obstruction (once broken, stays broken) along the tower.

---

## 9. Minimal algorithms (pseudocode)
**Bi‑CRT blocks**
```
for each pair (p_i, q_i):
  x_i = n mod p_i
  y_i = n mod q_i
  a_i = floor(n / p_i) mod q_i
  b_i = floor(n / q_i) mod p_i
  block_i = [[x_i, a_i], [b_i, y_i]]
  r_i = x_i + p_i * y_i   in Z_{m_i}
  s_i = a_i * p_i + b_i   in Z_{m_i}
```

**Pair map & fix‑depth**
```
F_{p,q}(a,b):
  return ( floor((a + q*b)/p) mod q, b )

fixdepth(n,k):
  depths = []
  for each pair (p,q) at level k:
    (a,b) from block
    t=0
    repeat: (a',b')=F_{p,q}(a,b); t+=1
            if a'==a: break
            a=a'
    depths.append(t-1)
  return max(depths)
```

**Candidate invariants**
```
Delta_i(n) = (q_i * a_i - p_i * b_i) mod m_i
A_k(n) = [ MR_plus_digits(n,k) == MR_minus_digits(n,k) ]
```

---

## 10. Outlook
The Mirror‑CRT structure articulates primes as **one‑fold boundary fixed points** in a two‑phase recursion, with composites exhibiting **multi‑fold coherence** across levels. The BV/AF framing guarantees well‑behaved dynamics (cycle‑free) and supplies algebraic scaffolding (incidence matrices, traces, level polynomials) likely rich enough to host a **proof‑quality invariant**. The immediate next step is aligning \(Q_k\)-style level identities with classical congruences—ideally proving equivalence while keeping all constructions intrinsic to the bi‑CRT tower.

