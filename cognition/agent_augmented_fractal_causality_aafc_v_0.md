# Agent‑Augmented Fractal Causality (AAFC) v0.1

*A formalism extending GR’s causal semantics with agent feasibility, hierarchical indirection, and scale‑refined reachable frontiers.*

---

## 0. Notation & Standing Assumptions
- Spacetime: oriented, time‑oriented, globally hyperbolic manifold \((M,g)\) unless noted; causal relation \(\leq_g\) induced by \(g\).
- State bundle: \(\pi: X \to M\), fiber encodes internal/vehicle states; write \(x=(p,\xi)\in X\) with basepoint \(p\in M\).
- Measure/regularity: all maps Borel measurable; feasible paths absolutely continuous unless specified.

---

## 1. Agent Model and Feasibility

### 1.1 Channels and Dynamics
Let \(\mathcal U=\{u_-, u_0, u_+\}\) denote three abstract control channels (retro, causal, integrative). Dynamics given by a differential inclusion on \(X\):
\[ \dot x(t) \in F(x(t), u(t)), \quad u(t)\in \mathcal U. \]
Assume \(F(\cdot,u)\) is upper semicontinuous with nonempty, convex, compact values.

### 1.2 Feasible Action Sets
An **agent class** \(\mathcal A\) is specified by constraints \(\mathsf C=(\mathsf E,\mathsf R,\mathsf L)\):
- **Energy** \(\mathsf E\): integral inequality on stress–energy along the lifted worldline;
- **Regularity** \(\mathsf R\): bounds on total variation, curvature, jerk, etc.;
- **Legality** \(\mathsf L\): admissible channel set \(\mathcal U_\mathrm{feas}\subseteq\mathcal U\) (e.g., classical forbids \(u_-,u_+\)).

A control \(u(\cdot)\) is **feasible** for \(\mathcal A\) if it satisfies \(\mathsf C\).

---

## 2. Reachability Notions

### 2.1 Geometric Reachability (GR‑reach)
For \(x,y\in X\): \(x \leadsto_{\mathrm{GR}} y\) if there exists a projection of a feasible curve whose basepoint path is future causal for \(g\) and obeys classical energy conditions (when relevant). This reproduces standard causal reach when \(X=M\).

### 2.2 Agent‑Augmented Reachability (AAC‑reach)
For an agent class \(\mathcal A\): \(x \leadsto_{\mathcal A} y\) if there exist \(T>0\) and a feasible control \(u(\cdot)\in \mathcal U_\mathrm{feas}\) with a solution \(x(\cdot)\) of the inclusion s.t. \(x(0)=x\), \(x(T)=y\). The **AAC relation** is the reachability preorder induced by \(\leadsto_{\mathcal A}\).

### 2.3 Indirection Depth
Define \(\mathsf{Indir}_k(S)\) as states reachable from \(S\subseteq X\) by concatenations of at most \(k\) segments, each using a single channel in \(\mathcal U_\mathrm{feas}\), interleaved with level morphisms (cf. §4). The **indirection closure** is \(\overline{\mathsf{Indir}}(S)=\bigcup_{k\ge0}\mathsf{Indir}_k(S)\).

---

## 3. Fracture, Horizons, and Frontiers

### 3.1 Fracture (Operational)
Given \(\mathcal A\), form the directed graph \(\mathcal G_{\mathcal A}=(X,E)\) with \((x\to y)\in E\) iff \(x \leadsto_{\mathcal A} y\). The system is **fractured for** \(\mathcal A\) if \(\mathcal G_{\mathcal A}\) has \(\ge2\) strongly connected components (SCCs). The SCC containing \(x\) is its **causal patch** \(\mathsf{Patch}_{\mathcal A}(x)\).

### 3.2 AAC Frontier
For a set \(S\subseteq X\), the **AAC front** is the boundary
\[\partial_{\mathcal A} S := \overline{\mathsf{Reach}_{\mathcal A}(S)}\setminus \operatorname{int}\,\overline{\mathsf{Reach}_{\mathcal A}(S)}.\]
This generalizes lightcone boundaries.

