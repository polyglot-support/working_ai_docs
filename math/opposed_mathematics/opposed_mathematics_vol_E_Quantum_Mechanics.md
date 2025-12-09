# Opposed Mathematics — Vol. E: Quantum Correspondence & Non‑signaling (v1)

> Purpose. Connect Opposed Mathematics (OM) to standard finite‑dimensional quantum theory: pick cyclotomic phases `Ξ = μ_n ⊆ U(1)`, define inner products (Plancherel), derive Born semantics, exhibit superposition/entanglement via character constraints, formalize measurement and non‑signaling, and obtain gate sets from legality‑aware subdivision plus character shifts. Provide examples and targets for soundness/faithfulness.

---

## E0. Setup & Conventions
- Fix finite abelian configuration space `X = ∏_j G_j` (Vol. B) and phase group `Ξ = μ_n = {e^{2πi k/n} : 0≤k<n}`.
- Coefficients: `ℕ_{≥0}[Ξ]` at the deterministic layer (Vol. A/C); complex embedding `ι: Ξ ↪ U(1) ⊂ ℂ` for Hilbert semantics.
- Reduction: `red_⊕` removes opposed contributions to `𝓝` before Hilbert evaluation.

---

## E1. Cyclotomic Phases

### E1.1 Phase Group & Characters
- Take `Ξ = μ_n`. For any finite abelian `G`, its dual `Ĝ = Hom(G, U(1))` is finite; choose an injective homomorphism `ι_n : Ξ ↪ U(1)` and, when needed, embed `Ĝ` phases via the group pairing.

### E1.2 Plancherel Inner Product
For functions `ψ,φ : X → ℂ` (post‑embedding), define
```
⟨ψ, φ⟩ := ∑_{x∈X} ψ(x) · overline{φ(x)}.
```
For multi‑character coefficients, extend linearly after mapping `ℕ_{≥0}[Ξ]` to `ℂ` by `∑ a_χ χ ↦ ∑ a_χ ι(χ)`.

### E1.3 Born Semantics
Given a (normalized) state vector `Ψ ∈ ℂ^{|X|}`, the probability of an event `S ⊆ X` is
```
Pr[S] = ∑_{x∈S} |Ψ(x)|^2.
```
In OM, compute `ψ_det = red_⊕(ψ)` first, then embed to `Ψ = ι∘ψ_det / ||ι∘ψ_det||` (when nonzero). The `𝓝` contributions map to 0 amplitude.

### E1.4 Fourier/Plancherel Equivalence
For any factor `G ≅ ⊕_p Z_{p^{k}}`, the discrete Fourier transform (DFT) over `G` is unitary; characters supply an orthonormal basis. The choice `Ξ = μ_n` with `n` divisible by all `p^{k}` supports exact character phases.

---

## E2. Superposition & Entanglement

### E2.1 Superposition
States add linearly in the group ring before reduction; after embedding, this is standard vector addition. Constructive/destructive interference is determined by `⊕`‑normalization of character labels at each `x∈X`.

### E2.2 Product vs. Constrained States
Let `X = G_A × G_B`. A **product state** has the form `ψ_A ⊗ ψ_B`. A **constrained (EPR‑like) state** is defined by a global relation `R ⊆ X` such as
```
Ψ(x_A,x_B) ∝ 1_R(x_A,x_B) · χ(x_A),   with  R = { (x, −x) : x∈G }
```
for some `χ ∈ Ĝ`. Paths violating `R` cancel under `⊕` (Vol. C), leaving correlations enforced by the constraint.

### E2.3 Example: Bell‑type over Z₂
- Let `G = Z_2`, `Ξ = μ_4`. Define `ψ(0,0)=1·(+), ψ(1,1)=1·(+)`, zero elsewhere. After embedding, `Ψ = (|00⟩ + |11⟩)/√2`.
- Local basis change via red/green spiders (Vol. D) reproduces stabilizer correlations; CHSH‑type settings realized by choosing phase labels in `μ_8` (extension of `Ξ`).

---

## E3. Measurements & Non‑signaling

### E3.1 Local Measurements
- **Character evaluation** on subsystem `A`: for `χ ∈ Ĝ_A`, apply the diagonal unitary `D_χ : |x_A⟩ ↦ χ(x_A)|x_A⟩`, then reduce `⊕`, then compute outcome probabilities by Born’s rule. Projective measurements are implemented by the SCFA counit/unit (Vol. D) in the chosen basis.

