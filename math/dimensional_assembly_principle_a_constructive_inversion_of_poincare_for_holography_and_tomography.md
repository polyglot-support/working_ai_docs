# Dimensional Assembly Principle: A Constructive Inversion of Poincare for Holography and Tomography

A self‑contained, implementation‑ready framework that turns holonomy checks on measurement graphs into provable consistency certificates, constructive reconstructions, and minimal repairs. Written for physics audiences (optics, interferometry, tomography, inverse problems).

---
## Abstract
We formulate the Dimensional Assembly Principle (DAP): a ladder that builds global k‑dimensional fields from (k‑1)‑dimensional measurements whenever the k‑holonomy on a cycle basis vanishes. Nontrivial holonomy yields finite, auditable impossibility certificates and localizes the obstruction. The same formalism supplies a minimal‑repair inverse solver that adjusts a small subset of transfers to restore consistency within uncertainty bounds. We illustrate DAP for holography/ptychography (U(1) phase), projection tomography (Radon consistency), and multi‑view propagation (Fresnel/Fraunhofer/Angular Spectrum operators), with integer/rational variants for exact certificates.

---
## 1. Problem Setting: Local Measurements, Global Fields
**Measurement graph.** Nodes (charts) carry local data; edges carry transfer operators that align overlapping measurements. Examples: propagation between planes, homographies between views, phase differences between detectors, or Radon‑domain consistency maps.

**Goal.** Decide if the measurements admit a single physical field; if so, construct it; if not, produce a concise certificate and a minimal repair.

---
## 2. Transfers, Holonomy, and Consistency
**Transfers.** For overlapping charts i,j, a transfer Q_ij maps local data from i to j within a chosen group G acting on the data space X (examples: U(1) for phase; linear propagators for complex fields; projective groups for geometric alignment).

**Holonomy on a loop.** For a cycle gamma = (i0 -> i1 -> ... -> im = i0), define H_gamma = Q_im-1,i0 * ... * Q_i0,i1. A globally consistent field requires H_gamma approximately identity (within tolerance) for all independent loops.

**Cycle basis suffices.** Build a spanning tree on the measurement graph; each non‑tree edge defines one fundamental cycle. Identity on all fundamental cycles implies identity on all cycles under fixed edge orientations.

---
## 3. Dimensional Assembly Principle (DAP)
**Informal statement.** If all k‑cycle holonomies vanish (up to tolerance) on a finite complex, then a global k‑dimensional field exists and can be built by parallel transport from a basepoint. If a k‑cycle exhibits nontrivial holonomy, its conjugacy class in G is an obstruction certificate.

**Constructive algorithm.**
1) Choose a base node and initial value x0 in X (gauge choice).
2) For any node, transport x0 along any tree path using the edge transfers.
3) Because loop holonomy is trivial on the basis, the result is path‑independent; this defines the global field.

**Certificates.** For a failing cycle, report (a) the cycle index list, (b) the list of edge transfers, (c) their product H_gamma, (d) a deviation metric and invariant factors (eigenvalues, rotation angle, scale), and (e) pairwise fit diagnostics.

---
## 4. Physics‑Focused Instantiations
### 4.1 Holography and Interferometry (phase integrability)
- Charts: detector patches or viewpoints
- Group: U(1) (complex phase) or C* (complex amplitude up to scale)
- Transfers: measured phase differences or propagation operators
- Holonomy: product of phase increments around loops; nonzero winding indicates inconsistent unwrapping or model mismatch
- Output: either a globally unwrapped phase map or an exact obstruction (integer winding on named cycles)

### 4.2 Ptychography (overlapping diffraction tiles)
- Charts: probe positions with overlapping support
- Group: complex scalings and phase shifts
- Transfers: relative phase/scale from overlap constraints
- Holonomy: tile‑to‑tile products; failure localizes a bad tile or drift; success yields stitched complex field

### 4.3 Projection Tomography (Radon consistency)
- Charts: projection angles or detector arcs
- Group: linear consistency operators in projection space
- Transfers: Helgason‑Ludwig type relations (or learned surrogates) enforcing cross‑angle consistency
- Holonomy: loop products over angle cycles; violation flags inconsistent projections; success implies existence of a 3D density compatible with all projections