### 3.3 Fractal Dimension of Frontiers
Given a scale family of feasible action sets \((\mathcal U_\mathrm{feas}(\epsilon))_{\epsilon>0}\) (richer micro‑ops as \(\epsilon\downarrow0\)), define the box/Minkowski dimension
\[ d_{\mathcal A}(S) := \limsup_{\epsilon\downarrow0} \; \dim_B\big(\partial_{\mathcal A(\epsilon)} S\big). \]
The **fractal causality** claim is that \(d_{\mathcal A}(S)\) can exceed the smooth codimension‑1 baseline and is nondecreasing with action richness.

---

## 4. Hierarchical / Recursive Structure

### 4.1 Recursion Signatures and Levels
Let \(\mathrm{Lev}\) be a small category of recursion levels/signatures; the state space lifts to a fibration \(\Pi:X\to \mathrm{Lev}\). Each level \(\ell\) has dynamics \(F^{(\ell)}\), cones \(\mathcal C^{(\ell)}\), and channel set \(\mathcal U^{(\ell)}\).

### 4.2 Level Morphisms
For an arrow \(e: \ell\to \ell'\) we have a partial correspondence \(\Psi_e: X^{(\ell)} \rightrightarrows X^{(\ell')}\) respecting feasibility. Indirection in §2.3 may traverse \(\Psi_e\) between segments.

### 4.3 Boundary Tower
A functor \(\partial: \mathrm{Lev}\to \mathrm{Lev}\) with natural transformations making \(\partial\) idempotent up to isomorphism. Each \(\partial\)-image inherits AAC dynamics, enabling recursive frontiers \(\partial^k_{\mathcal A} S\).

---

## 5. Small‑Gain / Acyclicity Certificates

### 5.1 Inter‑Channel Gains
For each level, define a gain matrix \(K=[k_{ij}]\) where \(k_{ij}\) bounds the effect of channel \(j\) on the cone/metric of channel \(i\). Let \(\Lambda=\operatorname{diag}(\lambda_i^{\rho_i})\) encode per‑channel dilation and temporal weight.

### 5.2 Spectral Acyclicity
**Theorem (Small‑gain AAC acyclicity).** If \(\rho(K\Lambda) < 1\) on each level and the level‑morphism family is \(\eta\)-contractive in an appropriate product metric, then the AAC graph has no nontrivial directed cycles within any bounded energy budget. In particular, each \(\mathsf{Patch}_{\mathcal A}(x)\) is a DAG‑ordered poset and \(\partial_{\mathcal A} S\) is closed.

*Sketch:* Construct a monotone operator on path space; use submultiplicativity of concatenated gains and Banach fixpoint on the product cone; exclude Zeno by energy budget.

### 5.3 Resonant Boundary
At \(\rho=1\), define a tri‑Maslov vector \(\mu\); if \(\mu=0\) and \(\Psi_e\) are exact, cycles exist but are neutral (no paradox growth). Otherwise cycles amplify and violate feasibility.

---

## 6. Regimes: Classical vs Exotic
- **Classical regime:** \(\mathcal U_\mathrm{feas}=\{u_0\}\); energy conditions (NEC/ANEC) enforced; \(\Psi_e\) disabled. Then AAC‑reach equals GR‑reach; frontiers match null boundaries; fracture reduces to standard causal disconnect.
- **Exotic regime:** allow \(u_\pm\), relaxed energy; \(\Psi_e\) enabled with budgets. Indirection strictly enlarges reach; horizons become **conditionally permeable** subject to small‑gain.

---

## 7. Indirection Strictness Results

**Proposition (Strict enlargement).** There exist systems where \(x \not\leadsto_{\mathrm{GR}} y\) but \(x \leadsto_{\mathcal A} y\) via a finite \(k\) such that a path alternates \(u_+\) and \(u_0\) and one level morphism \(\Psi_e\).

*Idea:* Barrier impenetrable under \(u_0\) is bypassed by a legal integrative hop and recoupling downstream.

