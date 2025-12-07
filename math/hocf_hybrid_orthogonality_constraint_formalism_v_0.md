# Hybrid Orthogonality Constraint Formalism (v0.1)

*A compact framework for orthogonality-driven constraints, anti-constraints, and their interactions, with LCM/CRT-scalable enforcement.*

---

## 0. Preliminaries & Notation

- Let **G** be a compact abelian group with Haar probability measure. Typical choices below:
  - Cyclic: \(C_M=\mathbb Z/M\mathbb Z\)
  - Boolean: \((\mathbb Z_2)^k\)
  - Finite field additive groups: \((\mathbb F_{q^m},+)\)
  - Polynomial quotients: \(k[x]/(M(x))\)
  - Direct products / tensor products thereof.
- Signal/state is a **positive measure** or nonnegative function \(\mu\in L^1(G)\cap L^2(G)\). Inner product \(\langle f,g\rangle=\int_G f\,\overline g\,d\mathrm{Haar}\).
- **Characters** \(\widehat G\): continuous homomorphisms \(\chi:G\to S^1\). Fourier coefficients \(\widehat{\mu}(\chi)=\int_G \chi\,d\mu\).
- A **constraint set** \(\mathcal C\subset L^2(G)\) is a closed linear subspace (or an affine translate thereof) specified spectrally (via characters) or geometrically (via subgroup structure).
- The **anti-constraint** of \(\mathcal C\) is the orthogonal complement \(\mathcal C^\perp\). Enforcing \(\mathcal C\) means projecting onto \(\mathcal C\); dumping correlation means projecting onto \(\mathcal C^\perp\).
- **Protected modes** \(T\subset\widehat G\): a set of characters whose Fourier coefficients must remain exactly preserved by updates.
- **Idempotent coset averages**: for subgroup \(H\le G\), the uniform measure \(m_H\) satisfies \(m_H\!*\,m_H=m_H\), and its Fourier transform is the indicator of \(H^\perp=\{\chi\in\widehat G: \chi|_H\equiv 1\}\).
- **Scaling by LCM/CRT**: refine a modulus (integer or polynomial) by \(M\mapsto \mathrm{lcm}(M,M')\). All constructions below embed functorially through CRT.

---

## 1. Orthogonality Sources (atoms & projectors)

Each scheme gives a mutually orthogonal family and a projector calculus that is positive-preserving (via convolution with idempotents or subgroup averages). All support LCM/CRT refinement.

### 1.1 Additive characters on cycles (DFT on \(C_M\))
- Characters: \(\chi_k(x)=e^{2\pi i kx/M}\), \(k\in\mathbb Z_M\). Orthogonality: \(\sum_{x\bmod M}\chi_k\overline{\chi_\ell}=0\) for \(k\neq\ell\).
- Projector onto a frequency set \(S\subset\mathbb Z_M\): \(P_S f=\sum_{k\in S}\widehat f(k)\,\chi_k\).
- Subgroup idempotents: for divisor \(d\mid M\), uniform average on \(d\mathbb Z_M\) kills all characters with \(k\not\equiv 0\bmod M/d\).
- LCM lift: \(M\leadsto L=\mathrm{lcm}(M,M')\); characters embed by index lifting; idempotents lift by matching divisibility classes.

### 1.2 Walsh–Hadamard characters on \((\mathbb Z_2)^k\)
- Characters: \(\chi_u(x)=(-1)^{u\cdot x}\). Orthogonality via Hamming inner product.
- Projectors via FWHT masks; idempotents correspond to averaging over linear subspaces of \((\mathbb Z_2)^k\).
- Lifting: increase dimension \(k\to k'\) by appending axes; tensor with 1.1 on \(C_M\) for hybrid bases.

### 1.3 Subgroup-idempotent (coset-uniform) measures
- For \(H\le G\), \(m_H\) is a positive projector in time-domain and frequency-domain **selector**: \(\widehat{m_H}=\mathbf 1_{H^\perp}\).
- Use \(m_H\) to annihilate unwanted frequencies while preserving positivity and mass.
- Lifting: if \(G\hookrightarrow G'\) via CRT, choose \(H'\) with \((H')^\perp\) the pullback of \(H^\perp\).

### 1.4 Dirichlet (multiplicative) characters on \((\mathbb Z/n)^{\times}\)
- Orthogonality on the unit group; extend to \(C_n\) by zero-extension or via semidirect products when needed.
- Lifting: characters lift from conductor \(f\) to any \(n\) with \(f\mid n\); cross-modulus composition via CRT on units.

### 1.5 Ramanujan atoms \(c_q(\cdot)\)
- Integer-valued, orthogonal across distinct \(q\mid N\) on \(C_N\). Decompose arithmetic textures with exact integer combinatorics.
- Lifting: multiplicativity across coprime \(q\) ensures CRT-friendly scaling.

### 1.6 Finite-field trace characters
- Over \(\mathbb F_{q^m}\), additive characters \(\psi_a(x)=\exp\!\big(\tfrac{2\pi i}{q}\mathrm{Tr}_{\mathbb F_{q^m}/\mathbb F_q}(ax)\big)\) are orthogonal for distinct \(a\).
- Lifting: \(m\to m'\) with \(m\mid m'\) via trace transitivity; tensor with 1.1/1.2 as needed.

### 1.7 Polynomial-CRT characters on \(k[x]/(M(x))\)
- Additive characters indexed by residues modulo \(M(x)\); orthogonality from \(k[x]\)-linearity.
- Lifting: \(M(x)\leadsto \mathrm{lcm}(M,M')\) in \(k[x]\); factorwise extension through CRT.

### 1.8 Quadratic-phase (chirp) characters over \(p^k\) or \(\mathbb Q_p\)
- Compose the additive character with a nondegenerate quadratic form; orthogonality by Gauss sum cancellation.
- Lifting: Hensel lifting on the local prime powers; global adelic control by adding primes and increasing \(k\).

### 1.9 Cyclotomic partitions / multiplicative subgroups of \(C_M^{\times}\)
- Average uniformly over cosets of a multiplicative subgroup; Fourier-side block selectors (Gaussian periods).
- Lifting: choose subgroup order dividing \(\varphi(M)\); refine \(M\) so the same order embeds.

### 1.10 Tensor-separable products
- If \(G=G_1\times\cdots\times G_d\), characters tensor; projectors and idempotents factor. Enables multidimensional separable constraints.
- Lifting: refine any axis independently, preserving separability and exactness on protected slices.

---

## 2. Constraints and Anti-Constraints

### 2.1 Spectral constraints
Pick a set of characters \(T\subset\widehat G\) that must be preserved (protected) or annihilated (forbidden).
- **Preserve** \(T\): constrain updates to keep \(\widehat{\mu}(\chi)\) fixed for all \(\chi\in T\).
- **Annihilate** \(A\subset\widehat G\): apply projector \(P_{A^c}\) or convolve with an idempotent whose annihilator contains \(A\).
- **Anti-constraint** of preserving \(T\): free variation in \(T^c\) only; of annihilating \(A\): free variation in \(A\) only.

### 2.2 Subgroup (geometric) constraints
Choose \(H\le G\).
- Enforce invariance under \(H\): convolve with \(m_H\) (averaging along \(H\)-cosets). Fourier-side keeps only \(H^\perp\).
- Anti-constraint: fluctuate only along cosets **modulo** \(H\) (i.e., supported in \((H^\perp)^c\) spectrally).

### 2.3 Operator constraints
Let \(A:L^2(G)\to \mathcal H\) be linear. Enforce \(A\mu=b\) by projection onto the affine subspace \(\{\mu: A\mu=b\}\). If \(A\) is diagonal in the chosen character basis (e.g., convolution or subgroup averaging), projection is trivial. Otherwise use splitting (\S4).

---

## 3. LCM/CRT Refinement and Exactness

Let \(G\hookrightarrow G'\) be a refinement by \(\mathrm{lcm}\) (integer or polynomial). Denote the pullback map on characters by \(\iota^*:\widehat{G'}\to\widehat G\).

**Divisibility Lemma (Exactness under refinement).** If the protected set \(T\subset\widehat G\) is closed under pullback from \(\widehat{G'}\) (i.e., all refinements of \(\chi\in T\) remain in \(T\)), then any update that exactly preserves \(T\) before refinement continues to preserve \(T\) after refinement, provided the update commutes with the embedding (e.g., permutations, subgroup averages, or convolutions with idempotents that also lift).

**Idempotent Lifting.** If \(H\le G\) and \(H'\le G'\) satisfy \((H')^\perp=\iota^{*-1}(H^\perp)\), then \(m_{H'}\) is a lift of \(m_H\); consequently, protected/forbidden spectra remain exactly enforced across refinements.

---

## 4. Projection Mechanics (strict, soft, dynamic)

Let \(\mathcal C_1,\mathcal C_2\) be two constraint subspaces (possibly from different orthogonality sources on the **same** or **product** group).

### 4.1 Strict intersection (hard constraints)
Project onto \(\mathcal C_1\cap\mathcal C_2\) by **alternating projections** or Dykstra’s algorithm. If the projectors \(P_1,P_2\) **commute** (e.g., both are convolution idempotents on an abelian \(G\)), then \(P_{\cap}=P_1P_2=P_2P_1\). Otherwise, convergence rate depends on the **Friedrichs angle** \(\theta\) between the subspaces; error decays like \(\cos^2\theta\) per cycle.

### 4.2 Soft coupling (penalized)
Minimize \(E_1(\mu)+E_2(\mu)+\tfrac{\lambda}{2}\|B\mu\|^2\) where \(B\) measures cross-violation (e.g., correlation between two character families). Use ADMM or Douglas–Rachford splitting with per-step **positive** operations (permutations + subgroup averages + idempotent convolutions) and only spectral readouts.

### 4.3 Dynamic switching
Let \(\lambda\) depend on residuals; keep hysteresis \(\epsilon_{\rm soft}<\epsilon_{\rm hard}\) to prevent chatter. Promote to strict projection when protected-mode residuals exceed \(\epsilon_{\rm hard}\); relax when below \(\epsilon_{\rm soft}\).

---

## 5. Interactions Between Orthogonality Types

Consider two groups \(G_a,G_b\) with characters \(\widehat G_a,\widehat G_b\). Build a product space \(G=G_a\times G_b\). Three archetypes:

1. **Separable (commuting projectors):** constraints realized by idempotent convolution on each axis (e.g., Walsh × DFT). Projectors commute \(\Rightarrow\) exact simultaneous enforcement, \(P_{\cap}=P_a\otimes P_b\).
2. **Linked via pullback/pushforward:** a map \(T:G_b\to G_a\) (e.g., sampling/parameterization). Cross-orthogonality is enforced by \(B(\mu_a,\mu_b)=\langle \mu_a, T\mu_b\rangle=0\). Implement with a spectral **cross-Gram** \(G_{\alpha\beta}=\langle \phi_\alpha, T\psi_\beta\rangle\) and low-rank corrections.
3. **Noncommuting projectors:** e.g., additive vs multiplicative characters on the same cycle. Use alternating projections; quantify coupling via the angle between the subspaces. Insert a dump idempotent \(m_H\) whose annihilator covers the *unprotected* overlap to keep updates positive.

**Compatibility Test.** Two constraint projectors \(P,Q\) commute iff both are convolution by idempotent measures (true on abelian groups) **and** their corresponding annihilators are unions of character cosets that are stable under each other’s subgroup structure. Otherwise expect low-rank cross terms.

---

## 6. Worked Templates

### 6.1 DFT (cycle) + Walsh (boolean)
- \(G=C_M\times (\mathbb Z_2)^k\).
- Protect low DFT modes \(K\subset \mathbb Z_M\) and low-order Walsh modes \(U\subset (\mathbb Z_2)^k\). Projector is \(P = P_K^{\text{DFT}}\otimes P_U^{\text{Walsh}}\).
- LCM lift: \(M\to L\), keep the same \(K\) interpreted modulo \(L\); add axes to Walsh as needed. Exactness preserved.

### 6.2 Dirichlet + DFT
- On \(C_M\), use additive characters for geometry and Dirichlet characters on \((\mathbb Z/M)^{\times}\) to impose multiplicative symmetries.
- Enforce additive constraint by subgroup averaging on \(d\mid M\). Enforce multiplicative constraint by averaging over a subgroup of \((\mathbb Z/M)^{\times}\). Alternating projections converge; if both are idempotent convolutions (extend multiplicative average to a measure on \(C_M\)), they commute.

### 6.3 Polynomial-CRT + Finite-field trace
- Take \(G=k[x]/(x^{m})\). Characters via coefficient dot product. Couple to \(H=(\mathbb F_{q^m},+)\) through a linear isomorphism of vector spaces (when \(k=\mathbb F_q\)). Then constraints are conjugate via a change of basis; projectors commute.

### 6.4 Quadratic-phase within p-adic refinement
- Protect linear characters up to order \(p^r\). Enforce a chirp nulling constraint by convolving with an idempotent supported on a lattice where the quadratic phase is stationary. Hensel-lift to \(p^{r+1}\) without disturbing protected linear modes.

---

## 7. Algorithms (positivity-safe, CRT/LCM scalable)

**Primitive moves** (all positivity-preserving):
1. **Permutation/translation:** reindex or translate on \(G\) (characters pick up phases; magnitudes preserved).
2. **Subgroup average:** \(\mu\leftarrow \mu * m_H\). Kills frequencies not in \(H^\perp\), preserves mass.
3. **Convex merge:** \(\mu\leftarrow (1-\alpha)\mu + \alpha\,\nu\) with \(\nu\ge 0\). Used for ADMM/DRS proximal steps.

**Strict projection to \(\mathcal C\):** choose the idempotent convolution (or spectral mask) that realizes \(P_\mathcal C\); apply once.

**Intersection (two constraints):**
- If commuting: one pass \(\mu\leftarrow P_2 P_1\mu\).
- If not: alternate \(\mu\leftarrow P_2 P_1 \mu\) until residual below tolerance; optionally interleave a dump \(m_H\) to hide residuals on unprotected spectra.

**Soft coupling (ADMM sketch):**
- Split variable \(\mu=a=b\). Minimize \(E_1(a)+E_2(b)+\frac{\rho}{2}\|a-b\|^2\).
- \(a\)-update: projector for constraint 1; \(b\)-update: projector for constraint 2; dual update: translation. All steps are permutations/averages/convex merges.

**Dynamic switching:** monitor protected-mode error; raise/lower \(\rho\) and switch to strict projection when needed.

**Scaling by LCM:** when \(G\to G'\), lift \(\mu\) by pullback or zero-stuffing; lift idempotents and masks via divisibility; continue with the same projector pipeline.

---

## 8. Complexity

- DFT/FWHT/additive-FFT on products: \(O(N\log N)\) where constant factors split per axis.
- Idempotent convolutions over subgroups: linear in support size (often \(O(N/d)\) for divisor \(d\)).
- Cross-type coupling via low-rank cross-Gram: \(O(rN)\) per iteration for rank \(r\) blocks.

---

## 9. Design Recipes (quick picks)

1. **Exact spectral preservation + coarse nulling:** DFT (1.1) with subgroup idempotents (1.3).
2. **Binary structures:** Walsh (1.2), optionally tensor with DFT (1.10) for mixed periodic/boolean control.
3. **Arithmetic textures:** Ramanujan atoms (1.5) + DFT (1.1).
4. **Field-linear algebra:** finite-field trace (1.6), easy lifting in degree; great for code-friendly transforms.
5. **Polynomial locality:** polynomial-CRT (1.7) for fast, integer-only CRT parallelism.
6. **Curved phases:** quadratic-phase (1.8) for focusing/defocusing constraints at p-adic scales.

---

## 10. Open Extensions

- Beyond abelian: compact groups with noncommutative harmonic analysis (careful—idempotents no longer commute).
- Adaptive selection of dump subgroups \(H\) to minimize distortion subject to protected-mode exactness.
- Learning cross-Gram structure for automatic soft coupling between disparate orthogonality families.

---

## 11. Minimal Axioms for Implementation

1. Work on a compact abelian \(G\) (or product) with FFT-like transforms available.
2. Only use positivity-preserving primitives (permutations, subgroup averages, convex merges).
3. Express each constraint as either a spectral mask or an idempotent convolution.
4. For interactions, ensure either commuting projectors or use alternating projections/ADMM with monitored residuals.
5. Scale by LCM/CRT; lift protected masks and idempotents by divi