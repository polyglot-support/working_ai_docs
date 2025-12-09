# Opposed Mathematics — Vol. C: Interference Path Geometry (IPG) (v1)

> Purpose. Define an interference-native calculus over finite abelian configuration spaces with characters and cancellation. States are path-summed amplitudes valued in `ℕ_{≥0}[Ξ]` with `⊕`-reduction at coincident endpoints. We introduce the hierarchy of minimal logics `E_k`, recursive cascades (legal division, symmetry quotients, character shifts), invariants (centroid, non-signaling marginals, opposition mass), and split vector geometry (deterministic/Hilbert completions).

---

## C0. Preliminaries
- Fix a finite index set of subsystems `J`. For each `j ∈ J`, let `G_j` be a finite abelian group (Vol. B). The configuration space is `X := ∏_{j∈J} G_j`.
- Characters: a finite abelian phase group `Ξ` (Vol. A), optionally embedded in roots of unity.
- Coefficients: the `Ξ`-group ring with nonnegative integer coefficients, `ℕ_{≥0}[Ξ]` (formal sums `∑_χ a_χ · χ`, `a_χ ∈ ℕ_{≥0}`).
- Cancellation: `⊕` with neutral `𝓝` (Vol. A). Reduction to normal form removes opposed contributions.

---

## C1. States, Paths, and Amplitudes

### C1.1 Path Category `Path(X)`
- **Objects:** points of `X`.
- **Morphisms (paths):** finite composable words of generators `γ : x → y`. Composition by concatenation; identities are empty paths.
- **Monoidal product:** cartesian on objects (tupling), concatenation on paths; used for parallel composition.

### C1.2 Amplitude Functor
A strict monoidal functor `A : Path(X) → ℕ_{≥0}[Ξ]` such that
- `A(γ₂ ∘ γ₁) = A(γ₂) · A(γ₁)` (multiplicative along time),
- `A(γ ⊗ γ') = A(γ) ⊗ A(γ')` (separable across disjoint subsystems),
- base weights for generators are chosen from `Ξ` (phase labels) with unit coefficient.

### C1.3 Endpoint Amplitudes & Interference
For each `y ∈ X`, the raw endpoint amplitude is
```
Â(y) :=  ⨁_{γ : *→y}  A(γ)     (formal ⊕-sum over all paths ending at y)
```
where `*` encodes the chosen initial condition(s). The **state** is the reduced map
```
ψ(y) := red_⊕(Â(y)) ∈ ℕ_{≥0}[Ξ] ∪ {𝓝}.
```
Opposed phases at `y` cancel to `𝓝`; aligned phases add.

### C1.4 Observables (Character Evaluations)
For `θ ∈ Ξ` (or a character `χ ∈ Ẋ := Hom(X, U(1))`), define a linear functional
```
M_θ(f) := ⟨θ, f⟩ = ∑_{χ} a_χ · ⟨θ, χ⟩,   with ⟨θ, χ⟩ := 1 if θ=χ else 0.
```
More generally, for `χ ∈ Ẋ`, let `M_χ(f) := ∑_x χ(x) · f(x)` after projecting coefficients to complex phases via the Ξ→U(1) embedding.

---

## C2. Hierarchy of Minimal Logic

### C2.1 Effect Algebras `E_k`
For each arity `k ≥ 0`, define the effect algebra
```
E_k := (Predicates on X^k with values in ℕ_{≥0}[Ξ] ∪ {𝓝}, ⊕, overline{·}, 𝓝)
```
with pointwise `⊕` followed by reduction. Predicates are finitely supported unless stated otherwise.

### C2.2 Inclusions and Depth
- **Inclusion:** curry a `(k)`-ary predicate to `(k+1)`-ary by ignoring the new coordinate (or tensoring with a neutral test). This yields embeddings `E_k ↪ E_{k+1}` preserving `⊕` and `𝓝`.
- **Interaction (entanglement) depth:** for a state `ψ` on `X^k`, define `depth(ψ)` as the minimal `k'` such that the image of `ψ` in `E_{k'}` factorizes across a nontrivial partition after `⊕`-reduction. Nonfactorizable states have depth ≥ 2.

### C2.3 Composition Rules
`E_k` is closed under conjunction-like composition given by convolution over shared variables and `⊕`-reduction. Associative/commutative up to renaming and reduction.

---

## C3. Cascades & Recursion

### C3.1 Operators
1) **Legal division:** apply `div_n` (Vol. B) componentwise to applicable `G_j` factors; phases propagate, characters pass through unchanged.
2) **Symmetry quotients:** collapse along a subgroup `H ≤ X` by identifying `x ~ x+h`; only paths respecting the quotient survive `⊕`.
3) **Character shifts:** multiply amplitudes by a fixed `ξ ∈ Ξ` (global phase) or by a character `χ ∈ Ẋ` (coordinate-dependent phase).

