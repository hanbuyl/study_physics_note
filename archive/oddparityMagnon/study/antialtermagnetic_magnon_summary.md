# Antialtermagnetic Magnons and Nonrelativistic Thermal Edelstein Effect — Summary

## 1. Background: New Classification of Compensated Magnets

Compensated magnets (zero net magnetization) have been traditionally classified as antiferromagnets. The recent discoveries of **altermagnetism** and **antialtermagnetism** have fundamentally reshaped this classification.

The key criterion is the **parity of spin-split band structure**:

| Classification | Spin polarization | Symmetry | Magnetic order |
|----------------|------------------|----------|----------------|
| Altermagnet | $s_{nk} = s_{n(-k)}$ (even) | Inversion preserved | Collinear |
| Odd-parity magnet | $s_{nk} = -s_{n(-k)}$ (odd) | Inversion broken | Noncollinear |
| Antialtermagnet | Odd + collinear texture | Inversion broken + extra symmetry | Noncollinear/noncoplanar |

All these spin splittings arise **purely from exchange interactions**, without spin-orbit coupling.

## 2. Four Requirements for Odd-Parity Spin Texture

For odd-parity spin polarization to emerge without spin-orbit coupling, four conditions must be simultaneously satisfied:

1. **Broken $\mathcal{PT}$ symmetry** — no combined inversion-time-reversal symmetry
2. **Broken $\mathcal{P}$ (inversion) symmetry**
3. **Nonsymmorphic time-reversal symmetry $\mathcal{T}\tau$** — time reversal + fractional lattice translation
4. **Noncollinear magnetic order** — collinear arrangements yield only even-parity or spin-degenerate bands

## 3. Role of Magnons

Magnons are bosonic quasiparticles representing collective spin excitations in long-range ordered magnets.

**Limitations of conventional antiferromagnets:**
- Magnons of opposite spin polarization are degenerate
- Weak spin-orbit coupling mixes them into spin-zero modes
- Limited utility for spin manipulation

**Breakthrough in altermagnets:**
- Exchange-driven even-parity spin-split magnons
- Spin polarization robust against weak spin-orbit coupling
- Spin-selective magnon transport enabled

**Central question of this paper:** Can odd-parity magnetic order imprint fundamentally new structures onto magnon excitations?

## 4. Three Models and Results

### 4.1 Model I: Vector p-wave Magnet (Kagome Lattice)

**Magnetic structure:**
- Noncoplanar spin arrangement on a kagome lattice
- Spins within each triangular plaquette are mutually orthogonal (90° order)
- Ferroic ordering along $\tau_2$, antiferroic ordering along $\tau_1$ (doubling the unit cell)

**Hamiltonian:**
$$\mathcal{H} = \frac{F}{2S^2\hbar^4} \sum_{\langle ij\rangle_1} (\mathbf{S}_i \cdot \mathbf{S}_j)^2 + \frac{J_3}{2\hbar^2} \sum_{\langle ij\rangle_3} \mathbf{S}_i \cdot \mathbf{S}_j + \frac{J_6}{2\hbar^2} \sum_{\langle ij\rangle_6} \mathbf{S}_i \cdot \mathbf{S}_j$$

- $F > 0$: biquadratic interaction stabilizing 90° order
- $J_3, J_6$: bilinear Heisenberg interactions (3rd, 6th nearest neighbors)
- Parameters: $J_3 = 2J_6 = F$

**Results:**
- 6 magnon bands (6 spins per magnetic unit cell)
- 3 linear Goldstone modes + 1 accidental zero-energy mode
- **p-wave spin texture**: spin winds exactly once in the xy plane along isoenergy lines
- Spin texture is **noncollinear** (not restricted to a global axis) → "vector odd-parity magnet"
- Spin point group: ${}^{\bar{1}}1^{2_x}m^{2_y}m^{1}m$

### 4.2 Model II: p-wave Antialtermagnet (Kagome Lattice)

