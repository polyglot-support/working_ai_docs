# Prime–Parametric Fractal Number System (v2)

This is a streamlined, self-contained formalism for the **prime–parametric fractal number system**. It keeps the original spirit (primes + primorials + braids + recursion) but is:

- structurally simpler,
- algebraically explicit,
- implementation-oriented.

---
## 1. Core Objects

### 1.1 Truncation Parameters
We work with finite truncations:

- `N_p` – number of primes used.
- `N_r` – number of primorial levels.
- `N_b` – number of braid strands.
- `L_max` – max braid word length.

Let the first `N_p` primes be
\[\mathbb{P}_N = \{p_1,\dots,p_{N_p}\}.\]
Define **primorials**
\[P_k = \prod_{i=1}^k p_i, \quad k=1,\dots,N_r.\]

### 1.2 Braid Space
Let \(\mathcal{B}_{N_b}\) be the braid group on `N_b` strands. We represent a braid \(\sigma\) as a reduced word over generators \(\sigma_1,\dots,\sigma_{N_b-1}\) with length
\[L(\sigma) \le L_{\max}.\]

We assume a **word metric** \(d_B\) on braids (e.g. edit distance after reduction).

### 1.3 Prime–Parametric State Space
Define the truncated **state manifold**
\[\mathcal{F}_N = \mathbb{R} \times \prod_{p\in\mathbb{P}_N} S^1_p \times \prod_{k=1}^{N_r} S^1_{P_k} \times \mathcal{B}_{N_b},\]
with
- \(S^1_p = \mathbb{R}/(2\pi/p)\mathbb{Z}\),
- \(S^1_{P_k} = \mathbb{R}/(2\pi/P_k)\mathbb{Z}\).

A **prime–parametric number** is a point
\[z = (a, \{\phi_p\}, \{\psi_k\}, \sigma) \in \mathcal{F}_N,\]
where
- \(a \in \mathbb{R}\) (base amplitude),
- \(\phi_p \in [0,2\pi/p)\) (prime phase),
- \(\psi_k \in [0,2\pi/P_k)\) (primorial phase),
- \(\sigma \in \mathcal{B}_{N_b}\) (braid pattern).

This is the **finite configuration** that approximates an infinite prime–parametric object.

---
## 2. Canonical Projection to \(\mathbb{R}^2\)

We define a canonical projection
\[\pi : \mathcal{F}_N \to \mathbb{R}^2, \quad z \mapsto (r,\theta).\]

### 2.1 Weights
Use:
- prime weights: \(w_p = 1/p^2\),
- primorial weights: \(w_k = 1/P_k\),
- braid weight: \(w_b = 1/N_b\).

Let:
- braid complexity \(C(\sigma)=L(\sigma)\),
- braid height \(H(\sigma)\) = sum of (signed) crossing heights in the word.

### 2.2 Radial Component
\[r(z) = |a|\sqrt{1 + \sum_{p\in\mathbb{P}_N} w_p\,\phi_p^2 + \sum_{k=1}^{N_r} w_k\,\psi_k^2 + w_b C(\sigma)}.\]

### 2.3 Angular Component
\[\theta(z) = \arg(a) + \sum_{p\in\mathbb{P}_N} \frac{\phi_p}{p} + \sum_{k=1}^{N_r} \frac{\psi_k}{P_k} + \frac{H(\sigma)}{N_b}.\]

We will write
\[(r,\theta) = \pi(z).\]

---
## 3. Braid–Prime Coupling

To make multiplication nontrivial and geometry-aware, we couple braids and primes.

### 3.1 Strand Assignments
Each prime \(p\) is mapped to a strand index
\[s_p = (p \bmod N_b) + 1 \in \{1,\dots,N_b\}.\]

### 3.2 Linking Number (Abstracted)
We assume an integer **linking functional**
\[\text{link} : \mathcal{B}_{N_b} \times \mathcal{B}_{N_b} \times \mathbb{P}_N \times \mathbb{P}_N \to \mathbb{Z}\]
that measures how strands \(s_p\) and \(s_q\) are intertwined when braids \(\sigma_1,\sigma_2\) are composed and closed. Implementation details can vary; we only require:

1. **Antisymmetry** in \(p,q\): \(\text{link}(\sigma_1,\sigma_2,p,q) = -\text{link}(\sigma_1,\sigma_2,q,p)\).
2. **Bilinearity** in braid concatenation.

### 3.3 Coupling Kernel
Define
\[\kappa(p;\sigma_1,\sigma_2) = \sum_{q\in\mathbb{P}_N} \frac{\text{link}(\sigma_1,\sigma_2,p,q)}{\operatorname{lcm}(p,q)\sqrt{pq}}.\]

This is a small real-valued perturbation that shifts the prime phases during multiplication.

---
## 4. Algebra on \(\mathcal{F}_N\)

We define addition, multiplication, and some auxiliary operations.

### 4.1 Modular Angle Arithmetic
For each prime or primorial component, arithmetic is taken modulo the corresponding period:

