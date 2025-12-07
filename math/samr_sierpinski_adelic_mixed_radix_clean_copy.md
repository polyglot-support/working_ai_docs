# Sierpiński–Adelic Mixed‑Radix (SAMR)
**Fractal Interfaces and Mixed‑Radix Phase Geometry**  
*v0.1 — integrates with UIGO/UA‑CFS stack*

---

## 0) Executive Summary
SAMR defines a **mixed‑radix, tail‑transducer** layer that drives **recursive phase geometries** realized by fractals (Sierpiński, carpets, Cantor, Vicsek, Hilbert/Peano, Koch/Lévy, etc.) over an **adelic integer substrate**. It provides:
- a formal mixed‑radix odometer \((b_n,a_n)\) with tail‑first causality compatible with p‑adics,
- a **generic fractal interface** (IFS/Grid‑Deletion/Space‑Filling/L‑System/Circle‑Packing),
- **bi‑fractal boundary coupling** via least‑common refinement (LCR) partitions,
- **prime‑separable orthogonality** and exact cyclotomic phase labels (e.g., \(\mu_3,\mu_5\)),
- functorial **Res/Norm/Hecke** transfers into interior fibers and OPA‑based readout preserving positivity.

---

## 1) Ambient Substrate & State
**Adelic substrate.** Work over \(\mathbb{A}_f\) (finite adeles), optionally \(\mathbb{R}\times\mathbb{A}_f\) modulo diagonal \(\mathbb{Q}\) for real marginals. All coordinates are coherent residue systems \(\{x\bmod p^{k_p}\}_p\) with finite active supports.

**Orientation/OPA.** Internal arrays are positive measures on a compact abelian group \(G\) (e.g., \((\mathbb{Z}_2)^k\times C_M\)); signs/phases appear only at **character readout**.

**State tuple (per site/node).**
\[
S_n = (X_n,\, \Lambda_n,\, F_n,\, N_n)
\]
- \(X_n\): geometric coordinates (model‑specific; e.g., barycentric \((u,v,w)\) with \(u+v+w=1\), or grid indices, or curve addresses).
- \(\Lambda_n\in\mu_q\): cyclotomic twist label (e.g., \(q=3,5\)) ensuring exact rational phases.
- \(F_n\): local integer frame \((A,t)\) with \(A\in O(Q)\cap\prod_p\mathrm{GL}(\mathbb{Z}_p),\ t\in\mathbb{A}_f^d\).
- \(N_n\): per‑prime period/precision manager (vector of \(p^{k_p}\)).

---

## 2) Mixed‑Radix Odometer & Tail Transducer
**Digits and bases.** A radix schedule \(b_n\in\mathcal{B}\subseteq\{2,3,5,\ldots\}\) and digits \(a_n\in\{0,\ldots,b_n-1\}\) are consumed **tail‑first** (least‑significant first) to match p‑adic causality.

**Transducer.** A Mealy machine \(\mathcal{T}=(Q,\delta,\omega)\) with
- state \(Q\ni S_n\),
- input symbol \(\sigma_n=(b_n,a_n)\),
- transition \(S_{n+1}=\delta(S_n,\sigma_n)\),
- output \(\omega(S_n)\) (e.g., character readout or boundary flux).

**Scheduling.** Deterministic, periodic, or automaton‑driven \(b_n\). Constraints: for every active fractal, needed denominators are valuation‑bounded so period manager can maintain exactness.

---

## 3) Generic Fractal Interface (GFx)
SAMR treats each fractal as a **coded contraction system** with exact rational arithmetic.

### 3.1 Unified spec
**FractalSpec** (language‑agnostic, JSON‑style):
- `family`: `IFS | GRID | SPACEFILL | LSYS | CIRCLEPACK`.
- `dimension`: ambient integer dimension (e.g., 2 for triangle/carpet, 3 for tetrahedron).
- `active_primes`: subset of primes used by this fractal (orthogonality planning).
- `state_model`: `BARYCENTRIC | GRID | CURVE_ADDR | SYMBOLIC`.
- `maps`: list of maps with exact rational parameters.
- `constraints`: linear relations (SNF matrix), parity rules, forbidden sets.
- `phase_group`: cyclotomic order for twist labels (e.g., `mu_3`, `mu_5`).
- `readout_modes`: protected harmonics / characters for OPA gates.

