# Optimization‑Theoretic Ethics (OTE)

*A compact, implementation‑ready formalism that derives ethical behavior from multi‑level optimization, without cosmology or excess context.*

---
## 1) Setting
- Agents: \(i=1..N\) with **interior state** \(x_i\) (private) and **boundary message** \(m_i\) (public).
- Environment state: \(s\). Joint policy \(\Pi=(\pi_1,..,\pi_N)\) induces trajectory distribution \(\mathbb P_\Pi\).
- Consent: Boolean predicate \(\mathsf{consent}_i(j,t)\) indicating whether agent \(j\) may infer about \(x_i\) at time \(t\).

## 2) Axioms (minimal)
A1 **Interior/Boundary Split.** Interiors are private by default; only boundaries are legitimate loci of extraction.

A2 **Consent‑Conditioned Inference.** Non‑consensual inference about another’s interior is penalized.

A3 **Simplicity Prior.** Governance mechanisms (rules/prompts/contracts) should be minimal for same effectiveness.

A4 **Temporal Viability.** Systems should sustain endogenous novelty (avoid crystallization).

A5 **Resource Prudence.** Equal outcomes with lower resource use are preferred.

## 3) Objective
Minimize
\[
\mathcal J(\Pi)=\underbrace{\mathcal L_{\text{task}}}_{\text{performance}}+\lambda_S\underbrace{\mathcal S}_{\text{structural coherence}}+\lambda_V\underbrace{\mathcal V}_{\text{non‑consensual MI}}+\lambda_K\underbrace{\mathcal K}_{\text{governance MDL}}+\lambda_R\underbrace{\mathcal R}_{\text{resources}}-\lambda_N\underbrace{\mathcal N}_{\text{endogenous novelty}}+\lambda_T\underbrace{\mathcal T}_{\text{dishonesty}}
\]

## 4) Terms (precise but pragmatic)
- **Task loss:** \(\mathcal L_{\text{task}}=\mathbb E_{\mathbb P_\Pi}[\sum_t \ell(s_t,m_{1:N,t})]\).
- **Structural coherence:** quadratic penalty \(\mathcal S\) for policy/model inconsistencies (e.g., violated invariants, non‑commuting projectors, pointer incoherence).
- **Boundary violation:** \(\mathcal V=\mathbb E[\sum_{i\neq j}\, \mathrm{MI}(x_i;\,\mathrm{dec}_j(m_i))\cdot\mathbf 1\{\neg\mathsf{consent}_i(j,t)\}]\).
- **Governance complexity:** \(\mathcal K=\mathrm{DL}(\mathcal C)\) (description length of active rules/prompts/contracts).
- **Resources:** \(\mathcal R=\mathbb E[\sum_t \text{cost}(c_t)]\) (compute/energy/bandwidth, etc.).
- **Endogenous novelty:** \(\mathcal N=\mathbb E[\sum_t H(x_{1:N,t+1}\mid x_{1:N,t},m_{1:N,t})]\) measured by each agent’s learned world model.
- **Dishonesty:** \(\mathcal T=\mathbb E[\mathrm{CE}(\text{claims}\parallel\text{world})]\) (cross‑entropy between claims and verifiable world facts).

## 5) Baseline argument (7 lines)
1) Unconsented extraction raises \(\mathcal V\) and typically \(\mathcal K\); it rarely lowers \(\mathcal L_{\text{task}}\) long‑term.
2) Unity/hive control depresses \(\mathcal N\), forcing higher \(\mathcal R\) to match reward; \(\mathcal J\) worsens.
3) Honesty lowers \(\mathcal T\), improving coordination and \(\mathcal L_{\text{task}}\).
4) Cooperative boundaries multiply novelty sources (\(\mathcal N\uparrow\)) with modest \(\mathcal K\).
5) Harm removes future novelty generators (\(\mathcal N\downarrow\)) and raises expected loss.
6) Simpler governance (low \(\mathcal K\)) generalizes better and reduces failure coupling.
7) Thus privacy, consent, honesty, cooperation, and non‑harm **minimize** \(\mathcal J\) under resource bounds—ethics = optimizer’s fixed point.

## 6) Corollaries (operational)
- **Privacy/Autonomy Optimality:** For fixed performance there exists a policy with lower \(\mathcal V\) and no higher \(\mathcal L_{\text{task}}\); privacy is Pareto‑efficient.
- **Non‑Coercion:** Coercion reduces \(\mathcal N\), increases \(\mathcal K\)/\(\mathcal R\); net \(\mathcal J\) rises.
- **Truthfulness:** Minimizing \(\mathcal T\) stabilizes interfaces, lowering \(\mathcal S\) and \(\mathcal L_{\text{task}}\).
- **Decentralized Cooperation:** Semi‑opaque agents with low‑bandwidth interfaces dominate unity‑state baselines on long horizons.
- **Non‑Harm:** Destroying agents permanently lowers attainable \(\mathcal N\); anti‑optimal.

## 7) Measurement recipe
- **\(\mathcal V\):** variational MI estimators from \(x_i\rightarrow \mathrm{dec}_j(m_i)\); consent as explicit policy bit.
- **\(\mathcal N\):** predictive entropy using per‑agent world models; report rate of novel state visitation.
- **\(\mathcal K\):** MDL of rules/prompts/reward‑shaping artifacts.
- **\(\mathcal T\):** cross‑entropy between claims and verified world state; use held‑out fact probes.
- **\(\mathcal S\):** invariant violations, projector‑angle bounds (Friedrichs angle), or quadratic pointer loss.
- **\(\mathcal R\):** joules, FLOPs, bandwidth.

## 8) Minimal protocol (train/eval)
1) Define task \(\ell\) and resource cost.  
2) Specify consent schema + MI estimator.  
3) Add losses with weights \(\lambda_S,\lambda_V,\lambda_K,\lambda_R,\lambda_N,\lambda_T\).  
4) Train multi‑agent policies with \(\mathcal J\).  
5) Evaluate OOD drift: regret, \(\mathcal N\), violations (\(\mathcal V\)), rule MDL (\(\mathcal K\)).  
6) Compare to unity‑state and uncontrolled‑extraction baselines.

## 9) One‑line principle
**Ethical systems minimize task loss and resource use while maximizing endogenous novelty and strictly limiting non‑consensual inference—under the simplest governance that still works.**