- For \(\phi_p\): modulo \(2\pi/p\).
- For \(\psi_k\): modulo \(2\pi/P_k\).

We write `⊕` for angle addition modulo its period where useful.

### 4.2 Addition
Given
\[z_i = (a_i, \{\phi_p^{(i)}\}, \{\psi_k^{(i)}\}, \sigma_i), \quad i=1,2,\]
we define
\[z_1 + z_2 = (a_1+a_2, \{\phi_p^{(1)} \oplus \phi_p^{(2)}\}, \{\psi_k^{(1)} \oplus \psi_k^{(2)}\}, \sigma_1\sigma_2).\]

Here \(\sigma_1\sigma_2\) is braid word concatenation followed by reduction, truncated to length \(L_{\max}\).

### 4.3 Primorial Tensor Product
For primorial phases we use a slightly nonlinear combination to encode multiplicative structure:
\[\psi_k^{(1)} \otimes \psi_k^{(2)} = \Big(\psi_k^{(1)} + \psi_k^{(2)} + \frac{\psi_k^{(1)}\psi_k^{(2)}}{2\pi/P_k}\Big) \bmod \frac{2\pi}{P_k}.\]

This is a simple, implementation-friendly variant of the original tensor rule.

### 4.4 Multiplication
Define the product \(z_1 z_2\) as
\[z_1 z_2 = (a_1 a_2, \{\phi_p^{\text{new}}\}, \{\psi_k^{\text{new}}\}, \sigma_1 \circ \sigma_2),\]
where
\[\phi_p^{\text{new}} = (\phi_p^{(1)} + \phi_p^{(2)} + \kappa(p;\sigma_1,\sigma_2)) \bmod \frac{2\pi}{p},\]
\[\psi_k^{\text{new}} = \psi_k^{(1)} \otimes \psi_k^{(2)},\]
\(\sigma_1 \circ \sigma_2\) is geometric braid composition with reduction and truncation.

This makes multiplication **non-commutative** in general because the braid sector is non-commutative.

### 4.5 Hadamard Product
A pointwise “phase–phase” product:
\[z_1 \odot z_2 = (a_1 a_2, \{\phi_p^{(1)}\phi_p^{(2)} / (2\pi/p)\}_{p}, \{\psi_k^{(1)}\psi_k^{(2)} / (2\pi/P_k)\}_{k}, \sigma_1\sigma_2).\]

This is mainly useful as a secondary composition operator in algorithms.

### 4.6 Exponential Flow
For \(t \in \mathbb{R}\):
\[\exp_N(t z) := (e^{ta},\{t\phi_p \bmod 2\pi/p\},\{t\psi_k \bmod 2\pi/P_k\}, \sigma^{\lfloor t \rfloor}),\]
where \(\sigma^m\) is \(m\)-fold braid composition with truncation.

This defines a simple 1-parameter flow on \(\mathcal{F}_N\).

---
## 5. Recursive Fractal Encoding

The key idea: use **polar projection** to obtain integers, then re-embed them as prime–parametric states, recursively.

### 5.1 Canonical Integer Embedding
For an integer \(n \ge 2\), define \(\tau_N(n) \in \mathcal{F}_N\) as
\[\tau_N(n) = \big(n,\{\phi_p(n)\},\{\psi_k(n)\},\beta(n)\big).\]

A simple choice:
- \(\phi_p(n) = 2\pi (n \bmod p)/p\),
- \(\psi_k(n) = 2\pi (n \bmod P_k)/P_k\),
- \(\beta(n)\) = braid constructed from residue pattern \(n \bmod P_k\) across levels.

The braid \(\beta(n)\) encodes how \(n\) sits in the primorial lattice (e.g. ordering of residues, gcd structure, etc.).

### 5.2 Recursive Operator
Let \((r,\theta) = \pi(z)\). For depth \(d \ge 0\), define
\[\mathcal{R}_0(z) = z,\]
\[\mathcal{R}_d(z) = \big(\mathcal{R}_{d-1}(\tau_N(\lfloor r \rfloor)),\; \mathcal{R}_{d-1}(\tau_N(\lfloor 10^k \theta \rfloor))\big),\]
for some fixed integer scaling factor \(k\) (e.g. \(k=3\)).

Thus \(\mathcal{R}_d(z)\) lives in a binary tree of depth \(d\) whose nodes are elements of \(\mathcal{F}_N\). It encodes a **self-similar decomposition** of \(z\): the radial and angular parts become new base integers at deeper levels.

### 5.3 Fractal Arithmetic (Sketch)
Operations on recursive states \(\mathcal{R}_d(z)\) can be defined recursively:

- **Fractal addition**: apply `+` at each corresponding node, top-down.
- **Fractal multiplication**: use `z_1 z_2` at leaves and propagate coupling terms upward.

This yields depth-dependent operations that approximate a putative infinite-depth limit as \(d \to \infty\).

