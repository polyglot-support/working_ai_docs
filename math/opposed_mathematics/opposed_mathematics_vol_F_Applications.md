# Opposed Mathematics — Vol. F: Applications & Algorithms (v1)

> Purpose. Deliver practical toolchains built on OM: (F1) opposed FFT/CRT with legality guards and centroid preservation; (F2) homology with opposition (character‑graded chains, 𝓝‑witnesses, intersection pairings); (F3) program rewriting & compilers (confluent normalizers, diff/patch with opposites, reversible steps); (F4) probability & inference (interference‑native probabilities, constraint propagation with non‑signaling). Includes algorithms, complexity, and implementation sketches.

---

## F0. Preliminaries
- Use Vol. A (⊕, overline, 𝓝, Ξ), Vol. B (div_n, CRT), Vol. C (IPG), Vol. D (†‑SMC & spiders), Vol. E (cyclotomic embedding, Born semantics).
- Data representations: sparse maps with character buckets; legality tables for each `G` factor.

---

## F1. Opposed FFT / CRT

### F1.1 Goal
Compute discrete Fourier transforms over `G ≅ ⊕_p Z_{p^{k}}` with **legality‑aware factorization**, preserving centroids and supporting `⊕`‑normalization.

### F1.2 Factorization with Legality Guards
1) **CRT split:** `DFT_G = ⊗_p DFT_{Z_{p^{k}}}`.
2) **Radix steps:** for `Z_{p^{k}}`, use Cooley–Tukey when factoring `p^{k} = ab` with `gcd(a,b)=1`.
3) **Legality gates:** phase splits using `n`th roots require `Ξ` to contain `μ_n`. If missing, either (i) restrict to legal sublayer of the data where `div_n` is admissible, or (ii) lift `Ξ` to a cyclotomic extension.

### F1.3 Centroid‑Preserving Transform
Maintain complex mean (centroid) invariants per factor:
```
Cent(ψ) = (1/|G|) ∑_{x∈G} φ(x)·ψ(x),    φ: embedding to S¹ per Vol. B.
```
Balanced subdivision steps `div_n` (when legal) preserve `Cent` (Vol. B); radix schedule chosen to keep this invariant exact.

### F1.4 Algorithm (Sketch)
```
OpposedFFT(ψ, G, Ξ):
  if G = ⊕_p Z_{p^k}: return ⊗_p OpposedFFT(ψ_p, Z_{p^k}, Ξ)
  if G = Z_m with m=ab, gcd(a,b)=1:
    ψ' ← stride-split into a×b lattice
    apply character shifts for twiddle factors (require μ_a, μ_b ⊆ Ξ)
    recursively OpposedFFT on sizes a and b
    return ⊕-reduce per index; track centroid
```
**Complexity.** `O(|G| log |G|)` arithmetic when all roots available; overhead `O(|G|)` for `⊕`‑normalization per stage (hash‑cancel in character buckets).

### F1.5 Applications
- Balanced multiresolution analysis over finite groups.
- Mixed‑radix QFT steps for gate synthesis (Vol. E).

---

## F2. Homology with Opposition

### F2.1 Character‑Graded Chain Complexes
Define chain groups `C_k` as free modules spanned by oriented `k`‑cells with coefficients in `ℕ_{≥0}[Ξ]`. Boundary maps `∂_k: C_k → C_{k-1}` use character labels instead of signs:
```
∂_k(σ^k) = ⊕_i  χ_i · σ^{k-1}_i
```
where `χ_i ∈ Ξ` encodes the orientation contribution. Opposed faces cancel to `𝓝`.

### F2.2 𝓝‑Witnesses
Cycles homologous to zero in classical homology may reduce to `𝓝` but remain **witnessed** as balanced opposition rather than numeric zero. Record `𝓝`‑classes to distinguish spaces with balanced but nontrivial cancellation structure.

### F2.3 Intersection Pairings
Intersection forms become character‑paired bilinear maps `⟨·,·⟩_Ξ: H_k × H_{n-k} → ℕ_{≥0}[Ξ] / ⊕`. Perfect opposition across a pairing reduces to `𝓝` (balanced trivial), revealing refined nulls.

