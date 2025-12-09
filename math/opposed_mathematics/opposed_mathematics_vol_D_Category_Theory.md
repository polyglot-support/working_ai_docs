# Opposed Mathematics — Vol. D: Category Theory & Diagrammatics (v1)

> Purpose. Package Opposed Mathematics (OM) into a dagger-symmetric monoidal category (†-SMC) with a commutative †-Frobenius algebra for cancellation, a phase-spider calculus parameterized by the character group Ξ, and functors to classical and quantum semantics. Provide rewrite rules, soundness targets, and interfaces to other volumes.

---

## D0. Preliminaries & Notation
- Base data from Vol. A–C: cancellation `(⊕, overline{·}, 𝓝)`, character group `Ξ`, finite abelian groups from Vol. B, and IPG states from Vol. C.
- We write `⊗` for monoidal product, `;` (or `∘`) for composition, `†` for dagger, and `I` for the tensor unit.

---

## D1. Dagger–Symmetric Monoidal Scaffold

### D1.1 Category `OMCat`
- **Objects (wires):** finite products of **factors** of two kinds:
  1) Group factors `G` (finite abelian groups, possibly decomposed primewise),
  2) Character factors `Ξ^k` (finite phase registers).
  Write a generic object as `A ::= G₁ ⊗ ··· ⊗ G_m ⊗ Ξ^{k}`.

- **Morphisms:** **opposed maps** `(f, σ)` where `f` is a relation/map built from Vol. B/C primitives (group homomorphisms, legal division partial isos with sections, symmetry quotients/inclusions) and `σ` multiplies by a character-valued phase (Vol. C character shifts). Composition is relational composition with multiplicative phase accumulation, followed by pointwise `⊕`-reduction on multiplicities when applicable.

### D1.2 Monoidal Structure
- Tensor on objects: juxtaposition of factors; on morphisms: block product `(f⊗g, σ⊗τ)`.
- **Unit:** `I` is the empty tensor (scalars = closed diagrams), identified with `Ξ`-graded natural numbers modulo `⊕` (Vol. A oriented magnitudes).
- **Symmetry:** standard wire swap `β_{A,B}: A⊗B → B⊗A`.

### D1.3 Dagger
- On morphisms `(f, σ)`: the dagger is the relational converse with conjugate phase: `(f, σ)^{†} := (f^{⊤}, σ^{-1})`. On partial isos (legal divisions), `†` is the corresponding section.
- Check: `(g∘f)^{†} = f^{†}∘g^{†}`, `(f⊗g)^{†} = f^{†}⊗g^{†}`, and `f^{††}=f`.

### D1.4 Duals (Compact Structure)
- For each factor `A`, choose a dual `A*` with unit/counit cups/caps given by the diagonal and evaluation against the group-character pairing. This yields a **dagger-compact** structure enabling string-diagram bending.

---

## D2. Frobenius Algebra for Cancellation

### D2.1 Object and Structure Maps
Pick an object `C` (a single wire that stores an exclusory multiset over atoms or endpoints) and equip it with:
- **Multiplication** `μ : C⊗C → C` (cancellation sum),
- **Unit** `η : I → C` (inject nil `𝓝`),
- **Comultiplication** `δ : C → C⊗C` (copy/split),
- **Counit** `ε : C → I` (delete/observe),
subject to the following.

### D2.2 Algebraic Laws
- **Commutative Frobenius:** `(C, μ,η,δ,ε)` satisfies
  - (Associative, Unital) `(μ∘(μ⊗id)) = (μ∘(id⊗μ))`, `μ∘(η⊗id) = id = μ∘(id⊗η)`.
  - (Coassociative, Counital) `( (id⊗δ)∘δ ) = ( (δ⊗id)∘δ )`, `(ε⊗id)∘δ = id = (id⊗ε)∘δ`.
  - (Frobenius law) `(δ∘μ) = (μ⊗id)∘(id⊗δ) = (id⊗μ)∘(δ⊗id)`.
  - (Commutativity) `μ∘β = μ`, `(β∘δ) = δ`.
- **†-structure:** `μ^{†} = δ`, `η^{†} = ε` (special commutative †-Frobenius algebra, SCFA).

### D2.3 Cancellation Axiom (Opposition)
- There exists an involution `inv : C → C` modeling `overline{·}` such that
  - `μ ∘ (id⊗inv) ∘ Δ_e = η ∘ !` on *elementary opposed pairs*, where `Δ_e` injects a pair `(A, overline(A))` and `! : I → I` is the unique scalar. Diagrammatically: **opposed pair annihilates to nil**.
- **Normal-form confluence:** add a rewriting rule `•—• → ◦` (two spiders with opposite phases fuse to nil node), and prove Church–Rosser in Vol. G.

### D2.4 Scalar Semantics
- Closed diagrams in `OMCat` evaluate to `Ξ`-graded naturals modulo `⊕`; the empty diagram is `η;ε`.

---

## D3. Phase Spiders & ZX-on-OM

### D3.1 Phase Spiders
- A **phase spider** is a connected `C`-spider with a label `θ ∈ Ξ` (or `θ` a character of the underlying group factor) that multiplies its scalars by `θ`.
- **Fusion:** two spiders of the same color add phases: `Spider(θ) ∘ Spider(φ) = Spider(θ·φ)`.
- **Opposition:** `Spider(θ) ∘ Spider(θ^{-1}) = Spider(1)`; if the legs pair into an opposed configuration, the result reduces to `𝓝` via D2.3.

