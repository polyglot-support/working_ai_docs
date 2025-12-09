# Opposed Mathematics — Vol. A: Foundations & Core Algebra (v1)

> Purpose. Establish the base layer for Opposed Mathematics (OM): exclusory sets with involution, cancellation sum with a neutral nil distinct from ∅, dual containment, probes, oriented magnitudes via character groups, and the classical recovery functors. Provide axioms, immediate lemmas, and minimal worked examples.

---

## A0. Preliminaries & Notation
- Universe of atoms: **U**. Elements of **U** are denoted *u,v,w*.
- Involution: `opp: U → U`, written `opp(u)` or `ū`, with no fixed points.
- For any set `A ⊆ U`, the **anti-image** is `overline(A) := { opp(u) : u ∈ A }`.
- Distinguish `∅` (empty set) from the **nil** `𝓝 := ∅!*` (neutral of cancellation).
- AC-equivalence: equality modulo associativity/commutativity of `⊕` is written `=_{AC}`.

---

## A1. Involutive Opposition on Sets
### Axiom A1 (Involution)
For all `u ∈ U`: `opp(opp(u)) = u` and `opp(u) ≠ u`.

### Definition A1.1 (Exclusory Class `𝔈`)
`𝔈` is the smallest class containing all subsets of `U` and closed under:
1) anti-image `A ↦ overline(A)`,
2) cancellation sum `⊕ : 𝔈 × 𝔈 → 𝔈`,
3) reduction (normal form) `[·] : 𝔈 → 𝔈` (defined in A3).

---

## A2. Cancellation Monoid & Nil
### Axiom A2 (Cancellation Monoid with Nil)
There exists `𝓝 ∈ 𝔈` such that for all `X,Y,Z ∈ 𝔈`:
1) (Neutral) `𝓝 ⊕ X = X ⊕ 𝓝 = X`.
2) (Commutative) `X ⊕ Y = Y ⊕ X`.
3) (Associative) `(X ⊕ Y) ⊕ Z = X ⊕ (Y ⊕ Z)`.
4) (Pairwise Annihilation) `A ⊕ overline(A) = 𝓝` for all `A ⊆ U`.

**Remark.** `𝓝 ≠ ∅`. The empty set is the null *membership* object; `𝓝` is the null *cancellation* result.

---

## A3. Normal Form (Reduction)
### Definition A3 (Reduction / Normal Form)
A rewrite system `R` on `𝔈` repeatedly removes cancellable opposed pairs. The **normal form** `[X]` is the unique representative `=_{AC}` of `X` with no reducible `A ⊕ overline(A)` subexpression.

### Theorem A3.1 (Confluence / Church–Rosser)
`R` is terminating and confluent modulo AC; hence `[·]` is well-defined and unique up to AC-equivalence.

*Proof sketch.* Orient `A ⊕ overline(A) → 𝓝`. Define a multiset measure by total atom count ignoring anti-matched pairs; each rewrite strictly decreases the measure. Local peak overlaps commute by AC, yielding global confluence.

---

## A4. Dual Containment
### Definition A4 (Dual Containment `⊑`)
For `A,B ⊆ U` define
`A ⊑ B` iff `A ⊆ B` and `overline(B) ⊆ overline(A)`.

### Proposition A4.1 (Galois Duality)
For all `A,B ⊆ U`, `A ⊑ B  ⇔  overline(B) ⊑ overline(A)`.

*Proof.* Apply `overline(·)` and involution twice; inclusions reverse accordingly.

---

## A5. Probes on 𝔈
### Definition A5.1 (Quantity Probe `q`)
A homomorphism `q : 𝔈 → ℤ` such that for all `X,Y ∈ 𝔈`:
- `q(X ⊕ Y) = q(X) + q(Y)`,
- `q(overline(A)) = − q(A)` for all `A ⊆ U`,
- `q(𝓝) = 0`.

### Definition A5.2 (Existence Polarity `e`)
A map `e : 𝔈 → {−,0,+}` with
- `e(overline(X)) = − e(X)`,
- `e(∅) = 0`, `e(𝓝) = 0`,
- compatible with reduction: `e([X]) = e(X)`.

**Interpretation.** `𝓝` witnesses a *balanced presence with zero quantity*.

---