**Magnetic structure:**
- Same kagome lattice but with different staggering pattern
- In-plane spins staggered along $\tau_1$; all spin components staggered along $\tau_2$
- $[C_{2z} \| E | \tau_1]$ symmetry introduced → in-plane spin components vanish

**Key difference from Model I:**
- In-plane spin polarization = 0 (enforced by symmetry)
- **Only $s_z$ survives** → collinear spin texture in momentum space
- $s_{nk}^z = -s_{n(-k)}^z$ (odd parity preserved)

**Results:**
- 12 magnon bands (12 spins per magnetic unit cell)
- 4 zero-energy modes (3 Goldstone + 1 accidental)
- p-wave character: opposite spin polarization at opposite momenta
- **Antialtermagnet**: noncoplanar in real space, yet collinear in momentum space
- Spin point group: ${}^{2_z}1^{\bar{1}}1^{2_y}2/{}^{1}m$

### 4.3 Model III: f-wave Antialtermagnet (Stacked Triangular Lattice)

**Magnetic structure:**
- 3D stacked triangular lattice
- 3 orthogonal spins per layer, two layers related by time reversal
- $[C_{3[111]} \| E | \tau_1]$ symmetry → collinear spin texture along [111] direction
- 3-fold rotation symmetry → triple the number of nodal planes

**Hamiltonian:**
$$\mathcal{H} = \frac{F}{2S^2\hbar^4} \sum_{\langle ij\rangle_1} (\mathbf{S}_i \cdot \mathbf{S}_j)^2 + \frac{J_2}{2\hbar^2} \sum_{\langle ij\rangle_2} \mathbf{S}_i \cdot \mathbf{S}_j + \frac{J_\perp}{2\hbar^2} \sum_{\langle ij\rangle_\perp} \mathbf{S}_i \cdot \mathbf{S}_j$$

- Parameters: $J_2 = -J_\perp = -F$

**Results:**
- 6 magnon bands
- **f-wave spin texture**: 3 symmetry-protected nodal planes at 30°, 150°, 270°
- Lower/upper 2 bands become degenerate at nodal planes
- Spin point group: ${}^{\bar{3}}1^{m}6/{}^{1}m^{m}m^{1}m$

## 5. Nonrelativistic Magnonic Thermal Edelstein Effect

An asymmetric magnon population in spin-polarized bands induces a net magnetization.

**Mechanism:**
- A temperature gradient $-\nabla T$ modifies the magnon distribution
- Nonequilibrium magnetization generated: $\langle S_\mu \rangle = \sum_\nu \chi_{\mu\nu}(-\nabla_\nu T)$
- This is the **thermal Edelstein effect**

**Results for p-wave antialtermagnet:**
- Magnon spin fully along z → only $\chi_{zx}$ and $\chi_{zy}$ are nonzero
- Thermally activated
- Angular dependence of nonequilibrium spin polarization: **p-orbital shape**
- With increasing temperature, the p-orbital pattern rotates by ~180° and expands

**Key implications:**
- Edelstein effect realized purely from exchange interactions, without spin-orbit coupling
- The partial-wave character of the spin texture directly determines the angular dependence of the Edelstein response

## 6. Key Contributions

1. **Theoretical foundation of antialtermagnetic magnons**: first proof that odd-parity spin order transfers to the magnon band structure
2. **Noncoplanar antialtermagnet discovery**: extends antialtermagnetism beyond coplanar systems
3. **p-wave and f-wave magnon spin textures**: realized with isotropic Heisenberg exchange alone
4. **Nonrelativistic thermal Edelstein effect prediction**: temperature-gradient-induced magnetization directly reflects spin texture symmetry
5. **Doubled material candidates**: insulating + noncoplanar magnets added to the antialtermagnet pool

## 7. Future Directions

- Experimental verification via inelastic neutron spectroscopy/polarimetry
- Realistic modeling with spin-orbit coupling included
- Ab-initio search for insulating antialtermagnet candidates
- Applications in thermal spin logic and quantum information technologies
