# DORM — Dual Orthogonal Recursive Manifold (v0.1)

*A geometric extension layered on top of IPGA / NF‑IPGA, modeling “manifold of manifold pointers” and dual space↔time recursion with holographic mixing. This is separate from the IPGA docs, but compatible in spirit and tooling.*

---

## 1) Concept
- **Shells:** Reality is organized in nested shells (levels) `k = 0..L−1`. Each shell carries *dual bases*: space and time components for each spatial axis. For 3 axes this gives a 6‑vector per shell: `x_k = [Sx,Sy,Sz, Tx,Ty,Tz]`.
- **Pointers:** Between shells, information is transported by **orthogonal pointer maps** `P_k : x_k → x_{k+1}`. These mix:
  - **Within axes** (2D rational rotations on each (S_i, T_i) pair), and
  - **Across axes** (3D rational rotations on the S‑triplet and T‑triplet separately).
- **Dual compatibility:** Each shell enforces **space⊥time**: the dot product `⟨S_k, T_k⟩ = 0`. This models the “pairwise orthogonalization” you described.
- **Holographic mixing:** Cross‑axis rotations encode angular redundancy—information from inner shells is redundantly projected into outer shells via `P_k`.

---

## 2) Mathematics
- **State:** `x = (x_0, …, x_{L−1}) ∈ ℚ^{6L}` (exact rationals).
- **Constraints as quadratic energy:**
  - **Pointer coherence:** `r_k := x_{k+1} − P_k x_k` for `k = 0..L−2`.
  - **Orthogonality:** `o_k := ⟨S_k, T_k⟩ = 0` for each shell.
- **Global energy (exact):**
```
E(x) := ∑_k ‖r_k‖²  +  γ ∑_k o_k²  =  xᵀ Q x,   Q = ∑ (A_iᵀ A_i).
```
Here `A_i` are the linear rows encoding each residual; `γ>0` weights orthogonality.
- **Diffusion / solver:** Gradient descent with a *contractive* linear step `x ← (I − s Q) x` (with small rational `s`) monotonically decreases `E` and converges to harmonic configurations.
- **Rational orthogonals:** We use Pythagorean triples to build 2D/3D **rational orthogonal** rotations, so everything stays in `ℚ`.

---

## 3) Operations
- **Flip (space↔time):** Swapping roles is represented by multiplying by `J = diag(0,I; I,0)` per axis or per shell; `J²=I`.
- **Compose pointers:** Total pointer from level `i` to `j` is the product `P_{j−1}⋯P_i` (still rational orthogonal).
- **Holographic projection:** Information at inner shells appears at outer shells via `P_k` compositions; angular redundancy lives in the cross‑axis components.

---

## 4) Invariants & Quantities
- **Orthogonality residuals:** `o_k = ⟨S_k, T_k⟩`.
- **Pointer residuals:** `‖r_k‖²` across levels.
- **Energy decay:** Monotone under diffusion: `E_{t+1} ≤ E_t`.
- **Gauge:** Rotations that act identically on both triplets commute with orthogonality; their effect can be tracked as a symmetry.

---

## 5) Python API (mini‑lib)
- `DORM(levels=3, gamma=1)` — build shell stack and default rational rotations `R (2×2), U (3×3)`.
- `pointer_matrices()` — return `(R,U)` and assembled `P_k`.
- `energy(x)` — exact `Fraction` energy.
- `step(x, s)` — one diffusion step with rational `s`.
- Helpers to compute per‑shell orthogonality and per‑link pointer residuals.

---

## 6) Demo Plan (what the notebook runs)
1) Show the rational rotation blocks `R` and `U`.
2) Initialize `x` with small rational seeds at `L=3` shells.
3) Run 20 diffusion steps; display energy decay (exact fractions and floats).
4) Report final orthogonality residuals `o_k` and pointer residual norms `‖r_k‖²`.

---

## 7) Outlook & Links to IPGA
- **Analogy to IPGA:** `Q` plays the role of a Laplacian on the pointer graph; diffusion is a harmonic projector.
- **Bridging NF‑IPGA:** Assign each shell to a place layer (finite/arch) and couple exponents to DORM states via linear maps; study how spectral gaps interact.
- **Physics hook:** Treat `S_k/T_k` as dual solvability bases; flipping via `J` leaves `E` invariant → “computation‑invariance” across space/time interpretations.

---

## 8) Boundary‑conditioned one‑shot solve (Dirichlet & Neumann/Target)
**Goal.** Solve the pointer‑coherence problem in a single global step, then enforce exact S/T orthogonality via exponent‑space projection.

### Setup
- Shell states: `x_k = [d^S_k; d^T_k] ∈ ℚ^{2m}` on IPGA edge space (vertical ⊕ mirror), `k=0..L−1`.
- Pointer: `x_{k+1} ≈ P x_k`, with `P = (U ⊕ U) · (R ⊕ … ⊕ R)` rational‑orthogonal (3‑4‑5 rotations within S/T per edge, and across edges in disjoint pairs).
- Residual per link: `r_k := x_{k+1} − P x_k`.
- Metric on signatures: `G := diag(L_W, L_W)` where `L_W = Mᵀ W M` is the IPGA weighted Laplacian; energy `‖r_k‖_G² = r_kᵀ G r_k`.

### Quadratic program (exact)
Minimize the pointer energy
```
min_x  ½ Σ_{k=0}^{L−2} ‖x_{k+1} − P x_k‖_G² = ½ xᵀ H x,   H = Σ R_kᵀ G R_k,
```
subject to linear boundary conditions:
- **Dirichlet at shell 0:** `x_0 = x⁰` (anchored initial dual signatures)
- **Either** **Neumann at top:** `r_{L−2} = 0` (free end), **or** **Target exponents at top:**
  `E_top x_{L−1} = [e^S_target; e^T_target]` with `E_top = diag(M, M)`.

We assemble a single **KKT system**
```
[ H   Cᵀ ] [x] = [0]
[ C    0 ] [λ]   [b]
```
with exact rational arithmetic and solve by Gauss–Jordan elimination. This yields the unique minimizer under the chosen boundary conditions.

### Exact S/T orthogonality (one‑step projection)
After solving for `x`, we enforce, per shell, the exact exponent orthogonality
```
⟨e^S_k, e^T_k⟩_W = 0,
```
by a single Gram–Schmidt update in exponent space: `d^T_k ← d^T_k − α·R e^S_k`, where `α=⟨e^T_k,e^S_k⟩_W/⟨e^S_k,e^S_k⟩_W` and `R` is the canonical right‑inverse of `M` (vertical cumulative sums, mirrors zero). This maintains IPGA structure and achieves the “geometric interference” solve in one pass.

### What the notebook runs
- Builds `H`, Dirichlet constraints from a neutral ratio seed at `k=0`, and two alternatives at the top shell:
  1) **Neumann** (`r_{L−2}=0`),
  2) **Target exponents** (e.g., `(3/5)` for S, `(2/7)` for T).
- Solves exactly via KKT, then reports **per‑shell inner products** `⟨e^S,e^T⟩_W` and **energies** before/after the orthogonalization step, plus **pointer residual norms** `‖r_k‖_G²`.

**Remark.** The pointer energy is quadratic/convex; boundary constraints are linear; the S/T orthogonality is enforced *exactly* afterward by a single rational projection (no iterative descent). This realizes the intended one‑step “geometric interference” solver.

*End of v0.1.*

