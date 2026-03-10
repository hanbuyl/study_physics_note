# **Antialtermagnetic Magnons and Nonrelativistic Thermal Edelstein Effect**

Robin R. Neumann<sup>®</sup>, <sup>1,2,\*</sup> Rodrigo Jaeschke-Ubiergo<sup>®</sup>, <sup>3</sup> Ricardo Zarzuela<sup>®</sup>, <sup>3</sup> Libor Šmejkal<sup>®</sup>, <sup>4,5</sup> Jairo Sinova<sup>®</sup>, <sup>3,6</sup> and Alexander Mook<sup>®</sup><sup>1</sup>

<sup>1</sup>Institute of Solid State Theory, University of Münster, D-48149 Münster, Germany <sup>2</sup>Institute of Physics and Halle-Berlin-Regensburg Cluster of Excellence CCE, Martin Luther University Halle-Wittenberg, D-06099 Halle (Saale), Germany <sup>3</sup>Institute of Physics, Johannes Gutenberg University Mainz, D-55128 Mainz, Germany <sup>4</sup>Max Planck Institute for the Physics of Complex Systems, 01187 Dresden, Germany <sup>5</sup>Max Planck Institute for Chemical Physics of Solids, 01187 Dresden, Germany <sup>6</sup>Department of Physics, Texas A&M University, College Station, TX, USA (Dated: March 6, 2026)

Odd-parity magnets are noncollinear compensated magnets with spin-split band structure in the absence of spin-orbit coupling and dipolar interactions. In contrast to altermagnets, their spin-polarized band structure breaks inversion symmetry, but preserves time-reversal symmetry rendering their spin texture odd in momentum space. Here, we study the spin dynamics of the magnetic texture and compute the band structure and spin polarization of magnons. We present minimal spin models of noncoplanar odd-parity magnets free of relativistic interactions that host p- and f-wave spin textures for the magnetic excitations. We demonstrate that two of these models exhibit collinear spin textures, i.e., the magnon spin polarization is restricted to a global (quantization) axis independent of the momentum giving rise to *antialtermagnetism*, previously associated primarily with coplanar ground states. Finally, the nonrelativistic magnonic thermal Edelstein effect—a nonequilibrium magnetization induced by a temperature gradient—is shown to exist for p-wave magnets in linear response and inherits its anisotropic angular dependence from the partial-wave character of the spin-polarized band structure. Our findings suggest that insulating antialtermagnets are promising candidates for magnon spintronics applications.

*Introduction.* The recent discovery of altermagnetism [1, 2], and its odd-parity counterpart, antialtermagnetism [3, 4], has fundamentally reshaped our understanding of compensated magnetic systems. These phases demonstrate that nontrivial spin-split electronic band structures can emerge without spinorbit coupling or net magnetization. In altermagnets, the spin expectation value of an electron with momentum k in band *n* is even under momentum inversion, satisfying  $s_{nk} = s_{n(-k)}$ , whereas odd-parity magnets host antisymmetric spin polarization,  $s_{nk} = -s_{n(-k)}$ . Such odd-parity spin textures emerge without spin-orbit coupling when four key ingredients coincide: (i) broken combined inversion-time-reversal ( $\mathcal{PT}$ ) symmetry, (ii) broken inversion ( $\mathcal{P}$ ) symmetry, (iii) a nonsymmorphic time-reversal symmetry  $(\mathcal{T}\tau)$  that pairs time reversal  $(\mathcal{T})$  with a fractional lattice translation ( $\tau$ ) [5], and (iv) noncollinear magnetic order. Collinear magnets feature either even-parity spin splitting or spin-degenerate band structures owing to their spinonly symmetries [1, 2]. Antialtermagnets [4] are odd-parity magnets that possess a collinear spin texture in momentum space. The momentum-dependent spin polarization and unconventional spin-charge interconversion of antialtermagnets have positioned them as promising candidates for next-generation spintronics [6–9]. Yet one essential aspect remains unexplored: the dynamics of these unconventional magnetic orders.

Magnetic dynamics in long-range ordered phases are goverened by magnons – the bosonic quasiparticles representing collective spin excitations. They offer distinct advantages over electronic carriers for spin information transport, including low dissipation, long coherence, and full compatibility with insulating platforms [10]. In conventional antiferromagnets, however, magnons of opposite spin polarization are degenerate and are easily mixed into spin-zero modes by weak spin-orbit

coupling, limiting their usefulness for spin manipulation. Altermagnets overcome this constraint by hosting exchange-driven even-parity spin-split magnons whose spin polarization can remain robust against weak spin-orbit coupling, enabling spin-selective and symmetry-controlled magnon transport [11–39]. The existence of altermagnetic magnons with even-parity splitting naturally raises the question of whether odd-parity magnetic order can imprint fundamentally new structures onto magnon excitations.

In this work, we close this gap by establishing the theoretical foundation of antialtermagnetic magnons. We show that the odd-parity character of the antialtermagnetic spin order is transferred to the magnon band structure, resulting in spin excitations with opposite spin polarization at +k and -k. This symmetry-protected locking of spin and propagation direction—normally associated with relativistic spin—orbit coupling in noncentrosymmetric systems [40, 41]—emerges here purely from exchange interactions. Using minimal models based solely on bilinear and biquadratic isotropic Heisenberg exchange, we uncover p- and f-wave magnon spin textures with clear experimental signatures. Most notably, we predict a nonrelativistic magnonic thermal Edelstein effect—a temperature-gradient-induced magnetization—that directly reflects the symmetry of the underlying magnon spin texture.

Magnons in unconventional magnets. Magnons in altermagnets [Fig. 1(a)] owe their even-parity spin polarization to the collinearity of the magnetic ground state. The quantized magnon spin and inversion symmetry of the band structure follow from the collinear spin-only group [42]  $\mathbf{r}_{so} = \mathrm{SO}(2) \times \mathbb{Z}_2^{[C_2T||T]}$ , where SO(2) contains all rotations of arbitrary angles about the collinear spin axis and  $\mathbb{Z}_2^{[C_2T||T]} = \{[E \parallel E], [C_2T \parallel T]\}$  contains the identity E and  $[C_2T \parallel T]$ 

![](_page_1_Figure_1.jpeg)

<span id="page-1-0"></span>Figure 1. Magnons in unconventional magnets. (a) Altermagnets possess collinear magnetic ground states giving rise to two linear Goldstone magnons with quantized spins and even-parity splitting. The spin is confined to a global quantization axis producing a collinear spin texture. (b), (c) Noncoplanar odd-parity magnets generally possess  $\mathcal{T}\tau$  symmetry and exhibit three linear Goldstone magnons with nonquantized spins. (b) Vector odd-parity magnets lack additional symmetries to constrain the magnon spin to a global axis. The magnon spin must be treated as a vector that lives in two- or three-dimensional space. (c) Antialtermagnets are odd-parity magnets with additional symmetries that constrain the magnon spin to a global axis. Although not quantized, the magnon spin forms a collinear spin texture and can be treated as a scalar. Originally proposed in coplanar systems [3], here we uncover antialtermagnets in noncoplanar systems, which exhibit a n-fold spin rotation  $C_n^s$  and a translation  $\tau'$  with  $n \geq 2$ .

that combines time reversal  $\mathcal{T}$  with a two-fold rotation  $C_2$  about an axis perpendicular to the collinear axis [1, 12]. In this framework of spin symmetries, the operations acting in spin space (left of "||") and those acting in real space (right of "||") are independent in the absence of spin-orbit coupling.

Magnons in odd-parity magnets [Fig. 1(b)] owe their antisymmetric spin polarization to a noncollinear spin arrangement in real space. Noncollinear systems with the symmetry  $\mathcal{T}\tau$  (short for  $[\mathcal{T} \parallel \mathcal{T} \mid \tau]$ , where the operation left of "]" is the point-group operation, while the operation right of "]" corresponds to a translation) are characterized by a spin translation group [43] [44]  $G_{st} = {}^{\bar{1}}1 = \{[E \parallel E], [\mathcal{T} \parallel \mathcal{T}]\}$ . This symmetry enforces an odd-parity-wave character in all spin components independently. In contrast to altermagnets, odd-parity magnets generally lack additional symmetries that restrict the dimension of the spin texture implying that the spin has to be treated as a vector rather than a scalar. We call those odd-parity magnets with a noncollinear spin texture in momentum space "vector odd-parity magnets".