### F2.4 Algorithms
- **Boundary assembly:** build sparse boundary matrices with character entries.
- **Reduction:** Smith normal form generalized to character‑graded entries; use `⊕`‑aware row/column ops with bucketed cancellation.
- **Complexity:** similar to classical persistent homology but with per‑entry character hashing; practical `~ O(N^ω)` worst‑case, `O(E log E)` typical for sparse complexes.

### F2.5 Examples
- Oriented square/cube complexes where opposite faces carry inverse characters; classical `H_1` trivial, OM reveals `𝓝`‑witness cycles.

---

## F3. Program Rewriting & Compilers

### F3.1 Confluent Normalizers
Use Vol. D rewrite system (spider fusion, opposed cancellation, Hopf rules) to obtain **canonical normal forms**. Guarantees deterministic compilation targets (no critical‑pair ambiguity).

### F3.2 Diff/Patch with Opposites
Represent edits as opposed operations; merging two patches `P` and `overline{P}` yields `𝓝`. Conflicts become residual unmatched fragments after `⊕`‑reduce.

### F3.3 Reversible Steps
Legal `div_n` gates and symmetry isos are invertible; compilers can track exact reversibility. Opposed edits allow safe rollback (`edit ⊕ anti‑edit = 𝓝`).

### F3.4 Tooling
- **IR:** OM‑diagram AST (Vol. D) with phase annotations.
- **Passes:** normalization, legality check/hoisting, centroid preservation check, cyclotomic lift if required.
- **Correctness:** by confluence and semantic functors (Vol. D/E).

---

## F4. Probability & Inference

### F4.1 Interference‑Native Probabilities
Represent factors as predicates in `E_k` with `ℕ_{≥0}[Ξ]` weights. Global state is the `⊕`‑reduced product; probabilities arise after embedding to `ℂ` and Born evaluation (Vol. E). Interference occurs **symbolically** before numeric evaluation.

### F4.2 Constraint Propagation (Non‑signaling)
Message passing over factor graphs preserves marginals on untouched variables by Vol. E non‑signaling. Local updates (character shifts/divisions) commute with marginalization over disjoint scopes.

### F4.3 Algorithms
- **Opposed Belief Propagation (oBP):** messages are character‑bucketed multisets; combine with `⊕`‑reduce; project to probabilities for queries.
- **Variable Elimination:** elimination order chosen to respect legality (to avoid unavailable roots); intermediate factors simplified by `⊕`.
- **Complexity:** as in classical BP/VE with extra bucket ops; `⊕`‑reduce is linear in bucket size.

### F4.4 Examples
- Two‑slit style inference: two coherent factors on a variable produce cancellation at a subset of outcomes (𝓝); downstream marginals reflect non‑signaling invariance.

---

## F5. Implementation Sketches

### F5.1 Core Types
```
-- Character bucket (multiset over Ξ)
newtype Bucket = Map Xi Nat

-- State and factor
newtype State  = Map X Bucket
newtype Factor = Map Scope (Map Assignment Bucket)

-- FFT API
opposedFFT :: State -> Group -> Xi -> State

-- Homology
boundary :: Cell -> [(Face, Xi)]
smithXi  :: Matrix Xi -> SNF

-- Rewriting
normalize :: Diagram -> Diagram

-- Inference
bp :: [Factor] -> Query -> Prob
```

### F5.2 Practical Notes
- Use hash‑maps keyed by `(index, Xi)` for O(1) bucket cancels.
- Precompute inverses `n^{-1} mod p^{k}` per prime power.
- Provide a “cyclotomic lift” mode to enlarge `Ξ` on demand.

---

## F6. Formal Targets (proved in Vol. G)
- **(F‑FFT)**: OpposedFFT correctness and centroid preservation.
- **(F‑HOM)**: Character‑graded homology agrees with classical homology after `Ξ→1` and `𝓝→0` projection; detects additional `𝓝`‑witness invariants.
- **(F‑COMP)**: Rewriter confluence ⇒ compiler determinism.
- **(F‑INF)**: oBP marginals coincide with classical marginals after projection; interference effects appear only in phase‑sensitive queries.

