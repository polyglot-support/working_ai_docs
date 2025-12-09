# Operative Variational Lambda Calculus
## Document I: The Calculus
### Draft v0.3

---

### 1. Overview

This document specifies the **Operative Variational Lambda Calculus (OVLC)**—a typed lambda calculus extended with:

- **Geometric localization**: Terms are situated at geometric loci
- **Variational operators**: First-class variation and extremization
- **Opposed composition**: Tensioned pairing with resolution dynamics
- **Scheduled evaluation**: Explicit control over evaluation ordering
- **Co-geometric navigation**: Movement through configuration space

The calculus is parametric over choice of geometric substrate. Document II specifies the Holographic Spinal Architecture as one such substrate; Document III introduces Programmable Geometric Algebras.

---

### 2. Sorts

The calculus operates over four primitive sort families:

#### 2.1 Geometric Sorts

```
Geom       ::= G[d, a]              -- geometry of dimension d, arity a
             | G ⊗ G'               -- product geometry
             | G / ~                -- quotient geometry
             | G ↑ G'               -- fibered geometry (G over base G')
             | ∂(G)                 -- boundary of G
             | G*                   -- co-geometry (configuration space dual)
```

**Parameters**:
- `d ∈ ℕ`: dimension
- `a ∈ ℕ⁺`: arity (degrees of freedom per dimension)

#### 2.2 Schedule Sorts

```
Sched      ::= ε                    -- null (immediate)
             | s ; s'               -- sequential composition
             | s ∥ s'               -- parallel composition
             | s ◁ φ                -- guarded by predicate φ
             | ∮ s                  -- cyclic (repeating)
             | s ⊛ n                -- n-fold iteration
             | s @ G                -- schedule localized to geometry
```

Schedules form a monoid under sequential composition with `ε` as identity.

#### 2.3 Path Sorts

```
Path       ::= id(G)                -- identity path at G
             | p · p'               -- path composition
             | p⁻¹                  -- path reversal
             | τ(params)            -- elementary transformation
             | geodesic(G, x, y)    -- geodesic path in G from x to y
```

Paths through co-geometry space encode transformations between geometric configurations.

#### 2.4 Variation Sorts

```
Var        ::= δ[C]                 -- variation along direction C
             | δ*                   -- adjoint variation
             | ∫δ                   -- integrated variation
```

---

### 3. Types

#### 3.1 Base Types

```
Type       ::= Unit                 -- trivial type
             | T → T'               -- function type
             | T × T'               -- product type
             | T + T'               -- sum type
             | T @ G                -- geometric localization
             | [s]T                 -- scheduled type
             | Var(T)               -- variational type (T with variations)
             | T ⊕ T'               -- opposed type
```

#### 3.2 Geometric Type Formers

```
             | Sect(G, F)           -- sections of bundle F over G
             | Hom(G, G')           -- geometric morphisms
             | Config(G)            -- configuration type of G
             | Path(G; x, y)        -- path type in G
```

#### 3.3 Type Localization

The localization `T @ G` indicates that inhabitants of `T` are situated at geometry `G`. Key rules:

```
    (T → T') @ G  ≅  (T @ G) → (T' @ G)     -- functions preserve locus
    (T × T') @ G  ≅  (T @ G) × (T' @ G)     -- products preserve locus
    (T @ G) @ G'  ≅  T @ (G ⊗ G')           -- nested localization
```

---

### 4. Term Syntax

#### 4.1 Core Lambda Terms

```
Term   ::= x                                -- variable
         | λ(x : T) . e                     -- abstraction
         | e e'                             -- application
         | (e, e')                          -- pairing
         | π₁(e) | π₂(e)                    -- projections
         | inl(e) | inr(e)                  -- injections
         | case e of inl(x) → e₁ | inr(y) → e₂
```

#### 4.2 Geometric Terms

```
         | e @ G                            -- localize term at geometry
         | relocate(e, p)                   -- relocate along path p
         | navigate(e, p)                   -- navigate through co-geometry
         | fiber(e, x)                      -- fiber of e over point x
         | section(f)                       -- construct section from fiber map
```

#### 4.3 Scheduled Terms

```
         | e [s]                            -- scheduled evaluation
         | now(e)                           -- force immediate evaluation
         | defer(e, s)                      -- defer by schedule s
         | await(e₁, e₂)                    -- e₂ awaits completion of e₁
```

#### 4.4 Variational Terms

```
         | vary[p] e                        -- variational extension along path p
         | δ(e)                             -- variational derivative
         | δ(e)/δ(x)                        -- functional derivative
         | extremize(e, C)                  -- find extremum subject to C
         | ∫[G] e                           -- integrate over geometry G
```