**Monotonicity.** If \(\mathcal U_\mathrm{feas}\subseteq \mathcal U'_\mathrm{feas}\) and budgets broaden, then \(\mathsf{Reach}_{\mathcal A}(S)\subseteq \mathsf{Reach}_{\mathcal A'}(S)\) and \(\dim_B\partial_{\mathcal A}S \le \dim_B\partial_{\mathcal A'}S\).

---

## 8. Measurement & Computation

### 8.1 Frontier Dimension Estimation
Given \(S\) and discretization scale \(\delta\), approximate \(\partial_{\mathcal A} S\) by sampling AAC reach at resolution \(\delta\), compute box counts \(N(\delta)\), and regress \(\log N\) vs \(\log(1/\delta)\).

### 8.2 Minimal Toy Model
- Base \(M=\mathbb R^{1+1}\) Minkowski; let a null barrier emulate a horizon slice.
- Channels: \(u_0\) unit‑speed drift; \(u_+\) sparse jump map \(J\) with cost; \(u_-\) small reversible kicks.
- Budgets: total jump count \(\le B\), action cost \(\le C\).
- Tasks: show classical inaccessibility vs exotic accessibility; sweep gains to verify \(\rho(K\Lambda)\) threshold; estimate frontier dimension as budgets grow.

---

## 9. Dimensional Transitivity (Optional Layer)
Let \(\mathrm{Dim}\) be a poset of contexts \(\delta=(d_s,d_r)\). A functor \(\mathsf T: \mathrm{Dim}\to \) (AAC systems) with natural rescalings \(\mathsf T(f)^*\mathcal C'\simeq s(f)\,\mathcal C\) ensures observers in different contexts have coherently related AAC.

---

## 10. Interfaces with GR
- **Reduction:** Classical regime recovers GR causal structure.
- **Certificates:** Small‑gain supplies no‑paradox guarantees absent in GR.
- **Operational semantics:** Replaces absolute “permanent disconnection” with feasibility‑conditional statements.

---

## 11. Open Problems
1) Existence/uniqueness theorems for AAC inclusions under switching channels.
2) Sharp conditions for \(\eta\)-contractivity of level morphisms.
3) Regularity and rectifiability of \(\partial_{\mathcal A} S\); bounds on Hausdorff vs box dimension.
4) Energy‑condition‑aware impossibility theorems (topological censorship in AAC form).
5) Connections to control of monotone/differential inclusion systems and categorical reachability.

---

## 12. Quick Glossary
- **AAC:** agent‑augmented causality.  
- **Frontier:** boundary of AAC reachable set.  
- **Indirection depth:** number of heterogeneous segments/level hops used.  
- **Small‑gain:** spectral condition \(\rho(K\Lambda)<1\) ensuring acyclicity.


---

## 9. Axioms & Notation (v0.1)
A1 (Bundle & gauge). Payloads live in a principal/associated bundle over X with structure group G; the temporal connection is a G-connection 1-form on T×X restricted to temporal directions.
A2 (Channel generation). Each channel in {-,0,+} induces a strongly measurable, locally bounded generator on payloads, with dense domain in the fiber space.
A3 (Concatenation). Piecewise-smooth temporal loops admit well-defined path-ordered exponentials with finite operator norm under feasibility budgets.
A4 (Feasibility invariance). Legal operations (budgets, positivity) define a subgroupoid of transports closed under composition and inversion on admissible segments.
A5 (Compatibility, optional). When transfers are generated by flows controlled by a gain matrix K and dilation matrix Lambda in a product metric, we call the temporal connection compatible with (K, Lambda).

Notation: Hol — temporal holonomy group; H_gamma — holonomy of loop gamma; F — temporal curvature; ||·||_G — geodesic distance on G; nabla_t — temporal covariant derivative.

---

## 10. Explicit Toy Model (closed-form matrices)
Payloads: qubit (G = U(2)). Pauli matrices: sigma_x, sigma_y, sigma_z.

