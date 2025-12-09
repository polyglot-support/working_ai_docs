# Opposed Mathematics — Vol. B: Finite Abelian Geometry & Balanced Subdivision (v1)

> Purpose. Develop the finite-abelian group layer used by Opposed Mathematics (OM): primary decomposition/CRT, legality-aware division, recursive subdivision, and geometric realization (centroid/phase). Interfaces cleanly with Vol. A (cancellation & characters) and Vol. D (categorical packaging).

---

## B0. Preliminaries & Notation
- All groups are finite abelian, written additively.
- `ord(G) := |G|` (group order). For `m ∈ ℕ`, write `Z_m := ℤ/mℤ`.
- Character group of `Z_m`: `\widehat{Z_m} ≅ Z_m` via `k ↦ (x ↦ e^{2πi kx/m})`.
- For integer `n`, the endomorphism `μ_n : G → G`, `x ↦ n x`.
- Legal division by `n` means `μ_n` is bijective on the component under consideration.

---

## B1. Primary Decomposition & CRT

### B1.1 Structure Theorem
Every finite abelian group `G` decomposes into its `p`-primary components
\[
G \cong \bigoplus_{p \in \mathcal{P}} G_{(p)}, \quad G_{(p)} \cong \bigoplus_{i=1}^{r_p} Z_{p^{k_{p,i}}},
\]
where `\mathcal{P}` is the finite set of primes dividing `|G|`.

### B1.2 Endomorphisms Componentwise
For integers `n`, the map `μ_n` acts diagonally:
\[
μ_n\big|_{G_{(p)}} \text{ is invertible } \iff p \nmid n.
\]
Hence `μ_n` is an automorphism of `G` iff `gcd(n, |G|)=1`.

### B1.3 CRT Coordinates
If `G ≅ Z_m` with `m = \prod_p p^{k_p}`, then
\[
Z_m \cong \bigoplus_p Z_{p^{k_p}}
\]
canonically via the Chinese Remainder Theorem (CRT). All constructions below are compatible with this splitting.

### B1.4 Circle Realization (Phase Geometry)
Embed `Z_m` into the unit circle via
\[
\phi_m : Z_m \to S^1,\quad [x] \mapsto e^{2\pi i x / m }.
\]
On a direct sum `\bigoplus_j Z_{m_j}`, use the product embedding and average phases to define centroids componentwise.

---

## B2. Legality & Division

### B2.1 Balanced Division Map (Global Case)
If `gcd(n, |G|)=1`, define
\[
\mathrm{div}_n : G \to G, \quad \mathrm{div}_n(x) := n^{-1} x,
\]
where `n^{-1}` is the inverse of `μ_n` in `End(G)`. This is a group automorphism satisfying `n · \mathrm{div}_n(x)=x`.

### B2.2 Legal Sublayer (Non-Coprime Case)
If `gcd(n,|G|) \neq 1`, define the **legal sublayer**
\[
G^{\langle n \rangle} := nG = \{ n y : y \in G \} = \mathrm{Im}(μ_n).
\]
On `G^{\langle n \rangle}`, `μ_n` has a right-inverse. Choose any section `σ_n : G^{\langle n \rangle} \to G` with `μ_n ∘ σ_n = id` and set
\[
\mathrm{div}_n(x) := σ_n(x) \quad (x \in G^{\langle n \rangle}).
\]
Different sections differ by elements of `\ker(μ_n)`; see invariants below for quantities independent of this choice.

### B2.3 Canonical Sections via CRT
When `G ≅ \bigoplus_p Z_{p^{k_p}}`, define `σ_n` componentwise by solving `n y_p ≡ x_p (mod\ p^{k_p})`:
- If `p \nmid n`, use Hensel/unit inverse: `y_p ≡ n^{-1} x_p`.
- If `p \mid n`, only `x_p` in `n Z_{p^{k_p}}` are admissible; choose minimal-representative preimages.
This yields a canonical `σ_n` once coordinate conventions are fixed.

### B2.4 Centroid Invariance (Phase Geometry)
For cyclic `Z_m` with `gcd(n,m)=1`, the circle embedding satisfies
\[
\frac{1}{m} \sum_{x \in Z_m} \phi_m(x) = 0, \quad \phi_m(\mathrm{div}_n(x)) = \phi_m(x)^{n^{-1}}.
\]
For any finite multiset `A ⊆ Z_m`, the centroid (mean on `S^1`) is invariant under `\mathrm{div}_n`:
\[
\mathrm{Centroid}(\phi_m[A]) = \mathrm{Centroid}(\phi_m[\mathrm{div}_n(A)]).
\]
For non-coprime `n`, restrict to `nZ_m` and apply the same statement to admissible elements.

---

## B3. Recursive Subdivision

### B3.1 Multi-step Legality
Given a sequence `(n_1, n_2, …, n_t)`, define a partial map
\[
\mathrm{Div}_{\vec n} := \mathrm{div}_{n_t} \circ \cdots \circ \mathrm{div}_{n_1}
\]
with domain precisely those elements that remain in the legal sublayer at each step:
\[
\mathrm{Dom}(\mathrm{Div}_{\vec n}) = G^{\langle n_1 \rangle} \cap \mathrm{div}_{n_1}^{-1}\big(G^{\langle n_2 \rangle}\big) \cap \cdots.
\]
By B1.2, legality reduces componentwise to the condition `p \nmid n_j` on the `p`-primary where required.

