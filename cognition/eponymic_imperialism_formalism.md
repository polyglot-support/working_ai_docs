## Eponymic Imperialism: A Formal Model of Abstraction Capture in Scientific Systems (Clean Draft)

### Abstract
Scientific naming conventions frequently privilege *personal eponyms* over *functional descriptors*, producing an epistemic distortion that binds abstract ideas to specific cultural, linguistic, and institutional contexts. This framework — **Eponymic Imperialism** — treats such naming as **abstraction capture**, wherein conceptual universality is constrained by the cultural identity of its signifier. The effect narrows access to knowledge and suppresses cross-domain integration by generalists, whose work depends on higher-level abstraction rather than disciplinary specialization.

---

### 1. Definitions
| Term | Definition |
|---|---|
| **Eponymic Encoding** | Binding an abstract or universal concept to a proper name (e.g., “Schrödinger’s Cat”). |
| **Abstraction Capture** | When an idea’s general form is constrained by the linguistic, cultural, or institutional origin of its terminology. |
| **Eponymic Imperialism** | Dominance of named-person signifiers that enforce cultural gatekeeping over scientific and mathematical universals. |
| **Cognitive Accessibility Gradient (CAG)** | Additional cognitive/cultural load required to access a concept due to non-descriptive naming. |
| **Generalist Cognitive Field (GCF)** | The meta-domain where integrative, cross-disciplinary reasoning occurs at higher abstraction than individual specializations. |

---

### 2. The Eponymic Feedback Loop
1. **Discovery** → An idea emerges within a cultural setting.
2. **Attribution** → The concept is anchored to a discoverer’s name, not the phenomenon.
3. **Institutionalization** → Textbooks, journals, and curricula canonize the eponym.
4. **Gatekeeping** → Access presumes familiarity with name, culture, and discipline.
5. **Abstraction Collapse** → Cross-domain transferability decreases; universality is lost.

Formalization:
\[ A_{\text{pure}} \xrightarrow{\text{naming}} A_{\text{captured}} = A_{\text{pure}} \otimes C_{\text{culture}} \]
where \(A_{\text{pure}}\) is the ideal abstraction and \(C_{\text{culture}}\) the cultural signature. The tensor product \(\otimes\) represents binding abstract form to cultural structure.

---

### 3. Cognitive Impact
The accessibility cost grows with linguistic, cultural, and specialization loads:
\[ CAG = f(L, C, S) \]
where \(L\) = linguistic complexity, \(C\) = cultural distance, \(S\) = specialization density.

Knowledge diffusion across fields decays with rising CAG:
\[ \text{Cross-domain transfer rate} \propto e^{-CAG} \]

#### Examples of Cross-Domain Hindrance
- **Physics**: *Einstein–Rosen bridges* obscure a transferable structure of **spacetime connectivity** (and its analogues in topology and networks) behind two surnames. A descriptive label like **geodesic-connecting wormhole metric** better advertises the underlying structure.
- **Biology**: *Mendel’s laws* are framed as a discoverer’s property rather than **genetic probability distributions** or **inheritance operators**, obscuring ready equivalences with information theory and Bayesian models.

**Policy Implication:** Treat CAG as an educational design constraint. Prefer descriptive labels in curricula, glossaries, and standards to reduce CAG and invite integrative reasoning across languages and cultures.

---

### 4. Generalists as Integrative Catalysts
Generalists operate over abstractions extracted from many domains. If each domain \(D_i\) has semantic field \(S_i\), the generalist’s workspace is the union of abstract projections:
\[ G = \bigcup_i \operatorname{Proj}_A(S_i) \]
where \(\operatorname{Proj}_A\) extracts invariant structures (relations, symmetries, transformations). Eponymic labels fragment these invariants by masking isomorphisms across fields.

---

### 5. Epistemic Consequences
- **Reduced Universality:** Historical references replace relational structure.
- **Blocked Transfer:** Isomorphic patterns wear discipline-specific names that hide equivalence.
- **Pedagogical Inefficiency:** Students memorize tokens instead of models.
- **Cognitive Waste:** Fields reinvent vocabulary for the same structures.
- **Suppressed Generalism:** Systems reward narrow fluency; penalize high-level synthesis.

---

### 6. Historical and Cultural Note
Einstein’s thought experiments de-personalized physics to invite **conceptual empathy**; Nobel redirected recognition toward contributions **to humanity** rather than to fame. Both gestures align with the claim that knowledge is not owned; names should not gatekeep universals.

---

### 7. Toward a Descriptive Science Lexicon (Expanded)
A non-exhaustive map from eponyms → descriptive forms. Use, adapt, or extend.