---
## 6. Geometry on \(\mathcal{F}_N\)

### 6.1 Metric
Define the squared distance
\[d_N(z_1,z_2)^2 = |a_1-a_2|^2 + \sum_{p\in\mathbb{P}_N} \frac{\Delta\phi_p^2}{p^2} + \sum_{k=1}^{N_r} \frac{\Delta\psi_k^2}{P_k} + \frac{1}{N_b} d_B(\sigma_1,\sigma_2)^2,\]
where each phase difference is taken with the minimal wrap-around on the circle.

This turns \(\mathcal{F}_N\) into a finite-dimensional metric space.

### 6.2 Curvature Functional
We can define a synthetic “curvature” \(K_N(z)\) encoding prime / primorial resonance:
\[K_N(z) = C(\sigma) + \sum_{p,q\in\mathbb{P}_N} \frac{\sin\big(\pi p\phi_p / (q\phi_q + \varepsilon)\big)}{\operatorname{lcm}(p,q)} + \sum_{k,m=1}^{N_r} \frac{\sin\big(\pi P_k\psi_k / (P_m\psi_m + \varepsilon)\big)}{P_k P_m},\]
with small \(\varepsilon>0\) for stability.

Heuristically, high \(|K_N(z)|\) indicates strong resonance between prime and primorial phases.

---
## 7. Algorithms (Implementation View)

Below, `state` means an element of \(\mathcal{F}_N\).

### 7.1 Encode an Integer
```python
def encode_number(n, primes, primorials, N_b, L_max):
    # primes: list of p
    # primorials: list of P_k
    a = float(n)

    phi = {p: 2*math.pi * (n % p) / p for p in primes}
    psi = {P: 2*math.pi * (n % P) / P for P in primorials}

    sigma = build_braid_from_residues(n, primorials, N_b, L_max)
    return (a, phi, psi, sigma)
```

### 7.2 Multiply Two States
```python
def multiply(z1, z2, primes, primorials):
    a1, phi1, psi1, sig1 = z1
    a2, phi2, psi2, sig2 = z2

    a = a1 * a2

    phi = {}
    for p in primes:
        coupling = kappa(p, sig1, sig2, primes)  # braid–prime coupling
        angle = phi1[p] + phi2[p] + coupling
        phi[p] = angle_mod_prime(angle, p)

    psi = {}
    for P in primorials:
        psi[P] = primorial_tensor(psi1[P], psi2[P], P)

    sigma = compose_braids(sig1, sig2)
    sigma = reduce_truncate_braid(sigma)

    return (a, phi, psi, sigma)
```

### 7.3 Recursive Encode
```python
def recursive_encode(z, depth, primes, primorials, N_b, L_max, k=3):
    if depth == 0:
        return z

    r, theta = polar_project(z, primes, primorials)

    zr = encode_number(int(math.floor(r)), primes, primorials, N_b, L_max)
    zt = encode_number(int(math.floor((10**k) * theta)), primes, primorials, N_b, L_max)

    return (
        recursive_encode(zr, depth - 1, primes, primorials, N_b, L_max, k),
        recursive_encode(zt, depth - 1, primes, primorials, N_b, L_max, k),
    )
```

### 7.4 Complexity (Order-of-Magnitude)
For fixed truncation parameters:

- Encode integer: \(O(N_p + N_r + N_b^2)\) (braid construction dominates).
- Multiply: \(O(N_p^2 + N_r + L_{max}^2)\) if coupling and braid ops are dense.
- Recursive encode to depth \(d\): \(O(d (N_p + N_r + N_b^2))\) per branch, with total nodes \(O(2^d)\).

---
## 8. Conceptual Add-On: Bi–Parametric View

We can interpret \(z\in\mathcal{F}_N\) as carrying **two coupled layers**:

1. **Arithmetic layer**: the real scalar \(a\) and primorial phases \(\{\psi_k\}\) encode multiplicative and valuation-like information.
2. **Geometric layer**: prime phases \(\{\phi_p\}\) plus braid \(\sigma\) encode a discrete geometry / topology over the prime index set.

The recursive operator \(\mathcal{R}_d\) then builds a **fractal tower** where each level re-quantizes the geometric layer back into the arithmetic layer and vice versa.

This bi–parametric structure is what makes the system suitable as a playground for:

- prime gap / resonance experiments,
- cryptographic constructions based on braids + prime structure,
- exotic feature spaces for ML that preserve multiplicative arithmetic.

---
## 9. How to Use This v2 Formalism

- Treat \(\mathcal{F}_N\) as your **working numeric type**.
- Use `encode_number` to map integers into this type.
- Use `multiply`, `+`, and optional `⊙` to build arithmetic.
- If you need self-similarity or infinite-precision–style behaviour, wrap objects in `recursive_encode` and define your operations recursively on that tree.

All of this is finite, computable, and tunable via `(N_p, N_r, N_b, L_max, depth)` so you can dial in the tradeoff between structure and cost.