#### 4.5 Opposed Terms

```
         | e ⊕ e'                           -- opposed pairing
         | tension(e)                       -- extract tension from opposed pair
         | resolve(e)                       -- find equilibrium
         | bias(e, λ)                       -- bias resolution by factor λ
```

#### 4.6 Operative Terms

```
         | algebra { ... }                  -- algebra definition (see §7)
         | A · e                            -- apply algebra A to term e
         | A ∘ A'                           -- algebra composition
         | A @ G                            -- situate algebra at geometry
```

---

### 5. Typing Rules

#### 5.1 Core Rules

```
                x : T ∈ Γ
    [Var]      ────────────
                Γ ⊢ x : T


                Γ, x : T ⊢ e : T'
    [Abs]      ────────────────────
                Γ ⊢ λ(x:T).e : T → T'


                Γ ⊢ e : T → T'    Γ ⊢ e' : T
    [App]      ────────────────────────────────
                Γ ⊢ e e' : T'
```

#### 5.2 Geometric Localization

```
                Γ ⊢ e : T    G : Geom
    [Loc]      ────────────────────────
                Γ ⊢ e @ G : T @ G


                Γ ⊢ e : T @ G    p : Path(G, G')
    [Reloc]    ──────────────────────────────────
                Γ ⊢ relocate(e, p) : T' @ G'

                (where T' = transport(T, p))


                Γ ⊢ e : T @ G    p : G* →* G'*
    [Nav]      ─────────────────────────────────
                Γ ⊢ navigate(e, p) : T' @ G'

                (navigation through co-geometry)
```

#### 5.3 Scheduled Evaluation

```
                Γ ⊢ e : T    s : Sched
    [Sched]    ──────────────────────────
                Γ ⊢ e [s] : [s]T


                Γ ⊢ e : [s]T    s reduces to ε
    [Force]    ──────────────────────────────────
                Γ ⊢ now(e) : T


                Γ ⊢ e₁ : [s₁]T₁    Γ ⊢ e₂ : T₁ → [s₂]T₂
    [Await]    ─────────────────────────────────────────────
                Γ ⊢ await(e₁, e₂) : [s₁;s₂]T₂
```

#### 5.4 Variational Rules

```
                Γ ⊢ e : T @ G    p : Path(G*)
    [Vary]     ─────────────────────────────────
                Γ ⊢ vary[p] e : Var(T) @ tube(G, p)


                Γ ⊢ e : Var(T)
    [Delta]    ─────────────────
                Γ ⊢ δ(e) : δT

                (δT is the tangent type to T)


                Γ ⊢ e : Var(T)    C : Constraint
    [Extr]     ─────────────────────────────────
                Γ ⊢ extremize(e, C) : T

                (returns critical point, may fail)
```

#### 5.5 Opposed Composition

```
                Γ ⊢ e : T    Γ ⊢ e' : T'    T ⋈ T' defined
    [Opp]      ──────────────────────────────────────────────
                Γ ⊢ e ⊕ e' : T ⊕ T'


                Γ ⊢ e : T ⊕ T'
    [Tens]     ─────────────────────
                Γ ⊢ tension(e) : ℝ≥0


                Γ ⊢ e : T ⊕ T'    tension(e) > 0
    [Res]      ──────────────────────────────────
                Γ ⊢ resolve(e) : Equil(T, T')
```

---

### 6. Reduction Semantics

#### 6.1 Core Reductions (β, η)

```
    (λ(x:T).e) e'  ──β──▶  e[e'/x]

    λ(x:T).(e x)   ──η──▶  e          (x ∉ FV(e))
```

#### 6.2 Geometric Reductions

```
    relocate(e @ G, id(G))     ──▶  e @ G

    relocate(relocate(e, p₁), p₂)  ──▶  relocate(e, p₁ · p₂)

    navigate(navigate(e, p₁), p₂)  ──▶  navigate(e, p₁ · p₂)

    fiber(section(f), x)  ──▶  f(x)
```

#### 6.3 Schedule Reductions

```
    e [ε]  ──▶  e

    e [s₁ ; s₂]  ──▶  (e [s₁]) [s₂]

    e [s₁ ∥ s₂]  ──▶  parallel(e [s₁], e [s₂])

    e [s ◁ φ]  ──▶  if φ then e [s] else e [await(φ); s]

    e [∮ s]  ──▶  e [s ; ∮ s]     (unfold cycle)
```

#### 6.4 Variational Reductions