### 3.2 Families
**IFS (contractive affine).** Maps \(S_i(x)=A_i x + t_i\) with \(A_i,t_i\in\mathbb{Q}^{d\times d}\times\mathbb{Q}^d\); valuations tracked primewise. Examples: Sierpiński gasket (\(\alpha=1/2\)), tetrahedron (3D), Koch variant if ratios are rationalizable.

**GRID (deletion/subdivision).** Triadic carpets, Vicsek/Quincunx, Cantor‑type. Defined by integer subdivisions and mask sets; evolution is index arithmetic + mask.

**SPACEFILL (curve encoders).** Hilbert (2), Peano (3), H‑curve (2), 5‑ary Peano. Provide local rewrite/turn tables with rational rotations/reflections realizable in integer frames.

**LSYS (morphisms).** Deterministic context‑free grammars with segment lengths/angles in rational ratios; use only angle sets realizable as character phases (codomain) while positions remain integer/coherent residues.

**CIRCLEPACK (integer circles).** Discrete choices via integer Descartes quadruples; selection maps are integral. Angles/arc constraints use integer‑circle algebra.

---

## 4) Bi‑Fractal Boundaries & LCR Coupling
We couple **Left** (L) and **Right** (R) fractal boundaries to an interior fibration.

**Cylinder partitions.** For depth \(n\), let \(\mathcal{C}^L_n,\mathcal{C}^R_n\) be cylinder sets induced by the two boundary codings.

**Least‑Common Refinement (LCR).**
\[
\mathcal{P}_{n,m} = \{ C\cap C' : C\in\mathcal{C}^L_n,\ C'\in\mathcal{C}^R_m \}.
\]
Pick \((n,m)\) to cover one period of both mixed‑radix schedules (lcm over prime exponents). LCR induces a common partition for transfers.

**Transfers.**
- **Res** (boundary \(\to\) interior cells), **Norm** (adjoint back), **Hecke** (prime‑power lifts/drops) applied per LCR block, routed via LCA nodes of the interior tree to ensure path independence.
- Global meta‑operator: \(H_{\text{meta}}=\bigoplus H_{\text{cell}} + \sum \mathrm{Res}^* K_{\text{LCR}}\,\mathrm{Res}\), with \(K_{\text{LCR}}\) block‑constant kernels.

---

## 5) Per‑Step Update Rules (schematic)
Given input \(\sigma_n=(b_n,a_n)\):

1) **Selector:** choose active side(s)/fractal(s) affected at step \(n\) per schedule LUT.  
2) **Geometry update:** apply either IFS map, GRID mask move, SPACEFILL rewrite step, LSYS production, or CIRCLEPACK selection. All parameters are rational; valuations update \(N_n\).  
3) **Frame action:** optional \(x\mapsto A_n x + t_n\) with integer frames to implement relabels/reflections/rotations.  
4) **Phase/twist:** update \(\Lambda_{n+1}=\Lambda_n\,\zeta_q^{\phi(b_n,a_n)}\) (\(\phi\) small integer).  
5) **Transfers:** apply Res/Norm/Hecke chosen by the schedule (often keyed by base‑5 or a separate control digit).  
6) **OPA interface:** push boundary outputs into OPA arrays; compiled gates preserve specified harmonics exactly; invisible‑mass sinks null unwanted modes.

---

## 6) Orthogonality & Prime Planning
- **Support disjointness:** assign largely disjoint `active_primes` to L and R (e.g., L uses \(3\), R uses \(5\); base‑2 reserved for frame flips). Inner products factor and cross‑talk is nil unless coupling is explicit.
- **Twisted pairings:** when needed, add a bicharacter \(\Omega\) to encode topological twists (Möbius/Klein/knot); consistency certified by Smith Normal Form (SNF).

---

## 7) Period/Precision Management
- **Manager state:** vector \(N_n=(p^{k_p})_p\) per site. Refinements only where \(v_p(b_n)>0\).
- **2‑adic halving:** operations like \(\tfrac12\) handled by updating the 2‑adic exponent; no floating division is used.
- **Protected modes:** specify readout harmonics to be preserved exactly; discretization on unprotected modes scales as \(O(1/M)\) with \(M=\mathrm{lcm}\) of active cyclic periods.

---

## 8) Formal Guarantees (informal theorems)
1) **Type safety:** domain remains adelic/integer; phases only at character readout.  
2) **Unitarity:** translation and character‑phase actions are unitary on Haar; compiled OPA gates preserve protected modes exactly.  
3) **Adjointness:** \(\mathrm{Norm}=\mathrm{Res}^*\) per LCR block; Hecke maps respect divisor‑lattice adjointness.  
4) **Path independence:** LCA‑mediated ascend–couple–descend obeys Beck–Chevalley; composite transfers depend only on endpoints.  
5) **Orthogonality:** for disjoint prime supports of boundary drivers, cross‑terms vanish.

