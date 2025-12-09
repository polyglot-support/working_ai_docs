# Opposed Mathematics — Vol. H: Implementor’s Guide (Types & APIs) (v1)

> Purpose. Provide concrete data types, APIs, and reference algorithms to implement Opposed Mathematics (OM): cancellation algebra and characters (H1), normalization and confluence‑safe rewriting (H2), IPG runtime for states/paths/evaluation (H3), and interop pathways to classical linear algebra and serialization (H4). Language‑agnostic, with typed sketches in TypeScript/TS, Rust, and Python.

---

## H0. Design Principles
1) **Layer separation** (Vol. A–D): cancellation `⊕` ≠ group addition; character ops factored; division legality explicit.
2) **Canonical normal forms**: every public API returns `⊕`‑reduced outputs.
3) **CRT first**: factor group ops along prime powers; avoid large‑mod inverses.
4) **Sparse by default**: bucket counts by characters; aggressively cancel.
5) **Deterministic rewriting**: order‑independent via confluence (Vol. G1).

---

## H1. Core Types

### H1.1 Characters & Buckets
**TS**
```ts
export type Xi = string;           // e.g., "1","-1","i","-i"; or "e^{2πi k/n}"
export type Count = number;        // ℕ≥0
export type Bucket = Map<Xi, Count>;  // ℕ≥0[Ξ]
```
**Rust**
```rust
pub type Count = u64;
#[derive(Clone, Eq, PartialEq, Hash)] pub struct Xi(pub u32); // index into μ_n
pub type Bucket = hashbrown::HashMap<Xi, Count>;
```

### H1.2 Nil & Exclusory Expressions (Cancellation Algebra)
```ts
export type Nil = { tag: "Nil" };              // 𝓝
export type Atom<T> = { tag: "Atom", v: T };
export type Anti<T> = { tag: "Anti", x: Expr<T> };
export type Plus<T> = { tag: "Plus", l: Expr<T>, r: Expr<T> };
export type Expr<T> = Nil | Atom<T> | Anti<T> | Plus<T>;
```

### H1.3 Groups and CRT
```ts
export interface FinAb {
  order(): bigint;                           // |G|
  add(x: any, y: any): any;                  // group addition
  smul(n: bigint, x: any): any;              // n·x
  eq(x: any, y: any): boolean;
}
export interface Cyclic extends FinAb { m(): bigint; }
export interface CRTBlock { p: number; k: number; }  // Z_{p^k}
export interface CRTDecomp { blocks: CRTBlock[] }
```

### H1.4 States & Factors (IPG)
```ts
export type Point = readonly any[];          // x ∈ X = ∏ G_j
export type State = Map<Point, Bucket>;      // ψ: X → ℕ≥0[Ξ]
export interface Factor {                    // local predicate/transform
  scope: number[];                           // indices of variables
  table: Map<readonly any[], Bucket>;        // sparse potentials
}
```

---

## H2. Normalization Algorithms

### H2.1 Opposed Cancellation (Bucket Level)
**Goal**: reduce `Bucket` by canceling `χ` with `χ^{-1}` pairs; remove zero counts.
```ts
export function invertXi(chi: Xi): Xi { /* table or arithmetic in μ_n */ }
export function oplusBucket(b: Bucket): Bucket {
  const out = new Map<Xi, Count>();
  for (const [chi, a] of b) {
    if (a === 0) continue;
    const inv = invertXi(chi);
    const k = Math.min(a, out.get(inv) ?? 0);
    if (k > 0) {                         // cancel cross with existing inverse
      const invRem = (out.get(inv)! - k);
      if (invRem === 0) out.delete(inv); else out.set(inv, invRem);
      const aRem = a - k;
      if (aRem > 0) out.set(chi, (out.get(chi) ?? 0) + aRem);
    } else {
      out.set(chi, (out.get(chi) ?? 0) + a);
    }
  }
  return out;                              // 𝓝 if out.size===0 at call‑site
}
```
**Complexity**: O(|Ξ′|) per bucket, where Ξ′ is the set of occupied characters.

### H2.2 Expression Normal Form (Confluence‑safe)
```ts
export function reduceExpr<T>(x: Expr<T>): Expr<T> {
  // post‑order; use hash‑cons for structural sharing
  switch (x.tag) {
    case "Nil": return x;
    case "Atom": return x;
    case "Anti": {
      const y = reduceExpr(x.x);
      return { tag: "Anti", x: y };
    }
    case "Plus": {
      const a = reduceExpr(x.l), b = reduceExpr(x.r);
      // Detect A ⊕ overline(A)
      if (isOpposed(a, b)) return { tag: "Nil" };
      return canonPlus(a, b);              // AC‑sorted tree for deterministic form
    }
  }
}
```
**Notes**: `isOpposed` checks structural involution; `canonPlus` flattens and sorts children (multiset canonicalization). Confluence ensured by Vol. G1.

### H2.3 Parallelization
- **Bucket‑level**: shard by key ranges of `(index, Xi)`; use lock‑free counters; perform pairwise cancels in each shard, then cross‑shard reconciliation for inverse pairs.
- **State‑level**: partition `X` lexicographically; normalize buckets independently, then merge identical points with `⊕`.
- **Diagram rewriting**: use e‑graphs with phase‑aware equivalence; apply rewrite saturations then extract minimal cost normal forms.

---

## H3. IPG Runtime