Antialtermagnetism [3, 4], in addition to odd-parity spin polarization, requires a collinear spin polarization in momentum space. This was originally realized by considering a coplanar spin arrangement in real space, which leads to a spin-only group  $\mathbf{r}_{so} = \mathbb{Z}_2^{|C_2T||T|}$ . Here,  $C_2$  is a two-fold rotation along the axis perpendicular to the coplanar spins. This coplanar symmetry, together with  $\mathcal{T}$ , enforces a collinear spin texture in momentum space whose polarization is perpendicular to the coplanar spins.

In this Letter, we propose an alternative mechanism to realize antialtermagnets in *noncoplanar* magnets [Fig. 1(c)]. Here, the noncoplanar spins are engineered to have a high-order spintranslation group  $\mathbf{G}_{\mathrm{st}} = {}^n 1^{\bar{1}} 1$ , generated by the symmetries  $\mathcal{T} \boldsymbol{\tau}$  and  $C_n^s \boldsymbol{\tau}' = [C_n \parallel E \mid \boldsymbol{\tau}']$ . This arrangement generates collinear spin polarization of the magnon bands along the spin rotation axis of  $C_n$  ( $n \geq 2$ ), despite the noncoplanarity in real-space. In the following we introduce models for general odd-parity magnons hosted by noncoplanar magnetic ground states in three scenarios: (i) p-wave vector odd-parity magnet with noncollinear spin texture in momentum space; (ii) p-wave antialtermagnet with collinear spin texture in momentum space; (iii) f-wave antialtermagnet with collinear spin texture in momentum space.

Model of vector p-wave magnet. First, we consider the noncoplanar magnetic texture on the kagome lattice displayed in Fig. 2(a) [3]. The spins in each triangular plaquette are mutually orthogonal. This local magnetic structure is repeated along the  $\tau_2$  direction (ferroic ordering), while it is staggered along the  $\tau_1$  direction (antiferroic ordering), doubling the unit cell of the kagome lattice and installing time-reversal symmetry within the point group. Importantly, the order breaks inversion symmetry because a point inversion at the center of the hexagon flips the in-plane spin components, but leaves the out-of-plane component invariant. This operation can be remedied by a spin rotation about the z axis by 180°, which makes  $\mathcal{P}^*$  =  $[C_{2z} \parallel \mathcal{P}]$  a symmetry of the system.  $\mathcal{P}^*$  maps k to -k, but leaves  $s_z$  invariant such that  $s_z$  is even in momentum space and, due to the additional  $\mathcal{T}\tau_1$  symmetry,  $s_z$  vanishes (or must be degenerate). Thus, this magnetic texture is noncoplanar (i.e., three-dimensional) in real space but causes a coplanar (i.e., twodimensional) quasiparticle spin texture in momentum space. Overall, the spin point group is  ${}^{\bar{1}}1^{2_x}m^{2_y}m^1m$  [see Supplemental Material (SM) [45]].

To investigate magnons in this system, the described magnetic configuration needs to be realized as the classical ground state of a spin Hamiltonian, which we construct as

<span id="page-1-1"></span>
$$\mathcal{H} = \frac{F}{2S^2\hbar^4} \sum_{\langle ij\rangle_1} \left( \mathbf{S}_i \cdot \mathbf{S}_j \right)^2 + \frac{J_3}{2\hbar^2} \sum_{\langle ij\rangle_3} \mathbf{S}_i \cdot \mathbf{S}_j + \frac{J_6}{2\hbar^2} \sum_{\langle ij\rangle_6} \mathbf{S}_i \cdot \mathbf{S}_j,$$
(1)

where  $\hbar$  is the reduced Planck constant,  $S_i$  is the spin operator with spin quantum number S on site i, and the sums run over first  $(\langle ij\rangle_1)$ , third  $(\langle ij\rangle_3)$ , and sixth  $(\langle ij\rangle_6)$  nearest neighbors. The biquadratic interaction F>0 stabilizes the classical  $90^\circ$  order between nearest neighbors. The bilinear Heisenberg interactions  $J_3$  and  $J_6$  form a network of three disconnected triangular lattices, where they couple collinear spins in Fig. 2(a), which are parallel and antiparallel in a stripe order on each of the three triangular lattices. The ordering vector  $\mathbf{Q}$  of the sublattice stripes is identical for the three sublattices. Classically, the stripe order is stable in the regime where  $J_3>0$  and  $J_3/8< J_6< J_3$  [46–48], although quantum fluctuations generally shift the phase boundaries [48–50]. In the following, we work with the parameters  $J_3=2J_6=F$ , where the stripe

![](_page_2_Figure_1.jpeg)

<span id="page-2-0"></span>Figure 2. Vector p-wave kagome model. (a) Lattice structure, magnetic ground state configuration, and magnetic interactions F,  $J_3$ ,  $J_6$ . The gray transparent quadrangle indicates the magnetic unit cell and the red and blue triangles distinguish the opposite local spin configurations related by time reversal. (b) Magnon band structure along a high-symmetry path in the first Brillouin zone [high-symmetry points indicated in (c)]. (c), (d) Isoenergy lines for (c)  $\varepsilon = 5FS$  and (d)  $\varepsilon = 10FS$ . In panels (b)–(d), the color represents the spin angle within the xy plane [see inset of (d)], while the line thickness corresponds to the magnitude of the spin. Note that the  $k_x$  and  $k_y$  axes are rotated by 30° with respect to the x and y axes [see panel (a)]. The parameters are  $J_3 = 2J_6 = F$ .

order is stable against quantum fluctuations. For details of the magnon dispersion and spin polarization calculations within a large-*S* spin-wave theory, please refer to the End Matter and the SM [45].

The magnon band structure and magnon spin polarization are shown in Fig. 2(b) along a high-symmetry path in the first Brillouin zone [high-symmetry points indicated in Fig. 2(c)]. Since the magnetic unit cell contains six spins [indicated by the gray quadrangle in Fig. 2(a)], there are six magnon bands, three of which are linear Goldstone modes as expected for a magnetically compensated ground state that spontaneously breaks all three generators of the SO(3) symmetry of  $\mathcal{H}$  [51–53]. Moreover, we observe an *accidental* zero-energy mode at the S point not protected by the Goldstone theorem, which is known for stripe-ordered magnets on the triangular lattice and which is gapped out by quantum fluctuations [47, 54].

The in-plane orientation of the spin is encoded in the color of the bands, while the line thickness represents the magnitude of the spin polarization. Indeed, the magnon spin polarization is odd in momentum space, i.e.,  $s_{nk} = -s_{n(-k)}$  for each band n and wave vector k. This is reflected in the complementary colors at opposite momenta in Fig. 2(b). Two isoenergy cuts at  $\varepsilon = 5FS$  and  $\varepsilon = 10FS$  are shown in Fig. 2(c) and (d), respectively. Tracing a closed isoenergy line, the spin polarization winds exactly once in the xy plane, demonstrating the p-wave nature of the spin texture. Notably, the spin polarization is not restricted to a global axis, i.e., there is no collinear spin texture in this model. Since even for a closed isoenergy line the magnitude of the spin does not vanish, the nodal lines depend on the spin direction as well as the energy and are generally curved. This is because there is no symmetry fixing the nodal line.

Model of p-wave antialtermagnet. Next, we consider a distinct classical ground state. We abandon the ferroic ordering along the  $\tau_2$  direction and instead stagger (i) the in-plane spins

along  $\tau_1$  and (ii) all spin components along  $\tau_2$ , as visualized in Fig. 3(a). This magnetic configuration constitutes a classical ground state of the Hamiltonian  $\mathcal{H}$  in Eq. (1) and is degenerate with the previously discussed state, since the spins remain mutually orthogonal and the collinear sublattices continue to form a stripe pattern. The key difference is that the Q vectors associated with the three orthogonal stripe orders forming the kagome lattice are no longer identical. Because the relative orientations of these Q vectors do not influence the ground-state energy—spins belonging to different stripe patterns are coupled only via biquadratic interactions—we employ the same model parameters as before. The aforementioned staggering introduces  $[C_{2\tau} \parallel E \mid \tau_1]$  as a spin space group symmetry, enforcing the vanishing of the *in-plane* spin components of the magnons, while breaking the  $P^*$  symmetry that previously suppressed  $s_z$ . Thus, the spin point group  $\frac{2}{z}1^{\bar{1}}1^{2y}2/^{1}m$  (see SM [45]) enforces an exclusive out-of-plane spin polarized magnon band structure with odd parity, i.e.,  $s_{nk}^z = -s_{n(-k)}^z$ .