#### Physics & Engineering
| Eponym | Descriptive Form |
|---|---|
| Schrödinger’s Cat | Quantum Observation Paradox |
| Heisenberg’s Uncertainty Principle | Conjugate Measurement Limit |
| Hilbert Space | Complete Inner Product Space |
| Maxwell’s Equations | Unified Electromagnetic Field Relations |
| Newton’s Laws | Classical Motion Axioms |
| Faraday’s Law | Electromagnetic Induction Relation |
| Lenz’s Law | Inductive Opposition Rule |
| Ohm’s Law | Electrical Resistance Relation |
| Kirchhoff’s Laws | Network Conservation Relations |
| Ampère’s Law | Magnetostatic Circulation Relation |
| Coulomb’s Law | Electrostatic Inverse-Square Relation |
| Gauss’s Law | Field-Flux Conservation Relation |
| Hubble’s Law | Cosmic Recession–Distance Proportionality |
| Planck’s Constant | Quantum of Action |
| Pauli Exclusion Principle | Fermion State Non-Cooccupation Rule |
| Fermi–Dirac Statistics | Fermion Occupancy Distribution |
| Bose–Einstein Condensate | Ground-State Bosonic Coherence Phase |
| Doppler Effect | Frequency Shift Under Relative Motion |
| Zeeman/Stark Effects | Spectral Splitting by Field Coupling |
| Snell’s Law | Refraction Angle Relation |
| Huygens’ Principle | Wavefront Propagation Construction |
| Bragg’s Law | Lattice Diffraction Condition |
| Hooke’s Law | Linear Elastic Response |
| Bernoulli’s Principle | Flow Pressure–Velocity Relation |
| Pascal’s Principle | Fluid Pressure Transmission |
| Archimedes’ Principle | Buoyancy–Displaced Fluid Relation |

#### Chemistry & Biology
| Eponym | Descriptive Form |
|---|---|
| Boyle’s Law | Gas Pressure–Volume Relation |
| Charles’s Law | Gas Temperature–Volume Relation |
| Avogadro’s Number | Particles per Mole Constant |
| Boltzmann Constant | Energy–Temperature Proportionality |
| Arrhenius Equation | Temperature–Rate Exponential Relation |
| Gibbs Free Energy | Usable Chemical Potential |
| Hess’s Law | Path-Independent Enthalpy Sum |
| Beer–Lambert Law | Absorbance–Concentration Relation |
| Le Chatelier’s Principle | Equilibrium Response Heuristic |
| Michaelis–Menten Kinetics | Saturating Enzyme Rate Law |
| Mendel’s Laws | Genetic Inheritance Distributions |
| Darwinian Evolution | Adaptive Selection Process |
| Watson–Crick Model | Complementary Double-Helix Structure |

#### Mathematics, CS, and Information
| Eponym | Descriptive Form |
|---|---|
| Fourier Transform | Frequency Decomposition Operator |
| Laplace Transform | Exponential Kernel Integral Transform |
| Euler’s Formula/Identity | Exponential–Trigonometric Equivalence |
| Bayes’ Theorem | Conditional Probability Update |
| Pythagorean Theorem | Orthogonal Distance Relation |
| Riemann Hypothesis | Zeta-Zero Critical Line Conjecture |
| Fermat’s Last Theorem | Integer Power Sum Constraint |
| Hilbert’s Problems | Foundational Research Program List |
| Noether’s Theorem | Symmetry–Conservation Correspondence |
| Gödel’s Incompleteness | Formal System Undecidability Limits |
| Turing Machine | Abstract Computation Model |
| Nyquist–Shannon Sampling | Bandlimit–Sampling Sufficiency Theorem |

#### Systems, Society, and “Laws” of Practice
| Eponym | Descriptive Form |
|---|---|
| Occam’s Razor | Minimal Sufficiency Principle |
| Pareto Principle | Heavy-Tail Contribution Pattern |
| Zipf’s Law | Rank–Frequency Power Law |
| Moore’s Law | Semiconductor Doubling Trend |
| Metcalfe’s Law | Network-Value Quadratic Scaling |
| Amdahl’s Law | Parallel Speedup Limit |
| Little’s Law | Queue Throughput–WIP Relation |
| Goodhart’s Law | Target-Metric Deformation Principle |
| Campbell’s Law | Evaluation–Corruption Tendency |
| Murphy’s Law | Failure Expectancy Heuristic |
| Dunbar’s Number | Social Cohesion Capacity Estimate |

*(Note: Some eponyms honor historically marginalized contributors or encode important lineage; the reform aims to **add** descriptive labels, not erase history.)*

---

### 8. Implementation Notes
- **Curriculum**: Pair every eponym with a descriptive alias at first mention.
- **Glossaries**: Maintain open, multilingual, machine-readable mappings.
- **Tools**: Use AI translation/annotation layers to auto-expand eponyms in texts.
- **Publications**: Encourage descriptive titles and abstracts alongside eponyms.

---

### 9. Conclusion
Eponymic Imperialism reifies history over structure, culture over universality, and authority over understanding. Renaming toward functional abstraction re-opens science to its polyglot inheritance, enabling generalists and specialists to collaborate on shared structures. This is not only linguistic reform but an **ontological correction** to the systemic *error space* that constrains collective progress.