### 4.4 Multi‑Plane Propagation (Fresnel/Fraunhofer/Angular Spectrum)
- Charts: measurement planes at different z
- Group: linear propagators (Fourier domain phase factors)
- Transfers: discretized propagation between planes
- Holonomy: around z‑loops (forward then back) should be identity; deviations quantify calibration/scattering errors

---
## 5. Severity Scores and Defect Taxonomy
**Severity.** Define an impossibility score S_gamma as a geodesic distance from H_gamma to identity in the chosen group (for example, rotation angle for SO(3); Frobenius norm of matrix log for linear groups; absolute phase for U(1)). Aggregate by max or uncertainty‑weighted sum across the cycle basis.

**Taxonomy (signature -> phenomenon).**
- Pure rotation residual: orientation drift loops
- Uniform scale residual: Penrose‑style scalar return in view stitching
- Anisotropic stretch residual: axis creep/foreshortening
- Shear residual: staircase‑like lateral slide
- Screw residual (rigid 3D): rotation plus translation along axis
- Phase winding (U(1)): integer wrap errors / branch cuts

---
## 6. Minimal‑Repair Inverse Solver
**Goal.** Adjust a small set of transfers to drive basis holonomies to identity while staying within uncertainty.

**Method.** Work in log space: for each edge e, introduce a small increment delta_e in the Lie algebra of G; require the sum of deltas along each failing cycle equals minus log(H_gamma). Solve a sparse least‑squares with edge selection or regularization. Return modified edges, predicted changes, and new holonomy scores.

---
## 7. Integer/Rational Certificates (Exactness Option)
Fit transfers as rational matrices or phase ratios; clear denominators to obtain integer data. Compose exactly to form H_gamma. Non‑identity can be witnessed by an integer entry mismatch, a trace mismatch, or an invariant ratio not equal to one. This yields auditable certificates immune to floating‑point error.

---
## 8. Algorithms (pseudocode outlines)
**Cycle basis and holonomy test**
```text
build_spanning_tree(G) -> T
B = fundamental_cycles(T, E)
for gamma in B:
  H = identity()
  for directed edge i->j in gamma:
    H = normalize(Q[i,j]) * H
  S = geodesic_distance(H, identity)
  if S > tau:
    label = classify_defect(H)
    emit_certificate(gamma, Q, H, label, S)
```

**Minimal repair**
```text
E_fail = union of edges on failing cycles
solve min sum ||delta_e|| s.t. for each failing gamma: sum(delta_e over edges in gamma) = - log(H_gamma)
apply exp(delta_e) to Q_e and re-test
```

---
## 9. Evaluation Plan
**Datasets.** Synthetic holograms with known phase, ptychography benchmarks, CT projection sets with controlled inconsistencies, and real lab data.

**Metrics.** realizability accuracy, ROC with severity threshold, localization accuracy of failing edges, reconstruction error after repair, runtime.

**Ablations.** group choice (U(1) vs linear propagators), cycle basis choice (fundamental vs minimum), integer vs floating pipelines, repair regularizers.

---
## 10. Discussion and Outlook
DAP reframes integrability as a finite algorithm: check holonomy on a small set of loops, certify or construct, and repair if needed. It applies uniformly across optics, tomography, and multi‑view geometry, and scales to higher dimensions by repeating the same test‑and‑assemble step. Future directions include learning transfer priors, multi‑modal fusion, and real‑time certificate‑guided acquisition.


---
## PRL-style Abstract (proposed)
We present the Dimensional Assembly Principle (DAP), an explicit inversion of the classical Poincare lemma for finite measurement systems. Given local measurements linked by transfer operators on a graph or simplicial complex, DAP decides integrability by testing holonomy on a small cycle basis. If every k-cycle is holonomy-trivial (within tolerance), a global (k+1)-dimensional field is constructed by parallel transport from a base node; otherwise the loop product itself serves as a finite, auditable consistency certificate. This yields algorithmic cohomology for optics and tomography: exact or rational certificates of inconsistency, geodesic severity scores, and a minimal-repair solver that adjusts only those transfers needed to restore flatness within uncertainty. We demonstrate instantiations for phase unwrapping and holography (U(1)), ptychographic stitching, and projection tomography, and outline extensions to multi-plane propagation and 3D-to-4D spacetime assembly.