### H3.1 Construction & Evaluation
```ts
export function emptyState(): State { return new Map(); }
export function addAmp(st: State, x: Point, chi: Xi, c: Count=1): State {
  const b = st.get(x) ?? new Map<Xi, Count>();
  b.set(chi, (b.get(chi) ?? 0) + c);
  st.set(x, b);
  return st;
}
export function reduceState(st: State): State {
  const out = new Map<Point, Bucket>();
  for (const [x, b] of st) {
    const r = oplusBucket(b);
    if (r.size > 0) out.set(x, r);        // else 𝓝 at x → drop bucket
  }
  return out;
}
```

### H3.2 Legality‑Checked Transforms
```ts
export interface DivGate { n: bigint; }      // apply only on legal factors
export function applyDiv(
  st: State, factors: FinAb[], mask: boolean[], n: bigint
): State {
  const out = new Map<Point, Bucket>();
  for (const [x, b] of st) {
    const y = x.slice();
    let legal = true;
    for (let j=0;j<x.length;j++) if (mask[j]) {
      if (!isCoprime(n, factors[j].order())) { // non‑coprime
        const inLegal = inLegalSublayer(factors[j], n, x[j]);
        if (!inLegal) { legal=false; break; }
        y[j] = sectionDiv(factors[j], n, x[j]);
      } else {
        y[j] = mulInv(factors[j], n, x[j]);
      }
    }
    if (legal) mergeBucket(out, y as Point, b);
  }
  return reduceState(out);
}
```
**Helpers**: `isCoprime`, `mulInv` via per‑prime tables; `inLegalSublayer` checks `x∈nG`; `sectionDiv` returns canonical preimage (Vol. B2.3).

### H3.3 Symmetry Quotients
```ts
export function quotient(
  st: State, rel: (x: Point) => string  // class id string
): State {
  const out = new Map<string, Bucket>();
  for (const [x, b] of st) addBucket(out, rel(x), b);
  // choose canonical rep for each class id → Point map
  return materializeClasses(out);
}
```

### H3.4 Character Shifts & Measurement
```ts
export function shiftAll(st: State, phase: Xi): State {
  const out = new Map<Point, Bucket>();
  for (const [x, b] of st) {
    const b2 = new Map<Xi, Count>();
    for (const [chi,a] of b) b2.set(mulXi(chi, phase), a);
    out.set(x, b2);
  }
  return reduceState(out);
}

export function measureXi(st: State, chi: Xi): Count {
  let s = 0; for (const [, b] of st) s += (b.get(chi) ?? 0); return s;
}
```

### H3.5 Born Semantics Interop
```ts
export function toComplex(
  st: State, embed: (chi: Xi) => Complex
): Map<Point, Complex> {
  const out = new Map<Point, Complex>();
  for (const [x, b] of reduceState(st)) {
    let z = 0+0i;
    for (const [chi,a] of b) z += a * embed(chi); // ℂ
    out.set(x, z);
  }
  return out;
}
```
Normalize and compute probabilities with `|z|² / ∑|z|²` (Vol. E).

---

## H4. Interop

### H4.1 Linear Algebra Bridges
- **DFT/QFT**: provide `toVector(st, basis)` then apply library FFTs; legality gates ensure needed roots exist or lift `Ξ`.
- **Sparse BLAS**: map `State` to CSR/COO matrices for factor graphs and homology matrices (Vol. F2); store character indices as small ints.

### H4.2 Classical Projection
- `projectClassical(st)` collapses `Ξ→1`, `𝓝→0`: convert buckets to integer counts by `∑ a_χ`.
- Guarantees: projections of OM algorithms reproduce classical outputs (Vol. G2).

### H4.3 Serialization
**JSON (stable)**
```json
{
  "xi": {"kind": "mu", "n": 8},
  "groups": [ {"Z": 8}, {"Z": 3} ],
  "state": [
    {"x": [0,0], "bucket": [["1", 2], ["-1", 1]]},
    {"x": [3,1], "bucket": [["i", 1]]}
  ]
}
```
**Binary**: `(varint n)(varint #groups)(blocks…)(#terms)(point…)(#chars)(charId,count)…`.

### H4.4 Validation & Testing
- **Golden tests**: small `Z_m` with known legal `n`, confirm centroid invariance and opposed cancellations.
- **Semantic parity**: compare `toComplex`+FFT outputs with direct classical pipelines on random seeds.
- **ZX rewrite parity**: verify compiler normal forms agree with FdHilb numerics for stabilizer circuits.

---

## H5. Performance Notes
- Precompute `μ_n` inverse tables per `p^k` block; store in a compact LUT.
- Use SIMD for complex embedding aggregation in `toComplex`.
- Cache `reduceState` results (hash of bucket multiset) when running cascades.

---

## H6. Security & Soundness
- Enforce layer separation at the type level (newtypes for `Bucket` vs. numeric vectors).
- Assert legality preconditions; provide a `liftCyclotomic(n)` to extend `Ξ` safely.
- Make normalization idempotent and total; expose only normalized states from public APIs.

---

## H7. Minimal End‑to‑End Example
```
// X = Z_8 × Z_3, Ξ = μ_8
let ψ = emptyState();
ψ = addAmp(ψ, [0,0], "1", 1);
ψ = addAmp(ψ, [4,0], "-1", 1);   // opposed on first factor
ψ = reduceState(ψ);                 // may produce 𝓝 at [·]
ψ = applyDiv(ψ, [Z8, Z3], [true,false], 5n); // legal on Z8 (inv=5 mod 8)
const amp = toComplex(ψ, embedMu8); // Born semantics
```

---

## H8. Roadmap
- Add `e-graph` backend for Vol. D rewrites.
- GPU kernels for bucket cancel and CRT‑based divisions.
- Formalize the API in a Lean/Coq extraction layer to certify normalization and legality.