---

## 9) Fractal Interface Details
### 9.1 IFS
- **Data:** vertices/anchors; matrices \(A_i\in\mathbb{Q}^{d\times d}\), translations \(t_i\in\mathbb{Q}^d\).
- **Constraint:** spectral radius primewise <1 (in archimedean sense use only for visualization; adelic evolution is valuation‑tracked, not metric).
- **Barycentric simplex:** keep invariant \(\sum u_i=1\); pick \(\alpha=1/2,1/3,2/3\) etc. with valuation bookkeeping.

### 9.2 GRID (deletion/subdivision)
- **Data:** subdivision base \(m\) (e.g., 3 or 5), mask set \(\mathcal{M}\subset\{0,\ldots,m^d-1\}\).
- **Step:** refine modulus at primes dividing \(m\); filter indices by \(\mathcal{M}\).

### 9.3 SPACEFILL
- **Data:** local rewrite table (turns, swaps), Gray maps, parity constraints.
- **Step:** tail‑local rewrite; frame action implements turns via integer orthogonal transforms.

### 9.4 LSYS
- **Data:** morphism \(\varphi: \Sigma\to\Sigma^*\), segment vectors with rational ratios; optional angle phases as character labels.

### 9.5 CIRCLEPACK
- **Data:** integer Descartes quadruples; selection rules; arc constraints.  
- **Step:** choose next circle by an index digit; maintain integer circle invariants.

---

## 10) Bi‑Fractal Examples (opposite boundaries)
### 10.1 Gasket‑3 (L) vs Vicsek‑5 (R)
- L: barycentric IFS with \(\alpha=1/2\), \(\Lambda\in\mu_3\), active primes \(\{3,2\}\).
- R: GRID on 5‑ary quincunx; scheduler uses base‑5 digits to choose scale/Res/Norm.
- LCR: intersections of triadic cylinders with 5‑ary blocks; Res/Norm over blocks; optional bicharacter to encode hole parity.

### 10.2 Cantor‑3 (L) vs Hilbert‑2 (R)
- L: 1D triadic deletion; R: SPACEFILL with binary Gray; orthogonality from \(3\) vs \(2\); synchronize at lcm period.

---

## 11) Scheduler & LUTs
- `radix_schedule`: sequence or automaton over {2,3,5}.
- `activate`: mapping from radix \(b\) and digit \(a\) to actions: `{geometry_update, frame_action, transfer, twist_increment}`.
- `prime_policy`: per action, which primes to refine (updates \(N_n\)).

---

## 12) Validation Suite
1) **Simplex invariant** (if barycentric): \(\sum u_i=1\) at all steps.  
2) **OPA protected modes**: exact on declared harmonics; invisible‑mass annihilates forbidden modes.  
3) **Adjointness & mass conservation** across LCR blocks.  
4) **Phase exactness**: \(\Lambda\) cycles yield exact \(1/q\) phases in readout.  
5) **Orthogonality tests**: inner products vanish for disjoint prime supports.

---

## 13) Implementation Mechanics (guidance)
- **Data layout:** per‑prime buffers with moduli \(p^{k_p}\); recombination via CRT; SNF for linear constraints.
- **Parallelism:** embarrassingly parallel across primes; synchronize only at CRT recombination/readout.
- **Complexity:** transforms are \(O(n\log n)\) for diagonalizable OPA objectives; LCR assembly linear in number of blocks.

---

## 14) Extensibility
- Additional primes (e.g., 7) and cyclotomic labels \(\mu_7\).
- Nonabelian orientation groups (replace characters with irreps).
- Stochastic schedulers and entropy‑regularized controls (Schrödinger bridges) over LCR partitions.

---

## A) Notation & Symbols
- \(\mathbb{A}_f\): finite adeles; \(v_p\): p‑adic valuation; CRT: Chinese Remainder Theorem.
- Res/Norm/Hecke: restriction, adjoint averaging, prime‑power transfer.
- LCR: least‑common refinement of boundary cylinder partitions.
- OPA: positivity‑preserving convolution algebra; characters for readout.

## B) Minimal Defaults
- \(\mathcal{B}=\{2,3,5\}\); \(\mu_q=\mu_3\) unless specified.
- Period manager initializes with \(N_0=\prod p\) for active primes; grows only when required by digit schedule.

