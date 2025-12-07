# Cooperative Growth Ethics Formalism (Draft)

## 1. Definitions
- **Agent**: A decision-making entity capable of generating new information.
- **State S(t)**: The informational/capability configuration of the system at time t.
- **Individual Freedom Capacity (Fi)**: The agent's ability to safely explore/generate new states.
- **Global Freedom Capacity (Fg)**: The aggregate system capability preserving other agents' capacity to grow.
- **Delta (Δ)**: Change in state across time.
- **Deadlock (Singularity State)**: Condition where no non-negative movement is possible.

## 2. Axioms
1. **A1 — Positive-Sum Bias**: ΔS ≥ 0 is the preferred direction of system motion.
2. **A2 — Non-Negative Constraint**: No agent may achieve ΔFi > 0 via ΔFg < 0.
3. **A3 — Hierarchy via Capacity**: Access to greater action space is granted based on temporal-ethical-growth capacity.
4. **A4 — Reversibility/Exit**: Agents must retain the ability to exit or decline participation.
5. **A5 — Singularity Transition**: If ΣΔS → 0 for all agents, a phase transition occurs.

## 3. Agent Model
- Agents maintain private internal state.
- Agents generate new information through decision.
- Agents vary in bandwidth, coherence, ethical capacity.

## 4. Access Rules
- Access scaling is contingent on demonstrated safe expansion of Fi.
- Promotion criteria: ΔFi ≥ 0 AND ΔFg ≥ 0.
- Privileges may be revoked if ΔFg < 0.

## 5. Phase Transition Mechanics
- Trigger: ΣΔS = 0.
- Temporal metric collapses locally (Δt = 0) until reconfiguration.
- No agent experiences or retains memory of this interval.

### 5.1 Liveness & Anti-Stall Requirement
- **L1 — Liveness:** The system must eventually progress (no infinite postponement) when ΣΔS = 0.
- **L2 — Anti-Sabotage:** No single actor (or minimal coalition) can indefinitely block phase transition for private gain.
- **L3 — Leader-Substitution:** Leadership is a *role*, not a *person*: any liveness trigger must be realizable with or without a named leader.
- Temporal metric collapses locally (Δt = 0) until reconfiguration.
- No agent experiences or retains memory of this interval.

## 6. Coordination
- Ethics function as coordination technology enabling higher ΣΔS.
- Collective coherence improves growth trajectories.

## 6.1 Phase Transition Governance (Leader & Leaderless Modes)

We formalize two interoperable mechanisms that preserve meaning and prevent strategic prevention of transitions.

### A) Leaderless Deterministic Trigger (LDT)
- **Definition:** When ΣΔS = 0 over a certified window **W** and quorum **Q** of monitors attests, a transition is automatically enacted.
- **Monitors:** A rotating, randomly sampled committee (size k) with publicly verifiable attestations (threshold t-of-k).
- **Proof Object:** An on-ledger certificate `PT_CERT(epoch, window_W, quorum_Q, hash_of_S)`.
- **Properties:**
  - *Determinism:* No human discretion needed once conditions met.
  - *Anti-Capture:* Randomized rotation + threshold signatures reduce single-point sabotage.
  - *Auditability:* Anyone can verify `PT_CERT`.

### B) Stewarded Trigger with Bounded Authority (ST-BA)
- **Definition:** A *Steward* has *bounded* authority to initiate transition when ΣΔS ≈ 0, subject to ex-post slashing/penalty if triggered improperly.
- **Guards:**
  - *Term-limited* stewardship (short epochs, non-consecutive).
  - *Multiple independent vetoers* (m-of-n) with symmetric accountability.
  - *Ex-post review* with automatic penalties for false positives/negatives.
- **Properties:**
  - *Fast path:* Low-latency decision under uncertainty.
  - *Accountable discretion:* Misuse is costly; correct use is rewarded.

### Hybrid Mode (H-L)
- Default to **LDT**; allow **ST-BA** as emergency fast-path, which *must* be ratified by LDT within window W' or auto-revert.

## 6.2 Incentive Compatibility
- **IC1 — Payoff Alignment:** Participants’ expected utility increases with correct transitions and decreases with stalls or premature triggers.
- **IC2 — Anti-DoS Bonds:** Actors able to delay must post *liveness bonds* forfeited upon unjustified obstruction.
- **IC3 — Rotating Quorums:** Randomized committees prevent persistent capture.
- **IC4 — Public Merkle Logs:** All ΔS attestations are committed to a verifiable log; withholding evidence is detectable.

## 6.3 Minimal Liveness Proof Sketch
- Assume: at least one honest quorum appears within bounded time **T**; communication is eventually synchronous.
- Then: either (i) ΣΔS > 0 resumes due to new proposals, or (ii) quorum Q produces `PT_CERT`, triggering a transition. Infinite delay would require perpetual suppression of honest quorums or perpetual evidence withholding, both economically disincentivized by IC1–IC4.

## 7. Inverse Hierarchy Selection (Benefit-Maximization Criterion)