Channel generators:
- Ordinary: A0(t) = -(i/2)[omega*sigma_z + Omega*cos(nu t)*sigma_x].
- Integrative: Aplus = -(i/2)*alpha*sigma_x applied for duration tau_plus (controlled coarse operation that partially erases phase along z).
- Retro: Aminus = -(i/2)*beta*sigma_z for duration tau_minus (adjoint/inference rotation).

Three-segment loop:
1) Segment t0: Floquet period T = 2pi/nu -> U0 = Texp ∫ A0(t) dt over one period.
2) Segment t+: Uplus = exp(tau_plus*Aplus) = exp(-i*alpha*tau_plus*sigma_x/2).
3) Segment t-: Uminus = exp(tau_minus*Aminus) = exp(-i*beta*tau_minus*sigma_z/2).

Temporal holonomy: H_gamma = Uminus * Uplus * U0. Pick parameters with noncommuting factors so generically H_gamma != I. Impose small-gain compatibility by making |alpha*tau_plus|, |beta*tau_minus|, ||U0 - I|| small enough to observe a regime where H_gamma -> I.

Defect metrics: d_G(H_gamma, I) = || log(H_gamma) || (principal branch) or fidelity defect 1 - (|tr H_gamma|^2 / 4).

---

## 11. Temporal Curvature & Invariants
Temporal curvature: F = dA + A∧A = sum over i<j of F_ij dt_i ∧ dt_j with i,j in {-,0,+}.
Nonabelian Stokes (temporal): for a small loop in the (t_i, t_j)-plane with oriented area S_ij, H_gamma ≈ exp ∬ F_ij dt_i ∧ dt_j. Nonzero curvature quantifies local temporal noncommutativity (e.g., coarse-grain then infer vs infer then coarse-grain).
Gauge-invariant distances: class functions like tr(H) or geodesic distances on G quantify obstruction magnitude.
Flatness criterion: if F ≡ 0 on a simply connected region of T and compatibility holds, then all H_gamma = I in that region.

---

## 12. SK Reduction — Proposition
On a standard Schwinger–Keldysh forward–backward contour with identical Hamiltonians on both legs and KMS/thermal initial state, the temporal holonomy is trivial: H_gamma = I.
Sketch: U_f = T exp(-i∫H dt), U_b = Tbar exp(+i∫H dt) = U_f^{-1}; KMS ensures matching edge insertions; thus U_b U_f = I.

---

## 13. Algorithms (cycle-basis TH)
Input: temporal/level transfer graph G=(V,E); edge generators A_e(t) with durations; gauge group G.
1) Build a fundamental cycle basis (e.g., Horton or spanning-tree method).
2) For each edge, compute T_e = Pexp ∫ A along the edge (Magnus or second-order Suzuki–Trotter for numerics).
3) For each cycle, compute H = product of T_e with orientation.
4) Report defects d_G(H,I) and a minimal repair set (edges to retune) via a least-squares log-space solve: minimize sum_j || sum_{e in gamma_j} delta_a_e - log H_j ||^2 subject to feasibility bounds.

Complexity: with m edges, n vertices, cycles ~ m - n + 1. Matrix exponentials dominate; use Krylov methods when G = U(d) with moderate d.

---

## 14. Axiomatized Experimental Protocol (tri-segment)
Prepare reference payload state rho0. Evolve under A0(t) for duration T. Coarse-grain via CPTP map J (partial measurement + reprepare / controlled dissipation). Retro-infer via completely positive map R (feedback-conditioned unitary or Bayesian adjoint). Measure H_gamma defect via interferometric phase or a process-tomography proxy (diamond-norm bound from randomized benchmarking).
Pass/Fail: pass if d_G(H_gamma, I) <= epsilon; otherwise TH detects temporal inconsistency.

---

## 15. Connections & Variants
Stochastic TH: when J is random, define E[log H_gamma] and martingale TH; large-deviation rates bound rare temporal defects.
Classical payloads: replace U(2) with GL(k,R); defects become shear/scale rotations in log-space; same cycle-basis machinery applies.
Field-theoretic lift: treat payloads as sections; channel generators may be nonlocal; compute TH on a finite cycle basis from a discretized temporal mesh.