```
    δ(c)  ──▶  0                       (c constant)

    δ(e + e')  ──▶  δ(e) + δ(e')       (linearity)

    δ(e · e')  ──▶  δ(e)·e' + e·δ(e')  (Leibniz)

    δ(vary[p] e)  ──▶  tangent(e, p)

    extremize(e, C) ──▶  solve(δ(e) = 0 subject to C)
```

#### 6.5 Opposed Reductions

```
    tension(e ⊕ e')  ──▶  ‖e‖ + ‖e'‖ - 2⟨e, e'⟩

    resolve(e ⊕ e')  ──▶  
        fixed_point(λx. balance(project(e, x), project(e', x)))

    bias(e ⊕ e', λ)  ──▶  (λ·e) ⊕ ((1-λ)·e')
```

---

### 7. Operative Algebras

An **operative algebra** is a first-class entity specifying a structured computation:

```
Algebra ::= algebra {
    name        : Identifier
    generators  : [(op_name : Op_Type)]
    relations   : [Equation]
    carrier     : Type
    locus       : Geom | Derived
    schedule    : Sched
}
```

#### 7.1 Algebra Application

```
                Γ ⊢ A : Algebra    Γ ⊢ e : A.carrier @ A.locus
    [AlgApp]   ────────────────────────────────────────────────
                Γ ⊢ A · e : A.carrier @ A.locus [A.schedule]
```

#### 7.2 Algebra Composition

```
                Γ ⊢ A : Algebra    Γ ⊢ A' : Algebra    compatible(A, A')
    [AlgComp]  ────────────────────────────────────────────────────────
                Γ ⊢ A ∘ A' : Algebra
```

Compatibility requires: `A.carrier @ A.locus` can be transported to `A'.carrier @ A'.locus`.

#### 7.3 Algebra Relocation

```
                Γ ⊢ A : Algebra    G : Geom    path : A.locus →* G
    [AlgReloc] ───────────────────────────────────────────────────
                Γ ⊢ A @ G : Algebra[locus := G]
```

---

### 8. Metatheory

#### 8.1 Type Safety

**Theorem (Preservation)**: If `Γ ⊢ e : T` and `e ──▶ e'`, then `Γ ⊢ e' : T'` where `T' ≤ T` (subtype or equal).

**Theorem (Progress)**: If `∅ ⊢ e : T` then either `e` is a value, or `∃e'. e ──▶ e'`, or `e` is blocked on a schedule guard.

#### 8.2 Geometric Coherence

**Theorem (Path Independence)**: For homotopic paths `p ≃ p'`:
```
    relocate(e, p) ≡ relocate(e, p')
```

**Theorem (Navigation Consistency)**: Co-geometry navigation preserves type structure up to transported equivalence.

#### 8.3 Variational Coherence

**Theorem (Variation Nilpotence)**: `δ(δ(e)) = 0` (exterior derivative property).

**Theorem (Extremization Soundness)**: If `extremize(e, C) ──▶ v`, then `δ(e)[v] = 0` and `C(v) = true`.

#### 8.4 Opposition Dynamics

**Theorem (Resolution Existence)**: For compatible `T ⊕ T'`, resolution always produces a value (though possibly at a limit point).

**Theorem (Tension Monotonicity)**: Under resolution dynamics, tension is non-increasing.

---

### 9. Notation Summary

| Symbol | Meaning |
|--------|---------|
| `G[d,a]` | Geometry of dimension d, arity a |
| `T @ G` | Type T localized at geometry G |
| `[s]T` | Type T with schedule s |
| `e [s]` | Term e evaluated on schedule s |
| `δ(e)` | Variational derivative of e |
| `vary[p] e` | Variational extension along path p |
| `e ⊕ e'` | Opposed composition |
| `resolve(e)` | Find equilibrium of opposed term |
| `A · e` | Apply algebra A to term e |
| `navigate(e, p)` | Navigate e through co-geometry along p |

---

### 10. Relation to Other Calculi

**Simply-typed λ-calculus**: OVLC without geometric localization, schedules, variation, or opposition.

**Linear λ-calculus**: Related to the resource-tracking aspects of schedules.

**Differential λ-calculus**: The variational fragment `δ`, `vary` extends differential λ-calculus.

**Spatial type theory**: Geometric localization `@ G` relates to spatial/modal type theories.

**Process calculi**: Schedules and parallel composition relate to π-calculus and session types.

---

*This document specifies the pure calculus. See Document II for the Holographic Spinal Architecture substrate, and Document III for Programmable Geometric Algebras.*