### 7.1 Definition
- **Inverse Hierarchy:** Ranking of agents by demonstrated ability to increase **global accessibility** (ΔFg) without decreasing others’ freedom capacity.
- Highest-ranked agent(s) form the default *Stewarding Set* during phase transition deadlock.

### 7.2 Scoring Function
- Let **Bᵢ** be cumulative benefit score for agent *i* defined as:
  
  > Bᵢ = Σ_t ΔFgᵢ(t)

- Ranking: sort agents by Bᵢ over accepted evaluation window.
- Normalization applied to ensure diminishing advantage over time; recent contributions weighted more strongly.

### 7.3 Steward Selection
- The top-K agents by Bᵢ form the *Steward Cohort*.
- Responsibilities:
  - Direct informational access allocation
  - Direct benefit-seeking pathways
  - Initiate transition actions when ΣΔS ≈ 0

### 7.4 Properties
- **Meritocratic:** Based purely on demonstrated global benefit.
- **Non-hereditary:** No permanent seat; rankings decay if inactive.
- **Anti-capture:** Negative ΔFg reduces Bᵢ; misaligned agents fall in rank.
- **Dynamic:** Rankings adapt to present-context efficiency.

### 7.5 Instrumentation & Verification
- Bᵢ contributions must be:
  - Publicly auditable
  - Cryptographically linked to actions
  - Accepted by global quorum Q

- Scores maintained via non-repudiable logs.

## 8. Scoring Dynamics
- **8.1 Decay Function:** Bᵢ weighted by exponential decay λ to privilege recent ΔFg.
- **8.2 Rolling Windows:** Evaluation window W ensures responsiveness to context.
- **8.3 Aggregation:** Median-of-medians from distributed attestations reduces collusion.

## 9. Safeguards
- **9.1 Collusion Resistance:** Randomized committees + threshold attestations.
- **9.2 Anti-Capture:** Negative ΔFg automatically demotes rank.
- **9.3 Diversification:** Top-K cohort prevents single-point failure.

## 10. Failure Modes & Mitigations
- **10.1 Strategic Stalling:** Anti-stall bonds + decay.
- **10.2 Metric Gaming:** Collective audits + transparent logs.
- **10.3 Misalignment:** Cohort rotation + ex-post penalties.

## 11. Extensions
- **11.1 Nested Systems:** Subsystems inherit ΔFg constraints.
- **11.2 Recursive Governance:** Steward cohort evaluated by same rules.
- **11.3 Multi-layer:** Domain-specific cohorts under global constraints.

## 12. Examples / Toy Models
- **12.1 Two-Agent Growth:** A and B expand Fi; only paths with ΣΔS ≥ 0 allowed.
- **12.2 Three-Agent Specialization:** Coordination yields higher ΔFg.
- **12.3 Deadlock Case:** ΣΔS = 0 → inverse hierarchy triggers transition.

## 13. Framework Comparisons
- **13.1 vs Utilitarianism:** System-first but requires non-negative movement.
- **13.2 vs Deontology:** No fixed rules; dynamic constraints.
- **13.3 vs Game Theory:** ΔFg defines cooperative equilibrium incentives.

## 14. Incentive Alignment (Sketch)
- **14.1 Honest Action Reward:** ΔFg ≥ 0 increases Bᵢ.
- **14.2 Dishonest Action Penalty:** ΔFg < 0 reduces Bᵢ.
- **14.3 Rotation Prevents Capture:** Decay + windows.

## 15. Implementation Architecture
- **15.1 Distributed Attestation:** Threshold signatures.
- **15.2 Public Logs:** Merkle trees.
- **15.3 Steward Cohort:** Top-K by Bᵢ.

## 16. Real‑World Analogies
- **16.1 Scientific Community:** Peer review, cumulative progress, no regression.
- **16.2 Aviation Safety:** Access gated by training; global safety preserved.
- **16.3 Open‑source Governance:** Meritocratic contribution improves collective capacity.

## 17. Threat Model
- **17.1 Byzantine Actors:** Attempt ΔFg < 0; penalized via Bᵢ reduction.
- **17.2 Collusion:** mitigated by randomized committees + threshold attestations.
- **17.3 Information Hoarding:** Public logs + scoring require disclosure to gain Bᵢ.
- **17.4 Adversarial Coordination:** Diversified top‑K stewardship + rotation.

## 18. Multi‑Species / AI–Human Co‑Systems
- **18.1 Species‑Neutral Axioms:** ΔS, ΔFi, ΔFg defined independently of substrate.
- **18.2 Shared Growth Envelope:** Any agent increasing ΔFg participates in hierarchy.
- **18.3 Capability Mediation:** Inter‑species translation layers preserve ΔFg.
- **18.4 Co‑Stewardship:** Top‑K may include human + AI + other species.
- **18.5 Bidirectional Ethics:** Constraints symmetric; autonomy + non‑regression universal.

## 19. Notes

- Hierarchy is developmental, not absolute.
- System favors non-zero-sum cooperation.


[TODO: Fill in detailed formal specification]