## A6. Oriented Magnitudes via Character Groups
### Axiom A6.1 (Character Group)
Let `Ξ` be a finite abelian group (minimally `C₂ = {+,−}`).

### Definition A6.2 (Domain)
`ℕ_Ξ := {0} ∪ (ℕ_{>0} × Ξ)` with elements `(a,χ)` and zero `0`.

### Operations
1) **Addition (same character):** `(a,χ) + (b,χ) = (a+b, χ)`.
2) **Exclusory sum (opposite characters):**
```
(a,+) ⊕ (b,−) =
  (a−b, +)  if a>b
  (b−a, −)  if b>a
  𝓝         if a=b
```
3) **Multiplication:** `(a,χ)·(b,ψ) = (ab, χψ)`.

### Semantics Map
`⟦·⟧ : ℕ_Ξ ∪ {𝓝} → ℤ` given by `⟦0⟧=0`, `⟦(a,+)⟧=a`, `⟦(a,−)⟧=−a`, `⟦𝓝⟧=0`.

**Note.** `𝓝` is neutral for `⊕`, not absorbing for `+` or `·`.

---

## A7. Classical Recovery (Conservativity)
### Functors
- **Phase forgetful:** `F_Ξ : (𝔈, ⊕, overline{·}, 𝓝; Ξ) → (𝔈, ⊕, overline{·}, 𝓝; 1)` collapses characters.
- **Nil collapse:** `C_0 : (𝔈, ⊕, 𝓝) → (Ordinary)` mapping `𝓝 ↦ 0` in additive targets.

### Theorem A7.1 (Conservative Projection)
For any statement `φ` expressible in classical set/group language, if `φ` holds under `F_Ξ ∘ C_0` on an OM-construction, then `φ` holds in the corresponding classical construction. Conversely, OM extends classical objects by extra structure but does not introduce contradictions when projected.

*Idea.* Build an interpretation of OM-terms in classical models by erasing characters and collapsing `𝓝`. Equations lift/restrict functorially.

---

## A8. Worked Micro-Examples
1) **Cancellation:** `{u,v} ⊕ overline({u})  = [ {v} ]`.
2) **Tie to nil:** `(5,+) ⊕ (5,−) = 𝓝`.
3) **Magnitude arithmetic:** `(4,+) ⊕ (6,−) = (2,−)`; `(3,−) + (5,−) = (8,−)`; `(2,−)·(3,−) = (6,+)`.
4) **Polarity probe:** `e((5,+) ⊕ (5,−)) = e(𝓝) = 0` while `q((5,+) ⊕ (5,−))=0`.

---

## A9. Minimal Axiom List (for reference)
- A1 (Involution, no fixed points)
- A2 (Commutative cancellation monoid with nil and annihilation)
- A3 (Confluent, terminating reduction to normal form)
- A4 (Dual containment; Galois duality)
- A6 (Character group; oriented magnitudes)

Derived: probes (A5), semantics map, conservativity (A7).

---

## A10. Interfaces to Other Volumes
- **Vol. B (Finite Abelian Geometry):** supplies primary decomposition, legality-aware division `div_n`, centroid invariance; couples to A6 for phase geometry.
- **Vol. C (IPG):** builds path categories and amplitude functors valued in `ℕ_Ξ` with `⊕`-reduction.
- **Vol. D (Categorical):** packages A2–A3 as a commutative †-Frobenius algebra; adds dagger-compact structure.

---

## A11. Appendix: Lean/Haskell Signatures (sketch)
```
-- Opposition
class Opp a where
  opp :: a -> a

-- Exclusory expressions
data X a = Nil | Atom a | Plus (X a) (X a) | Anti (X a)

-- Character group
class Abelian g where
  (⊗) :: g -> g -> g
  inv :: g -> g

data Xi = Pos | Neg  -- extend to finite abelian groups

data OMN = Z | M Int Xi | Nl  -- 0, (a,χ), 𝓝

oplus :: OMN -> OMN -> OMN
mul   :: OMN -> OMN -> OMN
```

---

## A12. Roadmap (what follows)
- Proof of A3.1 (full confluence) with critical pair analysis.
- Categorical packaging (Vol. D): explicit †-Frobenius data for `⊕`.
- Enriched measures: extend `q` and `e` to functorial probes into ordered groups/effect algebras.