### E3.2 Marginals & Invariance (Non‑signaling)
For `X = A×B`, any local operation `R_A` built from: legal divisions on `A`, character shifts on `A`, and symmetry quotients factoring only through `A`, satisfies
```
Marg_B( red_⊕( (R_A ⊗ id_B) ψ ) ) = Marg_B( red_⊕( ψ ) ).
```
*Sketch.* Each generator preserves the `B`‑marginal: divisions permute phases within the `A` fiber; character shifts multiply by unit‑modulus phases; quotients sum over `A`‑cosets but `⊕`‑cancellation occurs inside the fiber, leaving the `B` sum unchanged. Linearity gives the general case.

### E3.3 Post‑selection & Conditioning
Conditioning on a local measurement outcome corresponds to restricting `ψ` to a subpredicate in `E_k` and renormalizing. Correlations may change, but the *a priori* `B` marginal prior to conditioning is invariant (no signaling).

---

## E4. Gate Sets via Legality

### E4.1 Balanced Subdivision as Unitaries
If `gcd(n, |G_j|)=1` on a factor `G_j`, `div_n` is a permutation of `G_j` (Vol. B) and hence a unitary on `ℂ^{|G_j|}`. In diagrams, `DivGate(n)` is invertible with inverse `DivGate(n^{-1})`.

### E4.2 Phase Gates
Character shifts `χ ∈ Ĝ_j` act as diagonal unitaries on `G_j`. The set of all such shifts forms an abelian group of commuting phase gates.

### E4.3 Generating Fragments
- **Stabilizer fragment (qubit‑like):** with `G=Z_2`, `Ξ=μ_4`, the red/green SCFAs, `DivGate(−1)` (swap), and phase gates generate the Clifford group; ZX‑on‑OM rules suffice for completeness in this fragment (Vol. D).
- **Cyclotomic extensions:** with `Ξ=μ_{2^k}` and `G=Z_{2^k}`, `DivGate(2^{±1})` and primitive `μ_{2^k}` phases approximate dense unitary sets (with additional mixing gates coming from CRT across factors).

### E4.4 Toward Full QM
Dense `Ξ ⊆ U(1)` plus CRT‑mixing across factors yields universal gate sets on large composite systems; non‑Clifford phases (e.g., `T`‑like gates via `μ_8`) extend beyond stabilizers. Legality conditions act as arithmetic **admissibility constraints** for which roots/splits (hence unitaries) exist natively.

---

## E5. Worked Examples
1) **Two‑qubit Clifford:** derive `H, S, CNOT` from red/green spiders (Vol. D), character shifts in `μ_4`, and group addition maps; verify `HZH=X` and entangling action of CNOT.
2) **CRT‑composed gate:** on `Z_8 ⊕ Z_3`, `DivGate(5)` acts as `DivGate(5 mod 8)` on the 8‑cycle and `DivGate(2)` on the 3‑cycle; both unitary; compose with phase shifts for mixed‑radix QFT steps.
3) **Non‑signaling demo:** start with the Bell‑type state; apply any `A`‑local sequence of `DivGate`s and character shifts; compute `B` marginal before/after—identical.

---

## E6. Formal Statements (proved in Vol. G)
- **(E‑Planch)**: The embedding `ι ∘ red_⊕` followed by Plancherel yields a valid inner product space; Born probabilities agree with standard complex amplitudes.
- **(E‑NS)**: Non‑signaling for local operations generated by legal divisions, character shifts, and appropriate quotients.
- **(E‑Cliff)**: For `Ξ=μ_4`, the OM ZX‑fragment is sound and complete for stabilizer circuits under the semantics functor `Q` (Vol. D).
- **(E‑Univ)**: With dense cyclotomic phases and CRT mixing, the gate set generated by legal `DivGate`s and phase gates is universal on `ℂ^{|X|}` (under standard number‑theoretic conditions).

---

## E7. Implementation Notes
- Normalize (`red_⊕`) before numerical evaluation; track `𝓝` explicitly to avoid spurious amplitude leakage.
- Precompute legality tables per factor; map `DivGate(n)` to permutations (unitaries) when coprime.
- Use sparse complex vectors with phase hashing keyed by `Ξ` elements for efficient simulation.