### D3.2 Mixed Bases (Green/Red)
- Introduce two complementary SCFAs on each group factor (e.g., Z/X bases for `Z_m`), both living inside `OMCat`:
  - **Green spiders (Z):** copy computational basis, phases live in `Ξ`.
  - **Red spiders (X):** copy Fourier basis via Vol. B/C character pairing.
- **Bialgebra laws** hold between the complementary SCFAs, yielding a ZX-like calculus with phase labels in `Ξ`.

### D3.3 Rewrite Rules (Core)
1) **Spider fusion:** same color ⇒ fuse, multiply phases.
2) **Identity/loop:** removing trivial loops yields scalar factors consistent with Vol. C inner product.
3) **Opposed cancellation:** spider with `θ` meeting spider with `θ^{-1}` on all matched legs reduces to `𝓝`.
4) **Hopf/Copy rules:** standard ZX rules adapted to group factors (copying characters, distributing phases).

### D3.4 Confluence = Normal-Form Uniqueness
- The rewrite system above is terminating and confluent modulo monoidal axioms (Vol. G proof). Normal forms coincide with `⊕`-reduced algebraic normal forms from Vol. A/C.

---

## D4. Classical & Quantum Functors

### D4.1 Forgetful Functors (Classical)
- `U₀ : OMCat → Set/Rel` (erase Ξ, collapse `𝓝→0`, forget dagger): sends objects to underlying sets, morphisms to relations/maps. **Conservative** on classical equalities (Vol. G).
- `U_{Ab} : OMCat → Ab` (additive): send group factors to abelian groups, spiders to additive operations; opposition becomes additive inverse only after projection.

### D4.2 Quantum Semantics (Finite-Dim Hilb)
- Choose an embedding `Ξ ↪ U(1)` and `G ↦ ℂ^{|G|}` with computational basis. Define
  - `⟦C⟧` as the standard SCFA on `ℂ^{|G|}` (copy/delete computational basis),
  - phase spiders as diagonal unitaries with eigenvalues in `Ξ`,
  - red spiders as the Fourier-dual SCFA.
- **Functor** `Q : OMCat → FdHilb` is †-monoidal, sending cancellation rewrites to equalities of linear maps; opposed annihilation models destructive interference. Stabilizer fragment recovers standard ZX when `Ξ=μ_4`.

### D4.3 Soundness & Faithfulness Targets
- **Soundness:** every diagram equality provable in OMCat holds in `FdHilb` under `Q`.
- **Faithfulness (fragment):** on the stabilizer fragment (spiders with phases in `μ_4` and legal divisions corresponding to Clifford generators), `Q` is faithful up to global phase and `𝓝`-collapse.

---

## D5. Interfaces & Examples
- **Interfaces:**
  - Vol. A: `⊕` and `𝓝` realized as SCFA; oriented magnitudes appear as scalars.
  - Vol. B: legal divisions become partial isos/gates; CRT guides factorwise semantics.
  - Vol. C: path amplitudes compose as string diagrams; non-signaling corresponds to yanking/counit laws.

- **Examples:**
  1) **Hadamard/DFT on `Z_2`:** red/green spiders with `Ξ=μ_4` derive `H^2=I`, `HZH=X`.
  2) **Opposed annihilation:** a 2-leg spider with `θ` meeting one with `θ^{-1}` reduces to `𝓝` (empty scalar) in OMCat; maps to zero vector contribution in `FdHilb`.
  3) **Legal division gate:** a gate labeled `n^{-1}` exists exactly when `gcd(n,|G|)=1`; becomes a permutation/unitary in `FdHilb`.

---

## D6. Formal Statements (proved in Vol. G)
- **(D-†SMC)**: `OMCat` is a dagger-symmetric monoidal category with duals.
- **(D-Frob)**: `(C, μ,η,δ,ε)` forms a commutative special †-Frobenius algebra.
- **(D-ZX)**: The phase-spider rewrite system is terminating & confluent modulo SMC axioms; normal forms agree with Vol. A/C reductions.
- **(D-SND)**: `Q` is †-monoidal and sound; faithfulness on stabilizer fragment with `Ξ=μ_4`.

---

## D7. Implementation Sketch (Rewriter)
```
-- Core diagram AST
data Obj = G Factor | Xi Int | I

data Morph
  = Id Obj
  | Compose Morph Morph
  | Tensor  Morph Morph
  | Spider  { color :: Color, phase :: Xi, legsIn :: Int, legsOut :: Int }
  | Cancel  -- μ
  | Copy    -- δ
  | Unit    -- η
  | Counit  -- ε
  | Swap Obj Obj
  | DivGate Integer  -- legal n^{-1} (partial)

rewrite :: Morph -> Morph  -- applies (fusion, Hopf, oppose-cancel, etc.)
```

---

## D8. Roadmap
- Prove (D-†SMC) and (D-Frob) rigorously.
- Establish bialgebra relations between complementary SCFAs and lift ZX completeness theorems to the OM setting for the stabilizer fragment.
- Extend `Q` to dense cyclotomic phases `Ξ ⊆ U(1)` and analyze completeness scopes.
