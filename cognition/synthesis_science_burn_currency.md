# Burn-Based Opinion Geometry for Synthesis Systems

## A Geometric Epistemics Formalism for Inflationary–Burn Governance

---

## Abstract

We introduce a formalism for **burn-based opinion currencies** inside the broader field of **synthesis science / geometric epistemics**: the study of how intelligent systems synthesize structure over geometric spaces of possibility, evidence, and conflict.

An **inflationary, non-transferable opinion credit** is issued continuously to agents and **burned** whenever they exert high-impact governance actions (e.g., determining primacy of content, approving structural changes, escalating disputes). The inflation–burn dynamics define an **opinion geometry** that:

1. Encodes **intensity-weighted preferences** without collapsing into plutocracy.
2. Couples directly to the **expansion–contraction–integration** loop of synthesis systems.
3. Interacts with **EGPT-style** inclusion/exclusion, potentiality/impossibility, and tiered risk/hazard domains.

We formalize agents, credits, burn actions, and their coupling to synthesis flows, and state design constraints for stability and anti-capture.

---

## 1. Field and Scope

We work within a geometric epistemics / synthesis science setting:

* A system maintains a **synthesis state** (S_t) consisting of:

  * A content geometry (topics, artifacts, architectures).
  * An epistemic geometry (evidence, correctness, hazard classes).
  * A governance geometry (opinions, conflicts, resolutions).

* System evolution proceeds in **synthesis steps** (expansion, contraction, integration, reconfiguration) that transform (S_t \to S_{t+1}).

We add a **burn-based opinion layer**: a resource that agents expend to exert *intense* influence over these transitions, subject to rules that preserve democratic access and limit capture.

---

## 2. Opinion Credits and Spaces

Let:

* (\mathcal{A}) = set of agents (humans, orgs; models are treated separately).
* (\mathcal{D}) = set of **domains** (e.g., pedagogy, infra, safety), indexed by (k).
* (\mathcal{T}) = discrete time steps.

### 2.1 Opinion Credits

**Definition 2.1 (Opinion Credit).**
For agent (a \in \mathcal{A}), domain (k \in \mathcal{D}), and time (t \in \mathcal{T}), the **opinion credit balance** is:

[
c_a^{(k)}(t) \in \mathbb{R}_{\ge 0}
]

Credits are:

1. **Inflationary:** new credits are periodically issued to agents (Section 3).
2. **Non-transferable:** (c_a^{(k)}) cannot be transferred between agents.
3. **Burnable:** specific governance actions consume and irreversibly destroy credits.

### 2.2 Opinion State and Supply

**Definition 2.2 (Opinion Supply Vector).**
The **global opinion state** at time (t) is:

[
C(t) = {c_a^{(k)}(t)}_{a \in \mathcal{A}, k \in \mathcal{D}}
]

The **total supply** in domain (k) is:

[
S^{(k)}(t) = \sum_{a \in \mathcal{A}} c_a^{(k)}(t)
]

We allow domain-specific supply and dynamics to reflect that “being good at X” does not automatically confer influence over Y.

---

## 3. Issuance, Inflation, and Decay

### 3.1 Issuance

**Definition 3.1 (Issuance Function).**
Let (I_a^{(k)}(t) \ge 0) denote newly issued credits to agent (a) in domain (k) at time (t). Then:

[
c_a^{(k)}(t+1) = c_a^{(k)}(t) + I_a^{(k)}(t) - B_a^{(k)}(t) - D_a^{(k)}(t)
]

where (B_a^{(k)}(t)) are burned credits (Section 4) and (D_a^{(k)}(t)) are decayed credits.

Typical issuance patterns:

* **Base issuance:** each eligible agent receives a baseline (I_0^{(k)}) per period.
* **Contribution-linked issuance:** additional issuance based on constructive contributions in domain (k) (accepted content, reviews, mentorship, etc.).

### 3.2 Decay and Caps

To prevent hoarding and long-term domination:

**Definition 3.2 (Credit Decay).**
A simple decay rule is:

[
D_a^{(k)}(t) = \lambda^{(k)} , c_a^{(k)}(t) \quad \text{with } 0 \le \lambda^{(k)} \le 1
]