### C3.2 Cascade Map
Given a sequence of operators `R_1, …, R_t`, define
```
R := R_t ∘ ··· ∘ R_1,     ψ ↦ red_⊕( R(ψ) ).
```
Domain is restricted by legality gates (for divisions) and quotient compatibility.

### C3.3 Invariants
- **Centroid invariance:** the circular centroid in each cyclic factor is preserved by legal divisions (Vol. B) and by character shifts of unit modulus.
- **Non-signaling marginals:** for disjoint factorization `X = A × B` and any local operation on `A` composed of the operators above,
```
Marg_B( red_⊕( R_A ⊗ id_B (ψ) ) ) = Marg_B( red_⊕( ψ ) ).
```
- **Opposition mass monotonicity:** the total coefficient sum `∑_χ a_χ` is nonincreasing under pure cancellations; character shifts preserve it; legal division preserves it on legal components.

### C3.4 Fixed Points & Self-Similarity
States invariant under a step (e.g., `div_n` plus a matching character shift) form fixed points; cascades may converge to self-similar interference patterns (fractal tilings in phase geometry).

---

## C4. Split Vector Geometry

### C4.1 Deterministic Space `V_det`
`V_det := { finitely supported ψ : X → ℕ_{≥0}[Ξ] } / ≡_⊕`, with `⊕`-normalization quotienting opposed pairs to `𝓝`.

### C4.2 Hilbert-like Completion `H_prob`
Embed `Ξ` into `U(1)` and extend to complex coefficients. Define an inner product via character pairing:
```
⟨ψ, φ⟩ := ∑_{x∈X}  ⟨ψ(x), φ(x)⟩_Ξ,   with  ⟨∑ a_χ χ, ∑ b_η η⟩_Ξ := ∑_χ a_χ · \overline{b_χ}.
```
Complete the span to get `H_prob` (ℓ² over X with character coordinates). The Born-style probability of an event is the squared norm after projecting coefficients along the Ξ→U(1) embedding.

### C4.3 Limit Theorems
- **Cascade martingale:** for a filtration given by symmetry quotients, the sequence of conditional expectations of `ψ` is a martingale in `H_prob`; almost-sure and L² convergence follow under boundedness.
- **Interference law of large numbers:** under independent character shifts with zero mean, normalized sums converge to `𝓝` in `V_det` and to zero vector in `H_prob`.

---

## C5. Worked Examples
1) **Two-site EPR over `Z_2`:** `X = Z_2 × Z_2`, `Ξ = μ_4`. Define `ψ(0,0)=1·(+), ψ(1,1)=1·(+)`, zero elsewhere. Local character evaluations in conjugate bases yield perfectly correlated outcomes with invariant marginals (non-signaling).
2) **Legal split on `Z_{12}`:** apply `div_3` to a distribution supported on `3Z_{12}`; visualize preimages as 3-gons; centroid preserved.
3) **Symmetry quotient:** on `Z_4 × Z_4`, quotient by diagonal `⟨(1,1)⟩`; only paths respecting `x−y ≡ const` survive; entangled support appears as a single coset class.

---

## C6. Interfaces & Implementation Notes
- **Interfaces:**
  - Vol. A: `⊕`-normalization and character arithmetic.
  - Vol. B: `div_n` legality and geometric invariants.
  - Vol. D: dagger-compact packaging; `⊕` as a commutative †-Frobenius algebra; diagrammatic rewrites correspond to `⊕`-normalization.
- **Runtime:**
  - Represent `ψ` as sparse maps `x ↦ (a_χ)`; normalization via hash-based cancel of `(χ, χ^{-1})` pairs.
  - Division uses CRT-backed canonical sections.
  - Non-signaling checks use precomputed marginals and invariance lemmas.

---

## C7. Formal Statements (to prove in Vol. G)
- **(C-LIN)**: `A` is strict monoidal; endpoint reduction defines a well-posed state.
- **(C-NS)**: Non-signaling marginals for local cascades on disjoint factors.
- **(C-FP)**: Fixed-point characterization for combined `div_n` + character shift operators.
- **(C-MART)**: Martingale convergence for cascade filtrations in `H_prob`.

---

## C8. Type Signatures (sketch)
```
-- State over X
newtype State = Map X (MultiXi)   -- MultiXi = ℕ_{≥0}[Ξ]

-- Core ops
oplusReduce   :: State -> State
charShift     :: Xi -> State -> State
applyDivLegal :: Integer -> State -> State  -- partial: no-op outside legal sublayer
symmQuotient  :: Subgroup X -> State -> State

-- Observables / measurement
measureXi     :: Xi -> State -> Integer
measureChar   :: (X -> Complex) -> State -> Complex

-- Marginals
marginal      :: (X -> Y) -> State -> Map Y MultiXi
```