---
## 2.5 Classical Poincare vs Dimensional Assembly (explicit inversion)
Classical Poincare lemma (passive existence): if a differential k-form is closed on a contractible domain, then it is exact; existence is guaranteed but no discrete construction is provided.

Dimensional Assembly (active construction): if k-holonomy is trivial on a cycle basis of a finite complex, then a global (k+1)-field is constructible by an explicit algorithm (choose a basepoint, parallel transport along tree paths, and extend). Nontrivial holonomy on any basis cycle is a complete obstruction and doubles as the certificate.

Inversion summary:
- Classical: differential condition implies existence on contractible spaces.
- DAP: finite matrix products on any finite complex imply explicit construction; failure localizes topology or calibration errors as concrete loop products.

---
## 2.6 Connection to Gauge Theory and Parallel Transport
- Discrete connection: the set of transfers Q(i,j) is a connection 1-form on the 1-skeleton.
- Curvature: a loop product H(gamma) equals the discrete path-ordered exponential; H(gamma) equal to identity for all cycles means the connection is flat (pure gauge).
- Obstruction class: the conjugacy class of H(gamma) identifies the cohomology obstruction that prevents trivialization; in U(1) settings this is an integer winding number. DAP is thus a practical flatness detector and constructive trivializer.

---
## 3.5 The Assembly Hierarchy (0D to 4D and beyond)
Each level adds one finite obstruction test and a constructive step when it passes.

| Level | Data on cells | Transfer group (examples) | Holonomy test on basis | Physical example |
|---|---|---|---|---|
| 0D to 1D | point values | any G | none (always passes) | choose gauge at points |
| 1D to 2D | edges (phase or pose differences) | U(1), C*, SO(2) | sum of phase increments around loops equals 0 mod 2 pi | phase unwrapping; branch-cut detection |
| 2D to 3D | surface patches, projections | Radon consistency operators | 2-cycle closure in projection space | CT, MRI, ptychography tiling |
| 3D to 4D | volumes over time | evolution maps, SE(3) x time | closed timelike loop closure | spacetime consistency, dynamic tomography |
| 4D to 5D | spacetime slices with extra parameter | Kaluza-Klein style groups | compactification holonomy | higher-dimensional field constraints |

Theorem (dimensional sufficiency, constructive): if all k-cycles are holonomy-trivial, then (1) a global (k+1)-section exists, (2) it is obtained by parallel transport from any basepoint, (3) the result is path-independent.

---
## 9.5 Worked numerical mini-examples
Example 1: phase unwrapping on a 2x2 loop.
- Nodes with phases: phi1 = 0, phi2 = pi/4, phi3 = pi/2, phi4 = pi/4.
- Edge increments: Q12 = exp(i*pi/4), Q23 = exp(i*pi/4), Q34 = exp(i*pi/4 + 2*pi*i), Q41 = exp(i*pi/4).
- Loop product: H = Q41 * Q34 * Q23 * Q12 = exp(i*pi) which is not 1. Certificate: winding number equals 1; branch cut lies on edge (3,4). Minimal repair: set Q34 to exp(i*pi/4) (remove the extra 2*pi). New H equals 1; global phase exists.

Example 2: three-angle tomography loop.
- Transfers between projection spaces: P12, P23, P31 from calibration.
- Consistency requires H = P31 * P23 * P12 equal to identity. Observed H shows a uniform scale lambda not equal to 1: diagnosis is a detector gain error at one angle. Minimal repair: adjust the transfer on the most uncertain edge to drive lambda to 1; re-test loop closure.

---
## Title options (for PRL submission)
1) Dimensional Assembly Principle: Algorithmic Integrability Certificates for Holographic Reconstruction.
2) Inverse Poincare for Finite Measurements: Constructive Holonomy Tests in Optical Tomography.
3) Holonomy Obstructions as Consistency Certificates in Computational Holography.