Additionally, we may impose a **per-agent cap** (C_{\max}^{(k)}) and clip balances:

[
c_a^{(k)}(t) \gets \min{c_a^{(k)}(t), C_{\max}^{(k)}}
]

This keeps influence **fresh** and tied to recent participation and trust.

---

## 4. Burn Actions and Intensity Signalling

Let (\mathcal{P}) be the set of **proposals / actions** that affect synthesis (e.g., “make variant (v) primary”, “change outline structure”, “escalate dispute”).

Each proposal (p \in \mathcal{P}) has:

* A **domain** (d(p) \in \mathcal{D}).
* A **hazard level** (h(p) \in {0,1,2,\dots}) (e.g., harmless → critical).
* A **type** (content primacy, structural change, safety override, etc.).

### 4.1 Burn Cost

**Definition 4.1 (Burn Cost Function).**
For agent (a), proposal (p), and time (t), the **burn cost** is:

[
\kappa(a, p, t) = \alpha_{d(p)} , \beta_{h(p)} , f(\ell_a(p,t))
]

where:

* (\alpha_{d(p)}) = domain weight (e.g., safety actions more expensive than UI tweaks).
* (\beta_{h(p)}) = hazard multiplier (higher for high-risk actions).
* (\ell_a(p,t)) = *intensity level* chosen by agent (a) for (p) at time (t).
* (f) is a **convex cost function**, e.g. (f(\ell) = \ell^2), enforcing that doubling intensity costs more than double credits.

The burned amount is:

[
B_a^{(d(p))}(t) \gets B_a^{(d(p))}(t) + \kappa(a,p,t)
]

Credits are destroyed: they **reduce** (S^{(d(p))}(t)).

### 4.2 Intensity-Weighted Opinion

**Definition 4.2 (Intensity Vote).**
The **intensity vote** of agent (a) on proposal (p) at time (t) is:

[
w_a(p,t) = g(\ell_a(p,t)) \quad \text{with } g \text{ increasing, e.g. } g(\ell) = \ell
]

A simple choice:

* (\ell) is an integer “vote level”.
* Cost: (\kappa \propto \ell^2).
* Influence: (w \propto \ell).

Then raising your voice gets linearly more powerful, but costs **quadratically** more credits.

**Definition 4.3 (Aggregate Opinion Field).**
The **opinion field** over proposals at time (t) is:

[
W(p,t) = \sum_{a \in \mathcal{A}} s_a(p,t) , w_a(p,t)
]

where (s_a(p,t) \in {-1, +1}) encodes support/opposition (or more general continuous sentiment).

---

## 5. Coupling to Synthesis: Expansion, Contraction, Integration

Let (\Omega_t) be the set of candidate configurations (content variants, outlines, architectures) under consideration at time (t). In previous work, each (\omega \in \Omega_t) has potentiality depth (\Pi(\omega)) and impossibility depth (\bar{I}(\omega)), and an **attention function** (A(\omega)) allocating cognitive resources.

We extend the attention allocation to incorporate burn-based opinion.

### 5.1 Attention with Opinion Weight

**Definition 5.1 (Opinion-Weighted Attention).**
For configuration (\omega) at time (t), define:

[
\tilde{A}(\omega,t) \propto A_{\text{base}}(\omega,t) \cdot \phi\big(W(\omega,t)\big)
]

where:

* (A_{\text{base}}) is derived from geometric / epistemic factors (potentiality, impossibility, evidence).
* (W(\omega,t)) is the net opinion field aggregated over proposals that act on (\omega).
* (\phi) is a monotone function (e.g., (1 + \lambda \tanh(W))) that modulates attention but does not fully override geometric constraints.

Thus, configurations with both **strong structural merit** and **intensely supported burns** get more cycles in the synthesis loop; those with deep impossibility or weak support get fewer.

### 5.2 Phase Coupling

* **Expansion:**
  Opinion signals can *open* new exploratory branches: burning credits to spawn alternative variants or to request expensive generative exploration.

* **Contraction:**
  Strong negative opinion (burned opposition) can prioritize the culling of certain branches, especially when aligned with high impossibility depth.