### B3.2 Arity Growth & Preimage Structure
For cyclic `Z_m` with `gcd(n,m)=1`, the preimage of a point under `μ_n` has exactly `gcd(n,m)=1` elements; more generally on a component `Z_{p^{k}}`, the fiber size of `μ_n` is `p^{\min(k, v_p(n))}`. Recursive subdivision produces regular `n`-gon layers in `S^1` whenever the step is legal.

### B3.3 Invariants Across Recursion
Let `A \subseteq G` finite multiset.
- **Centroid**: invariant under each legal `\mathrm{div}_n` (B2.4), hence under `\mathrm{Div}_{\vec n}`.
- **Componentwise mass**: counting measure in each `G_{(p)}` is preserved up to kernel choices; totals on legal components are invariant.
- **Character moments**: for any character `χ ∈ \widehat{G}` with `χ^n = 1` on the legal component, `\sum_{x∈A} χ(x)` is invariant under `\mathrm{div}_n`.

---

## B4. Geometry & Visualization

### B4.1 n-gon Preimages on `Z_m`
If `gcd(n,m)=1`, for any `x ∈ Z_m` the set `μ_n^{-1}(x)` maps under `\phi_m` to the vertices of a regular `n`-gon centered at `\phi_m(x)`'s `n`th-root locus; repeated subdivision stacks such polygons concentrically.

### B4.2 Phase Tilings Across `p`-Primary Factors
On `G ≅ \bigoplus_p Z_{p^{k_p}}`, legal `n` relative to a subset of primes produces phase tilings only on those components. Visualize as a product of circles where some factors refine (tiling by `n`-gons) while others remain coarse.

### B4.3 Examples
1) `G=Z_{12}`, `n=5`: legal. `5^{-1} ≡ 5 (mod 12)`, so `div_5([7])=[11]`. Preimages form 5-gons on the `S^1` embedding.
2) `G=Z_{12}`, `n=3`: illegal globally; restrict to `3Z_{12}={0,3,6,9}`. Choose canonical preimages mod 12 divided by 3.
3) `G=Z_{8} ⊕ Z_{3}`, `n=6`: legal on the `Z_3` factor, illegal on `Z_8`. Subdivide only the 3-component.

---

## B5. Interfaces to Other Layers
- **Vol. A (Characters & Cancellation).** Characters act multiplicatively alongside subdivision; cancellation `⊕` operates on multisets/images after subdivision without interfering with group addition.
- **Vol. C (IPG).** Path amplitudes valued in `ℕ_Ξ` use `div_n` to implement phase-splitting steps; legality gates which recursive refinements exist.
- **Vol. D (Category).** `div_n` are isomorphisms in the subcategory of components coprime to `n`; elsewhere they are partial isomorphisms with sections.

---

## B6. Algorithms & Complexity (Implementor Notes)
- **CRT Decomposition:** Precompute CRT tables for `m`; O(#primes) per operation.
- **Legality Check:** Factor `|G|` once; legality test per step is O(#primes).
- **Canonical Section:** For `Z_{p^k}`, solve `n y ≡ x (mod p^k)` via Hensel lifting in O(k) arithmetic ops when `p \nmid n`; otherwise check membership in `n Z_{p^k}` and pick minimal representative.
- **Centroid Tracking:** Maintain complex means for each cyclic factor; invariant checks are O(size(A)).

---

## B7. Formal Statements (ready for proof in Vol. G)
- **Theorem (Primewise Legality).** `div_n` exists on `G` iff it exists on every `G_{(p)}`; equivalently `gcd(n, |G|)=1`.
- **Proposition (Centroid Invariance).** For any finite multiset `A ⊆ Z_m`, `Centroid(φ_m[A]) = Centroid(φ_m[div_n(A)])` when `gcd(n,m)=1`; restricted form holds on `n Z_m`.
- **Lemma (Character Moment Preservation).** For any character `χ` with `χ^n = 1` on the legal component, `\sum χ` is invariant under `div_n`.

---

## B8. Example Library (to expand)
- Tables for `Z_m` with `m ≤ 32`: legal `n`, inverses `n^{-1} (mod m)`, canonical sections for non-coprime `n`.
- Visuals: 5-gon on `Z_{12}`, mixed tiling on `Z_8 ⊕ Z_3` for `n=6`.

---

## B9. Appendix: Type Signatures
```
-- Group interface
class FinAb g where
  zero  :: g
  add   :: g -> g -> g
  smul  :: Integer -> g -> g
  order :: g -> Integer

-- Division (partial)
data DivResult g = Div g | Illegal

divN :: Integer -> g -> DivResult g      -- global (coprime) case

-- Legal sublayer projection
inLegal :: Integer -> g -> Bool
canonSection :: Integer -> g -> Maybe g   -- defined iff inLegal n x
```