This is confirmed by the linear spin-wave calculation shown in Fig. 3(b). We identify 12 magnon bands and four zero-energy modes among them, of which three are enforced by the Goldstone theorem—the remaining fourth mode is expected to be accidental and to get gapped by fluctuations. The bands are colored according to their out-of-plane spin component, while the line thickness again represents the magnitude of the spin polarization. We find no nodal lines among the high-symmetry directions, where the spin polarization of all bands vanishes, but several bands are nearly unpolarized between  $\overline{M_2\Gamma M_2'}$  and all bands are unpolarized at  $\Gamma$ . Note that the Brillouin zone has hexagonal shape, but the 3-fold rotational symmetry is broken, giving rise to inequivalent high-symmetry paths connecting  $\Gamma$  and the K and M points indicated in Fig. 3(c) [55].

This symmetry breaking is further reflected in the isoenergy cut at  $\varepsilon = 5FS$  shown in Fig. 3(c). One verifies the *p*-wave character of the energy by the opposite spin polarization at

![](_page_3_Figure_1.jpeg)

<span id="page-3-0"></span>Figure 3. Antialtermagnetic p-wave kagome model. (a) Lattice structure and magnetic ground state configuration. The gray transparent quadrangle indicates the magnetic unit cell and the colored triangles distinguish the 4 different local spin configurations related by (the combination of) time reversal and 2-fold spin rotation. (b) Magnon band structure along a high-symmetry path in the first Brillouin zone [high-symmetry points indicated in (c)]. (c) Isoenergy lines for  $\varepsilon = 5FS$  in the first Brillouin zone (hexagon). In panels (b) and (c), the color represents the z component of the spin (see color bars), while the line thickness corresponds to its magnitude. The parameters are  $J_3 = 2J_6 = F$ .

opposite momenta for all bands. For the innermost closed isoenergy line, the spin changes sign twice—representing a single nodal line. For other bands, however, the spin polarization may change sign multiple times accidentally. These additional zeros are not protected by symmetry and may be removed by perturbations of the Hamiltonian. Only the spin degeneracy at the "nodal points"  $\Gamma$ ,  $M_1$ ,  $M_2$ , and  $M_3$  are protected by time-reversal symmetry. We emphasize that while this system is noncoplanar, it is an antialtermagnet due to the collinearity of the spin polarization in momentum space, that is a consequence of its rich spin translation group  $^{2_z}1^{\bar{1}}1$ .

Model of f-wave antialtermagnet. Although we have previously observed magnon bands with more than one nodal line, these zeros were accidental and, thus, not considered higherorder wave antialtermagnets. To realize a symmetry-protected f-wave magnon spin texture, we employ 3-fold rotation symmetry that triples the number of nodal lines/planes. For this purpose, we consider a three-dimensional lattice composed of stacked triangular layers as shown in Fig. 4(a). The magnetic unit cell contains three orthogonal spins per layer and two layers related by time reversal. Additionally, rotating the spins about the [111] axis by 120° interchanges the three spins within each layer, which can be compensated by a translation  $\tau_1$ . This  $[C_{3[111]} \parallel E \mid \tau_1]$  symmetry enforces a collinear reciprocal-space spin texture along the [111] spin-space direction. Furthermore, there are three nodal planes at 30°, 150°, and  $270^{\circ}$  with respect to the x axis that include the z axis and are related by 3-fold rotation symmetry. Overall, the spin point group is  ${}^{\bar{3}}1^m6/{}^1m^mm^1m$  (see SM [45]).

To stabilize the magnetic texture without frustration, we consider biquadratic nearest-neighbor coupling F > 0 and ferromagnetic next-nearest-neighbor coupling  $J_2 < 0$  within each layer, as well as antiferromagnetic interlayer coupling

 $J_{\perp} > 0$  between nearest neighbors:

$$\mathcal{H} = \frac{F}{2S^2\hbar^4} \sum_{\langle ij\rangle_1} \left( \mathbf{S}_i \cdot \mathbf{S}_j \right)^2 + \frac{J_2}{2\hbar^2} \sum_{\langle ij\rangle_2} \mathbf{S}_i \cdot \mathbf{S}_j + \frac{J_\perp}{2\hbar^2} \sum_{\langle ij\rangle_\perp} \mathbf{S}_i \cdot \mathbf{S}_j.$$
(2)

We choose the parameters as  $J_2 = -J_{\perp} = -F$ .

The angles of the nodal planes coincide with the  $\overline{\Gamma K}$  and  $\overline{\Gamma K'}$  directions, rendering the 6 magnon bands unpolarized along these lines [cf. Fig. 4(b)]. At the nodal surfaces, the lower two and the upper two bands become degenerate, while the middle two bands remain isolated, but their spin expectation values vanish.

Three bands intersect with the energy level  $\varepsilon = 2FS$  indicated by the dashed line in Fig. 4(b). Their isoenergy surfaces are shown in Fig. 4(c)–(h). Two of them are fully spin polarized and touch at the nodal planes, while one is isolated from the others and has a weak spin polarization because the isoenergy surface is closely surrounding the  $\Gamma$  point where its spin exactly vanishes. To summarize, this system corresponds to an f-wave antialtermagnet [3, 4], due to the *collinearity* of the spin polarization in momentum space, which emerges from the noncoplanar real-space spin configuration due to the higher-order spin translation group  $^{\bar{3}}1$  (see SM [45]), rather than from the coplanar spin-only group as in Ref. [4].

Nonrelativistic magnonic Edelstein effect. Since the magnon band structure is spin polarized, an asymmetric population of the magnon states can induce a finite net magnetization. As an example, the application of a temperature gradient can modify the magnon distribution and thereby lift the magnetic compensation generating a nonequilibrium magnetization according to  $\langle S_{\mu} \rangle = \sum_{\nu} \chi_{\mu\nu} (-\nabla_{\nu} T)$ , which is known as the thermal Edelstein effect.

We have computed the linear-response coefficients  $\chi_{\mu\nu}$  in Fig. 5 for the *p*-wave antialtermagnet model [recall Fig. 3]. Because the magnon spin is fully oriented along the *z* axis, there are only two nonzero components ( $\chi_{zx}$  and  $\chi_{zy}$ ), which are activated by temperature [56]. In the inset of Fig. 5, we present

![](_page_4_Figure_1.jpeg)

<span id="page-4-0"></span>Figure 4. Three-dimensional *f*-wave model consisting of stacked triangular lattices. (a) Real-space lattice, magnetic ground state configuration, and magnetic interactions *F*, *J*2, *J*⊥. Collinear magnetic sites are colored alike. The two layers in the magnetic unit cell are related by time reversal. (b) Band structure along a high-symmetry path in the first Brillouin zone (see inset). (c)–(h) Isoenergy surfaces for ε <sup>=</sup> <sup>2</sup>*FS* [dashed line in panel (b)]. Panels (c), (d) show band 1, (e), (f) show band 2, and (g), (h) show band 3 starting from the lowest energy in panel (b). The color in panels (b)–(h) represents the [111] component of the spin (see color bar). The parameters are *J*<sup>2</sup> = −*J*<sup>⊥</sup> = −*F*.

![](_page_4_Figure_3.jpeg)

<span id="page-4-1"></span>Figure 5. Temperature-dependent linear thermal Edelstein effect of the *<sup>p</sup>*-wave antialtermagnet with parameters *<sup>J</sup>*<sup>3</sup> <sup>=</sup> <sup>2</sup>*J*<sup>6</sup> <sup>=</sup> *<sup>F</sup>*. Here, <sup>τ</sup> is the relaxation time and *a* is the nearest-neighbor distance. Inset: Nonequilibrium *z* spin polarization as a function of the direction of −∇*T*. The angle of 0◦ corresponds to −∇*T* ∥ *x*ˆ. Different colors correspond to different temperatures (see legend). For better visibility, the data for *<sup>T</sup>* <sup>=</sup> <sup>0</sup>.01 (red curve) and 0.<sup>11</sup> *FS*/*k*<sup>B</sup> (purple curve) have been rescaled by a constant factor (see annotations). Solid and dashed lines indicate positive and negative sign, respectively.

the dependence of the nonequilibrium spin polarization on the direction of the applied temperature gradient. For a given temperature, we respectively find one lobe with positive (solid line) and one lobe with negative sign (dashed line) reminiscent of a *p* orbital. This shape implies a prominent anisotropy with large responses for temperature gradients applied in the direction of the lobes. Upon ramping up the temperature, the *p*-orbital-like pattern rotates by approximately 180◦ and expands in size. The elements with µ <sup>=</sup> *<sup>x</sup>*, *<sup>y</sup>* vanish because the magnon bands are unpolarized with respect to *s<sup>x</sup>* and *s<sup>y</sup>* rendering the corresponding Edelstein response zero. This situation is reversed in the *p*-wave vector odd-parity magnet without the collinear spin texture, where only the µ <sup>=</sup> *<sup>x</sup>*, *<sup>y</sup>*

components survive (see SM [\[45\]](#page-6-6)).

*Discussion and conclusion.* We have presented minimal models with ground states that support odd-parity magnetism relying only on bilinear Heisenberg and biquadratic interactions. The kagome models realize *p*-wave magnon spin polarization, while the stacked triangular lattice model hosts an *f*-wave spin texture. Notably, two of these *noncoplanar* models exhibit collinear spin textures [\[57–](#page-6-16)[61\]](#page-6-17), i.e., the magnon spin polarization is restricted to a global axis independent of the momentum. Hence, these noncoplanar odd-parity magnets realize antialtermagnets previously associated primarily with coplanar ground states [\[3\]](#page-5-3), demonstrating the possibility of engineering reciprocal-space spin textures by careful design of the magnetic ground state with symmetries that are not captured by the spin-only group. This allows control over the nonrelativistic thermal Edelstein effect, which directly reflects the symmetries of the spin texture. The magnonic Edelstein effect thus provides both a diagnostic tool for identifying *p*-wave antialtermagnetism in insulators and a potential mechanism for energy-efficient spin control in insulating systems. Our findings enlarge the set of potential material candidates for antialtermagnets two-fold by extending it not only to insulating magnets, but also to noncoplanar magnets.

Introducing magnons in antialtermagnets opens up several interesting questions for future research. The models presented herein have been idealized for simplicity, but may serve as toy models to predict unique signatures of antialtermagnetic dynamics in inelastic neutron spectroscopy/polarimetry [\[62–](#page-6-18) [65\]](#page-6-19), neutron spin echo spectroscopy [\[66](#page-6-20)[–68\]](#page-6-21), magneto-Raman spectroscopy [\[69](#page-6-22)[–71\]](#page-6-23), and in spin-polarized electron energy loss spectroscopy [\[72–](#page-6-24)[75\]](#page-7-0). As a next step, one may get closer to realistic materials by including spin-orbit coupling, which can be essential to realize the noncollinear magnetic ground states and to identify insulating candidates, e.g., by using abinitio methods.

By establishing that antialtermagnets can host spin-polarized magnons with protected odd-parity textures, this work opens a new pathway for magnon spintronics that combines the advantages of insulating materials with the symmetry-protected odd-parity spin-momentum locking previously exclusive to electronic systems. Our findings suggest that the dynamics of antialtermagnets represents a practical platform for low-dissipation spin information processing, with potential applications in thermal spin logic and quantum information technologies.

Acknowledgments. This work was funded by the German Research Foundation (DFG) as part of the German Excellence Strategy EXC3112/1-533767171 (Center for Chiral Electronics) and through TRR 277-328545488 (Project No. B04), TRR 173-268565370 (Projects No. A03 and B13), TRR 288-422213477 (Projects No. A09 and B05), and Project No. 504261060 (Emmy Noether Programme). We acknowledge support by the Dynamics and Topology Center (TopDyn) funded by the State of Rhineland-Palatinate.

Data availability. Upon reasonable request, the data associated with this article can be made available on Zenodo [76].

- <span id="page-5-0"></span>\* Correspondence email address: robin.neumann@unimuenster.de
- <span id="page-5-1"></span>[1] L. Šmejkal, J. Sinova, and T. Jungwirth, Beyond Conventional Ferromagnetism and Antiferromagnetism: A Phase with Nonrelativistic Spin and Crystal Rotation Symmetry, Physical Review X 12, 031042 (2022).
- <span id="page-5-2"></span>[2] L. Šmejkal, J. Sinova, and T. Jungwirth, Emerging Research Landscape of Altermagnetism, Physical Review X 12, 040501 (2022).
- <span id="page-5-3"></span>[3] A. B. Hellenes, T. Jungwirth, J. Sinova, and L. Šmejkal, Unconventional p-wave magnets (2024).
- <span id="page-5-4"></span>[4] T. Jungwirth, R. M. Fernandes, E. Fradkin, A. H. MacDonald, J. Sinova, and L. Šmejkal, Altermagnetism: An unconventional spin-ordered phase of matter, Newton 1, 100162 (2025).
- <span id="page-5-5"></span>[5] In principle, the requirement of nonsymmorphic time-reversal symmetry can be relaxed by suppressing even-parity spin components via spin-group symmetries, and odd-parity spin splitting can also arise in noncentrosymmetric materials [77–79]. Here, however, we focus exclusively on centrosymmetric odd-parity with nonsymmorphic time-reversal symmetry, since in this setting the odd-wave spin splitting is generated purely by magnetic order. As a result, even in the presence of spin-orbit coupling, the odd-parity character of the spin splitting is symmetry protected and remains intact as long as the magnetic order is preserved.
- <span id="page-5-6"></span>[6] B. Brekke, P. Sukhachov, H. G. Giil, A. Brataas, and J. Linder, Minimal Models and Transport Properties of Unconventional p-Wave Magnets, Physical Review Letters 133, 236703 (2024).
- [7] N. A. Á. Pari, R. Jaeschke-Ubiergo, A. Chakraborty, L. Šmejkal, and J. Sinova, Nonrelativistic linear Edelstein effect in helical EuIn<sub>2</sub>As<sub>2</sub>, Physical Review B 112, 024404 (2025).
- [8] A. Chakraborty, A. Birk Hellenes, R. Jaeschke-Ubiergo, T. Jungwirth, L. Šmejkal, and J. Sinova, Highly efficient non-relativistic Edelstein effect in nodal p-wave magnets, Nature Communications 16, 7270 (2025).
- <span id="page-5-7"></span>[9] Y. Yu, M. B. Lyngby, T. Shishidou, M. Roig, A. Kreisel, M. Weinert, B. M. Andersen, and D. F. Agterberg, Odd-Parity Magnetism Driven by Antiferromagnetic Exchange, Physical Review Letters 135, 046701 (2025).

- <span id="page-5-8"></span>[10] A. V. Chumak, V. I. Vasyuchka, A. A. Serga, and B. Hillebrands, Magnon spintronics, Nature Physics 11, 453–461 (2015).
- <span id="page-5-9"></span>[11] M. Naka, S. Hayami, H. Kusunose, Y. Yanagi, Y. Motome, and H. Seo, Spin current generation in organic antiferromagnets, Nature Communications 10, 10.1038/s41467-019-12229-y (2019).
- <span id="page-5-10"></span>[12] L. Šmejkal, A. Marmodoro, K.-H. Ahn, R. González-Hernández, I. Turek, S. Mankovsky, H. Ebert, S. W. D'Souza, O. Šipr, J. Sinova, and T. Jungwirth, Chiral Magnons in Altermagnetic RuO<sub>2</sub>, Physical Review Letters 131, 256703 (2023).
- [13] M. Gohlke, A. Corticelli, R. Moessner, P. A. McClarty, and A. Mook, Spurious symmetry enhancement in linear spin wave theory and interaction-induced topology in magnons, Phys. Rev. Lett. 131, 186702 (2023).
- [14] Q. Cui, B. Zeng, P. Cui, T. Yu, and H. Yang, Efficient spin Seebeck and spin Nernst effects of magnons in altermagnets, Physical Review B 108, L180401 (2023).
- [15] M. Weißenhofer and A. Marmodoro, Atomistic spin dynamics simulations of magnonic spin Seebeck and spin Nernst effects in altermagnets, Physical Review B 110, 094427 (2024).
- [16] Z. Liu, M. Ozeki, S. Asai, S. Itoh, and T. Masuda, Chiral Split Magnon in Altermagnetic MnTe, Physical Review Letters 133, 156702 (2024).
- [17] H. Yu, W. Feng, F. Zheng, and Y. Yao, Chiral magnons in an altermagnetic Janus  $Mn_2SeTe$  Monolayer, Computational Materials Today 4, 100021 (2024).
- [18] R. Hoyer, R. Jaeschke-Ubiergo, K.-H. Ahn, L. Šmejkal, and A. Mook, Spontaneous crystal thermal Hall effect in insulating altermagnets, Physical Review B 111, L020412 (2025).
- [19] D. Jost, R. B. Regmi, S. Sahel-Schackis, M. Scheufele, M. Neuhaus, R. Nickel, F. Yakhou, K. Kummer, N. Brookes, L. Shen, G. L. Dakovski, N. J. Ghimire, S. Geprägs, and M. F. Kling, Chiral Altermagnon in MnTe (2025).
- [20] K. Sourounis and A. Manchon, Efficient generation of spin currents in altermagnets via magnon drag, Physical Review B 111, 134448 (2025).
- [21] M. Daghofer, K. Wohlfeld, and J. v. d. Brink, Altermagnetic polarons (2025).
- [22] S. Lee and S. K. Kim, Effective Field Theory of a Noncollinear Altermagnet (2025).
- [23] S. Sarkar and A. Agarwal, Spin-split magnon bands induce pure spin current in insulating altermagnets (2025).
- [24] A. K. Siam and S. K. Kim, Chiral-split magnons in the S = 1 Shastry-Sutherland model (2025).
- [25] S. Khatua, V. P. Kravchuk, K. V. Yershov, and J. v. d. Brink, Magnon topology driven by altermagnetism (2025).
- [26] Z. Jin, Z. Zeng, J. Liu, T. Gong, Y. Su, K. Chang, and P. Yan, Interaction-Driven Altermagnetic Magnon Chiral Splitting (2025).
- [27] R. Yuan, W. J. Jankowski, K. Shen, and R.-J. Slager, Quantum Geometry of Altermagnetic Magnons Probed by Light (2025).
- [28] R. Hoyer, P. P. Stavropoulos, A. Razpopov, R. Valentí, L. Šmejkal, and A. Mook, Altermagnetic splitting of magnons in hematite α-Fe<sub>2</sub>O<sub>3</sub>, Physical Review B 112, 064425 (2025).
- [29] E. Syljuåsen, A. Qaiumzadeh, and A. Sudbø, Quantum geometry and magnon Hall transport in an altermagnet, Physical Review B 112, 064429 (2025).
- [30] N. Cichutek, P. Kopietz, and A. Rückriegel, Spontaneous magnon decay in two-dimensional altermagnets, Physical Review Research 7, 033208 (2025).
- [31] Z. Jin, T. Gong, J. Liu, H. Yang, Z. Zeng, Y. Cao, and P. Yan, Strong Coupling of Chiral Magnons in Altermagnets, Physical Review Letters 135, 126702 (2025).
- [32] R. Eto, M. Gohlke, J. Sinova, M. Mochizuki, A. L. Chernyshev, and A. Mook, Spontaneous magnon decays from nonrelativis-

- tic time-reversal symmetry breaking in altermagnets, [Physical](https://doi.org/10.1103/p4f5-w5m2) Review B 112[, 094442 \(2025\).](https://doi.org/10.1103/p4f5-w5m2)
- [33] W. Beida, E. S¸as¸ıoglu, C. Friedrich, G. Bihlmayer, ˘ Y. Mokrousov, and S. Blugel, Chiral split magnons in metal- ¨ lic g-wave altermagnets: insights from many-body perturbation theory, [npj Quantum Materials](https://doi.org/10.1038/s41535-025-00818-8) 10, 97 (2025).
- [34] V. P. Kravchuk, K. V. Yershov, J. I. Facio, Y. Guo, O. Janson, O. Gomonay, J. Sinova, and J. van den Brink, Chiral magnetic excitations and domain textures of *g*-wave altermagnets, [Physical](https://doi.org/10.1103/zn8d-ft9b) Review B 112[, 144421 \(2025\).](https://doi.org/10.1103/zn8d-ft9b)
- [35] N. Biniskos, M. dos Santos Dias, S. Agrestini, D. Svitak, K.-J. ´ Zhou, J. Posp´ısil, and P. ˇ Cerm ˇ ak, Systematic mapping of alter- ´ magnetic magnons by resonant inelastic X-ray circular dichroism, [Nature Communications](https://doi.org/10.1038/s41467-025-64322-0) 16, 9311 (2025).
- [36] N. Cichutek, P. Kopietz, and A. Ruckriegel, Quantum fluctua- ¨ tions in two-dimensional altermagnets, [Physical Review B](https://doi.org/10.1103/bdfg-djbs) 112, [174404 \(2025\).](https://doi.org/10.1103/bdfg-djbs)
- [37] R. Wiedmann, D.-B. Hering, V. Sulaiman, M. R. Walther, K. P. Schmidt, and G. S. Uhrig, Quantum eff[ects in the magnon spec](https://doi.org/10.48550/arXiv.2511.03528)[trum of 2D altermagnets via continuous similarity transforma](https://doi.org/10.48550/arXiv.2511.03528)[tions](https://doi.org/10.48550/arXiv.2511.03528) (2025).
- [38] C. Yan and J. Ni, [Competitive Orders in Altermagnetic Chiral](https://doi.org/10.48550/arXiv.2511.03922) [Magnons](https://doi.org/10.48550/arXiv.2511.03922) (2025).
- <span id="page-6-0"></span>[39] H. Bendin, A. Mook, I. Mertig, and R. R. Neumann, [D-](https://doi.org/10.48550/arXiv.2511.08357)[Wave Phonon Angular Momentum Texture in Altermagnets by](https://doi.org/10.48550/arXiv.2511.08357) [Magnon-Phonon-Hybridization](https://doi.org/10.48550/arXiv.2511.08357) (2025).
- <span id="page-6-1"></span>[40] R. Cheng, M. W. Daniels, J.-G. Zhu, and D. Xiao, Antiferromagnetic Spin Wave Field-Effect Transistor, [Scientific Reports](https://doi.org/10.1038/srep24223) 6[, 24223 \(2016\).](https://doi.org/10.1038/srep24223)
- <span id="page-6-2"></span>[41] G. Gitgeatpong, Y. Zhao, P. Piyawongwatthana, Y. Qiu, L. W. Harriger, N. P. Butch, T. J. Sato, and K. Matan, Nonreciprocal Magnons and Symmetry-Breaking in the Noncentrosymmetric Antiferromagnet, [Physical Review Letters](https://doi.org/10.1103/PhysRevLett.119.047201) 119, 047201 (2017).
- <span id="page-6-3"></span>[42] Spin-only groups encompass those symmetry elements that only transform the spin space, but leave the real space invariant.
- <span id="page-6-4"></span>[43] H. Watanabe, K. Shinohara, T. Nomoto, A. Togo, and R. Arita, Symmetry analysis with spin crystallographic groups: Disentangling effects free of spin-orbit coupling in emergent electromagnetism, [Physical Review B](https://doi.org/10.1103/PhysRevB.109.094438) 109, 094438 (2024).
- <span id="page-6-5"></span>[44] Strictly speaking, Gso is the point-group sector of the nontrivial spin translation group defined in Ref. [\[43\]](#page-6-4), which is obtained by projecting all translations into the identity.
- <span id="page-6-6"></span>[45] The Supplemental Material at [INSERT URL] contains the analytical expressions for the magnon Hamiltonians of the presented models, the details on the spin symmetry analysis, and the thermal Edelstein effect of the vector *p*-wave magnet.
- <span id="page-6-7"></span>[46] T. Jolicoeur, E. Dagotto, E. Gagliano, and S. Bacci, Groundstate properties of the S=1/2 Heisenberg antiferromagnet on a triangular lattice, [Physical Review B](https://doi.org/10.1103/PhysRevB.42.4800) 42, 4800 (1990).
- <span id="page-6-12"></span>[47] A. V. Chubukov and T. Jolicoeur, Order-from-disorder phenomena in Heisenberg antiferromagnets on a triangular lattice, [Phys](https://doi.org/10.1103/PhysRevB.46.11137)ical Review B 46[, 11137 \(1992\).](https://doi.org/10.1103/PhysRevB.46.11137)
- <span id="page-6-8"></span>[48] Z. Zhu, P. A. Maksimov, S. R. White, and A. L. Chernyshev, Disorder-Induced Mimicry of a Spin Liquid in YbMgGaO4, [Physical Review Letters](https://doi.org/10.1103/PhysRevLett.119.157201) 119, 157201 (2017).
- [49] Z. Zhu and S. R. White, Spin liquid phase of the *S* = 2 *J*<sup>1</sup> − *J*<sup>2</sup> Heisenberg model on the triangular lattice, [Physical Review B](https://doi.org/10.1103/PhysRevB.92.041105) 92[, 041105 \(2015\).](https://doi.org/10.1103/PhysRevB.92.041105)
- <span id="page-6-9"></span>[50] C. A. Gallegos, S. Jiang, S. R. White, and A. Chernyshev, Phase Diagram of the Easy-Axis Triangular-Lattice *J*<sup>1</sup> − *J*<sup>2</sup> Model, [Physical Review Letters](https://doi.org/10.1103/PhysRevLett.134.196702) 134, 196702 (2025).
- <span id="page-6-10"></span>[51] J. Goldstone, A. Salam, and S. Weinberg, Broken Symmetries, [Physical Review](https://doi.org/10.1103/PhysRev.127.965) 127, 965 (1962).

- [52] H. B. Nielsen and S. Chadha, On how to count Goldstone bosons, [Nuclear Physics B](https://doi.org/10.1016/0550-3213(76)90025-0) 105, 445 (1976).
- <span id="page-6-11"></span>[53] H. Watanabe and H. Murayama, Unified Description of Nambu-Goldstone Bosons without Lorentz Invariance, [Physical Review](https://doi.org/10.1103/PhysRevLett.108.251602) Letters 108[, 251602 \(2012\).](https://doi.org/10.1103/PhysRevLett.108.251602)
- <span id="page-6-13"></span>[54] J. Willsher, H.-K. Jin, and J. Knolle, Magnetic excitations, phase diagram, and order-by-disorder in the extended triangular-lattice Hubbard model, [Physical Review B](https://doi.org/10.1103/PhysRevB.107.064425) 107, 064425 (2023).
- <span id="page-6-14"></span>[55] In principle, it is sufficient to distinguish between K and K' as well as M and M' because of translational invariance. For example, K<sup>1</sup> and K<sup>3</sup> are related by a reciprocal lattice vector. However, the high-symmetry lines ΓK<sup>1</sup> and ΓK<sup>3</sup> are not equivalent, which is why we distinguish between equivalent points.
- <span id="page-6-15"></span>[56] Although the magnetic order is not stable at nonzero temperatures according to the Mermin-Wagner theorem [\[80\]](#page-7-4), a ferroic stacking with trivial interlayer coupling would stabilize the magnetic order without qualitatively changing the Edelstein response.
- <span id="page-6-16"></span>[57] B. A. Bernevig, J. Orenstein, and S.-C. Zhang, Exact SU(2) Symmetry and Persistent Spin Helix in a Spin-Orbit Coupled System, [Physical Review Letters](https://doi.org/10.1103/PhysRevLett.97.236601) 97, 236601 (2006).
- [58] J. Schliemann, Colloquium: Persistent spin textures in semiconductor nanostructures, [Reviews of Modern Physics](https://doi.org/10.1103/RevModPhys.89.011001) 89, 011001 [\(2017\).](https://doi.org/10.1103/RevModPhys.89.011001)
- [59] L. L. Tao and E. Y. Tsymbal, Persistent spin texture enforced by symmetry, [Nature Communications](https://doi.org/10.1038/s41467-018-05137-0) 9, 2763 (2018).
- [60] L. L. Tao and E. Y. Tsymbal, Perspectives of spin-textured ferroelectrics, [Journal of Physics D: Applied Physics](https://doi.org/10.1088/1361-6463/abcc25) 54, 113001 [\(2021\).](https://doi.org/10.1088/1361-6463/abcc25)
- <span id="page-6-17"></span>[61] K. Tenzin, B. Kilic, R. M. Sattigeri, Z. He, C. C. Ye, M. Costa, M. B. Nardelli, C. Autieri, and J. Sławinska, Persistent spin tex- ´ tures, altermagnetism and charge-to-spin conversion in metallic chiral crystals TM3X6, [npj Spintronics](https://doi.org/10.1038/s44306-025-00109-9) 3, 46 (2025).
- <span id="page-6-18"></span>[62] B. N. Brockhouse, Scattering of Neutrons by Spin Waves in Magnetite, [Physical Review](https://doi.org/10.1103/PhysRev.106.859) 106, 859 (1957).
- [63] A. W. Saenz, Spin Waves in Exchange-Coupled Complex Mag- ´ netic Structures and Neutron Scattering, [Physical Review](https://doi.org/10.1103/PhysRev.125.1940) 125, [1940 \(1962\).](https://doi.org/10.1103/PhysRev.125.1940)
- [64] P. A. McClarty, A. Gukasov, and J. G. Rau, Observing altermagnetism using polarized neutrons, [Physical Review B](https://doi.org/10.1103/PhysRevB.111.L060405) 111, [L060405 \(2025\).](https://doi.org/10.1103/PhysRevB.111.L060405)
- <span id="page-6-19"></span>[65] Q. Faure, D. Bounoua, V. Baledent, A. Gukasov, V. O. Garlea, ´ A. Ribeiro, J. G. Rau, S. Petit, and P. McClarty, [Altermagnetism](https://doi.org/10.48550/arXiv.2509.07087) [revealed by polarized neutrons in MnF](https://doi.org/10.48550/arXiv.2509.07087)<sup>2</sup> (2025).
- <span id="page-6-20"></span>[66] F. Mezei, Neutron spin echo: A new concept in polarized thermal neutron techniques, [Zeitschrift fur Physik A Hadrons and nuclei](https://doi.org/10.1007/BF01394523) ¨ 255[, 146 \(1972\).](https://doi.org/10.1007/BF01394523)
- [67] T. J. Hicks, T. Keller, and A. R. Wildes, Magnetic dipole splitting of magnon bands in a two dimensional antiferromagnet, [Journal](https://doi.org/10.1016/j.jmmm.2018.10.136) [of Magnetism and Magnetic Materials](https://doi.org/10.1016/j.jmmm.2018.10.136) 474, 512 (2019).
- <span id="page-6-21"></span>[68] T. Keller, H. Trepka, K. Habicht, and B. Keimer, Neutron Spin-Echo Instrumentation for Magnetic Scattering, [physica status](https://doi.org/10.1002/pssb.202100164) solidi (b) 259[, 2100164 \(2021\).](https://doi.org/10.1002/pssb.202100164)
- <span id="page-6-22"></span>[69] P. A. Fleury and R. Loudon, Scattering of Light by One- and Two-Magnon Excitations, [Physical Review](https://doi.org/10.1103/PhysRev.166.514) 166, 514 (1968).
- [70] M. G. Cottam, Theory of two-magnon Raman scattering in antiferromagnets at finite temperatures, [Journal of Physics C: Solid](https://doi.org/10.1088/0022-3719/5/12/022) State Physics 5[, 1461 \(1972\).](https://doi.org/10.1088/0022-3719/5/12/022)
- <span id="page-6-23"></span>[71] S. Sugai, S.-i. Shamoto, and M. Sato, Two-magnon Raman scattering in (La1−*x*Sr*x*)2CuO4, [Physical Review B](https://doi.org/10.1103/PhysRevB.38.6436) 38, 6436 (1988).
- <span id="page-6-24"></span>[72] M. Plihal, D. L. Mills, and J. Kirschner, Spin Wave Signature in the Spin Polarized Electron Energy Loss Spectrum of Ultrathin Fe Films: Theory and Experiment, [Physical Review Letters](https://doi.org/10.1103/PhysRevLett.82.2579) 82, [2579 \(1999\).](https://doi.org/10.1103/PhysRevLett.82.2579)

- [73] H. Ibach, D. Bruchmann, R. Vollmer, M. Etzkorn, P. S. Anil Kumar, and J. Kirschner, A novel spectrometer for spin-polarized electron energy-loss spectroscopy, Review of Scientific Instruments 74, 4089 (2003).
- [74] R. Vollmer, M. Etzkorn, P. S. A. Kumar, H. Ibach, and J. Kirschner, Spin-Polarized Electron Energy Loss Spectroscopy of High Energy, Large Wave Vector Spin Waves in Ultrathin fcc Co Films on Cu(001), Physical Review Letters 91, 147201 (2003).
- <span id="page-7-0"></span>[75] R. Vollmer, M. Etzkorn, P. S. Anil Kumar, H. Ibach, and J. Kirschner, Spin-polarized electron energy loss spectroscopy: a method to measure magnon energies, Journal of Magnetism and Magnetic Materials Proceedings of the International Conference on Magnetism (ICM 2003), 272-276, 2126 (2004).
- <span id="page-7-1"></span>[76] R. R. Neumann, R. Jaeschke-Ubiergo, R. Zarzuela, L. Šmejkal, J. Sinova, and A. Mook, Antialtermagnetic Magnons and Nonrelativistic Thermal Edelstein Effect, Zenodo (2025), [INSERT URL].
- <span id="page-7-2"></span>[77] S. Hayami, Y. Yanagi, and H. Kusunose, Spontaneous antisymmetric spin splitting in noncollinear antiferromagnets without spin-orbit coupling, Physical Review B 101, 220403 (2020).
- [78] M. Hu, O. Janson, C. Felser, P. McClarty, J. van den Brink, and M. G. Vergniory, Spin Hall and Edelstein effects in chiral non-collinear altermagnets, Nature Communications 16, 8529 (2025).
- <span id="page-7-3"></span>[79] X.-J. Luo, J.-X. Hu, and K. T. Law, Spin Symmetry Criteria for Odd-parity Magnets (2025).
- <span id="page-7-4"></span>[80] N. D. Mermin and H. Wagner, Absence of Ferromagnetism or Antiferromagnetism in One- or Two-Dimensional Isotropic Heisenberg Models, Physical Review Letters 17, 1133 (1966).
- <span id="page-7-5"></span>[81] T. Holstein and H. Primakoff, Field Dependence of the Intrinsic Domain Magnetization of a Ferromagnet, Physical Review 58, 1098 (1940).
- <span id="page-7-6"></span>[82] S. Toth and B. Lake, Linear spin wave theory for single-Q incommensurate magnetic structures, Journal of Physics: Condensed Matter 27, 166002 (2015).
- <span id="page-7-7"></span>[83] J. G. Rau, P. A. McClarty, and R. Moessner, Pseudo-Goldstone Gaps and Order-by-Quantum Disorder in Frustrated Magnets, Physical Review Letters 121, 237201 (2018).
- <span id="page-7-10"></span>[84] J. H. P. Colpa, Diagonalization of the quadratic boson hamiltonian, Physica A: Statistical Mechanics and its Applications 93, 327 (1978).
- <span id="page-7-11"></span>[85] R. Shindou, R. Matsumoto, S. Murakami, and J.-i. Ohe, Topological chiral magnonic edge mode in a magnonic crystal, Physical Review B 87, 174427 (2013).
- <span id="page-7-13"></span>[86] N. Okuma, Magnon Spin-Momentum Locking: Various Spin Vortices and Dirac magnons in Noncollinear Antiferromagnets, Physical Review Letters **119**, 107205 (2017).
- <span id="page-7-14"></span>[87] R. R. Neumann, A. Mook, J. Henk, and I. Mertig, Orbital Magnetic Moment of Magnons, Physical Review Letters 125, 117209 (2020).
- <span id="page-7-15"></span>[88] B. Li, A. Mook, A. Raeliarijaona, and A. A. Kovalev, Magnonic analog of the Edelstein effect in antiferromagnetic insulators, Physical Review B 101, 024427 (2020).

# END MATTER

## Holstein-Primakoff transformation

Here, we present the general concept of linear spin-wave theory and refer to the Supplemental Material [45] for the expressions for the specific models presented in the main text. The starting point is the classical ground state given by the orientations  $\hat{z}_i$  of the local spins at sites i. Using the Holstein-Primakoff transformation [81], the spin operators are expanded as [82, 83]

$$\frac{\mathbf{S}_{i}}{\hbar} = \left(S_{i} - a_{i}^{\dagger} a_{i}\right) \hat{\mathbf{z}}_{i} + \sqrt{S_{i}} \left[a_{i}^{\dagger} \left(1 - \frac{n_{i}}{2S_{i}}\right)^{1/2} \hat{\mathbf{e}}_{i}^{+} + \left(1 - \frac{n_{i}}{2S_{i}}\right)^{1/2} a_{i} \hat{\mathbf{e}}_{i}^{-}\right]$$
(3)

where  $S_i$  is the spin quantum number,  $\hbar$  the reduced Planck constant,  $a_i$  and  $a_i^{\dagger}$  bosonic annihilation and creation operators,  $n_i = a_i^{\dagger} a_i$  the number operator and  $\hat{e}_i^{\pm} = (\hat{x}_i \pm i\hat{y}_i)/\sqrt{2}$  auxiliary complex unit vectors where  $\hat{x}_i$ ,  $\hat{y}_i$ ,  $\hat{z}_i$  form a (right-handed) tripod.

Because of translation symmetry, we can label each site i by the unit cell u and the sublattice m and it is useful to describe the system in Fourier space:

<span id="page-7-12"></span>
$$a_{mk} = \frac{1}{\sqrt{N_{uc}}} \sum_{u} e^{-i\mathbf{k}\cdot(\mathbf{R}_{u} + \mathbf{r}_{m})} a_{mu}, \tag{4a}$$

$$a_{mk}^{\dagger} = \frac{1}{\sqrt{N_{\text{uc}}}} \sum_{u} e^{i\mathbf{k} \cdot (\mathbf{R}_{u} + \mathbf{r}_{m})} a_{mu}^{\dagger}. \tag{4b}$$

Here,  $\mathbf{R}_u$  is the position of the u-th unit cell and  $\mathbf{r}_m$  is the position of the m-th sublattice within a unit cell. In this representation, the bilinear Hamiltonian is diagonal in  $\mathbf{k}$  and can be written as

<span id="page-7-9"></span>
$$\mathcal{H}^{(2)} = \frac{1}{2} \sum_{k} \phi_{k}^{\dagger} H(k) \phi_{k}, \tag{5}$$

where

$$\boldsymbol{\phi}_{\boldsymbol{k}}^{\dagger} = \left( a_{1\boldsymbol{k}}^{\dagger} \dots a_{N\boldsymbol{k}}^{\dagger} \ a_{1(-\boldsymbol{k})} \dots a_{N(-\boldsymbol{k})} \right) \tag{6}$$

is the Nambu spinor with 2N entries (N is the number of sublattices) and

<span id="page-7-8"></span>
$$H(k) = \begin{pmatrix} A(k) & B(k) \\ B^*(-k) & A^*(-k) \end{pmatrix}$$
 (7)

is the Hamiltonian's kernel. Its structure is in principle arbitrary due to the redundancy of the Nambu space description, but one commonly chooses the one in Eq. (7) to install particle-hole symmetry. The Hermiticity of the Hamiltonian implies  $A(k) = A^{\dagger}(k)$  and  $B(k) = B^{\dagger}(-k)$ . The concrete expressions of A(k) and B(k) depend on the interactions embedded in  $\mathcal H$  and the magnetic ground state. Below, we provide general expressions for bilinear and biquadratic couplings.

In general, additive constants appear in Eq. (5), which correct the classical ground-state energy. Since we are interested in the magnon band structure, we omit those constants herein.

### **Bogoliubov transformation**

As a next step, the diagonalization of the kernel yields the one-particle energies:

$$T^{\dagger}(k)H(k)T(k) = E(k)$$

$$= \operatorname{diag}\left(\varepsilon_{1k} \ldots \varepsilon_{Nk} \varepsilon_{1(-k)} \ldots \varepsilon_{N(-k)}\right),$$
(8)

such that new normal-mode Nambu spinors can be defined:

$$\psi_{k}^{\dagger} = \phi_{k}^{\dagger} \left[ T^{\dagger}(k) \right]^{-1} = \left( b_{1k}^{\dagger} \dots b_{Nk}^{\dagger} b_{1(-k)} \dots b_{N(-k)} \right). \quad (9)$$

Since the diagonalization must leave the bosonic commutation rules intact, T(k) must be paraunitary, i.e., [84, 85]

$$T^{\dagger}(k)GT(k) = G. \tag{10}$$

where

$$G = \operatorname{diag}(1 \dots 1 -1 \dots -1). \tag{11}$$

#### **Bilinear interactions**

Considering generic bilinear spin-spin interactions described by

$$\mathcal{H} = \frac{1}{2\hbar^2} \sum_{mn} \sum_{uv} \mathbf{S}_{mu}^{\mathsf{T}} \boldsymbol{J}_{mn} (\boldsymbol{R}_m - \boldsymbol{R}_n) \mathbf{S}_{nv}, \tag{12}$$

where the sums run over all pairs of sublattices m and n and unit cells u and v, the bilinear magnon Hamiltonian amounts to [82, 83]

$$A_{mn}(\mathbf{k}) = \sqrt{S_m S_n} [\hat{\mathbf{e}}_m^+]^{\mathsf{T}} \mathcal{J}_{mn}(\mathbf{k}) \hat{\mathbf{e}}_n^- - \delta_{mn} \sum_{l=1}^N S_l \hat{\mathbf{z}}_m^{\mathsf{T}} \mathcal{J}_{ml}(\mathbf{0}) \hat{\mathbf{z}}_l,$$
(13a)

$$B_{mn}(\mathbf{k}) = \sqrt{S_m S_n} [\hat{\mathbf{e}}_m^+]^{\mathsf{T}} \mathcal{J}_{mn}(\mathbf{k}) \hat{\mathbf{e}}_n^+, \tag{13b}$$

where

$$\mathcal{J}_{mn}(\mathbf{k}) = e^{i\mathbf{k}\cdot(\mathbf{r}_m - \mathbf{r}_n)} \sum_{u} e^{i\mathbf{k}\cdot\mathbf{R}_u} \mathbf{J}_{mn}(\mathbf{R}_u)$$
 (14)

is the Fourier transform of  $J_{mn}(\mathbf{R})$ .

## **Biquadratic interactions**

Turning to biquadratic interactions, we focus on isotropic two-site terms:

$$\mathcal{H} = \frac{1}{2S^2\hbar^4} \sum \sum I_{mn} (\mathbf{R}_u - \mathbf{R}_v) (\mathbf{S}_{mu} \cdot \mathbf{S}_{nv})^2.$$
 (15)

We assume that all spins have the same spin quantum number S. After a lengthy derivation, we arrived at

$$A_{mn}(\mathbf{k}) = A_{mn}^{(1)}(\mathbf{k}) + A_{mn}^{(2)}(\mathbf{k}) + A_{mn}^{(3)}(\mathbf{k}), \tag{16a}$$

$$A_{mn}^{(1)}(\mathbf{k}) = -2S\,\tilde{I}_{mn}(\mathbf{k})(\hat{\mathbf{z}}_m \cdot \hat{\mathbf{z}}_n)^2,\tag{16b}$$

$$A_{mn}^{(2)}(\mathbf{k}) = 4S \,\tilde{I}_{mn}(\mathbf{k}) [(\hat{\mathbf{e}}_{m}^{+} \cdot \hat{\mathbf{e}}_{n}^{-})(\hat{z}_{m} \cdot \hat{z}_{n}) + (\hat{\mathbf{e}}_{m}^{+} \cdot \hat{z}_{n})(\hat{\mathbf{e}}_{n}^{-} \cdot \hat{z}_{m})],$$
(16c)

$$A_{mn}^{(3)}(\boldsymbol{k}) = 4S \,\delta_{mn} \sum_{l=1}^{N} \tilde{I}_{ml}(\boldsymbol{0}) (\hat{\boldsymbol{e}}_{m}^{+} \cdot \hat{\boldsymbol{z}}_{l}) (\hat{\boldsymbol{e}}_{m}^{-} \cdot \hat{\boldsymbol{z}}_{l}), \tag{16d}$$

$$B_{mn}(\mathbf{k}) = B_{mn}^{(1)}(\mathbf{k}) + B_{mn}^{(2)}(\mathbf{k}), \tag{16e}$$

$$B_{mn}^{(1)}(\mathbf{k}) = 4S\,\tilde{I}_{mn}(\mathbf{k})[(\hat{\mathbf{e}}_{m}^{+}\cdot\hat{\mathbf{e}}_{n}^{+})(\hat{z}_{m}\cdot\hat{z}_{n}) + (\hat{\mathbf{e}}_{m}^{+}\cdot\hat{z}_{n})(\hat{\mathbf{e}}_{n}^{+}\cdot\hat{z}_{m})],\tag{16f}$$

$$B_{mn}^{(2)}(\mathbf{k}) = 4S \,\delta_{mn} \sum_{l=1}^{N} \tilde{I}_{ml}(\mathbf{0}) (\hat{\mathbf{e}}_{m}^{+} \cdot \hat{\mathbf{z}}_{l})^{2}.$$
 (16g)

using the definition

$$I_{mn}(\mathbf{k}) = e^{i\mathbf{k}\cdot(\mathbf{r}_m - \mathbf{r}_n)} \sum_{u} e^{i\mathbf{k}\cdot\mathbf{R}_u} I_{mn}(\mathbf{R}_u). \tag{17}$$

### Magnon spin polarization

For the definition of the magnon spin we compare the expectation value of the total spin operator  $S_{\text{tot}} = \sum_i S_i$  in a one-magnon state  $|n\mathbf{k}\rangle = b_{n\mathbf{k}}^{\dagger}|0\rangle$  to the classical ground-state value:

$$\mathbf{s}_{n\mathbf{k}} = \langle n\mathbf{k} | \mathbf{S}_{\text{tot}} | n\mathbf{k} \rangle - \langle 0 | \mathbf{S}_{\text{tot}} | 0 \rangle. \tag{18}$$

Inserting the Holstein-Primakoff transformation [Eq. (3)] for  $S_{\text{tot}}$  and keeping only terms up to quadratic order in the bosonic operators yields [86, 87]

$$s_{nk} = -\hbar \sum_{m=1}^{N} \hat{z}_{m} \Big[ |T_{mn}(k)|^{2} + \big| T_{m,n+N}(-k) \big|^{2} \Big].$$
 (19)

### Linear thermal Edelstein effect

The linear response  $\langle S_{\mu} \rangle = \sum_{\nu} \chi_{\mu\nu} (-\nabla_{\nu} T)$  can be computed as [88]

$$\chi_{\mu\nu} = \frac{1}{VT} \sum_{k} \sum_{n=1}^{N} \tau_{nk} s_{nk}^{\mu} v_{nk}^{\nu} \varepsilon_{nk} \frac{\partial \rho(\varepsilon_{nk})}{\partial \varepsilon_{nk}}, \tag{20}$$

where V is the volume of the system, T is the temperature,  $\tau_{nk}$  is the relaxation time of the magnon in band n with wave vector k,  $s_{nk}^{\mu}$  is the spin expectation value,  $v_{nk}^{\nu}$  is the group velocity, and  $\rho(\varepsilon_{nk}) = \left[\exp\left(\frac{\varepsilon_{nk}}{k_BT}\right) - 1\right]^{-1}$  is the Bose function ( $k_B$  is the Boltzmann constant). We employ the constant relaxation time approximation ( $\tau_{nk} \equiv \tau$ ). Note that there is no intrinsic interband contribution to  $\chi_{\mu\nu}$  because it is odd under time-reversal symmetry and therefore vanishes in odd-parity magnets.