* **Integration:**
  When merging or promoting configurations, high positive opinion burn can tip between otherwise similar geometric candidates.

* **Reconfiguration:**
  Large-scale structural changes (tier reconfigurations) require significant burn across relevant domains, especially for high-hazard tiers.

---

## 6. Multi-Domain Opinion Geometry and Hazard

We now exploit the domain index (k) and hazard levels (h(p)).

### 6.1 Domain-Localized Credits

**Definition 6.1 (Domain-Localized Opinion Geometry).**
Each domain (k \in \mathcal{D}) has its own opinion supply (S^{(k)}(t)), issuance (I^{(k)}), decay (\lambda^{(k)}), and cost weights (\alpha_k).

This yields **domain-local opinion geometries**:

[
\mathcal{O}^{(k)}(t) = \big(C^{(k)}(t), \kappa^{(k)}, W^{(k)}(\cdot,t)\big)
]

An agent’s influence in domain (k) is largely determined by (c_a^{(k)}), decoupling influence across domains.

### 6.2 Hazard-Weighted Burn

**Definition 6.2 (Hazard Multiplier).**
Let (\beta_{h}) be an increasing function of hazard level (h):

[
\beta_0 = 1, \quad \beta_1 > 1, \quad \dots, \quad \beta_{H_{\max}} \gg 1
]

Then high-hazard proposals (e.g., medical advice, critical infra) are **expensive** to influence, forcing agents to burn significant credit and thereby:

* Reduce their future influence if their judgement proves poor.
* Slow down rapid swings in dangerous areas.

We may additionally couple post-mortems to future issuance in those domains, penalizing consistently harmful influence patterns.

---

## 7. Stability, Anti-Plutocracy, and Design Constraints

We state design constraints to keep the system democratic, stable, and resistant to capture.

### 7.1 Anti-Plutocracy

**Constraint 7.1 (Non-transferability).**
Opinion credits must be non-transferable between agents to avoid direct purchasing of influence.

**Constraint 7.2 (Freshness).**
Issuance, decay, and caps must be chosen such that:

* Long-term accumulation without participation is impossible.
* Recent constructive contributions significantly affect effective influence.

Together, these prevent “frozen oligarchies” of old influence.

### 7.2 Bounded Intensity

**Constraint 7.3 (Convex Cost).**
The burn cost function (f(\ell)) must be strictly convex and unbounded as (\ell \to \infty).

This ensures:

* A small number of agents cannot cheaply dominate by screaming; intensity is expensive.
* A broad coalition burning modestly can counter a few high-intensity actors.

### 7.3 Alignment with Epistemic Geometry

**Constraint 7.4 (Epistemic Override).**
Opinion fields must **modulate** but not override hard epistemic constraints:

* Proposals that violate core safety, legality, or well-established truths are **inadmissible**, regardless of burned support.
* EGPT-style impossibility and contradiction zones remain hard boundaries.

This keeps “burnable opinion” as a *governance layer*, not a replacement for evidence or reality.

---

## 8. Remarks and Extensions

1. **Temperature Interpretation.**
   The net burn (B^{(k)}(t) = \sum_a B_a^{(k)}(t)) vs issuance (I^{(k)}(t)) acts as a **temperature** for domain (k): high burn means high contention; low burn means consensus or apathy. Synthesis policies can throttle risky changes when temperature is high.

2. **Agent Role Separation.**
   Generative agents typically hold no credits; instead, humans spend credits to invoke high-cost agent processes (e.g., deep evaluations, multi-agent debates). This preserves human control while leveraging model capabilities.

3. **Coupling to Recursive Strata.**
   Opinion geometry can be layered atop recursive potentiality / impossibility strata: high burns on deep-tier reconfigurations trigger stricter review and safety cases, while lightweight surface changes stay cheap.

4. **Learning from Incidents.**
   Post-mortems feed back into both hazard classification (h(p)) and issuance functions (I_a^{(k)}), adjusting who is trusted where, and how expensive similar future actions should be.

5. **Geometric View.**
   At a high level, the burn-based opinion system adds a **resource-weighted measure** on the governance manifold of the synthesis system: an evolving field that shapes which paths through possibility space are explored, collapsed, or integrated, without erasing alternative branches.
