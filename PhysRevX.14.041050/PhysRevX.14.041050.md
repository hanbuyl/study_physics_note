# Realization of High-Fidelity CZ Gate Based on a Double-Transmon Coupler

<span id="page-0-3"></span>Rui Li<sup>®</sup>, <sup>1,\*</sup> Kentaro Kubo<sup>®</sup>, <sup>2</sup> Yinghao Ho, <sup>2</sup> Zhiguang Yan<sup>®</sup>, <sup>1</sup> Yasunobu Nakamura<sup>®</sup>, <sup>1,3,†</sup> and Hayato Goto<sup>®</sup>, <sup>2,1,‡</sup> <sup>1</sup>RIKEN Center for Quantum Computing (RQC), Wako, Saitama 351-0198, Japan <sup>2</sup>Frontier Research Laboratory, Corporate Research & Development Center, Toshiba Corporation, Saiwai-ku, Kawasaki 212-8582, Japan <sup>3</sup>Department of Applied Physics, Graduate School of Engineering, The University of Tokyo, Bunkyo-ku, Tokyo 113-8656, Japan

(Received 29 February 2024; revised 2 June 2024; accepted 26 September 2024; published 21 November 2024; corrected 4 December 2024)

Striving for higher gate fidelity is crucial not only for enhancing existing noisy intermediate-scale quantum devices, but also for unleashing the potential of fault-tolerant quantum computation through quantum error correction. A recently proposed theoretical scheme, the double-transmon coupler (DTC), aims to achieve both suppressed residual interaction and a fast high-fidelity two-qubit gate simultaneously, particularly for highly detuned qubits. Harnessing the state-of-the-art fabrication techniques and a model-free pulse-optimization process based on reinforcement learning, we translate the theoretical DTC scheme into reality, attaining fidelities of 99.90% for a controlled-Z gate and 99.98% for single-qubit gates. The performance of the DTC scheme demonstrates its potential as a competitive building block for superconducting quantum processors.

DOI: 10.1103/PhysRevX.14.041050 Subject Areas: Quantum Physics,
Ouantum Information

#### I. INTRODUCTION

Navigating the era of noisy intermediate-scale quantum (NISQ) devices [1] and pioneering the era of fault-tolerant quantum computing [2], the blooming of qubit technologies, including superconducting qubits [3–5], trapped ions [6,7], neutral atoms [8,9], photonics [10], and other solid-state qubits [11–13], has made substantial strides toward the exciting goal of realizing quantum advantage. Despite differing entities for qubit realization, achieving high-fidelity two-qubit gates stands as a pivotal and shared challenge. While considerable efforts have been invested in enhancing gate performance [14–19], superconducting qubits [20–24], in particular, exhibit promising potential due to their scalability [4,25] and modularity [26,27].

Within the realm of superconducting qubits, the transmon [28] has become a favorite in both academia and industry. This preference is rooted in its high coherence, achieved through cutting-edge design [28–30] and fabrication [31,32], coupled with its inherent simplicity that

<span id="page-0-0"></span>\*Contact author: rui.li.gj@riken.jp

<span id="page-0-2"></span><span id="page-0-1"></span>†Contact author: yasunobu@ap.t.u-tokyo.ac.jp †Contact author: hayato1.goto@toshiba.co.jp

Published by the American Physical Society under the terms of the Creative Commons Attribution 4.0 International license. Further distribution of this work must maintain attribution to the author(s) and the published article's title, journal citation, and DOI. facilitates easy controllability [33]. Diverse schemes based on transmons for implementing two-qubit gates have been proposed, encompassing fixed-frequency qubits [34] and tunable alternatives [35], each presenting a unique array of advantages and challenges. Fixed coupling with fixedfrequency qubits, whether through direct [36] or indirect [37] capacitive coupling, provides the feasibility of a straightforward microwave-driven two-qubit gate [38]. The delicate balance between high control speed and suppression of the so-called residual ZZ interaction is carefully considered to mitigate potential gate errors [39,40]. Remarkably, tunablecoupling schemes involving a single frequency-tunable transmon coupler (STC) [41] have garnered attention for their ability to achieve a high on-off ratio [42] of the ZZ interactions between qubits, a critical metric for estimating the potential to simultaneously achieve high fidelity in both single- and two-qubit gates. Notably, however, the absence of the residual ZZ interaction is confined to the so-called straddling regime [43,44], where a detuning between qubit frequencies is smaller than their anharmonicities, potentially leading to issues with extra frequency collisions in larger systems [45–47].

Quantum Information, Superconductivity

A novel coupling scheme, employing a coupler consisting of double transmons with a shared superconducting loop and an additional Josephson junction, has been proposed theoretically to overcome the drawback above and retain the benefits of its tunability [48–50]. The implementation of this double-transmon-coupler (DTC) scheme involves four transmons: Two transmons function as data qubits, while the

other two transmons serve as the coupler elements. The ZZ interaction between the two data qubits can be controlled by the magnetic flux through the DTC's loop and suppressed completely even for two qubits placed outside the straddling regime without sacrificing the speed of the controlled-Z (CZ) gate [48]. Moreover, the absence of the necessity for direct capacitive coupling between the two qubits positions them into a regime marked by minimal spectator error and enables flexible qubit-qubit distances, ultimately reducing both quantum and classical crosstalk [51–53].

Despite the advantages offered by the DTC scheme, achieving a high-fidelity CZ gate experimentally remains challenging, even though it has been theoretically proposed [48]. A numerically optimized pulse shape necessitates calculations based on the total energy levels of the four transmons (two data gubits and two coupler transmons). However, in practice, characterizing the full energy spectra as a function of the flux bias is a nontrivial task. This difficulty arises because strongly hybridized states between the qubits and coupler transmons at certain flux bias points hinder efficient readout. Regardless of the theoretically calculated pulse shape, opting for a commonly used Slepian pulse shape [22,54,55] can be an alternative choice. This method does not require detailed energy-level information, although it may not necessarily be the optimal choice. However, another challenge arises from the constrained bandwidth and unwanted dispersion of the circuits for pulse transmission [56]. This distorts the ideal pulse shape applied to the DTC loop, thereby impeding the realization of the ideal adiabatic process. Although a pulsetransient calibration method has been proposed to mitigate pulse distortion [22,56], reading out the states of coupler transmons requires additional resonators, further burdening an already complicated and crowded on-chip circuit.

In this work, we overcome these problems and experimentally demonstrate a high-fidelity CZ gate on a twoqubit device with a DTC. We design the chip considering both high coherence and fabrication feasibility. We achieve a high on-off ratio  $> 10^4$  for the ZZ interaction between the two qubits, a crucial factor for attaining high gate fidelities for both single- and two-qubit gates. At the idle bias point, a minimum residual ZZ interaction  $[2\pi \times (-6.3) \text{ kHz}]$  persists without compromising the single-qubit gate fidelities, which are measured to be over 99.98% through simultaneous randomized benchmarking [57]. We calibrate the distortion of the Z pulse applied on the DTC by utilizing the readout resonator of a qubit. Subsequently, through further optimization driven by a model-free reinforcement learning (RL) algorithm, we achieve a fast and optimized pulse for a high-fidelity CZ gate. The CZ-gate fidelity,  $99.90 \pm 0.01\%$ , demonstrated through Clifford interleaved randomized benchmarking [58–60], remains stable within a 12-hour time frame. For the error budget of the CZ gate, we highlight leakage and incoherent errors as the primary contributors.

#### II. DEVICE SETUP

The demonstration device for the DTC scheme comprises four transmons: two data transmons (Q1 and Q2) as qubits and two coupler transmons (C3 and C4). The frequency detuning between Q1 (4.314 GHz) and Q2 (4.778 GHz) is 464 MHz, which exceeds the respective anharmonicities of -212 and -199 MHz for Q1 and Q2 (see Appendix C). This configuration places the system outside the straddling regime. Each of these transmons consists of a single Josephson junction and a large shunt capacitance. They are positioned adjacent to each other at the center of the chip [Figs. 1(a) and 1(b)]. Q1 (Q2) is directly coupled to C3 (C4) capacitively. While it is inevitable to have other marginal capacitive couplings between the transmons, such as the one between Q1 and Q2, they are not essential and do not significantly hinder the achievement of the designed ZZ interaction for the CZ gate. Furthermore, a superconducting loop is formed by the Josephson junctions JJ3 and JJ4 of C3 and C4, respectively, connected by an additional Josephson junction JJ5. The DTC, represented by C3 and C4, is employed to mediate the coupling between Q1 and Q2 tuned by the magnetic flux  $\Phi_{ex}$  through the superconducting loop.

Each qubit has its own resonator for readout, while the two coupler transmons share a third resonator. All three resonators are  $\lambda/4$  coplanar waveguides, either capacitively or inductively coupled to a shared Purcell filter [61]. We distinguish the ground ( $|0\rangle$ ), first excited ( $|1\rangle$ ), and second excited states ( $|2\rangle$ ) for each of the two qubits with the single-shot dispersive readout through their respective readout resonators. For coupler transmons, we can discriminate only the ground state  $|00\rangle$  from other excited states by the readout through the shared resonator (see Appendix F for details). It is important to note that the resonator for the state readout of the coupler transmons is not necessary for calibrating the high-fidelity CZ gate. However, it proves useful and sufficient for characterizing the leakage error in this work.

Each of Q1 and Q2 has its dedicated microwave control line for driving the single-qubit *X* and *Y* rotations. A fast flux line shorted to the ground is inductively coupled to the superconducting loop of the DTC for delivering the fast CZ-gate pulse. Additionally, in the spectroscopic measurement for characterization, we utilize this flux line as the microwave control line for C3 and C4 through the weak capacitive coupling. Furthermore, a dc flux penetrating through the superconducting loop is generated with a superconducting coil mounted outside the sample package (see Appendix B for details). This coil is primarily used to maintain the flux bias at the idle bias point, where the smallest *ZZ* interaction between Q1 and Q2 is achieved

<span id="page-1-0"></span>Ignoring the contribution of the resonators and control lines, the system Hamiltonian can be approximated as [48]

![](_page_2_Figure_2.jpeg)

FIG. 1. (a) Schematic circuit diagram of the DTC scheme consisting of two data qubit transmons, Q1 and Q2, and two coupler transmons, C3 and C4, as well as their readout and control elements. (b) False-color picture of the real device. The colors correspond to the circuit elements in (a). The black holes are superconducting through-silicon vias (TSVs) distributed throughout the entire chip. The three panels at the bottom are magnified pictures of the areas (dotted rectangles) containing Josephson junctions. (c) Conceptual sketch of a toy model of the DTC scheme. Each of Q1 and Q2 couples to the plus (p) and minus (m) modes, represented by P and M, respectively. (+) and (-) indicate the signs of the effective couplings. (d) Energy spectra of the lowest four excited states as a function of the reduced flux bias  $\varphi_{ex}$ . The dots and solid lines are experimental and simulation results, respectively. The gray dash-dotted lines serve as guides for the four decoupled modes. The labels |Q1, Q2, P, M\rangle with (without) a tilde are the indication of eigenstates with (without) couplings among the four modes. The vertical dotted line indicates the idle bias point providing the minimum ZZ interaction between Q1 and Q2.

$$\hat{H} = \frac{4e^2}{2}\hat{\mathbf{n}}^{\mathrm{T}}\mathbf{C}^{-1}\hat{\mathbf{n}} - \sum_{i=1}^{4} E_{\mathrm{J}i}\cos\hat{\varphi}_i$$
$$-E_{\mathrm{J}5}\cos(\hat{\varphi}_4 - \hat{\varphi}_3 - \varphi_{\mathrm{ex}}), \tag{1}$$

where e represents the elementary charge,  $\hat{\mathbf{n}}$  is a vector  $\{\hat{n}_i\}$ , and  $\hat{n}_i$  and  $\hat{\varphi}_i$  represent the Cooper-pair number operator and phase-difference operator, respectively, with  $i \in \{1,2,3,4\}$  corresponding to the nodes of  $\{\mathrm{Q1},\mathrm{Q2},\mathrm{C3},\mathrm{C4}\}$ . The capacitance matrix  $\mathbf{C}$  is defined as  $\mathbf{C}_{ii} = \sum_{j=1}^4 C_{ij}$  and  $\mathbf{C}_{ij} = -C_{ij}$   $(i \neq j)$ . The reduced flux  $\varphi_{\mathrm{ex}} = 2\pi\Phi_{\mathrm{ex}}/\Phi_0$  denotes the extra phase introduced by the external flux  $\Phi_{\mathrm{ex}}$  divided by the flux quantum  $\Phi_0 \equiv h/(2e)$ .  $E_{\mathrm{J}i} = \Phi_0 I_{\mathrm{c}i}/(2\pi)$  represents the Josephson energy of Josephson junction i (JJi) with the critical current  $I_{\mathrm{c}i}$ , where  $i \in \{1,2,3,4,5\}$  corresponds to the five junctions shown in the circuit diagram.

To facilitate an intuitive understanding of the coupling mediated by the DTC, we employ a toy model in which two qubits are coupled via a fixed-frequency transmon (P) and a capacitively shunted flux qubit (CSFQ) (M) [Fig. 1(c); see Appendix D for the derivation]. The Hamiltonian can be quantized as

<span id="page-2-0"></span>
$$\begin{split} \hat{H} &= \omega_{1} \hat{a}_{1}^{\dagger} \hat{a}_{1} + \eta_{1} \hat{a}_{1}^{\dagger} \hat{a}_{1}^{\dagger} \hat{a}_{1} \hat{a}_{1} + \omega_{2} \hat{a}_{2}^{\dagger} \hat{a}_{2} \\ &+ \eta_{2} \hat{a}_{2}^{\dagger} \hat{a}_{2}^{\dagger} \hat{a}_{2} \hat{a}_{2} + \hat{H}_{p} + \hat{H}_{m} (\varphi_{ex}) \\ &+ g_{1p} \Big( \hat{a}_{1}^{\dagger} \hat{a}_{p} + \hat{a}_{1} \hat{a}_{p}^{\dagger} \Big) + g_{2p} \Big( \hat{a}_{2}^{\dagger} \hat{a}_{p} + \hat{a}_{2} \hat{a}_{p}^{\dagger} \Big) \\ &+ g_{1m} \Big( \hat{a}_{1}^{\dagger} \hat{a}_{m} + \hat{a}_{1} \hat{a}_{m}^{\dagger} \Big) - g_{2m} \Big( \hat{a}_{2}^{\dagger} \hat{a}_{m} + \hat{a}_{2} \hat{a}_{m}^{\dagger} \Big), \end{split}$$
(2)

where  $\omega_{1(2)}$  and  $\eta_{1(2)}$  denote the frequency and anharmonicity of Q1 (Q2), respectively.  $\hat{H}_{\rm p}$  represents the Hamiltonian of the fixed-frequency transmon P, while  $\hat{H}_{\rm m}$  represents the Hamiltonian of the flux-tunable CSFQ M. The coefficient  $g_{i{\rm p}(i{\rm m})}$  is the capacitive coupling between the qubit Qi and the p(m) mode, while  $\hat{a}$  and  $\hat{a}^{\dagger}$  are the lowering and raising operators. The opposite sign of the coupling between the two qubits and the m mode suggests an effective negative capacitance between Q2 and the m mode.

The energy spectra of the qubits and the DTC are illustrated in Fig. 1(d). We denote the diabatic states in the form of  $|Q1,Q2,P,M\rangle$  for the two qubits and the p and m modes, which are obtained by dropping all the coupling terms between the four modes in the toy-model Hamiltonian [Eq. (D15)]. The adiabatic states with a tilde,  $|Q1,Q2,P,M\rangle$ , are used to indicate hybridized states considering all the couplings and are the eigenstates of the Hamiltonian [Eq. (1)]. While the adiabatic states provide a precise description of the DTC scheme, the diabatic states provide an intuitive understanding. The simulation results based on the diagonalization of the Hamiltonian [Eq. (1)] are generated by fine-tuning the designed device parameters to

match the experimental data (see Appendix C for details). The good agreement between the theoretical model of the DTC and the experimental results confirms its validity. A marginal deviation in the simulation may be attributed to the unconsidered coupling between the transmons and their readout resonators as well as the control lines.

#### III. ZZ INTERACTION

<span id="page-3-0"></span>The DTC facilitates a high on-off ratio of the longitudinal ZZ interaction between the two qubits. By denoting the state energy as E, the ZZ interaction is formally defined as

$$\zeta = E_{\widetilde{|1100\rangle}} - E_{\widetilde{|1000\rangle}} - E_{\widetilde{|0100\rangle}} + E_{\widetilde{|0000\rangle}}. \eqno(3)$$

The origin of the ZZ interaction can be understood through the toy model by accessing the effective coupling between the qubits mediated by the p and m modes. Within the dispersive regime of the system, where  $|\Delta_{ip}| = |\omega_i - \omega_{\rm p}| \gg g_{i\rm p}$  and  $|\Delta_{i\rm m}| = |\omega_i - \omega_{\rm m}| \gg g_{i\rm m}$ , the effective coupling between two qubits is given by

<span id="page-3-1"></span>
$$g_{\text{eff}} = \frac{g_{1p}g_{2p}}{2} \left( \frac{1}{\Delta_{1p}} + \frac{1}{\Delta_{2p}} \right) - \frac{g_{1m}g_{2m}}{2} \left( \frac{1}{\Delta_{1m}} + \frac{1}{\Delta_{2m}} \right). \tag{4}$$

The contribution of the p mode can be viewed as a fixed coupling, whereas the tunability of the m-mode frequency results in a variable one.

The coupling strengths  $g_{ip}$  and  $g_{im}$  are approximately equal to each other, as the p and m modes share the same coupling capacitances to the qubits. The effective coupling  $g_{eff}$  can be tuned from negative to positive by adjusting the m-mode frequency across the p-mode frequency with the external flux  $\phi_{ex}$ . Therefore,  $g_{eff}$  can be tuned to either zero or a specific value, facilitating both negligible ZZ interaction for the decoupling and a significantly large one for implementing a CZ gate. While the dispersive approximation works well for the p mode, the strong coupling between the qubits and m mode at certain bias flux requires the analysis of interaction between three multilevel modes [22,62].

#### A. Minimum ZZ interaction

We designate the flux bias point that results in the minimum ZZ interaction as the idle bias point of the system. This idle bias point serves as the working point for single-qubit gate calibration and the start point for CZ-gate implementation. The flux bias corresponding to the idle bias point is maintained by the current supplied to the superconducting coil.

The ZZ interaction is measured using the pulse sequence of the joint amplification of ZZ interaction (JAZZ) method [63,64]. In the JAZZ sequence [Fig. 2(a)], the ZZ interaction introduces a relative phase  $\phi$  accumulated on the superposition state of Q1,  $|0\rangle + e^{i\phi}|1\rangle$ , which can

![](_page_3_Figure_13.jpeg)

FIG. 2. (a) JAZZ pulse sequence employed for measuring the ZZ interaction of the two qubits (Q1 and Q2) with applying the Z pulse to the coupler loop (CL) of the DTC. The final  $\pi/2$  pulse,  $\Phi_{\pi/2}(t)$ , of Q1 intentionally acquires a phase  $\phi$  that is linearly dependent on the interval t, providing a baseline frequency to improve the fitting. The sequence considered the margins between the pulses to avoid overlaps, which are not displayed for simplicity. (b) Z-pulse shape comprising a flattop pulse with a duration of t/2 as well as smooth Gaussian rise and fall edges with fixed duration. The flux introduced into the coupler loop of the DTC is proportional to the amplitude of the Z pulse. (c) Ground-state population of Q1,  $P_{|0\rangle}$ , measured at the idle bias point by the JAZZ sequence. The blue experimental data points are fitted with the gray solid line, and its ZZ interaction  $[2\pi \times (-6.3) \text{ kHz}]$  is extracted and illustrated in (d) with a yellow circle. (d) ZZ interaction  $\zeta$  as a function of the reduced flux  $\varphi_{\rm ex}$ . The blue data points are experimentally obtained. Simulation results (red line) are obtained by calculating the energy-level difference using original Hamiltonian [Eq. (1)]. The inset provides an enlarged view of the ZZ interaction near the idle bias point.

be read out from its population measurement,  $P_{|0\rangle} =$  $(1 - \cos \phi)/2$ . Therefore, the population is oscillating with the duration t, where t/2 is defined as the pulse duration of the applied Z pulse. Note that we sweep only the duration of the flattop of the Z pulse while keeping the duration of the Gaussian rise and fall edges fixed [Fig. 2(b)]. Therefore, the accumulated phase can be simply expressed as  $\phi = \zeta t/2 + \phi_0$ , where the first term arises from the ZZ interaction during the flattop pulse and the second term as a fixed phase resulting from the rise and fall edges. Because of the small magnitude of the ZZ interaction near the idle bias point, the oscillation of Q1 population measured with the JAZZ sequence becomes relatively slow. To precisely measure the oscillation frequency within a time limited by the qubit coherence time, we intentionally vary the phase of the final  $\pi/2$  gate,  $\Phi_{\pi/2}(t)$ , applied to Q1 linearly with the duration t. This introduces an additional relative phase  $\omega_{\rm b}t$ to the Q1's superposition state, thereby increasing the oscillation frequency with the baseline frequency  $\omega_{\rm b}$  and leading to improved fitting results. With the frequency  $\omega_{\mathrm{m}}$ 

extracted from the oscillating signal [Fig. 2(c)], the ZZ interaction is calculated as  $\zeta = 2(\omega_m - \omega_b)$ . The condition  $\omega_b > |\zeta/2|$  has been chosen to ensure a positive  $\omega_m$ , thereby avoiding confusion in the sign of  $\omega_m$  extracted from the oscillating signal with a cosine function.

By varying the amplitude of the Z pulse and measuring its induced oscillation frequency, a flux-dependent ZZ interaction can be resolved [Fig. 2(d)]. The simulated ZZ interaction calculated from the simulated energy levels with Eq. (3) is highly consistent with our measurement results. This consistency further confirms the validity of our methods. The minimum ZZ interaction is  $2\pi \times (-6.3)$  kHz, achieved with the external flux bias at  $\varphi_{\rm ex}/2\pi = 0.309$ . With such a small residual ZZ interaction at the idle bias point, we have confirmed that it has a negligible influence on the single-qubit gates. Through individual (simultaneous) randomized benchmarking, we achieve single-qubit gate fidelities of 99.985% (99.985%) for Q1 and 99.981% (99.983%) for Q2, with all fidelity uncertainties below 0.001% calculated from the fitting error (see Appendix G for details).

#### B. Maximum ZZ interaction

In contrast to the minimum ZZ interaction achieved at the idle bias point, the DTC allows for a significantly larger ZZ interaction when  $\varphi_{\rm ex}/2\pi \sim 0.5$ . We apply a similar approach for measuring the larger ZZ interaction using the JAZZ protocol. Because of the fast oscillation resulting from the large ZZ interaction, the extra oscillation introduced by varying the phase of the final  $\Phi_{\pi/2}(t)$  gate is no longer necessary. Instead, we fix its phase to  $90^{\circ}$  as a simple  $Y_{\pi/2}$  gate and extract ZZ interaction from the observed oscillation frequency given as  $\zeta = 2\omega_{\rm m}$ . The simulation results remain consistent with the measurement results [Fig. 3(a)]. A maximum ZZ interaction of  $2\pi \times (-82.5)$  MHz is obtained at the external flux  $\varphi_{\rm ex}/2\pi = 0.47$ . By comparing this with the minimum ZZ interaction at the idle bias point, we obtain an on-off ratio of  $1.3 \times 10^4$ .

When considering the subspace comprised solely of qubits, given the toy model in the dispersive regime, the energy-level repulsion between  $|02\rangle$  and  $|11\rangle$ , akin to the single-transmon-coupler case, contributes to the ZZ interaction. However, it is not applicable in the strong coupling regime, where larger ZZ interactions arises and a coupler-state-mediated process should be considered [62]. We denote the states  $|Q1,Q2,P,M\rangle$  as eigenstates numerically calculated from the Hamiltonian [Eq. (1)] by suppressing the qubit-coupler couplings, for the purpose of the following explanation. Starting from the idle flux point, the energy  $E_{|1100\rangle}$  decreases with increasing the flux bias because of the interaction between the diabatic states,  $|1100\rangle$  and  $|1001\rangle$  [Fig. 3(b)]. However, this does not lead to a large ZZ interaction, because the energy  $E_{|0100\rangle}$  also

![](_page_4_Figure_7.jpeg)

FIG. 3. (a) ZZ interaction  $\zeta$  measured by the JAZZ pulse sequence around the maximum ZZ interaction regime. The blue data points are extracted from the measurements, and the red line is calculated from the simulated energy levels. (b) Simulated energy levels of the higher excited states calculated from the original Hamiltonian [Eq. (1)]. The thick colored solid lines show the energy levels when the qubits and coupler transmons are hybridized, while the thin dashed lines show the energy levels assuming zero coupling between the qubits and coupler transmons. The vertical dotted line indicates the idle bias point, while the colored regimes labeled with  $\{A,B,C\}$  roughly indicate different contribution stages to the ZZ interaction.

similarly decreases given the interaction between  $|01\widetilde{00}\rangle$  and  $|00\widetilde{01}\rangle$  [region A in Fig. 3(b)]. With further increasing the flux bias, the contribution of the large ZZ interaction arises due to the large repulsion between  $|00\widetilde{02}\rangle$  and  $|10\widetilde{01}\rangle$ , which induces extra decrease of  $E_{|1100\rangle}$  mediated

by  $|1001\rangle$  [region *B* in Fig. 3(b)]. A slight decrease of the *ZZ* interaction magnitude in the range of 0.47  $< \varphi_{\rm ex}/2\pi < 0.5$  can be attributed to the repulsion from  $|2000\rangle$  and  $|0002\rangle$  to  $|1001\rangle$ , consequently increasing  $E_{|1100\rangle}$  [region C in Fig. 3(b)].

Such a large ZZ interaction is crucial for the implementation of a fast CZ gate for superconducting qubits. However, taking into account the highly complicated energy levels with multiple anticrossings, a finely tuned Z pulse should be provided for an adiabatic process to suppress the leakage error.

#### IV. CZ-GATE IMPLEMENTATION

## A. Preliminaries for CZ gate

First, let us emphasize the conditions of the idle bias point that are prepared before implementing the CZ gate. A persistent flux is introduced into the superconducting loop of the DTC, generated by the superconducting coil. The idle bias point is confirmed through the characterization of the JAZZ sequence, which gives the near-zero minimum

ZZ interaction magnitude. Then, the single-qubit gates for the two qubits are precisely calibrated with the Derivative Removal by Adiabatic Gate (DRAG) method [65,66]. We note that a CZ gate with high fidelity is realized through precise calibration of the controlled phase (CPHASE) gate exploiting the ZZ interaction. Therefore, single-qubit gates with high fidelities are essential, as they otherwise would introduce extra phases that could miscalibrate the CZ-gate phase during optimization.

Before the CZ-gate implementation, it is necessary to carefully calibrate the distortion of a Z pulse, which arises during the transmission along the fast flux line. However, the distortion characterization becomes tricky if there is no readout resonator for coupler's phase tomography. The DTC scheme shows its advantages in addressing this issue. First, the single tunable element among the four transmons simplifies the characterization process compared to the STC scheme, which usually consists of a tunable coupler and at least another tunable qubit [22]. Second, due to the large coupling and level repulsions between the qubits and coupler transmons, we can use the qubits to characterize the distorted Z pulse that is introduced into the DTC loop. A Ramsey-type experiment along with phase tomography [22], typically employed for pulse-distortion characterization, is detailed in Appendix H. Subsequently, a predistortion of the Z pulse is applied during the optimization and benchmarking of the CZ gate.

#### B. CZ-gate benchmarking

The ZZ interaction can be efficiently activated with an applied Z pulse applied through the DTC loop, resulting in a CPHASE gate defined as  $U_{\text{CPHASE}} = \text{diag}(e^{\mathrm{i}\theta_0}, e^{\mathrm{i}\theta_1}, e^{\mathrm{i}\theta_2}, e^{\mathrm{i}\theta_3})$ . A CZ gate is achieved with a  $\pi$  phase accumulated, i.e.,  $\theta_{\text{CZ}} = \theta_3 - \theta_1 - \theta_2 + \theta_0 = \pi$ . Though each of the two qubits contains only a single Josephson junction, usually considered as a fixed-frequency qubit, the substantial repulsion of their energy levels from the coupler transmons leads to a dynamical change of their frequencies during the CZ gate. Therefore, the inclusion of a commonly used error-free virtual-Z (VZ) gate [67] remains essential in the DTC scheme to compensate for the additional Z rotation ( $\theta_1$  or  $\theta_2$ ) of each qubit [Fig. 4(a)].

To optimize the CZ gate, we start with a Slepian pulse shape [54] as an initial guess and employ an optimization process driven by the RL algorithm, following the guidelines outlined in Ref. [68]. While the Z-pulse shape and VZ gates can be jointly optimized together [20], we choose to decouple them into two parts to enhance the efficiency of the optimization process (see Appendix I for details). The decoupled optimization process is pivotal for the DTC scheme, considering the high sensitivity of the VZ-gate phase to the shape of the Z pulse. After those meticulous optimizations, we confirm the implemented gate as a CZ gate through quantum process tomography (see Appendix J

for details). The achieved fidelity is approximately 95.9%, primarily affected by the state-preparation-and-measurement (SPAM) error [59,69].

A pure CZ-gate fidelity can be accessed through two-qubit standard and interleaved randomized benchmarking (SRB and IRB, respectively) [58–60]. A schematic of the SRB (IRB) sequence is illustrated in Fig. 4(a), where the survival probabilities  $P_{|0000\rangle}$  and  $P_{\mathcal{X}_1}$  are measured against the number m of the randomly selected Clifford gates with (without) CZ gates interleaved in the sequence. The total population in the computational subspace,  $P_{\mathcal{X}_1}$ , is defined as

$$P_{\mathcal{X}_1} = P_{|\widetilde{0000}\rangle} + P_{|\widetilde{0100}\rangle} + P_{|\widetilde{1000}\rangle} + P_{|\widetilde{1100}\rangle}, \qquad (5)$$

which is used for leakage randomized benchmarking (LRB) [70] and is fitted by

$$P_{\mathcal{X}_1}(m) = A + B\lambda_L^m, \tag{6}$$

as in Fig. 4(b). In the presence of leakage, the survival probability  $P_{|0000\rangle}$  estimated from the RB should be modeled using double exponential decays [71], which usually makes the fitting unreliable. To address this, we derive a single exponential decay model, fitting the results with

<span id="page-5-0"></span>
$$P_{|0000\rangle}(m) - P_{\mathcal{X}_1}(m)/d = C\lambda_r^m + D, \tag{7}$$

where d=4 is the dimension of the computational subspace [Fig. 4(c)] (see Appendix K for details). We note that the CZ-gate infidelity comprises two contributions: the leakage error  $L_1^{\rm CZ}$  estimated from  $\lambda_L$  and the gate error  $r^{\rm CZ}$  estimated from  $\lambda_r$ .

First, the leakage error  $L_1^{\text{SRB(IRB)}}$  is estimated by

$$L_1^{\text{SRB(IRB)}} = (1 - A)(1 - \lambda_L^{\text{SRB(IRB)}}).$$
 (8)

With the estimated reference leakage error  $L_1^{\rm SRB}$  and the interleaved one  $L_1^{\rm IRB}$ , the leakage error of the CZ gate can be calculated as

$$L_1^{\text{CZ}} = 1 - \frac{1 - L_1^{\text{IRB}}}{1 - L_1^{\text{SRB}}}.$$
 (9)

On the other hand, the error rate  $r^{\rm SRB(IRB)}$  in standard (interleaved) RB is defined (in a similar manner to the widely used methods [20,22,24]) as

$$r^{\text{SRB(IRB)}} = (1 - \lambda_r^{\text{SRB(IRB)}})(1 - 1/d).$$
 (10)

The CZ-gate error can be obtained as

![](_page_6_Figure_2.jpeg)

FIG. 4. (a) Pulse sequence for the randomized benchmarking (RB). It encompasses m randomly selected two-qubit Clifford gates  $(C_2^{(k)}; k = 1, ..., m)$ , with and without the CZ gates interleaved, concluding with a recovery Clifford gate  $(C_2^{\rm r})$ , denoted as standard RB (SRB) and interleaved RB (IRB), respectively. The entire sequence collectively functions as an identity operation applied to the two qubits. The population of  $|0000\rangle$ ,  $P_{|0000\rangle}$ , is finally measured (M) as the sequence fidelity. The population  $P_{\mathcal{X}_1}$  in the computational subspace,  $\mathcal{X}_1 = \{|0000\rangle, |0100\rangle, |1000\rangle, |1100\rangle\}$ , is also measured for leakage error benchmarking. The optimized CZ gate comprises a Z pulse with 48-ns duration applied to the coupler loop of the DTC and two virtual-Z (VZ) gates applied to the two qubits (see Appendix I for details). (b) Leakage RB (LRB). Each data point and its error bar are the average and standard deviation of measured results on ten randomly selected RB sequences illustrated in (a), respectively. Both the reference and interleaved results are fitted with exponential curves. (c) Standard and interleaved RB results characterizing the CZ-gate error. The error rates  $r^{\rm SRB}$  and  $r^{\rm IRB}$  and the CZ-gate error  $r^{\rm CZ}$  are calculated from the exponential fitting based on Eq. (7). (d) 12-hour time frame measurement of the CZ-gate error  $r^{\rm CZ}$  and corresponding leakage error  $L_1^{\rm CZ}$ , where the red and blue dashed lines depict the respective average errors. The last data point (pointed by a green arrow) of the CZ-gate error is calculated from the results in (c).

$$r^{\rm CZ} = 1 - \frac{1 - r^{\rm IRB}}{1 - r^{\rm SRB}} \approx \frac{(d-1)}{d} \left( 1 - \frac{\lambda_r^{\rm IRB}}{\lambda_r^{\rm SRB}} \right). \tag{11}$$

A typical result of LRB with the estimated leakage error  $L_1^{\rm CZ}$  of 0.027  $\pm$  0.006% is depicted in Fig. 4(b), along with an evaluation of the CZ-gate error of  $r^{\rm CZ}=0.090\pm0.009\%$  in Fig. 4(c).

To validate the stability of our results, we conduct the measurements of the CZ-gate error within a 12-hour time frame [Fig. 4(d)]. Throughout the measurement, the CZ-gate parameters are optimized only once at the beginning, while the single-qubit gates are repeatedly calibrated after each benchmarking sequence measurement. The six measured

CZ-gate errors  $r^{\rm CZ}$ , all below 0.1%, underscore the reliability and stability of our achievement. The average result gives the  $r^{\rm CZ}$  of 0.09  $\pm$  0.01%, while the leakage error  $L_1^{\rm CZ}$  [70,71] is also evaluated each time with an average of 0.030  $\pm$  0.003%.

Here, we note that the CZ-gate error  $r^{\rm CZ}$  introduced above is not equivalent to the gate infidelity in the presence of leakage error. The total CZ-gate infidelity  $(1 - \bar{F})$  encompasses both  $r^{\rm CZ}$  and the leakage error  $L_1^{\rm CZ}$  measured by LRB. Therefore, the total gate fidelity  $\bar{F}$  is given as [71]

$$\bar{F} = 1 - \frac{L_1^{\text{CZ}}}{d} - r^{\text{CZ}},$$
 (12)

which is evaluated to be  $99.90 \pm 0.01\%$  in our experiment.

Note that  $r^{\rm CZ}$  also incorporates contributions from leakage error. This inclusion is based on the assumption of a depolarizing leakage model for the qubit system, where  $\lambda_r = (1-L_1)(1-p_D)$  for Eq. (7), with  $p_D$  representing the depolarizing rate in the computational subspace [71]. Under this model, the total CZ-gate fidelity can also be expressed as

$$\bar{F} = 1 - L_1^{\text{CZ}} - \frac{d-1}{d} p_D^{\text{CZ}},$$
 (13)

<span id="page-7-0"></span>with the assumption of  $L_1^{\rm CZ}$ ,  $p_D^{\rm CZ} \ll 1$  (see Appendix K for details). This formulation provides a more explicit representation of the gate infidelity, delineating contributions from the leakage and depolarizing effects. Besides, it also provides the depolarizing-induced gate error  $r_D^{\rm CZ}$ :

$$r_D^{\text{CZ}} \equiv \frac{d-1}{d} p_D^{\text{CZ}} = r^{\text{CZ}} - \frac{d-1}{d} L_1^{\text{CZ}}.$$
 (14)

## C. CZ-gate error analysis

The CZ-gate errors are typically categorized into two parts: coherent and incoherent errors. Coherent errors primarily encompass nonadiabatic process-induced leakage error and imperfect CZ- and VZ-phase errors. Though difficult, these errors can be minimized through precise tuning of the control pulse. On the other hand, incoherent errors, arising from limited qubit coherence due to various noise sources, present a more challenging mitigation task. The leakage error can be directly measured simultaneously with the LRB experiment [22], and a coherent error rate <0.01% due to the finely calibrated phase error <1.5° can be considered negligible at the current stage [20]. Even with considerable efforts, however, estimating incoherent errors for high-fidelity two-qubit gates remains challenging [20–22,42]. Single-qubit coherence times are typically characterized to elucidate the incoherent error of a two-qubit gate. However, compared to the randomized benchmarking measurement, the separate decoherence measurements often underestimate the decoherence experienced by the qubits when the two-qubit gate is applied. Despite those imperfect error-budget estimations, they have provided guidance for enhancing gate fidelity to surpass the threshold [4,72] required for implementing the surface code [73,74] over the past decades. Therefore, we present here only our rough estimation of the contributors to the CZ-gate error and place more emphasis on the insights gained from the results.

The CZ-gate errors, with varying gate length, are measured using the CZ gate optimized with the same methods described above, simultaneously with the assessment of leakage error [Fig. 5(a)]. The leakage errors are relatively small (0.010%–0.035%), except for the one about 0.1% with the CZ-gate length of 40 ns, as illustrated by the leftmost point in Fig. 5(a). We attribute the sudden increase

![](_page_7_Figure_9.jpeg)

FIG. 5. (a) CZ-gate error  $r^{\rm CZ}$  and the corresponding leakage error  $L_1^{\rm CZ}$  measured and calculated from the RB results for various CZ-gate lengths. The error bars are calculated from the fitting error of the RB results. The error bars of the leakage error data are smaller than the symbol size. (b) Depolarizing-induced gate error  $r_D^{\rm CZ}$  calculated with Eq. (14). The data points and their standard deviations are calculated from the data in (a). The red line shows a linear fit. The cross marker is an obvious outlier, corresponding to a gate length of 40 ns, and is therefore excluded from the linear fitting.

of the leakage error to the failure of optimizing the Z-pulse shape in experiment for such a short gate length. This is supported by achieving a CZ-gate fidelity higher than 99.99% in numerical simulation by using a theoretically optimized pulse shape with a gate length of 40 ns. The discrepancy could be attributed to the bandwidth limitation of the electric devices and circuits and/or the failure of the RL-based optimization. We also observe a slight increase in the leakage error with gate length exceeding 100 ns. This is attributed to the fact that the contribution of the leakage error becomes much smaller compared to other errors, making it challenging to optimize precisely during the RL-based optimization process.

We model the depolarizing-induced error  $r_D^{\rm CZ}$  as the sum of incoherent errors (see Appendix L) and a gate-length-independent error  $r_0$ :

$$r_D^{\text{CZ}} = r_{\text{incoherent}} + r_0 = \frac{2}{5} \frac{t_{\text{gate}}}{T_{\text{eff}}} + r_0, \tag{15}$$

where  $t_{\rm gate}$  is the CZ-gate length and  $T_{\rm eff}$  represents the effective coherence time experienced by the entire system during the IRB experiment. We fit the gate-length dependence of the depolarizing-induced error with the linear model [Fig. 5(b)], except for the data marked as an obvious outlier. We attribute this outlier to a sudden drop in qubit coherence, which could be caused by the significantly stronger hybridization between the qubit and coupler with the requirement of such a short gate length. The high Pearson correlation coefficient (approximately 0.995) for the linear model, with a small p value ( $p < 10^{-9}$ ), indicates that the correlation is statistically significant. The negligibly small offset we obtain,  $r_0 = -0.0007 \pm 0.008\%$ , validates our assumption of the depolarizing error model.

In principle, the effective coherence time  $T_{\rm eff}$  mainly encompasses both  $T_1$  and  $T_{\phi}$  of the two qubits as well as the influence of the decoherence in the two coupler transmons, given they are highly coupled during the CZ gate. The linear relation is modeled with neglecting the 1/f flux noise, as it plays only a marginal role [22] (see Appendix L for details). Note that the effective coherence time  $T_{\rm eff}^{\rm exp}=23.9\pm1.5~\mu {\rm s}$  cannot be entirely predicted from the coherence time of the two individual qubits measured at the idle bias point,  $T_{\rm eff}^{\rm est} = 67.6 \pm 11.4 \,\mu \rm s$ , similarly to other works [20,21]. We attribute this to the possibility of additional decoherence introduced when the CZ gate is applied. We acknowledge that purity benchmarking can be employed to differentiate between coherent and incoherent errors [75]. However, the requirements for full state tomography, including states in the noncomputational subspace, as well as the explicit error budget when leakage error emerge, remain open questions that extend beyond the scope of this work.

#### V. CONCLUSION AND DISCUSSION

In this work, our primary demonstration focused on the DTC scheme, showcasing its high-performance experimentally. We began by presenting an intuitive model that describes the coupling mediated by the DTC. The toy model told us that Josephson junctions JJ3 and JJ4 could potentially be replaced by linear inductors to realize nearzero ZZ interaction at the idle bias point, while the nonlinearity of JJ5 must be taken into account to provide the tunable-coupling strength and enable the emergence of large ZZ interactions. We also achieved simultaneous high fidelity and stability in both single- and two-qubit gates. This achievement was made possible by the finely designed and fabricated transmons with high coherence, as well as a large on-off ratio of the qubit-qubit coupling achieved through carefully selected circuit parameters. With meticulous calibration, we effectively "turned off" the coupling by tuning the flux into the DTC loop to the idle bias point. Subsequently, we dynamically activated the coupling with an optimized Z pulse passing through the fast flux line. We opted for a CZ-gate length of 48 ns, striking a balance between leakage error and incoherent error, and achieved a CZ-gate fidelity of  $99.90 \pm 0.01\%$  stably during a 12-hour measurement.

To advance toward even higher gate fidelity, there remain issues that require thorough investigation and complete understanding. First, a shorter gate length for the CZ gate is preferred to mitigate the incoherent error. However, a faster CZ gate requires larger coupling capacitance, which may degrade qubit coherence because of its stronger coupling to the coupler transmons. Besides, another challenge lies in addressing the incapability to optimize such a short-duration pulse effectively for suppressing the leakage error. Second, there exists additional decoherence involved during the benchmark of the CZ gate, which may be due to

multilevel mixing of the total system and extra noise channels activated during the *Z* pulse.

We note that high-performance gate operation is not the sole metric for evaluating the quality of a qubit coupling scheme. The DTC scheme brings various other advantages, such as less frequency-collision probability due to highly detuned qubits, flexible spatial arrangement of qubits, and simplified control degrees of freedom related to the single tunability element. These attributes make it highly promising as a candidate for implementing NISQ applications and quantum error correction in the near future.

#### ACKNOWLEDGMENTS

We acknowledge K. Kusuyama and Y. Sakoda for the Ta-film deposition and A. Badrutdinov for the TSV-fabrication assistance. This research was partly funded by the Ministry of Education, Culture, Sports, Science and Technology (MEXT) Quantum Leap Flagship Program (Q-LEAP) (Grant No. JPMXS0118068682).

## **APPENDIX A: FABRICATION**

The fabricated sample chips are based on tantalum-filmbased superconducting circuits [31,32], which have been demonstrated to showcase an extended coherence time. In the fabrication process, a tantalum (Ta) film of around 135 nm thick is initially sputtered on a precleaned highresistivity (>10 k $\Omega$  cm) (100)-oriented silicon wafer at 300 °C. The growth of  $\alpha$ -Ta film is simply confirmed by the resistivity of approximately 15  $\mu\Omega$  cm [76] at ambient condition. Then, the resonators, qubit capacitances, and control lines are patterned through photolithography. After development, the exposed Ta film is subjected to reactive ion etching employing CF<sub>4</sub> gas [32]. Following the wafer cleaning procedure involving organic remover, oxygen plasma, and hydrofluoric acid, we create Dolan-bridgetype Josephson junctions through aluminum (Al) deposition and lift-off, employing electron-beam lithography [77]. Subsequently, through-silicon vias (TSVs) are produced using the Bosch process and are further metallized through Al deposition and lift-off, employing an additional photolithography step. Finally, the wafer is diced into  $2.5 \times$ 5-mm<sup>2</sup> chips, which are wire bonded to a home-designed printed circuit board (PCB).

#### APPENDIX B: MEASUREMENT SETUP

<span id="page-8-0"></span>Figure 6 depicts a schematic diagram illustrating the measurement setup. Under ambient conditions, two arbitrary waveform generators (AWGs) are employed. One AWG (Zurich Instruments SHFQC) stands out as it has the capability to directly generate signals up to 8.5 GHz without the requirement for additional mixers. This feature is leveraged for producing DRAG waveforms essential for qubit control. Moreover, the device excels in generating and demodulating multiple-frequency signals, facilitating

![](_page_9_Figure_2.jpeg)

FIG. 6. Schematic diagram of the measurement setup. In the device SHFQC, the RO and RI ports are used to generate and receive the microwave tones for qubit readout, respectively.

the simultaneous multiplexed readout of the three resonators. Another AWG device (Zurich Instruments HDAWG8) is employed for generating the Z pulse. It incorporates real-time precompensation to effectively mitigate distortion in the Z-pulse waveform. A dc source (Yokogawa GS200) is employed to supply a constant dc current to the superconducting coil, which is crucial for maintaining a stable and consistent flux bias in the coupler loop. All of these electronic devices are synchronized through a common rubidium frequency standard (Stanford Research Systems FS725), ensuring precise signal phase alignment.

For qubit readout and control, the waveforms are conveyed through coaxial cables, which are interconnected by a series of attenuators (XMA) positioned at various temperature stages upon reaching the base temperature of approximately 8 mK within the dilution refrigerator (BlueFors LD400). The microwave tone for qubit readout is transmitted through a circulator and subsequently reflected by the sample chip. Following this, the signal carrying the qubit information undergoes another transmission through the same circulator. Once it passes through

an isolator, the signal enters a home-built impedancematched Josephson parametric amplifier (IMPA) [78] via an additional circulator in the process. The pump and bias setups for the IMPA are omitted in the figure for the sake of simplicity. After being amplified and reflected by the IMPA, the signal is transmitted into the second circulator and redirected toward a sequence of isolators. Amplified at 4 K by a high-electron-mobility-transistor (HEMT) amplifier (LNF LNC4\_16C) and at 300 K by a low-noise microwave amplifier, the signal is then received and demodulated for qubit state discrimination. Each of the two qubits has its dedicated XY drive lines, while the control signals for XY and Z of the coupler transmons converge onto the fast flux line through a diplexer (QMC 0218LNM) before entering the fridge. To mitigate thermal excitation of the coupler modes while maintaining efficient control of XY and Z for coupler transmons, a low-pass filter (Mini-Circuits VLF-2250+) is employed. All these signals are transmitted through the cables into the package, which serves as the enclosure for holding the chip. Additionally, a dc current is applied to bias the DTC's loop, transmitted through a twisted pair line into a superconducting coil outside the sample package. To mitigate high-frequency noise, a homemade low-pass filter (<1.6 kHz) at the 4-K stage and a  $\pi$  filter (<1 MHz) at room temperature are implemented. To safeguard the qubit from environmental radiation [79], the sample chip and its PCB are initially enclosed within the copper-made sample package and further shielded magnetically with an aluminum can and a two-layer  $\mu$ -metal shield at the base temperature.

## APPENDIX C: DEVICE PARAMETERS

<span id="page-9-0"></span>The circuit parameters (Table I) are used for simulating the energy levels and ZZ interaction of the chip used in this work. The frequencies and anharmonicities of the transmon and resonator dressed states (Table II) are measured at the idle bias point with  $\varphi_{\rm ex}/2\pi=0.309$ . We note that the frequency detuning ( $\Delta_{21}/2\pi=464$  MHz) between the two qubits is larger than their anharmonicities, indicating that they are positioned outside of the straddling regime.

Given the complicated energy-level hybridization, the ZZ interaction can be precisely calculated only through

TABLE I. Circuit parameters for the simulation.

| Capacitance      | $C_{11}$        |          | $C_{22}$ | $C_{1}$  | 33       | $C_{44}$        |
|------------------|-----------------|----------|----------|----------|----------|-----------------|
| Value (fF)       | 91.86           | 5        | 91.79    | 110      | .27      | 106.36          |
| Critical current | $I_{\rm c1}$    |          | $I_{c2}$ | $I_{c3}$ | $I_{c4}$ | $I_{c5}$        |
| Value (nA)       | 26.13           | 3 3      | 31.93    | 47.73    | 47.68    | 10.32           |
| Capacitance      | C <sub>12</sub> | $C_{13}$ | $C_{14}$ | $C_{23}$ | $C_{24}$ | C <sub>34</sub> |
| Value (fF)       | 0.04            | 5.73     | 0.17     | 0.26     | 5.77     | 1.73            |

TABLE II. Dressed-state frequencies and anharmonicities of the transmons and readout resonators at the idle bias point. P and M stand for the plus- and minus-sign composite modes of the coupler transmons, behaving like a fixed-frequency transmon and a CSFQ, respectively.

| Qubit                                         | Q1             | Q2             | P              | M              |
|-----------------------------------------------|----------------|----------------|----------------|----------------|
| Readout frequency (GHz) Drive frequency (GHz) | 8.184<br>4.314 | 8.261<br>4.778 | 8.101<br>5.495 | 8.101<br>5.373 |
| Anharmonicity (MHz)                           | -212           | -199           | 01.50          | 0.070          |

numerical simulation. Therefore, we manually search the circuit parameters to achieve an acceptable minimum ZZ interaction at the idle bias point, as well as a sufficiently large ZZ interaction for a fast CZ gate. The following steps describe our procedure, where the presence of readout resonators and control lines is neglected because of their marginal influence on the ZZ interaction between qubits.

- (1) The frequencies of the two data qubits are chosen to be within 4–5.5 GHz, with anharmonicities around –200 MHz to enable fast single-qubit gates. A detuning of 500 MHz, which is larger than their anharmonicities, is used to demonstrate qubit operation outside the straddling regime.
- (2) Stray capacitances, such as  $C_{14}$ ,  $C_{23}$ , and  $C_{12}$ , are usually very small (<1 fF) and contribute minimally to the ZZ interaction. So, they can be neglected. The mutual capacitance  $C_{34}$ , though small, is comparable to the coupling capacitance and is usually considered as a fixed value during the search for other circuit parameters. This holds true even with minor changes to the structures around the DTC loop, where  $C_{34}$  arises. The stray capacitance values can be obtained using finite element analysis with commercial software like Sonnet or COMSOL.
- (3) The coupling capacitances  $C_g = C_{13} = C_{24}$  are chosen to be 5%–10% of the data qubit shunt capacitance, corresponding to a 100–200-MHz coupling between the data and coupler transmons empirically. A larger coupling capacitance results in a larger ZZ interaction, facilitating faster CZ gates. However, it permits only small variations in other parameters to achieve minimal ZZ interaction at the idle bias point. For the following simulation, we fix  $C_{13} = C_{24} = 5.7$  fF as an example. It should be noted, however, that this value should be finely tuned for optimal circuit parameters.
- (4) The ratio  $\alpha = E_{\rm J5}/E_{\rm J3} = E_{\rm J5}/E_{\rm J4}$  is first fixed to search for the circuit parameters  $C_{\rm c} \equiv C_{33} = C_{44}$  and  $E_{\rm Jc} \equiv E_{\rm J3} = E_{\rm J4}$ , as demonstrated in Figs. 7(a) and 7(b). We use  $\alpha = 0.216$ , the same as in our device, which should not be too large (<0.25, empirically). Intuitively, a larger  $C_{\rm c}$  and smaller  $E_{\rm Jc}$  lead to lower coupler-mode frequencies, resulting in stronger coupling between the data qubits and

![](_page_10_Figure_9.jpeg)

FIG. 7. Numerical simulation of the ZZ interaction with fixed parameters of  $\alpha=0.216$  for (a) and (b) and  $C_{\rm c}=108$  fF for (c) and (d). The minimum and maximum ZZ interactions,  $\zeta_{\rm min}$  and  $\zeta_{\rm max}$ , respectively, are obtained with different flux biases through the DTC loop for the idle bias point and fast CZ gate, respectively. The red stars shown in the figures indicate the parameters used for the experiment.

the DTC. This induces larger ZZ interactions for both the minimum and maximum ZZ interactions,  $\zeta_{\min}$  and  $\zeta_{\max}$ , respectively, obtained by varying the flux through the DTC. A parameter set of  $\{C_{\rm c}, E_{\rm Jc}\}$  is chosen to balance  $\zeta_{\min}$  at the idle bias point and  $\zeta_{\max}$  for achieving a fast CZ gate.

(5) We fix the value of  $C_c$  obtained in step 4 and search for the parameter set  $\{E_{Jc}, \alpha\}$ , as shown in Figs. 7(c) and 7(d). A larger  $\alpha$  induces a stronger coupling between the two coupler transmons, which indirectly increases the coupling between the two data qubits and their ZZ interaction. Therefore, these parameters should also be determined to balance the minimum and maximum ZZ interactions, similar to step 4.

The simple but effective procedure shown above demonstrates our search for the parameter set  $\{C_g, C_c, E_{Jc}, \alpha\}$  of the DTC. Steps 3–5 can be repeated several times to obtain an optimal set. A direct parameter search in the four-dimensional space would be possible but time consuming. Using our procedure, a desired parameter set that is feasible with current fabrication techniques can be easily obtained. We note that these values, shown in Table I, are slightly different from the theoretically designed ones, which is due to the fabrication error.

#### <span id="page-10-0"></span>APPENDIX D: TOY MODEL OF THE DTC

## 1. Toy model without qubits

We first derive a toy model of the DTC without considering the data qubits. Assuming the symmetric design of  $C_{33}=C_{44}=C_{\rm c}$  and  $E_{\rm J3}=E_{\rm J4}=E_{\rm J}$  as well as denoting  $E_{\rm J5}=\alpha E_{\rm J}$  ( $\alpha<1$ ), the Lagrangian of the DTC can be written as

$$\begin{split} L &= \left(\frac{\Phi_{0}}{2\pi}\right)^{2} \left[\frac{C_{33}}{2} (\dot{\varphi}_{p} + \dot{\varphi}_{m})^{2} + \frac{C_{44}}{2} (\dot{\varphi}_{p} - \dot{\varphi}_{m})^{2} + 2C_{34} \dot{\varphi}_{m}^{2}\right] \\ &+ E_{J} \cos{(\varphi_{p} + \varphi_{m})} + E_{J} \cos{(\varphi_{p} - \varphi_{m})} \\ &+ \alpha E_{J} \cos{(2\varphi_{m} + \varphi_{ex})} \\ &= \left(\frac{\Phi_{0}}{2\pi}\right)^{2} [C_{c} \dot{\varphi}_{p}^{2} + (C_{c} + 2C_{34}) \dot{\varphi}_{m}^{2}] \\ &+ 2E_{J} \cos{\varphi_{p}} \cos{\varphi_{m}} + \alpha E_{J} \cos{(2\varphi_{m} + \varphi_{ex})}, \end{split} \tag{D1}$$

<span id="page-11-3"></span>where  $\varphi_p \equiv (\varphi_3 + \varphi_4)/2$  and  $\varphi_m \equiv (\varphi_3 - \varphi_4)/2$ . The potential is defined as

$$V = -2E_{\rm J}\cos\varphi_{\rm p}\cos\varphi_{\rm m} - \alpha E_{\rm J}\cos(2\varphi_{\rm m} + \varphi_{\rm ex}). \quad (D2)$$

<span id="page-11-0"></span>For a given bias flux  $\varphi_{ex}$ , the minimum potential energy leads to

$$\begin{split} &\frac{\partial V}{\partial \varphi_{\rm p}} = 2E_{\rm J}\sin\varphi_{\rm p}\cos\varphi_{\rm m} = 0,\\ &\frac{\partial V}{\partial \varphi_{\rm m}} = 2E_{\rm J}\cos\varphi_{\rm p}\sin\varphi_{\rm m} + 2\alpha E_{\rm J}\sin\left(2\varphi_{\rm m} + \varphi_{\rm ex}\right) = 0. \end{split} \tag{D3}$$

<span id="page-11-1"></span>Note that in the first equation in Eq. (D3), assuming  $\cos \varphi_{\rm m}=0$ , would result in  $\partial^n V/\partial \varphi_{\rm p}^n=0$  for any order n. This solution does not correspond to a physically viable minimum-potential-energy position for the p mode. Therefore, the conditions

$$\varphi_{\rm p} = 2\pi \times k \quad (k = {\rm integer}),$$

$$\sin \varphi_{\rm m} + \alpha \sin (2\varphi_{\rm m} + \varphi_{\rm ex}) = 0,$$
(D4)

should be satisfied. Here, we disregard the condition  $\varphi_{\rm p}=\pi+2\pi\times k$ , as it results in a maximum energy potential rather than a minimum.

<span id="page-11-5"></span>At the idle bias point, the two coupler transmons are decoupled, which is indicated by the zero coupling term  $-E_{\rm J5}\cos\left(\varphi_4-\varphi_3-\varphi_{\rm ex}\right)=0$  at the minimum-potential-energy point. This leads to

$$\cos\left(2\varphi_{\rm m} + \varphi_{\rm ex}\right) = 0. \tag{D5}$$

Combined with the second line in Eq. (D4), the conditions

$$\sin \varphi_{\rm m} + \alpha \sin \left(2\varphi_{\rm m} + \varphi_{\rm ex}\right) = 0,$$
 
$$\cos \left(2\varphi_{\rm m} + \varphi_{\rm ex}\right) = 0 \tag{D6}$$

<span id="page-11-4"></span>result in

$$2\varphi_{\rm m} + \varphi_{\rm ex} = \pi/2 + k\pi,$$
  

$$\sin \varphi_{\rm m} = \pm \alpha.$$
 (D7)

In our device,  $\alpha \approx 0.216$ . Therefore, we estimate the bias flux at the idle bias point,  $\varphi_{\rm ex}^{\rm est}/2\pi=0.319$ , which is close to the measured idle-point flux  $\varphi_{\rm ex}^{\rm exp}/2\pi=0.309$ . Another solution of  $\varphi_{\rm ex}^{\rm est}/2\pi=-0.319$  is also reasonable due to the symmetry of the energy potential.

Given any  $\varphi_{ex}$ , we have

$$\begin{split} \cos\varphi_{\rm m} &= \sqrt{1-\sin^2\!\varphi_{\rm m}} \\ &= \sqrt{1-\alpha^2\!\sin^2\!\left(2\varphi_{\rm m}+\varphi_{\rm ex}\right)} \\ &\geq \sqrt{1-\alpha^2} \\ &\approx 0.976. \end{split} \tag{D8}$$

<span id="page-11-2"></span>It indicates that, given the small value of  $\alpha$ , the inductive energy of the p mode, whose coefficient is defined by  $-2E_{\rm J}\cos\varphi_{\rm m}$ , remains largely unchanged when we sweep the external flux. Therefore, we approximate the potential energies of the p and m modes separately as

$$V = -2E_{\rm J}\cos\varphi_{\rm p} - 2E_{\rm J}\cos\varphi_{\rm m} - \alpha E_{\rm J}\cos(2\varphi_{\rm m} + \varphi_{\rm ex}). \quad (D9)$$

In this approximation, the term  $\cos \varphi_{\rm p} \cos \varphi_{\rm m}$  is approximated as

$$\begin{split} \cos \varphi_{\rm p} \cos \varphi_{\rm m} &\approx \left(1 - \frac{\varphi_{\rm p}^2}{2} + \frac{\varphi_{\rm p}^4}{24}\right) \left(1 - \frac{\varphi_{\rm m}^2}{2} + \frac{\varphi_{\rm m}^4}{24}\right) \\ &\approx 1 - \frac{\varphi_{\rm p}^2}{2} + \frac{\varphi_{\rm p}^4}{24} - \frac{\varphi_{\rm m}^2}{2} + \frac{\varphi_{\rm m}^4}{24} + \frac{\varphi_{\rm p}^2 \varphi_{\rm m}^2}{4} \\ &\approx \cos \varphi_{\rm p} + \cos \varphi_{\rm m} - 1 + \frac{\varphi_{\rm p}^2 \varphi_{\rm m}^2}{4}. \end{split} \tag{D10}$$

The constant value of unity and the coupling term  $\varphi_p^2 \varphi_m^2$  are omitted to obtain the potential energy described in Eq. (D9). For comparison, we plot the two-dimensional potential energies in Eqs. (D2) [Fig. 8(a)] and (D9) [Fig. 8(b)]. Their difference [Fig. 8(c)] is considerably small around the potential minimum, i.e., the point used for the circuit quantization. Therefore, this approximation is valid with a negligible coupling between the two coupler modes. While it may not yield precise results like in numerical diagonalization, it offers an intuitive understanding of the DTC scheme and fits well the energy spectra shown in Fig. 1(d).

## 2. Hamiltonian of the toy model

We confine the following discussion to the symmetric qubit and DTC design, for simplicity, under the additional assumptions of  $C_{11}=C_{22}=C_{\rm q}$  and  $C_{13}=C_{24}=C_{\rm g}$ . The Lagrangian of two qubits coupled via a DTC is described as

![](_page_12_Figure_2.jpeg)

FIG. 8. Two-dimensional potential energies V at the idle bias point determined by Eq. (D7): (a) original [Eq. (D2)], (b) approximated [Eq. (D9)], and (c) their difference. In (a) and (b), the potential energy value at the minimum is offset to zero for easy comparison.

$$\begin{split} L &= K - V, \\ K &= \left(\frac{\Phi_0}{2\pi}\right)^2 \left[\sum_{i=1}^2 \frac{C_{ii}}{2} \dot{\varphi}_i^2 + \frac{C_{33}}{2} (\dot{\varphi}_{\rm p} + \dot{\varphi}_{\rm m})^2 \right. \\ &\quad \left. + \frac{C_{44}}{2} (\dot{\varphi}_{\rm p} - \dot{\varphi}_{\rm m})^2 + 2C_{34} \dot{\varphi}_{\rm m}^2 \right. \\ &\quad \left. + \frac{C_{13}}{2} (\dot{\varphi}_{\rm 1} - (\dot{\varphi}_{\rm p} + \dot{\varphi}_{\rm m}))^2 + \frac{C_{24}}{2} (\dot{\varphi}_{\rm 2} - (\dot{\varphi}_{\rm p} - \dot{\varphi}_{\rm m}))^2 \right], \\ V &= -\sum_{i=1}^2 E_{\rm Ji} \cos \varphi_i - 2E_{\rm J} \cos \varphi_{\rm p} - 2E_{\rm J} \cos \varphi_{\rm m} \\ &\quad \left. - E_{\rm J5} \cos \left( 2\varphi_{\rm m} + \varphi_{\rm ex} \right), \end{split} \tag{D11}$$

where  $C_{14}$  and  $C_{23}$  are considered negligible, for simplicity, and the potential energy V is approximated as in the decoupled DTC model. The kinetic energy can be written as

$$K = \left(\frac{\Phi_0}{2\pi}\right)^2 \left[\frac{C_{11} + C_{13}}{2} \dot{\varphi}_1^2 + \frac{C_{22} + C_{24}}{2} \dot{\varphi}_2^2 + \frac{C_{33} + C_{44} + C_{13} + C_{24}}{2} \dot{\varphi}_p^2 + \frac{C_{33} + C_{44} + C_{13} + C_{24} + 4C_{34}}{2} \dot{\varphi}_m^2 - C_{13} \dot{\varphi}_1 (\dot{\varphi}_p + \dot{\varphi}_m) - C_{24} \dot{\varphi}_2 (\dot{\varphi}_p - \dot{\varphi}_m) + (C_{33} + C_{13} - C_{44} - C_{24}) \dot{\varphi}_p \dot{\varphi}_m\right],$$
 (D12)

where the last term  $(C_{33}+C_{13}-C_{44}-C_{24})\dot{\varphi}_{\rm p}\dot{\varphi}_{\rm m}$  is neglected below, as  $C_{33}=C_{44}$  and  $C_{13}=C_{24}$  in a symmetric DTC design. The canonical conjugate variables are defined as

$$\begin{split} q_1 &= \frac{\partial L}{\partial \dot{\phi}_1} = \left(\frac{\Phi_0}{2\pi}\right)^2 [(C_{11} + C_{13})\dot{\phi}_1 - C_{13}(\dot{\phi}_p + \dot{\phi}_m)], \\ q_2 &= \frac{\partial L}{\partial \dot{\phi}_2} = \left(\frac{\Phi_0}{2\pi}\right)^2 [(C_{22} + C_{24})\dot{\phi}_2 - C_{24}(\dot{\phi}_p - \dot{\phi}_m)], \\ q_p &= \frac{\partial L}{\partial \dot{\phi}_p} = \left(\frac{\Phi_0}{2\pi}\right)^2 [(2C_{33} + C_{13} + C_{24})\dot{\phi}_p \\ &\quad - (C_{13}\dot{\phi}_1 + C_{24}\dot{\phi}_2)], \\ q_m &= \frac{\partial L}{\partial \dot{\phi}_m} = \left(\frac{\Phi_0}{2\pi}\right)^2 [(2C_{44} + C_{13} + C_{24} + 4C_{34})\dot{\phi}_m \\ &\quad - (C_{13}\dot{\phi}_1 - C_{24}\dot{\phi}_2)]. \end{split} \tag{D13}$$

By introducing  $\mathbf{q} = \{q_i\}$  and  $\boldsymbol{\varphi} = \{\varphi_i\}$ ,  $i \in \{1, 2, p, m\}$ , and defining  $\mathbf{q} = \mathbf{C}\dot{\boldsymbol{\varphi}}$ , the inversion of the capacitance matrix  $\mathbf{C}^{-1}$  is defined as

$$\mathbf{C}^{-1} = \begin{pmatrix} \frac{1}{\overline{C_{q}}} & 0 & \frac{1}{\overline{C_{gp}}} & \frac{1}{\overline{C_{gm}}} \\ 0 & \frac{1}{\overline{C_{q}}} & \frac{1}{\overline{C_{gp}}} & -\frac{1}{\overline{C_{gm}}} \\ \frac{1}{\overline{C_{gp}}} & \frac{1}{\overline{C_{gp}}} & \frac{1}{\overline{C_{p}}} & 0 \\ \frac{1}{\overline{C_{gm}}} & -\frac{1}{\overline{C_{gm}}} & 0 & \frac{1}{\overline{C_{m}}} \end{pmatrix}, \quad (D14)$$

where the symmetric DTC circuit parameters are assumed. Here, we set the coupling terms between the two data qubits to be zero, i.e.,  $\mathbf{C}_{12}^{-1} = \mathbf{C}_{21}^{-1} = 0$ , as they are negligible in the symmetric assumption. The differences between  $\widetilde{C}_{gp}$  and  $\widetilde{C}_{gm}$ ,  $\widetilde{C}_{p}$  and  $\widetilde{C}_{m}$  comes from the capacitance  $C_{34}$ , which is usually small with a negligible value of  $C_{34}$ . Consequently, the Hamiltonian is approximated as

<span id="page-12-0"></span>
$$\begin{split} H &= \mathbf{q}^{\mathrm{T}} \dot{\boldsymbol{\varphi}} - L \\ &= \frac{1}{2\widetilde{C_{\mathrm{q}}}} q_{1}^{2} - E_{\mathrm{J}1} \cos \varphi_{1} + \frac{1}{2\widetilde{C_{\mathrm{q}}}} q_{2}^{2} - E_{\mathrm{J}2} \cos \varphi_{2} \\ &+ \frac{1}{2\widetilde{C_{\mathrm{p}}}} q_{\mathrm{p}}^{2} - 2E_{\mathrm{J}} \cos \varphi_{\mathrm{p}} \\ &+ \frac{1}{2\widetilde{C_{\mathrm{m}}}} q_{\mathrm{m}}^{2} - 2E_{\mathrm{J}} \cos \varphi_{\mathrm{m}} - \alpha E_{\mathrm{J}} \cos \left(2\varphi_{\mathrm{m}} + \varphi_{\mathrm{ex}}\right) \\ &+ \frac{1}{\widetilde{C_{\mathrm{qp}}}} (q_{1} + q_{2}) q_{\mathrm{p}} + \frac{1}{\widetilde{C_{\mathrm{qm}}}} (q_{1} - q_{2}) q_{\mathrm{m}}, \end{split} \tag{D15}$$

which indicates that the two data transmon modes, defined by  $\{q_1, \varphi_1\}$  and  $\{q_2, \varphi_2\}$ , are coupled to the two coupler modes, p and m modes. Note that the p mode is approximated to be a fixed-frequency transmon qubit P, which is valid for small  $\alpha$ . On the other hand, the m mode acts as a capacitively shunted flux qubit (CSFQ) M [80], whose frequency can be tuned with external flux  $\varphi_{\rm ex}$ . In the last term of the Hamiltonian [Eq. (D15)], the coupling term

between Q2 and the m mode results in an effective capacitance with a negative value  $-\widetilde{C_{gm}}$ , which is crucial in demonstrating the quantized Hamiltonian [Eq. (2) in the main text] with a minus sign in front of the coupling term  $g_{2m}$ . The coupling  $g_{ip}$  and  $g_{im}$  can be calculated as

$$g_{1p} = \sqrt{\omega_{1}\omega_{p}} \frac{C_{g}}{2\sqrt{(C_{q} + C_{g})(C_{c} + C_{g})}},$$

$$g_{2p} = \sqrt{\omega_{2}\omega_{p}} \frac{C_{g}}{2\sqrt{(C_{q} + C_{g})(C_{c} + C_{g})}},$$

$$g_{1m} = \sqrt{\omega_{1}\omega_{m}} \frac{C_{g}}{2\sqrt{(C_{q} + C_{g})(C_{c} + 2C_{34} + C_{g})}},$$

$$g_{2m} = \sqrt{\omega_{2}\omega_{m}} \frac{C_{g}}{2\sqrt{(C_{q} + C_{g})(C_{c} + 2C_{34} + C_{g})}}.$$
 (D16)

The difference between the  $g_{ip}$  and  $g_{im}$  can be negligible when  $C_{\rm c}\gg 2C_{34}$  and  $\omega_{\rm p}=\omega_{\rm m}$ .

In the toy model, where the coupling mediated by the DTC is represented by a transmonlike mode P and a CSFQ-like mode M, the effective coupling strength is described

by Eq. (4). The condition  $g_{\rm eff}=0$  at the idle bias point is satisfied when  $\omega_{\rm p}\approx\omega_{\rm m}$ . Note that the terms for the p and m modes in the Hamiltonian [Eq. (D15)] become equivalent and give  $\omega_{\rm p}\approx\omega_{\rm m}$  when Eq. (D5) holds, given  $\widetilde{C_{\rm p}}\approx\widetilde{C_{\rm m}}$  due to the symmetric-circuit assumption in the toy model. Therefore, the approximate condition for the idle bias point is equivalently determined by Eqs. (4) and (D5).

We have derived an analytical toy model with symmetric parameters in the current design of DTC. Variation of these parameters can occur in real devices due to the fabrication error. The asymmetry of those parameters and undesired stray capacitances can result in additional coupling between the four modes, i.e., the two qubits and two coupler modes, which can be accurately determined only through numerical simulations.

## APPENDIX E: QUBIT COHERENCE

<span id="page-13-0"></span>By tuning the flux generated with the superconducting coil, the coherence times, including  $T_1$ ,  $T_2^R$ , and  $T_2^E$ , are carefully measured for each of the four lowest excitation modes involving Q1, Q2, P, and M [Figs. 9(a)–9(c)]. As a function of the flux through the DTC's loop, the modes are

![](_page_13_Figure_10.jpeg)

FIG. 9. Coherence times: (a)  $T_1$ , (b)  $T_2^R$ , and (c)  $T_2^E$  of the four-lowest excited states involving the two qubits Q1 and Q2 and two coupler modes P and M as a function of the flux bias through the coupler loop. Stability of the coherence times for (d) Q1 and (e) Q2 biased at the idle bias point for 17.5 h.

TABLE III. Dressed qubit coherence at the idle bias point.

| Coherence (µs) | $T_1$            | $T_2^{\rm R}$    | $T_2^{\mathrm{E}}$ |
|----------------|------------------|------------------|--------------------|
| Q1             | $228.6 \pm 30.4$ | $132.4 \pm 59.9$ | $358.9 \pm 47$     |
| Q2             | $205.3 \pm 26.0$ | $62.4 \pm 6.1$   | $129.8 \pm 13.3$   |

hybridized. For simplicity, however, in Fig. 9, we keep the labels of the dominant modes at the idle bias point. The colors in the plot correspond to the spectra in Fig. 1(d). The signal for  $T_1$  measurement is fitted with an exponential decay:  $P_{|1\rangle} = A + Be^{-t/T_1}$ , while for the signal decay envelope of  $T_2^{\rm R}$  and  $T_2^{\rm E}$  measurement, a fitting function of  $P_{|1\rangle} = A + Be^{-(t/T_2)^n}$  is used with n as a fitting parameter. Near the idle bias point (0.275  $< \varphi_{\rm ex}/2\pi < 0.325$ ),  $T_1$ of the coupler modes are lower than that of the qubits. This is due to the fact that the coupler modes have higher frequencies and are more sensitive to the dielectric loss because of the geometry [81]. In the strong-coupling regime  $(0.325 < \varphi_{\rm ex}/2\pi < 0.5)$ , the states of the four transmons become more hybridized, resulting in a decrease in  $T_1$  for the qubits and an increase in  $T_1$  for the coupler modes. The variation of both  $T_2^R$  and  $T_2^E$  mainly depends on the sensitivity of each dressed qubit to flux noise.

At the idle bias point, the stability of the coherence time are measured for qubits [Figs. 9(d) and 9(e)], and the averaged values are summarized in Table III. Both Q1 and Q2 demonstrate  $T_1 > 200 \,\mu\text{s}$ , a testament to the favorable impact of fabrication and geometrical design in mitigating dielectric noise. The energy level of Q1, which is far detuned from the coupler modes, is only marginally repelled by the coupler modes at the idle bias point. As a result, the  $T_2^R$  and  $T_2^E$  of Q1 are longer than the corresponding coherence time of Q2, owing to Q1's lower sensitivity to flux noise at the idle bias point. Possibly attributed to the thermal photon fluctuations in the resonator that dominate the lowfrequency noise, Q1 exhibits  $T_2^{\rm E}/T_1 \approx 1.57$ , slightly less than 2 [80]. In the meantime, for Q2, although not significantly, both  $T_2^{\rm R}$  and  $T_2^{\rm E}$  are further decreased due to the larger sensitivity to the flux noise, stemming from the nonnegligible repulsion caused by the coupler modes.

#### <span id="page-14-0"></span>APPENDIX F: STATE DISCRIMINATION

Accurate state discrimination with high fidelity is crucial for quantum error correction processes, notably in applications like the readout of the ancillary qubits in surface-code implementations [72]. Though the SPAM error associated with readout fidelity does not impede our characterization of the CZ-gate fidelity, an enhanced readout fidelity is beneficial for improving the experimental efficiency. In this work, the single-shot readout is performed at the idle bias point, where two qubits are nearly decoupled and far detuned from the coupler modes. Therefore, we denote the qubit state with  $|Qi\rangle$  as it

approximates the diabatic (bare) state, which is the eigenstate of the fully decoupled system [22]. While the two coupler modes, the p and m modes, are also approximated to be decoupled at the idle bias point, we denote their states with  $|P,M\rangle$  for simplicity.

We independently prepare the qubit states of  $|0\rangle$ ,  $|1\rangle$ , and  $|2\rangle$ , followed by single-shot measurements of the corresponding resonators for Q1 and Q2 [Figs. 10(a) and 10(b)]. In the case of the coupler modes P and M, only the first excited state is taken into account, assuming that the transition to the second excited state can be deemed negligible during both single-qubit and CZ-gate implementations. Because of the shared resonator and unoptimized resonator parameters, only the ground states  $|00\rangle$  can be distinguished from the other excited states  $|xx\rangle$  ( $|10\rangle$ ,  $|01\rangle$ , and  $|11\rangle$ ) [Fig. 10(c)]. We note that this is sufficient for leakage-error characterization, given that the computational subspace ( $\{|0000\rangle, |1000\rangle, |0100\rangle, |1100\rangle\}$ ) comprises only the ground state of the coupler modes.

Subsequently, unsupervised learning through k-means clustering is employed for the state discrimination of the qubits and coupler modes. After training the k means with the single-shot results, we calculate the assignment probability matrix (Table IV). The lower fidelity associated with higher energy levels for all qubits is attributed to incoherent errors. It is worth mentioning that a higher fidelity could potentially be achieved with a faster readout by meticulously designing the resonators and optimizing the readout pulse shape [82].

# APPENDIX G: SINGLE-QUBIT GATE FIDELITIES

<span id="page-14-1"></span>At the idle bias point, the residual ZZ interaction persists at  $2\pi \times (-6.3)$  kHz. To verify that it does not impact the current single-qubit gate fidelities, we compare the fidelities measured using randomized benchmarking (RB) for both individual and simultaneous executions (Fig. 11). In the individual case, we conduct single-qubit randomized benchmarking for Q1 (Q2) while maintaining Q2 (Q1) in its ground state. Subsequently, we perform simultaneous randomized benchmarking to unveil the additional error resulting from the residual ZZ interaction. Throughout the benchmarking process, the single-qubit gates, with a duration of 48 ns for both Q1 and Q2, are repeatedly calibrated using the DRAG method. This is crucial to mitigate control errors that may arise from the device instability, particularly due to the temperature drift.

We fit the sequence fidelity [Figs. 11(b) and 11(c)] with the exponential equation

$$P_{|0\rangle} = Ap^m + B,\tag{G1}$$

where m denotes the number of randomly selected Clifford gates. The average single Clifford gate error is calculated as

![](_page_15_Figure_2.jpeg)

FIG. 10. Single-shot readouts of the three resonators for the state discrimination of (a) Q1, (b) Q2, and (c) coupler modes P and M. Each point in the *I-Q* plane represents one demodulation result obtained from the SHFQC device. The cross markers represent the mean value for the corresponding states. In (a) and (b), each input state in the legend is prepared and measured 5000 times, while in (c) 3000 times.

TABLE IV. Qubit assignment probability matrix. P(m|n) represents the probability of reading out the  $|m\rangle$  state given the prepared state  $|n\rangle$ .  $|xx\rangle$  includes all the excited states of the coupler modes  $|P, M\rangle$ .

|                          |              | Pi           | repared state | n           |
|--------------------------|--------------|--------------|---------------|-------------|
| $\overline{Q1 \ P(m n)}$ |              | $ 0\rangle$  | 1>            | 2>          |
| Readout state m          | $ 0\rangle$  | 0.9933       | 0.0006        | 0.0061      |
|                          | $ 1\rangle$  | 0.0121       | 0.9787        | 0.0092      |
|                          | $ 2\rangle$  | 0.0060       | 0.0257        | 0.9683      |
| Q2 $P(m n)$              |              | $ 0\rangle$  | $ 1\rangle$   | $ 2\rangle$ |
| Readout state m          | $ 0\rangle$  | 0.9973       | 0.0017        | 0.0010      |
|                          | $ 1\rangle$  | 0.0231       | 0.9704        | 0.0065      |
|                          | $ 2\rangle$  | 0.0196       | 0.0398        | 0.9406      |
| Couplers $P(m n)$        |              | $ 00\rangle$ | $ xx\rangle$  |             |
| Readout state m          | $ 00\rangle$ | 0.9871       | 0.0129        |             |
|                          | $ xx\rangle$ | 0.0622       | 0.9378        |             |

$$r = (1 - p)(1 - 1/d),$$
 (G2)

where d=2 is the dimension of the Hilbert space for single-qubit measurement. Given the average number (1.875) of physical gates per one Clifford gate calculated from its decomposition [60,83], the single-qubit gate error  $r_{\rm SQ}$  equals to r/1.875. The high single-qubit gate fidelities for both Q1 and Q2 can be attributed to their high coherence at the idle bias point. Comparing the individual and simultaneous gate fidelities for either Q1 or Q2, the nearly identical gate errors suggest that the ZZ interaction of  $2\pi \times (-6.3)$  kHz is not the current limiting factor for single-qubit gate fidelity. The even higher fidelity for Q2 in the simultaneous measurement compared to the individual case could be attributed to variation of the coherence time.

![](_page_16_Figure_2.jpeg)

FIG. 11. (a) Randomized-benchmarking sequence for single-qubit gates for Q1 (left), Q2 (middle), and simultaneous ones (right).  $C_1^{(k)}$  (k=1,...,m) represents the randomly selected Clifford gates for a single qubit, applied m times in one sequence.  $C_1^{\rm T}$  is the recovery gate that renders the entire sequence equivalent to an identity gate. The measurement (M) reads out the  $|0\rangle$  state with the probability  $P_{|0\rangle}$ , which serves as the sequence fidelity. (b),(c) Results of the individual and simultaneous randomized benchmarking for Q1 and Q2, respectively. The data points are fitted with exponential curves, with the error bar representing the standard deviation of the sequence fidelities measured from ten randomly selected sequences shown in (a). Errors  $r_{\rm ind}$  and  $r_{\rm sim}$  measured individually and simultaneously, presented in (b) and (c), respectively, are the single-qubit gate errors calculated from the fitting results.

With the coherence measurement at the idle bias point (see Appendix E), the estimation for the single-qubit-gate incoherent error  $(r_{SO}^{incoherent})$  is given by [20,84]

$$r_{\text{SQ}}^{\text{incoherent}} = \frac{t_{\text{gate}}}{3} \left( \frac{1}{T_1} + \frac{1}{T_{\phi}} \right),$$
 (G3)

where  $t_{\rm gate}=48$  ns represents the single-qubit-gate duration used in our case.  $T_1$  is directly measured, while  $T_\phi$  is estimated as  $1/T_\phi=1/T_2^{\rm E}-1/2T_1$ . The influence originating from flux noise is considered negligible, given the long  $T_2^{\rm R}$ . This is attributed to the fact that the two qubits are less sensitive to flux variations in the vicinity of the system idle bias point. The errors introduced by  $T_1$  and  $T_\phi$  for Q1 are  $7.0\times10^{-5}$  and  $6\times10^{-6}$ , respectively. Therefore, the incoherent error contributes only approximately 50% to the total gate error. We posit that the residual error arises from coherent errors attributed to the instability of the control pulse. This rationale underscores our repeated implementation of single-qubit gate calibration during both single-and two-qubit gate randomized benchmarking. For Q2,

the errors introduced by  $T_1$  and  $T_\phi$  are  $7.8 \times 10^{-5}$  and  $8.3 \times 10^{-5}$ , respectively. While the total incoherent error constitutes more than 85% of the total gate error, we believe that the larger error induced by  $T_\phi$  may be overestimated due to its estimation influenced by the flux noise.

# <span id="page-16-0"></span>APPENDIX H: Z-PULSE DISTORTION CALIBRATION

We follow and extend the idea for correcting the *Z*-pulse distortion, as detailed in Ref. [22]. A perfectly square-shaped *Z* pulse ideally ceases when it is completed. However, due to distortion, its lasting influence persists even after it finished [56]. Consequently, the turn-off transients of a square-shaped *Z* pulse with a fixed amplitude and duration are measured to calibrate the flux-transient parameters for predistortion.

A tunable qubit, whose frequency is sensitive to the applied flux through the fast flux line, is typically employed as a sensor for capturing the step response. Normally, the coupler is utilized because its frequency can be directly tuned by the applied Z pulse. However, in the DTC scheme, the qubit Q2 could also be employed. This is due to its frequency being significantly repelled by the coupler energy level in the range of  $0.375 < \varphi_{\rm ex}/2\pi < 0.45$ , which demonstrates an indirect susceptibility to the applied flux. This alternative choice makes it possible to perform distortion calibration without the need for the readout resonator for coupler transmons.

The transients of the Z pulse can be characterized using a Ramsey-type experiment [Fig. 12(a)]. Typically, a  $\pi/2$ 

![](_page_16_Figure_12.jpeg)

FIG. 12. (a) Sequence for measuring the short-term distortion of a Z pulse. A square-shaped Z pulse of 48 ns is applied between a Ramsey-like sequence with varying the duration t after the Z pulse. "Tomo" stands for a single-qubit gate for quantum phase tomography. (b) Sequence for measuring the long-term distortion. A square-shaped Z pulse of 10  $\mu$ s is first applied on Q2. Following the variation of a duration t, a Ramsey-like sequence with a fixed interrogation time (approximately 500 ns) and phase tomography is employed to discern the enduring impact of the Z pulse. (c),(d) Extracted phase accumulations due to distortion with correction (orange circles) and without correction (blue circles) for (c) short- and (d) long-term cases, respectively.

TABLE V. Flux-transient parameters for pulse distortion calibrated either by short-term or long-term measurement.

| Short-term calibrated |           | Long-ter | Long-term calibrated |  |  |
|-----------------------|-----------|----------|----------------------|--|--|
| $\tau$ (ns)           | Amplitude | τ (μs)   | Amplitude            |  |  |
| 603.3                 | -0.0104   | 400.5    | 0.12                 |  |  |
| 79.45                 | -0.0137   | 71.02    | 0.038                |  |  |
|                       |           | 13.60    | 0.00525              |  |  |

pulse is applied in the beginning to create a superposition state  $(|0\rangle + |1\rangle)/\sqrt{2}$  of Q2. The turn-off transients of the Z pulse accumulate a relative phase on the state of Q2,  $(|0\rangle + e^{i\phi(t)}|1\rangle)/\sqrt{2}$ , where the  $\phi(t)$  is finally measured by state tomography. With the step response described by multiple exponential combination, the  $\phi(t)$  can be expressed as

$$\phi(t) = \phi_0 \sum_{k} a_k \left( e^{-(t/\tau_k)} - e^{-(t+\tau_{\text{pulse}})/\tau_k)} \right), \quad \text{(H1)}$$

where  $\phi_0$  is a constant and  $\tau_{\text{pulse}}$  is the duration of the Z pulse. The parameters  $a_k$  and  $\tau_k$  are the flux-transient parameters fitted from the measured phase and used for predistortion.

First, we maintain the external flux bias at  $\varphi_{\rm ex}/2\pi \approx 0.42$ using the superconducting coil. A pulse sequence, as illustrated in Fig. 12(a), is employed to measure the short-term transients of the Z pulse, where the duration t is constrained by qubit decoherence. Because of the larger flux sensitivity of Q2 at this point,  $T_2^R$  is only approximately 3 µs. Therefore, for long-term distortion, especially those exceeding the coherence time of the qubit, a sequence depicted in Fig. 12(b) can be employed. To avoid passing through the anticrossing with the applied Z pulse in sequence (a), a smaller amplitude of the Z pulse is chosen. Although the accumulated phase  $\phi(t)$  is relatively small, it is sufficient for the short-term transient calibration. In sequence (b), the amplitude of the Z pulse can be larger, as all the qubits are at their ground states before the end of the Z pulse. To increase the accumulated phase  $\phi(t)$  for a better signal-to-noise ratio (SNR), the duration of the Z pulse is chosen to be relatively longer for long-term transient measurement. Figures 12(c) and 12(d) display the phases measured with or without Z-pulse corrections for short- and long-term transients, respectively. The fluxtransient parameters (Table V) are calibrated and utilized for the predistortion during the CZ-gate implementation.

# <span id="page-17-0"></span>APPENDIX I: CZ-GATE OPTIMIZATION BY REINFORCEMENT-LEARNING ALGORITHM

To achieve an optimal CZ gate, we employ a model-free optimization process driven by the RL algorithm. In particular, we employ the code adapted from Ref. [85],

utilizing the well-known proximal-policy-optimization (PPO) algorithm [86] as the agent. The agent is trained to provide the pulse shape of the CZ gate, autonomously learning to optimize it through feedback in the form of rewards. We deploy this agent on the same computer for the experiment without utilizing a GPU, typically completing the training process in about 2 h. We note that the primary

![](_page_17_Figure_11.jpeg)

FIG. 13. (a) JAZZ-N pulse sequence for the amplitude calibration of the Z pulse in a Slepian shape, where the repetition N = 4k + 1 with integer k. The fidelity of the sequence is assessed based on the population of Q2,  $P_{|1\rangle}$ . (b) JAZZ2-N pulse sequence for the Z-pulse shape calibration and optimization, where the repetition N = 2k with integer k. The fidelity of the sequence, assessed through  $P_{|00\rangle}$ , serves as the reward for the RL algorithm. (c) Measurement results according to the JAZZ-N sequence, as depicted in (a), aiming to finely tune the amplitude of the Slepian pulse. (d) Sequence fidelity evaluated, utilizing the JAZZ2-N sequence (N = 18) illustrated in (b), along the training epochs of the RL algorithm. The red line illustrates the average fidelities, while the blue lines represent error bars, each calculated from 20 trial shapes generated by the agents following the policy prescribed by the RL algorithm. (e) Representative instance showcasing the Slepian pulse shape (blue circles) as the initial shape for the RL algorithm, alongside the optimized pulse shape (red circles). The connecting lines illustrate the cubic spline interpolations. (f) Difference calculated from the interpolation results depicted in (e). (g) FFT amplitude of the shape difference depicted in (f).

time consumption is associated with waveform uploading into the device and policy updates in the agent.

As shown in Fig. 4(a), a CZ gate is decomposed into three gates, showcasing a Z pulse injected into the DTC's loop to determine the CZ phase, accompanied by two VZ gates applied to the respective qubits to compensate for the single-qubit rotation. The VZ-gate phase is highly sensitive to the shape of the Z pulse, attributed to the significant repulsion in the energy levels of the qubits from those of the coupler modes. Therefore, a joint optimization of the CZ and VZ phases becomes extremely difficult in the DTC scheme. Instead, we divide the optimization process into two steps. Initially, we optimize the Z-pulse shape to achieve a CZ phase of  $\pi$ , following the sequence advanced by the JAZZ method, without the requirement for applying the VZ gates. Subsequently, the optimization focuses on the VZ-gate phases while keeping the Z pulse optimized and held constant. In each optimization step, the relevant parameters are initially calibrated through a physics-based process. Following that, the calibrated parameters serve as the initial values for the subsequent RL algorithm. Upon completion, the optimized CZ gate is employed in the quantum process tomography and gate-fidelity characterization by the IRB experiment.

## 1. CZ-phase optimization

The JAZZ-N sequence depicted in Fig. 13(a) functions as a physics-based process utilized for the calibration of the Z pulse for a CZ gate. Adapted from the JAZZ method, a repeated  $(\pi - Z)^N$  pattern is employed to enhance the sequence fidelity sensitivity to pulse amplitude. In this experiment, a Slepian shape [Fig. 13(e)] is initially calculated with a desired duration and unit amplitude. Subsequently, the amplitude of the Z pulse is systematically adjusted through scaling in the AWG device during the experiment. Without considering the decoherence, the evolution of the states of two qubits based on the JAZZ-N sequence can be interpreted as

$$|00\rangle \xrightarrow{IX_{\pi/2}} |0\rangle \frac{1}{\sqrt{2}} (|0\rangle - i|1\rangle) = \frac{1}{\sqrt{2}} (|00\rangle - i|01\rangle)$$

$$\xrightarrow{Z} \frac{1}{\sqrt{2}} (e^{i\theta_{00}} |00\rangle - ie^{i\theta_{01}} |01\rangle)$$

$$\xrightarrow{X_{\pi}X_{\pi}} \frac{1}{\sqrt{2}} (e^{i\theta_{00}} |11\rangle - ie^{i\theta_{01}} |10\rangle)$$

$$\xrightarrow{Z} \frac{1}{\sqrt{2}} (e^{i(\theta_{00} + \theta_{11})} |11\rangle - ie^{i(\theta_{01} + \theta_{10})} |10\rangle)$$

$$\xrightarrow{\text{remove an overall phase } e^{i(\theta_{01} + \theta_{10})}} \frac{1}{\sqrt{2}} (e^{i\theta_{\text{CZ}}} |11\rangle - i|10\rangle)$$

$$\xrightarrow{\text{accumulate phase with } (N-1)/2 = 2k \text{ more times }} \frac{1}{\sqrt{2}} |1\rangle (e^{i(2k+1)\theta_{\text{CZ}}} |1\rangle - i|0\rangle)$$

$$\xrightarrow{IX_{\pi/2}} \frac{1}{\sqrt{2}} |1\rangle (-i(1 + e^{i(2k+1)\theta_{\text{CZ}}}) |0\rangle - (1 - e^{i(2k+1)\theta_{\text{CZ}}}) |1\rangle)$$

$$\xrightarrow{\text{measurement of } Q^2} P_{|1\rangle} = \frac{1 - \cos((2k+1)\theta_{\text{CZ}})}{2}.$$
(II)

Hence, the sequence fidelity, defined as  $P_{|1\rangle}$  of Q2, is expressed as  $(1-\cos{((2k+1)\theta_{CZ})})/2$ . Note that the single-qubit rotation is automatically omitted, thereby decoupling the fidelity from the VZ gates. Considering instances where N=9,41,101 with corresponding values of k=2,10,25, the measurement of  $P_{|1\rangle}$  is conducted by adjusting the amplitude of the Z pulse, as depicted in Fig. 13(c). As the repetition count N increases, a more finely calibrated amplitude is obtained.

Figure 13(e) displays a fine-tuned Slepian shape with a duration of 48 ns, featuring 2 ns of zero padding at both the

beginning and end of the pulse. Its original shape with unit amplitude is calculated based on the method described in Ref. [55]. Specifically, we start from the control parameter  $\theta$  with the definition

$$\theta = \arctan\left(H_x/H_z\right),\tag{I2}$$

given a reduced two-state Hamiltonian

$$H = H_x \sigma_x + H_z \sigma_z = \begin{pmatrix} H_z & H_x \\ H_x & -H_z \end{pmatrix}. \tag{I3}$$

A smooth tuning of  $\theta(t)$  is optimized to form a CZ gate, striking a balance between speed and adiabaticity. By selecting the Slepian function S(t) to derive the optimal pulse shape, the desired evolution of  $\theta(t)$  can be described as

$$\frac{d\theta}{dt} = S(t). \tag{I4}$$

Therefore, the evolution of the  $H_z/H_x=1/\tan\theta(t)$  can be obtained with  $\theta(t)=\int S(t)dt$ . To relate  $\theta(t)$  to the applied external flux, specifically the voltage z(t) of the arbitrary waveform generated by the AWG, we approximate  $H_z/H_x\approx Cz^2(t)$ . The coefficient C can be any constant, as we intend to normalize the final pulse shape to begin and end at zero, with a unit peak value. Despite the approximation, we observe a commendable performance of the

generated Slepian shape in our experiment. Additionally, it functions solely as an initial pulse, and a superior shape will be optimized using the RL algorithm. We note that the initial pulse shape can take various forms, such as Gaussian or cosine shapes. These shapes merely introduce model bias, which does not impact the final performance of the optimized shape but influences only the efficiency of the optimization process.

To enhance the sequence sensitivity to the Z-pulse shape and increase robustness to single-qubit gate errors, we employ the sequence, denoted as JAZZ2-N sequence and depicted in Fig. 13(b), to generate the sequence fidelity as the reward for the PPO agent. Similar to the previous sequence, the evolution of the two-qubit states based on JAZZ2-N sequence could be derived as

$$|00\rangle \xrightarrow{X_{\pi/2}X_{\pi/2}} \frac{1}{\sqrt{2}} (|0\rangle - i|1\rangle) \frac{1}{\sqrt{2}} (|0\rangle - i|1\rangle) = \frac{1}{2} (|00\rangle - i|01\rangle - i|10\rangle - |11\rangle)$$

$$\xrightarrow{Z} \frac{1}{2} (e^{i\theta_{00}} |00\rangle - ie^{i\theta_{01}} |01\rangle - ie^{i\theta_{10}} |10\rangle - e^{i\theta_{11}} |11\rangle)$$

$$\xrightarrow{X_{\pi}X_{\pi}} \frac{1}{2} (e^{i\theta_{00}} |11\rangle - ie^{i\theta_{01}} |10\rangle - ie^{i\theta_{10}} |01\rangle - e^{i\theta_{11}} |00\rangle)$$

$$\xrightarrow{Z} \frac{1}{2} (e^{i(\theta_{00} + \theta_{11})} |11\rangle - ie^{i(\theta_{01} + \theta_{10})} |10\rangle - ie^{i(\theta_{10} + \theta_{01})} |01\rangle - e^{i(\theta_{11} + \theta_{00})} |00\rangle)$$

$$\xrightarrow{\text{remove an overall phase } e^{i(\theta_{01} + \theta_{10})} \frac{1}{2} (e^{i\theta_{\text{CZ}}} |11\rangle - i|10\rangle - i|01\rangle - e^{i\theta_{\text{CZ}}} |00\rangle)$$

$$\xrightarrow{\text{accumulate phase with } N = 2k \text{ more times} \frac{1}{2} (e^{i(2k+1)\theta_{\text{CZ}}} |11\rangle - i|10\rangle - i|01\rangle - e^{i(2k+1)\theta_{\text{CZ}}} |00\rangle)$$

$$\xrightarrow{X_{\pi/2}X_{\pi/2}} \frac{1}{4} (e^{i(2k+1)\theta_{\text{CZ}}} (-|00\rangle - i|01\rangle - i|10\rangle + |11\rangle) + i(-i|00\rangle - |01\rangle + |10\rangle - i|11\rangle)$$

$$+ i(-i|00\rangle - |10\rangle + |01\rangle - i|11\rangle) - e^{i(2k+1)\theta_{\text{CZ}}} (|00\rangle - i|01\rangle - i|10\rangle - |11\rangle))$$

$$\xrightarrow{\text{amplitude of } |00\rangle} \frac{1}{4} (-e^{i(2k+1)\theta_{\text{CZ}}} + 1 + 1 - e^{(2k+1)\theta_{\text{CZ}}})$$

$$\xrightarrow{\text{measurement of Q1 and Q2}} P_{|00\rangle} = \frac{1 - \cos((2k+1)\theta_{\text{CZ}})}{2}.$$
(I5)

Therefore, the sequence fidelity, defined as  $P_{|00\rangle}$ , reaches unity when  $\theta_{\rm CZ} \longrightarrow \pi$ . Figure 13(d) illustrates the increasing fidelity as the training progresses. In each epoch, the PPO agent generates 20 waveforms based on the initial pulse and its policy. Initially, when the agent is not well trained, it generates nearly random pulse shapes with larger variations, leading to lower fidelities. After approximately 100 epochs of training, the agent produces all trial pulses that closely resemble the optimal one, resulting in high fidelity with smaller variations. At times, for a more refined optimization, we incrementally increase N and carry out the optimization process using the previously optimized pulse shape.

Figure 13(e) shows a representative example of a Slepian pulse along with its optimized shape. Throughout the

optimization process, the PPO agent generates 20 points for each pulse. When constructing the waveform using the AWG, a sampling rate of 2 GSa/s is employed, incorporating cubic interpolations of the aforementioned 20 points. We calculate the difference between the interpolated pulse shape [Fig. 13(f)] and analyze it in the frequency domain using fast Fourier transform (FFT) [Fig. 13(g)]. We observe that the agent is attempting to incorporate specific frequency components into the original pulse shape. This behavior implies a potential effort to compensate for the residual pulse distortion characterized by various short transient times with small amplitudes. Alternatively, this could be explained by the suppression of transitions in the high-energy levels around the anticrossings, forming an adiabatic process.

## 2. VZ-phase optimization

Once the Z pulse is calibrated, it is kept constant in the subsequent optimization for the two VZ gates. An initial physics-based calibration, illustrated in Fig. 14(a), is employed to independently measure the Z-pulse-induced phases (θ<sup>1</sup> and θ2) on Q1 and Q2, respectively. The Z pulse induces a relative phase θ<sup>1</sup>=<sup>2</sup>, which is iteratively repeated N times, between the superposition states created by the initial π=2 pulse. Subsequently, a state tomography is performed to extract the accumulated phase Nθ<sup>1</sup>=<sup>2</sup> from the qubit population measurements. Figure 14(c) displays typical measurement results, with a linear fitting applied to extract the value of θ<sup>1</sup>=<sup>2</sup>. We emphasize that an imprecise calibration of the qubit frequency introduces an additional phase, impeding the accurate calibration of the VZ gate. This issue can be addressed either by employing an echotype sequence (π=2-Z-π-I-Tomo) or through the calibration of the qubit frequency in advance. Besides, a slight imprecision in the VZ gates are acceptable based on the

![](_page_20_Figure_4.jpeg)

FIG. 14. (a) Ramsey-like pulse sequence designed for the VZphase calibration. When either Q1 or Q2 is measured, the other is held in the ground state. (b) Pulse sequence similar to the randomized benchmarking of the two-qubit Clifford gates. The sequence fidelity, evaluated using <sup>P</sup>j00i, serves as the reward in the optimization process driven by the RL algorithm. The pulse shape of the flux applied to the DTC's loop is preoptimized and held fixed during this measurement. (c) Separately measured single-qubit phases, respectively, accumulated on Q1 and Q2 in the sequence depicted in (a). The solid lines shows linear fittings of the corresponding data, which give the phase per cycle of 139.33° and −102.05° for Q1 and Q2, respectively. (d) Evaluation of the sequence fidelity, using the sequence depicted in (b), across the training epochs of the RL algorithm optimization for the VZ gates. The red line illustrates the average fidelities, while the blue lines represent error bars, each calculated from 20 trial VZ-gate pairs ([Q1, Q2]) generated by the agents.

current characterization, as the optimization process will be conducted to fine-tune and enhance its accuracy.

Utilizing the optimized Z pulse and initially calibrated VZ gates, we evaluate the sequence fidelity from the twoqubit randomized benchmarking [Fig. 14(b)] to further optimize the VZ gates. The Z pulse remains fixed during the optimization of the VZ gates, with the initially calibrated VZ gates serving as the initial values for the PPO agent. A typical optimized process is illustrated in Fig. 14(d), showcasing an increase in sequence fidelity as the agent undergoes its training. During each training epoch, the agent generates 20 pairs of VZ gates for Q1 and Q2. Subsequently, a set of five randomly selected Clifford-gate sequences, with <sup>m</sup> ¼ <sup>20</sup>, is employed for measurements. The average fidelity of the set is then obtained alongside each pair of the aforementioned VZ gates. As a result, the sequence fidelity exhibits a larger variation at the beginning of the training and then gradually stabilizes with smaller variations after 100 epochs. A larger value for m could be employed to finely tune the VZ gate. However, we observe that its accuracy is finally constrained by the readout fidelity. It is worth noting that further optimization of VZ gates through randomized benchmarking is crucial for minimizing the phase error and enhancing the CZ-gate fidelity.

In conclusion of this section, we independently optimize the Z pulse and VZ phases using the RL algorithm. The optimized CZ gate not only results in an adiabatic process that reduces the leakage error, but also diminishes the phase error. In addition to achieving high CZ-gate fidelity, it is crucial to emphasize training efficiency, especially in the context of scalability. Additional efforts should be devoted to a more rational design of the PPO agent to expedite convergence. Furthermore, an advanced setup with GPU acceleration is desirable to speed up calculations.

# APPENDIX J: QUANTUM PROCESS TOMOGRAPHY

<span id="page-20-0"></span>Quantum process tomography (QPT) is employed to assess the performance of a quantum gate. However, the fidelity estimated from QPT tends to be underestimated due to the presence of SPAM errors, especially given the current high gate performance. While a pure gate fidelity can be measured through the randomized benchmarking experiment, QPT demonstrates its advantage in constructing a more intuitive matrix representation of a quantum operator. We employ a Pauli transfer matrix (PTM) R [\[87\]](#page-29-0) to represent the quantum process of our optimized CZ gate. The PTM contains only real numbers within the range ½−1; <sup>1</sup> as its matrix elements, allowing for an intuitive representation as a 2D map. In addition, the trace preservation of a quantum map can be succinctly demonstrated as <sup>ð</sup>RÞ<sup>0</sup><sup>j</sup> <sup>¼</sup> <sup>δ</sup><sup>0</sup>j, representing physical processes that do not cause information leakage.

![](_page_21_Figure_2.jpeg)

FIG. 15. Quantum process tomography. (a) Ideal CZ-gate PTM  $\mathcal{R}_{CZ}^{ideal}$ . (b) Reconstructed CZ-gate PTM  $\mathcal{R}_{CZ}^{exp}$ . (c) Difference between the reconstructed and ideal CZ-gate PTMs,  $\mathcal{R}_{CZ}^{exp} - \mathcal{R}_{CZ}^{ideal}$ .

By using the QPT, a PTM  $\mathcal{R}_{CZ}$  of the CZ gate can be compiled over an overcomplete measurement set [88]. The PTM of CZ gate can be represented as  $(\mathcal{R}_{CZ})_{ii}$  =  $\langle i|\mathcal{R}_{\text{CZ}}|j\rangle$ , where  $i \in \{0, 1, 2, ..., 15\}$  corresponding to the 16 Pauli basis  $\{I, X, Y, Z\}^{\otimes 2}$ . Given  $\vec{p}$  represents the vectorized state density matrix in the Pauli basis, the state evolution with a CZ gate applied can be described as  $\vec{p}_{\text{out}} = \mathcal{R}_{\text{CZ}} \vec{p}_{\text{in}}$ . Therefore, a series of state-tomography experiments can be performed to reconstruct the matrix elements of  $\mathcal{R}_{CZ}$ . Based on this idea, initial states projected on axes in  $\{X+, X-, Y+, Y-, Z+, Z-\}^{\otimes 2}$  are independently prepared by the gates in  $\{Y_{\pi/2}, -Y_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2}, -X_{\pi/2},$  $X_{\pi/2}, I, X_{\pi}\}^{\otimes 2}$ , resulting in a total of 36 initial states. After applying the CZ gate to each initial state, a projection measurement is performed on the  $\{X+, X-, Y+, Y-, Y-, Y-, Y-, Y-, Y-, Y-, Y-, Y-, Y Z+, Z-\}^{\otimes 2}$  axes, resulting in a total of  $36 \times 36$  measurement outcomes. For each initial state, a final-state density matrix is reconstructed through state tomography, utilizing the projection measurement results on the  $\{X+, X-, \}$ Y+, Y-, Z+, Z- $\}$  $\otimes 2$  axes. Subsequently, the density matrix is vectorized in the Pauli basis. The total of 36 final-state vectors, along with their initial states, are then employed to reconstruct the PTM using a maximumlikelihood algorithm [89,90].

Figure 15 shows a representative QPT result of our twoqubit gate. The close resemblance between the ideal and experimental PTM intuitively indicates that the processing gate is a CZ gate. The gate fidelity 0.959 calculated based on the QPT results is given by [88]

$$\overline{F} = \frac{\text{Tr}[\mathcal{R}_{\text{ideal}}^{\text{T}} \mathcal{R}] + d}{d(d+1)},$$
(J1)

where d=4 for the two-qubit system. The difference between the ideal PTM and the experimentally reconstructed one reveals that  $(\mathcal{R}_{\text{CZ}}^{\text{exp}})_{0j} = \delta_{0j}$ , corresponding to the trace-preserving assumption utilized in the maximum-likelihood algorithm. Although a leakage error exists in the

CZ gate, its comparatively smaller magnitude compared to the SPAM error is believed not to significantly alter the conclusions drawn from the QPT experiment.

## APPENDIX K: CZ-GATE FIDELITY

<span id="page-21-0"></span>It is known that the widely used RB protocol needs to be modified in the presence of leakage errors [71]. Here, we explain the LRB and the protocol used in this work.

The system with leakage errors is modeled using the computational subspace  $\mathcal{X}_1$  (the two-qubit subspace in the present case) and the leakage subspace  $\mathcal{X}_2$  (the total state space is  $\mathcal{X}_1 \oplus \mathcal{X}_2$ ), as shown in Fig. 16, where  $\rho_1$  denotes the  $\mathcal{X}_1$  submatrix of the density matrix. In addition to errors in the computational subspace  $\mathcal{X}_1$ , there are two kinds of errors: leakage errors (population transfer from  $\mathcal{X}_1$  to  $\mathcal{X}_2$ ) with rate  $L_1$  and seepage errors (population transfer from  $\mathcal{X}_2$  to  $\mathcal{X}_1$ ) with rate  $L_2$ .

<span id="page-21-1"></span>Errors per Clifford gate in LRB are modeled by the following evolution of the density matrix as a function of the number of randomly selected Clifford gates, m:

$$\begin{split} \rho_1(m+1) &= (1-L_1)\mathcal{E}_D[\rho_1(m)] \\ &+ L_2\{1-\text{Tr}[\rho_1(m)]\}\frac{I_1}{d}, \end{split} \tag{K1}$$

![](_page_21_Figure_14.jpeg)

FIG. 16. Leakage error model.

<span id="page-22-0"></span>where  $I_1$  and d = 4 are the identity matrix and dimension of  $\mathcal{X}_1$ , respectively.  $I_1/d$  describes the maximally mixed state for  $\mathcal{X}_1$ , and

$$\mathcal{E}_D(\rho_1) = (1 - p_D)\rho_1 + p_D \text{Tr}(\rho_1) \frac{I_1}{d}$$
 (K2)

describes the trace-preserving depolarizing error in  $\mathcal{X}_1$  with probability  $p_D$ . The isotropy of the error model comes from twirling over Clifford gates.

In LRB, we consider the following two survival probabilities: the probability of the ideal output state  $|\psi_{\rm id}\rangle$ ,  $P_{\rm id}=\langle\psi_{\rm id}|\rho_1|\psi_{\rm id}\rangle$ , and the probability to be in  $\mathcal{X}_1$ ,  $P_{\mathcal{X}_1}={\rm Tr}(\rho_1)$ . From Eqs. (K1) and (K2), we write their evolutions per Clifford gate as

<span id="page-22-3"></span>
$$P_{\mathcal{X}_1}(m+1) = (1 - L_1 - L_2)P_{\mathcal{X}_1}(m) + L_2, \tag{K3}$$

<span id="page-22-4"></span>
$$P_{id}(m+1) = (1 - L_1)(1 - p_D)P_{id}(m) + \frac{[(1 - L_1)p_D - L_2]P_{\chi_1}(m) + L_2}{d}.$$
 (K4)

<span id="page-22-2"></span>Using these relations recursively, we obtain the survival probabilities after m Clifford gates followed by its ideal inversion as follows:

$$P_{\mathcal{X}_1}(m) = A + B\lambda_L^m,\tag{K5}$$

$$P_{\rm id}(m) - \frac{P_{\mathcal{X}_1}(m)}{d} = C\lambda_r^m, \tag{K6}$$

<span id="page-22-1"></span>where

$$\lambda_L = 1 - L_1 - L_2, (K7)$$

$$A = \frac{L_2}{L_1 + L_2},$$
 (K8)

$$B = P_{\mathcal{X}_1}(0) - A,\tag{K9}$$

$$\lambda_r = (1 - L_1)(1 - p_D),$$
 (K10)

$$C = P_{id}(0) - \frac{P_{\chi_1}(0)}{d}.$$
 (K11)

It is remarkable that the left-hand side of Eq. (K6) can be expressed by a single exponential decay without a constant term. Also note that the state preparation errors  $P_{id}(0)$  and  $P_{\mathcal{X}_1}(0)$  are included only in B and C, and, therefore, we can estimate the error-model parameters separately from the state preparation errors.

Finally, we consider the errors in the inversion of m Clifford gates and the measurement. If they were also isotropic and described similarly to Eqs. (K1) and (K2), the results could still be fitted to Eqs. (K5) and (K6) following

the relations in Eqs. (K3) and (K4). In RB, however, we set the initial and final states to the ground state  $|\widetilde{0000}\rangle$ , leading to biased (anisotropic) errors. We model the experimentally measured probabilities  $P_{X_1}^M(m)$  and  $P_{\mathrm{id}}^M(m)$  with the biased errors as follows:

$$P_{\mathcal{X}_1}^M(m) = P_{\mathcal{X}_1}(m) + L_{20}[1 - P_{\mathcal{X}_1}(m)], \tag{K12}$$

$$\begin{split} P_{\rm id}^{M}(m) &= P_{\rm id}(m) + L_{20}[1 - P_{\mathcal{X}_{1}}(m)] \\ &+ \gamma [P_{\mathcal{X}_{1}}(m) - P_{\rm id}(m)], \end{split} \tag{K13}$$

where  $L_{20}$  and  $\gamma$  are the rates of the population transfers from the leakage subspace  $\mathcal{X}_2$  and the subspace of  $\mathcal{X}_1$  orthogonal to  $|\widetilde{0000}\rangle$ , respectively, to  $|\widetilde{0000}\rangle$ . Note that isotropic errors have already been included in  $P_{\mathcal{X}_1}(m)$  and  $P_{\mathrm{id}}(m)$ .

<span id="page-22-6"></span>We, thus, obtain

$$P_{\mathcal{X}_1}^M(m) = A_M + B_M \lambda_L^m, \tag{K14}$$

<span id="page-22-5"></span>
$$P_{\mathrm{id}}^{M}(m) - \frac{P_{\mathcal{X}_{1}}^{M}(m)}{d} = C_{M}\lambda_{r}^{m} + D_{M}, \tag{K15}$$

where

$$A_M = (1 - L_{20})A + L_{20} \simeq \frac{L_2}{L_1 + L_2},$$
 (K16)

$$B_M = (1 - L_{20})B, (K17)$$

$$C_M = (1 - \gamma)C,\tag{K18}$$

$$\begin{split} D_{M} &= \frac{d-1}{d} \left[ (\gamma - L_{20}) P_{\mathcal{X}_{1}}(m) + L_{20} \right] \\ &\simeq \frac{d-1}{d} \left[ (\gamma - L_{20}) \bar{P}_{\mathcal{X}_{1}} + L_{20} \right], \end{split} \tag{K19}$$

where  $\bar{P}_{\mathcal{X}_1}$  is the average value of  $P_{\mathcal{X}_1}(m)$  with respect to m. This approximation, which allows us to regard  $D_M$  as a constant and consequently avoid unreliable fitting with double exponential decays, is valid because the dropped term  $[(d-1)/d](\gamma-L_{20})[P_{\mathcal{X}_1}(m)-\bar{P}_{\mathcal{X}_1}]$  is small compared to the main term  $C_M\lambda_r^m$  for the estimation of  $\lambda_r$  with Eq. (K15). Note that  $|\gamma-L_{20}|\ll 1$  and  $|P_{\mathcal{X}_1}(m)-\bar{P}_{\mathcal{X}_1}|\simeq |P_{\mathcal{X}_1}^M(m)-\bar{P}_{\mathcal{X}_1}^M|$  is about one order of magnitude smaller than  $\bar{P}_{\mathcal{X}_1}\simeq\bar{P}_{\mathcal{X}_1}^M$  [see Fig. 4(b)].

The LRB protocol used in this work is as follows. In the SRB part, we determine  $\lambda_L^{\text{SRB}}$ ,  $\lambda_r^{\text{SRB}}$ ,  $A_M^{\text{SRB}}$ ,  $B_M^{\text{SRB}}$ ,  $C_M^{\text{SRB}}$ , and  $D_M^{\text{SRB}}$  by fitting to the experimental data of  $P_{\chi_1}^{M,\text{SRB}}(m)$  and  $P_{\text{id}}^{M,\text{SRB}}(m) - P_{\chi_1}^{M,\text{SRB}}(m)/d$  according to Eqs. (K14) and (K15). The leakage and seepage rates are obtained as

$$L_1^{\text{SRB}} = (1 - \lambda_L^{\text{SRB}})(1 - A_M^{\text{SRB}}),$$
 (K20)

$$L_2^{\text{SRB}} = (1 - \lambda_I^{\text{SRB}}) A_M^{\text{SRB}}.$$
 (K21)

In the IRB part, we similarly obtain  $\lambda_L^{\rm IRB}$ ,  $\lambda_r^{\rm IRB}$ ,  $L_1^{\rm IRB}$ , and  $L_2^{\rm IRB}$  by fitting to the experimental data of  $P_{\chi_1}^{M,\rm IRB}(m)$  and  $P_{\rm id}^{M,\rm IRB}(m) - P_{\chi_1}^{M,\rm IRB}(m)/d$ . Assuming the CZ-gate error model similar to Eqs. (K1) and (K2), parameters for the CZ gate are determined as

<span id="page-23-2"></span><span id="page-23-1"></span>
$$1 - L_1^{\rm CZ} = \frac{1 - L_1^{\rm IRB}}{1 - L_1^{\rm SRB}},\tag{K22}$$

$$\lambda_r^{\text{CZ}} = (1 - L_1^{\text{CZ}})(1 - p_D^{\text{CZ}}) = \frac{\lambda_r^{\text{IRB}}}{\lambda_r^{\text{SRB}}}.$$
 (K23)

Finally, the average fidelity of the CZ gate is give by

$$\begin{split} \bar{F} &= (1 - L_1^{\text{CZ}}) \bigg( 1 - p_D^{\text{CZ}} + \frac{p_D^{\text{CZ}}}{d} \bigg) \\ &= \frac{d-1}{d} \lambda_r^{\text{CZ}} + \frac{1 - L_1^{\text{CZ}}}{d}, \end{split} \tag{K24}$$

which can be calculated with the experimentally determined values from Eqs. (K22) and (K23).

The average fidelity is approximately expressed as

$$\bar{F} \simeq 1 - \frac{d-1}{d} p_D^{CZ} - L_1^{CZ}.$$
 (K25)

That is, the infidelity is given by the sum of the depolarizing-induced error  $r_D^{\rm CZ} \equiv (d-1) p_D^{\rm CZ}/d$  in the computational subspace and the leakage error  $L_1^{\rm CZ}$ . It is also notable that the average fidelity can be expressed as

$$\bar{F} = 1 - \frac{d-1}{d} (1 - \lambda_r^{CZ}) - \frac{L_1^{CZ}}{d}.$$
 (K26)

Since the decay rate  $\lambda_r^{CZ}$  roughly corresponds to that estimated in the widely used RB neglecting leakage errors, the LRB gives the fidelity lower by  $L_1^{CZ}/d$  than such RB.

## APPENDIX L: INCOHERENT ERROR

<span id="page-23-0"></span>While the coherent error of a qubit gate can be minimized through the optimization of control pulses, incoherent errors stemming from various noise sources pose a challenge, as they are difficult to mitigate during measurement procedures. The decoherence of a qubit is typically intricate, such as qubit relaxation induced by charge noise [80], quasiparticles [91], and two-level systems [92]. Identifying these distinct noise sources is crucial for enhancing qubit coherence and reducing incoherent errors. However, delving into this complexity is beyond the scope of this work. Instead, we partition the impact of distinct

decoherence channels, consisting of relaxation and pure dephasing, to facilitate our error analysis.

We start from the 1/f flux noise, which is easily estimated experimentally [93]. Furthermore, its induced incoherent error can be simulated using a Monte Carlo method [22]. The error induced by flux noise can be deemed negligible, as demonstrated below, which simplifies the subsequent analysis. We note that various sources of 1/f-type noise, including charge noise, contribute to qubit dephasing. However, in a tunable scheme involving transmons, the dominant source is reasonably considered to be flux noise, induced by the fluctuation of the magnetic field in the DTC's loop. Subsequently, an error channel  $\mathcal{E}$ described by Kraus operators is employed to estimate the incoherent error induced by qubit energy relaxation and pure dephasing. Given a quantum error channel  $\mathcal{E}$  described by Kraus operators as (I denotes the identity operator and  $\rho$ denotes the state density)

$$\mathcal{E}(\rho) = \sum_{k} K_{k} \rho K_{k}^{\dagger}, \qquad \sum_{k} K_{k}^{\dagger} K_{k} = I, \qquad (L1)$$

the average fidelity for d-dimensional systems is given by [20,94]

$$F_{\text{ave}} = \frac{1}{d(d+1)} \sum_{k} \left[ \text{Tr}(K_k^{\dagger} K_k) + |\text{Tr}(K_k)|^2 \right], \quad \text{(L2)}$$

where d is 2 and 4, respectively, for single-qubit and two-qubit systems.

#### 1. Flux-noise-induced error

We reuse the data obtained in Appendix E for the flux-noise calculation. The measurement data for  $T_2^{\rm E}$  is reanalyzed using the formula  $P_{|1\rangle}=A+Be^{-\Gamma_{\rm exp}t-(\Gamma_\Phi^{\rm E}t)^2}$ , where  $\Gamma_{\rm exp}$  mainly accounts for the effects from  $T_1$  and white noise while  $\Gamma_\Phi^{\rm E}$  characterizes the impact of 1/f flux noise. With the frequency sensitivity of a qubit to the flux in the DTC loop, the decay rate induced by the 1/f flux noise is determined as [93]

$$\Gamma_{\Phi}^{\rm E} = \left(\frac{2\pi}{\Phi_0}\right) \sqrt{A_{\Phi} \ln 2} \left| \frac{\partial \omega}{\partial \varphi_{\rm ex}} \right|,\tag{L3}$$

where  $\sqrt{A_{\Phi}}$  is the amplitude of the flux-noise spectra  $S_{\Phi} = A_{\Phi}/|\omega|$ . By fitting  $\Gamma_{\Phi}^{\rm E}$  against its frequency sensitivity  $(\partial \omega/\partial \varphi_{\rm ex})$  for both Q1 and Q2 [Fig. 17(a)], the extracted flux-noise amplitudes are found to be  $\sqrt{A_{\Phi}} \sim 4.89~\mu\Phi_0$  and  $\sim 4.79~\mu\Phi_0$ , respectively. It is reasonable for the two qubits to exhibit similar flux noise, as their respective measured flux noise primarily originates from the shared DTC's loop.

Given the average 1/f flux-noise amplitude  $\sqrt{A_\phi} \sim 4.84~\mu\Phi_0$ , a Monte Carlo simulation can be conducted to

![](_page_24_Figure_2.jpeg)

FIG. 17. (a) Dephasing rate calculated from Hahn-echo measurements versus the flux sensitivity of the qubit frequency. Error bars are calculated from the fitting errors. The linear fits depicted by the red and blue solid lines are for Q1 and Q2, respectively. (b) Simulated CZ-gate error versus the CZ-gate length due to the 1/f flux noise.

capture the induced incoherent noise in the CZ gate implementation [22]. We initially designed an optimized pulse shape for the CZ gate theoretically for the simulation. Subsequently, we conducted 1000 simulations, where, in each iteration, an offset flux sampled from the measured flux-noise spectra was added to the optimized pulse. The induced error was calculated as  $(1 - F_{\text{sim}}^{\text{noise}}) - (1 - F_{\text{sim}}^{\text{ideal}})$ , where the  $F_{\rm sim}^{\rm ideal/noise}$  is the simulated gate fidelity [48] with and without sampled noise. The simulated CZ-gate errors contributed by the 1/f flux noise are obtained  $< 10^{-6}$  for the CZ-gate length within 40-320 ns [Fig. 17(b)], which can be considered negligible at the current stage. The simulation result aligns with the findings in Ref. [22], suggesting that the impact of long-time correlated flux noise is similarly negligible, particularly with the implementation of a short gate length in the DTC scheme.

#### 2. Relaxation-induced error

Denoting the amplitude damping as  $p_1 = 1 - e^{-t/T_1} \simeq t/T_1$ , with an operation time  $t \ll T_1$ , the Kraus operators describing the qubit relaxation of a two-qubit system are as follows [95]:

$$\begin{split} K_0^{(1)} &= \begin{pmatrix} 1 & 0 \\ 0 & \sqrt{1-p_1^{(1)}} \end{pmatrix} \otimes I \\ &= \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & \sqrt{1-p_1^{(1)}} & 0 \\ 0 & 0 & 0 & \sqrt{1-p_1^{(1)}} \end{pmatrix}, \quad \text{(L4)} \end{split}$$

$$K_{1}^{(1)} = \begin{pmatrix} 0 & \sqrt{p_{1}^{(1)}} \\ 0 & 0 \end{pmatrix} \otimes I$$

$$= \begin{pmatrix} 0 & 0 & \sqrt{p_{1}^{(1)}} & 0 \\ 0 & 0 & 0 & \sqrt{p_{1}^{(1)}} \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}, \quad (L5)$$

$$K_0^{(2)} = I \otimes \begin{pmatrix} 1 & 0 \\ 0 & \sqrt{1 - p_1^{(2)}} \end{pmatrix}$$

$$= \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & \sqrt{1 - p_1^{(2)}} & 0 \\ 0 & 0 & 0 & \sqrt{1 - p_1^{(2)}} \end{pmatrix}, \quad (L6)$$

$$K_{1}^{(2)} = I \otimes \begin{pmatrix} 0 & \sqrt{p_{1}^{(2)}} \\ 0 & 0 \end{pmatrix}$$

$$= \begin{pmatrix} 0 & \sqrt{p_{1}^{(2)}} & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & \sqrt{p_{1}^{(2)}} \\ 0 & 0 & 0 & 0 \end{pmatrix}, \tag{L7}$$

where  $K_k^{(q)}$  and  $p_1^{(q)}$  correspond to the qth qubit.

Using the above two-qubit Kraus operators and the formula in Eq. (L2), we obtain the average incoherent error due to relaxation of the qth qubit in the two-qubit systems:

$$1 - F_{\text{ave}}^{(q)} = 1 - \frac{3 - p_1^{(q)} + 2\sqrt{1 - p_1^{(q)}}}{5} \simeq \frac{2}{5} \frac{t}{T_1^{(q)}}.$$
 (L8)

## 3. Pure-dephasing-induced error

Since the flux noise is negligible as simulated above, we focus solely on the predominant contribution of pure dephasing from white noise. This contribution results in an exponential decay of the decoherence signal rather than a Gaussian profile. Therefore, with  $p_{\phi}=(1-e^{-t/T_{\phi}})/2 \simeq t/(2T_{\phi})$  denoting the phase-flip probability, the Kraus operators for pure dephasing of individual qubit in a two-qubit system are as follows [95]:

$$K_0^{(1)} = \sqrt{1 - p_{\phi}^{(1)}} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} \otimes I$$

$$= \sqrt{1 - p_{\phi}^{(1)}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}, \quad (L9)$$

$$K_{1}^{(1)} = \sqrt{p_{\phi}^{(1)}} \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \otimes I$$

$$= \sqrt{p_{\phi}^{(1)}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}, \quad (L10)$$

$$\begin{split} K_0^{(2)} &= I \otimes \sqrt{1 - p_{\phi}^{(2)}} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} \\ &= \sqrt{1 - p_{\phi}^{(2)}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}, \quad \text{(L11)} \end{split}$$

$$\begin{split} K_1^{(2)} &= I \otimes \sqrt{p_\phi^{(2)}} \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \\ &= \sqrt{p_\phi^{(2)}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}, \qquad \text{(L12)} \end{split}$$

where  $K_k^{(q)}$  and  $p_\phi^{(q)}$  correspond to the qth qubit.

Using the above two-qubit Kraus operators and the formula given in Eq. (L2), we obtain the following formula of the average infidelity for pure dephasing of the qth qubit in the two-qubit systems:

$$1 - F_{\text{ave}}^{(q)} = 1 - \frac{4p_{\phi}^{(q)}}{5} \simeq \frac{2}{5} \frac{t}{T_{\phi}^{(q)}}.$$
 (L13)

Note that this is in the same form as that for the amplitude damping in Eq. (L8).

In addition to the pure dephasing of individual qubits, we also consider the extra dephasing due to their coupling during the CZ gate, denoted as CZ dephasing. The Kraus operators for the two-qubit CZ dephasing are defined as follows:

$$K_{0} = \sqrt{1 - p_{\text{CZ}}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$
$$= \sqrt{1 - p_{\text{CZ}}} (I \otimes I), \tag{L14}$$

$$K_{1} = \sqrt{p_{\text{CZ}}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}$$
$$= \sqrt{p_{\text{CZ}}} \frac{I \otimes I + Z \otimes I + I \otimes Z - Z \otimes Z}{2}, \quad \text{(L15)}$$

where  $p_{\rm CZ} = (1 - e^{-t/T_{\rm CZ}})/2 \simeq t/(2T_{\rm CZ})$ .  $T_{\rm CZ}$  is the CZ dephasing time defined as  $\rho_{00,11} \to e^{-t/T_{\rm CZ}} \rho_{00,11}$ ,  $\rho_{10,11} \to e^{-t/T_{\rm CZ}} \rho_{10,11}$ , and  $\rho_{01,11} \to e^{-t/T_{\rm CZ}} \rho_{01,11}$ .

Using the above two-qubit Kraus operators and the formula given in Eq. (L2), we obtain the average infidelity for the CZ dephasing as follows:

$$1 - F_{\text{ave}} = \frac{3}{5} p_{\text{CZ}} \simeq \frac{3}{10} \frac{t}{T_{\text{CZ}}}.$$
 (L16)

## 4. Summary of incoherent error

Considering the aforementioned incoherent error analysis, the error induced by flux noise appears negligible given the current CZ-gate error level. Therefore, the incoherent error induced by relaxation and pure dephasing can be modeled as follows:

$$\begin{split} 1 - F_{\text{ave}} &\simeq \frac{2}{5} \frac{t}{T_{1}^{(1)}} + \frac{2}{5} \frac{t}{T_{1}^{(2)}} + \frac{2}{5} \frac{t}{T_{\phi}^{(1)}} + \frac{2}{5} \frac{t}{T_{\phi}^{(2)}} + \frac{3}{10} \frac{t}{T_{\text{CZ}}} \\ &\equiv \frac{2}{5} \frac{t}{T_{\text{eff}}}, \end{split} \tag{L17}$$

where  $T_{\rm eff}$  denotes the effective coherence time experienced by the two-qubit system.

Despite employing these error models, predicting the exact incoherent error of the CZ gate measured using randomized benchmarking still poses challenges.  $T_{\rm eff}^{\rm est} \approx 67.6 \pm 11.4~\mu {\rm s}$  estimated from  $T_1$  and  $T_\phi$  of two data qubits measured at the idle bias point is larger than the fitted value  $T_{\rm eff}^{\rm exp} \approx 23.9 \pm 1.5~\mu {\rm s}$  (Fig. 5), which suggests the presence of additional noise induced by the CZ gate. However, accurately extracting the coherence time during the CZ gate proves difficult, given the variability in the noise participation ratio during the gate operation. In particular, a thorough understanding and estimation are necessary to account for the additional contribution of CZ dephasing, which requires further investigation.

In conclusion of this section, we have developed a model to illuminate the potential reasons for the linear relationship between the incoherent gate error and gate length shown in Fig. 5. The incomplete explanation of Teff from the coherence measurement at the idle bias point necessitates further efforts in investigating decoherence during the CZ gate. Furthermore, identifying specific noise sources is crucial for guiding the mitigation of errors induced by these noise channels, which has already become a substantial subject in superconducting qubits and drawn significant attention in recent investigations.

- <span id="page-26-1"></span><span id="page-26-0"></span>[1] J. Preskill, Quantum computing in the NISQ era and beyond, Quantum 2[, 79 \(2018\).](https://doi.org/10.22331/q-2018-08-06-79)
- <span id="page-26-2"></span>[2] P. Shor, Fault-tolerant quantum computation, in Proceedings of 37th Conference on Foundations of Computer Science (IEEE, New York, 1996), pp. 56–65.
- <span id="page-26-15"></span>[3] Y. Nakamura, Y. A. Pashkin, and J. Tsai, Coherent control of macroscopic quantum states in a single-Cooper-pair box, [Nature \(London\)](https://doi.org/10.1038/19718) 398, 786 (1999).
- [4] F. Arute, K. Arya, R. Babbush, D. Bacon, J. C. Bardin, R. Barends, R. Biswas, S. Boixo, F. G. Brandao, D. A. Buell et al., Quantum supremacy using a programmable superconducting processor, [Nature \(London\)](https://doi.org/10.1038/s41586-019-1666-5) 574, 505 (2019).
- <span id="page-26-3"></span>[5] Y. Kim, A. Eddins, S. Anand, K. X. Wei, E. Van Den Berg, S. Rosenblatt, H. Nayfeh, Y. Wu, M. Zaletel, K. Temme et al., Evidence for the utility of quantum computing before fault tolerance, [Nature \(London\)](https://doi.org/10.1038/s41586-023-06096-3) 618, 500 (2023).
- <span id="page-26-5"></span><span id="page-26-4"></span>[6] J. I. Cirac and P. Zoller, Quantum computations with cold trapped ions, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.74.4091) 74, 4091 (1995).
- <span id="page-26-6"></span>[7] J. Benhelm, G. Kirchmair, C. F. Roos, and R. Blatt, Towards fault-tolerant quantum computing with trapped ions, [Nat.](https://doi.org/10.1038/nphys961) Phys. 4[, 463 \(2008\)](https://doi.org/10.1038/nphys961).
- <span id="page-26-7"></span>[8] A. Browaeys, D. Barredo, and T. Lahaye, Experimental investigations of dipole-dipole interactions between a few Rydberg atoms, J. Phys. B 49[, 152001 \(2016\).](https://doi.org/10.1088/0953-4075/49/15/152001)
- [9] D. Bluvstein, S. J. Evered, A. A. Geim, S. H. Li, H. Zhou, T. Manovitz, S. Ebadi, M. Cain, M. Kalinowski, D. Hangleiter et al., Logical quantum processor based on reconfigurable atom arrays, [Nature \(London\)](https://doi.org/10.1038/s41586-023-06927-3) 626, 58 (2024).
- <span id="page-26-8"></span>[10] H.-S. Zhong, H. Wang, Y.-H. Deng, M.-C. Chen, L.-C. Peng, Y.-H. Luo, J. Qin, D. Wu, X. Ding, Y. Hu et al., Quantum computational advantage using photons, [Science](https://doi.org/10.1126/science.abe8770) 370[, 1460 \(2020\)](https://doi.org/10.1126/science.abe8770).
- <span id="page-26-9"></span>[11] D. Loss and D. P. DiVincenzo, Quantum computation with quantum dots, [Phys. Rev. A](https://doi.org/10.1103/PhysRevA.57.120) 57, 120 (1998).
- [12] N. W. Hendrickx, W. I. Lawrie, M. Russ, F. van Riggelen, S. L. de Snoo, R. N. Schouten, A. Sammak, G. Scappucci, and M. Veldhorst, A four-qubit germanium quantum processor, [Nature \(London\)](https://doi.org/10.1038/s41586-021-03332-6) 591, 580 (2021).
- <span id="page-26-10"></span>[13] X. Rong, J. Geng, F. Shi, Y. Liu, K. Xu, W. Ma, F. Kong, Z. Jiang, Y. Wu, and J. Du, Experimental fault-tolerant universal quantum gates with solid-state spins under ambient conditions, [Nat. Commun.](https://doi.org/10.1038/ncomms9748) 6, 8748 (2015).
- <span id="page-26-11"></span>[14] J. P. Gaebler, T. R. Tan, Y. Lin, Y. Wan, R. Bowler, A. C. Keith, S. Glancy, K. Coakley, E. Knill, D. Leibfried, and

- D. J. Wineland, High-fidelity universal gate set for <sup>9</sup> Be<sup>þ</sup> ion qubits, Phys. Rev. Lett. 117[, 060505 \(2016\).](https://doi.org/10.1103/PhysRevLett.117.060505)
- [15] C. J. Ballance, T. P. Harty, N. M. Linke, M. A. Sepiol, and D. M. Lucas, High-fidelity quantum logic gates using trapped-ion hyperfine qubits, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.117.060504) 117, 060504 [\(2016\).](https://doi.org/10.1103/PhysRevLett.117.060504)
- [16] S. J. Evered, D. Bluvstein, M. Kalinowski, S. Ebadi, T. Manovitz, H. Zhou, S. H. Li, A. A. Geim, T. T. Wang, N. Maskara, H. Levine, G. Semeghini, M. Greiner, V. Vuletić, and M. D. Lukin, High-fidelity parallel entangling gates on a neutral-atom quantum computer, [Nature \(London\)](https://doi.org/10.1038/s41586-023-06481-y) 622, [268 \(2023\)](https://doi.org/10.1038/s41586-023-06481-y).
- [17] X. Xue, M. Russ, N. Samkharadze, B. Undseth, A. Sammak, G. Scappucci, and L. M. Vandersypen, Quantum logic with spin qubits crossing the surface code threshold, [Nature \(London\)](https://doi.org/10.1038/s41586-021-04273-w) 601, 343 (2022).
- [18] A. Noiri, K. Takeda, T. Nakajima, T. Kobayashi, A. Sammak, G. Scappucci, and S. Tarucha, Fast universal quantum gate above the fault-tolerance threshold in silicon, [Nature \(London\)](https://doi.org/10.1038/s41586-021-04182-y) 601, 338 (2022).
- <span id="page-26-12"></span>[19] T. Xie, Z. Zhao, S. Xu, X. Kong, Z. Yang, M. Wang, Y. Wang, F. Shi, and J. Du, 99.92%-fidelity CNOT gates in solids by noise filtering, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.130.030601) 130, 030601 [\(2023\).](https://doi.org/10.1103/PhysRevLett.130.030601)
- <span id="page-26-13"></span>[20] L. Ding, M. Hays, Y. Sung, B. Kannan, J. An, A. Di Paolo, A. H. Karamlou, T. M. Hazard, K. Azar, D. K. Kim, B. M. Niedzielski, A. Melville, M. E. Schwartz, J. L. Yoder, T. P. Orlando, S. Gustavsson, J. A. Grover, K. Serniak, and W. D. Oliver, High-fidelity, frequency-flexible two-qubit fluxonium gates with a transmon coupler, [Phys. Rev. X](https://doi.org/10.1103/PhysRevX.13.031035) 13, [031035 \(2023\).](https://doi.org/10.1103/PhysRevX.13.031035)
- <span id="page-26-19"></span>[21] J. Stehlik, D. M. Zajac, D. L. Underwood, T. Phung, J. Blair, S. Carnevale, D. Klaus, G. A. Keefe, A. Carniol, M. Kumph, M. Steffen, and O. E. Dial, Tunable coupling architecture for fixed-frequency transmon superconducting qubits, [Phys.](https://doi.org/10.1103/PhysRevLett.127.080505) Rev. Lett. 127[, 080505 \(2021\).](https://doi.org/10.1103/PhysRevLett.127.080505)
- <span id="page-26-18"></span>[22] Y. Sung, L. Ding, J. Braumüller, A. Vepsäläinen, B. Kannan, M. Kjaergaard, A. Greene, G. O. Samach, C. McNally, D. Kim, A. Melville, B. M. Niedzielski, M. E. Schwartz, J. L. Yoder, T. P. Orlando, S. Gustavsson, and W. D. Oliver, Realization of high-fidelity CZ and ZZ-free iSWAP gates with a tunable coupler, Phys. Rev. X 11[, 021058 \(2021\)](https://doi.org/10.1103/PhysRevX.11.021058).
- [23] V. Negîrneac, H. Ali, N. Muthusubramanian, F. Battistel, R. Sagastizabal, M. S. Moreira, J. F. Marques, W. J. Vlothuizen, M. Beekman, C. Zachariadis, N. Haider, A. Bruno, and L. DiCarlo, High-fidelity controlled-Z gate with maximal intermediate leakage operating at the speed limit in a superconducting quantum processor, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.126.220502) 126[, 220502 \(2021\).](https://doi.org/10.1103/PhysRevLett.126.220502)
- <span id="page-26-14"></span>[24] F. Marxer et al., Long-distance transmon coupler with CZ-gate fidelity above 99.8%, [PRX Quantum](https://doi.org/10.1103/PRXQuantum.4.010314) 4, 010314 [\(2023\).](https://doi.org/10.1103/PRXQuantum.4.010314)
- <span id="page-26-16"></span>[25] S. Krinner, S. Storz, P. Kurpiers, P. Magnard, J. Heinsoo, R. Keller, J. Luetolf, C. Eichler, and A. Wallraff, Engineering cryogenic setups for 100-qubit scale superconducting circuit systems, [Eur. Phys. J. Quantum Technol.](https://doi.org/10.1140/epjqt/s40507-019-0072-0) 6, [2 \(2019\).](https://doi.org/10.1140/epjqt/s40507-019-0072-0)
- <span id="page-26-17"></span>[26] A. Gold, J. Paquette, A. Stockklauser, M. J. Reagor, M. S. Alam, A. Bestwick, N. Didier, A. Nersisyan, F. Oruc, A. Razavi et al., Entanglement across separate silicon dies in a

- modular superconducting qubit device, [npj Quantum Inf.](https://doi.org/10.1038/s41534-021-00484-1) 7, [142 \(2021\)](https://doi.org/10.1038/s41534-021-00484-1).
- <span id="page-27-0"></span>[27] J. Niu, L. Zhang, Y. Liu, J. Qiu, W. Huang, J. Huang, H. Jia, J. Liu, Z. Tao, W. Wei et al., Low-loss interconnects for modular superconducting quantum processors, [National](https://doi.org/10.1038/s41928-023-00925-z) [electronics review](https://doi.org/10.1038/s41928-023-00925-z) 6, 235 (2023).
- <span id="page-27-1"></span>[28] J. Koch, T. M. Yu, J. Gambetta, A. A. Houck, D. I. Schuster, J. Majer, A. Blais, M. H. Devoret, S. M. Girvin, and R. J. Schoelkopf, Charge-insensitive qubit design derived from the Cooper pair box, Phys. Rev. A 76[, 042319 \(2007\)](https://doi.org/10.1103/PhysRevA.76.042319).
- [29] C. Wang, C. Axline, Y. Y. Gao, T. Brecht, Y. Chu, L. Frunzio, M. Devoret, and R. J. Schoelkopf, Surface participation and dielectric loss in superconducting qubits, [Appl. Phys. Lett.](https://doi.org/10.1063/1.4934486) 107, 162601 (2015).
- <span id="page-27-2"></span>[30] J. M. Martinis, Surface loss calculations and design of a superconducting transmon qubit with tapered wiring, [npj](https://doi.org/10.1038/s41534-022-00530-6) [Quantum Inf.](https://doi.org/10.1038/s41534-022-00530-6) 8, 26 (2022).
- <span id="page-27-3"></span>[31] A. P. Place, L. V. Rodgers, P. Mundada, B. M. Smitham, M. Fitzpatrick, Z. Leng, A. Premkumar, J. Bryon, A. Vrajitoarea, S. Sussman et al., New material platform for superconducting transmon qubits with coherence times exceeding 0.3 milliseconds, [Nat. Commun.](https://doi.org/10.1038/s41467-021-22030-5) 12, 1779 (2021).
- <span id="page-27-4"></span>[32] C. Wang, X. Li, H. Xu, Z. Li, J. Wang, Z. Yang, Z. Mi, X. Liang, T. Su, C. Yang et al., Towards practical quantum computers: Transmon qubit with a lifetime approaching 0.5 milliseconds, [npj Quantum Inf.](https://doi.org/10.1038/s41534-021-00510-2) 8, 3 (2022).
- <span id="page-27-5"></span>[33] J. A. Schreier, A. A. Houck, J. Koch, D. I. Schuster, B. R. Johnson, J. M. Chow, J. M. Gambetta, J. Majer, L. Frunzio, M. H. Devoret, S. M. Girvin, and R. J. Schoelkopf, Suppressing charge noise decoherence in superconducting charge qubits, Phys. Rev. B 77[, 180502\(R\) \(2008\).](https://doi.org/10.1103/PhysRevB.77.180502)
- <span id="page-27-6"></span>[34] C. Rigetti and M. Devoret, Fully microwave-tunable universal gates in superconducting qubits with linear couplings and fixed transition frequencies, [Phys. Rev. B](https://doi.org/10.1103/PhysRevB.81.134507) 81, 134507 [\(2010\).](https://doi.org/10.1103/PhysRevB.81.134507)
- <span id="page-27-7"></span>[35] L. DiCarlo, J. M. Chow, J. M. Gambetta, L. S. Bishop, B. R. Johnson, D. Schuster, J. Majer, A. Blais, L. Frunzio, S. Girvin et al., Demonstration of two-qubit algorithms with a superconducting quantum processor, [Nature \(London\)](https://doi.org/10.1038/nature08121) 460, [240 \(2009\)](https://doi.org/10.1038/nature08121).
- <span id="page-27-8"></span>[36] A. D. Patterson, J. Rahamim, T. Tsunoda, P. A. Spring, S. Jebari, K. Ratter, M. Mergenthaler, G. Tancredi, B. Vlastakis, M. Esposito, and P. J. Leek, Calibration of a cross-resonance two-qubit gate between directly coupled transmons, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.12.064013) 12, 064013 (2019).
- <span id="page-27-9"></span>[37] J. M. Chow, A. D. Córcoles, J. M. Gambetta, C. Rigetti, B. R. Johnson, J. A. Smolin, J. R. Rozen, G. A. Keefe, M. B. Rothwell, M. B. Ketchen, and M. Steffen, Simple all-microwave entangling gate for fixed-frequency superconducting qubits, Phys. Rev. Lett. 107[, 080502 \(2011\).](https://doi.org/10.1103/PhysRevLett.107.080502)
- <span id="page-27-10"></span>[38] E. Magesan and J. M. Gambetta, Effective Hamiltonian models of the cross-resonance gate, [Phys. Rev. A](https://doi.org/10.1103/PhysRevA.101.052308) 101, [052308 \(2020\).](https://doi.org/10.1103/PhysRevA.101.052308)
- <span id="page-27-11"></span>[39] S. Sheldon, E. Magesan, J. M. Chow, and J. M. Gambetta, Procedure for systematically tuning up cross-talk in the cross-resonance gate, Phys. Rev. A 93[, 060302\(R\) \(2016\).](https://doi.org/10.1103/PhysRevA.93.060302)
- <span id="page-27-12"></span>[40] A. Kandala, K. X. Wei, S. Srinivasan, E. Magesan, S. Carnevale, G. A. Keefe, D. Klaus, O. Dial, and D. C. McKay, Demonstration of a high-fidelity CNOT gate for

- fixed-frequency transmons with engineered ZZ suppression, Phys. Rev. Lett. 127[, 130501 \(2021\).](https://doi.org/10.1103/PhysRevLett.127.130501)
- <span id="page-27-13"></span>[41] F. Yan, P. Krantz, Y. Sung, M. Kjaergaard, D. L. Campbell, T. P. Orlando, S. Gustavsson, and W. D. Oliver, Tunable coupling scheme for implementing high-fidelity two-qubit gates, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.10.054062) 10, 054062 (2018).
- <span id="page-27-14"></span>[42] Y. Xu, J. Chu, J. Yuan, J. Qiu, Y. Zhou, L. Zhang, X. Tan, Y. Yu, S. Liu, J. Li, F. Yan, and D. Yu, High-fidelity, highscalability two-qubit gate scheme for superconducting qubits, Phys. Rev. Lett. 125[, 240503 \(2020\).](https://doi.org/10.1103/PhysRevLett.125.240503)
- <span id="page-27-15"></span>[43] P. Mundada, G. Zhang, T. Hazard, and A. Houck, Suppression of qubit crosstalk in a tunable coupling superconducting circuit, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.12.054023) 12, 054023 (2019).
- <span id="page-27-16"></span>[44] P. Zhao, D. Lan, P. Xu, G. Xue, M. Blank, X. Tan, H. Yu, and Y. Yu, Suppression of static ZZ interaction in an alltransmon quantum processor, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.16.024037) 16, 024037 [\(2021\).](https://doi.org/10.1103/PhysRevApplied.16.024037)
- <span id="page-27-17"></span>[45] M. Brink, J. M. Chow, J. Hertzberg, E. Magesan, and S. Rosenblatt, Device challenges for near term superconducting quantum processors: frequency collisions, in Proceedings of the 2018 IEEE International Electron Devices Meeting (IEDM) (IEEE, New York, 2018).
- [46] J. B. Hertzberg, E. J. Zhang, S. Rosenblatt, E. Magesan, J. A. Smolin, J.-B. Yau, V. P. Adiga, M. Sandberg, M. Brink, J. M. Chow et al., Laser-annealing Josephson junctions for yielding scaled-up superconducting quantum processors, [npj Quantum Inf.](https://doi.org/10.1038/s41534-021-00464-5) 7, 129 (2021).
- <span id="page-27-18"></span>[47] A. Osman, J. Fernández-Pendás, C. Warren, S. Kosen, M. Scigliuzzo, A. Frisk Kockum, G. Tancredi, A. Fadavi Roudsari, and J. Bylander, Mitigation of frequency collisions in superconducting quantum processors, [Phys. Rev.](https://doi.org/10.1103/PhysRevResearch.5.043001) Res. 5[, 043001 \(2023\)](https://doi.org/10.1103/PhysRevResearch.5.043001).
- <span id="page-27-19"></span>[48] H. Goto, Double-transmon coupler: Fast two-qubit gate with no residual coupling for highly detuned superconducting qubits, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.18.034038) 18, 034038 (2022).
- [49] K. Kubo and H. Goto, Fast parametric two-qubit gate for highly detuned fixed-frequency superconducting qubits using a double-transmon coupler, [Appl. Phys. Lett.](https://doi.org/10.1063/5.0138699) 122, [064001 \(2023\).](https://doi.org/10.1063/5.0138699)
- <span id="page-27-20"></span>[50] D. L. Campbell, A. Kamal, L. Ranzani, M. Senatore, and M. D. LaHaye, Modular tunable coupler for superconducting circuits, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.19.064043) 19, 064043 (2023).
- <span id="page-27-21"></span>[51] K. Kubo, Y. Ho, and H. Goto, High-performance multi-qubit system with double-transmon couplers towards scalable superconducting quantum computers, [arXiv:2402.05361.](https://arXiv.org/abs/2402.05361)
- [52] D. M. Abrams, N. Didier, S. A. Caldwell, B. R. Johnson, and C. A. Ryan, Methods for measuring magnetic flux crosstalk between tunable transmons, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.12.064022) 12[, 064022 \(2019\).](https://doi.org/10.1103/PhysRevApplied.12.064022)
- <span id="page-27-22"></span>[53] P. Zhao, Mitigation of quantum crosstalk in cross-resonancebased qubit architectures, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.20.054033) 20, 054033 [\(2023\).](https://doi.org/10.1103/PhysRevApplied.20.054033)
- <span id="page-27-23"></span>[54] W. H. Press, S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery, Numerical Recipes 3rd Edition: The Art of Scientific Computing (Cambridge University Press, Cambridge, England, 2007).
- <span id="page-27-24"></span>[55] J. M. Martinis and M. R. Geller, Fast adiabatic qubit gates using only σ<sup>z</sup> control, [Phys. Rev. A](https://doi.org/10.1103/PhysRevA.90.022307) 90, 022307 [\(2014\).](https://doi.org/10.1103/PhysRevA.90.022307)

- <span id="page-28-0"></span>[56] M. A. Rol, L. Ciorciaro, F. K. Malinowski, B. M. Tarasinski, R. E. Sagastizabal, C. C. Bultink, Y. Salathe, N. Haandbæk, J. Sedivy, and L. DiCarlo, Time-domain characterization and correction of on-chip distortion of control pulses in a quantum processor, [Appl. Phys. Lett.](https://doi.org/10.1063/1.5133894) 116, 054001 (2020).
- <span id="page-28-1"></span>[57] J. M. Gambetta, A. D. Córcoles, S. T. Merkel, B. R. Johnson, J. A. Smolin, J. M. Chow, C. A. Ryan, C. Rigetti, S. Poletto, T. A. Ohki, M. B. Ketchen, and M. Steffen, Characterization of addressability by simultaneous randomized benchmarking, Phys. Rev. Lett. 109[, 240504 \(2012\)](https://doi.org/10.1103/PhysRevLett.109.240504).
- <span id="page-28-2"></span>[58] A. D. Córcoles, J. M. Gambetta, J. M. Chow, J. A. Smolin, M. Ware, J. Strand, B. L. T. Plourde, and M. Steffen, Process verification of two-qubit quantum gates by randomized benchmarking, Phys. Rev. A 87[, 030301\(R\) \(2013\).](https://doi.org/10.1103/PhysRevA.87.030301)
- <span id="page-28-12"></span>[59] E. Magesan, J. M. Gambetta, B. R. Johnson, C. A. Ryan, J. M. Chow, S. T. Merkel, M. P. da Silva, G. A. Keefe, M. B. Rothwell, T. A. Ohki, M. B. Ketchen, and M. Steffen, Efficient measurement of quantum gate error by interleaved randomized benchmarking, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.109.080505) 109, 080505 [\(2012\).](https://doi.org/10.1103/PhysRevLett.109.080505)
- <span id="page-28-3"></span>[60] R. Barends, J. Kelly, A. Megrant, A. Veitia, D. Sank, E. Jeffrey, T. C. White, J. Mutus, A. G. Fowler, B. Campbell et al., Superconducting quantum circuits at the surface code threshold for fault tolerance, [Nature \(London\)](https://doi.org/10.1038/nature13171) 508, 500 [\(2014\).](https://doi.org/10.1038/nature13171)
- <span id="page-28-4"></span>[61] A. A. Houck, J. A. Schreier, B. R. Johnson, J. M. Chow, J. Koch, J. M. Gambetta, D. I. Schuster, L. Frunzio, M. H. Devoret, S. M. Girvin, and R. J. Schoelkopf, Controlling the spontaneous emission of a superconducting transmon qubit, Phys. Rev. Lett. 101[, 080502 \(2008\).](https://doi.org/10.1103/PhysRevLett.101.080502)
- <span id="page-28-5"></span>[62] J. Chu and F. Yan, Coupler-assisted controlled-phase gate with enhanced adiabaticity, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.16.054020) 16, 054020 [\(2021\).](https://doi.org/10.1103/PhysRevApplied.16.054020)
- <span id="page-28-6"></span>[63] J. Ku, X. Xu, M. Brink, D. C. McKay, J. B. Hertzberg, M. H. Ansari, and B. L. T. Plourde, Suppression of unwanted ZZ interactions in a hybrid two-qubit system, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.125.200504) 125[, 200504 \(2020\).](https://doi.org/10.1103/PhysRevLett.125.200504)
- <span id="page-28-7"></span>[64] S. Shirai, Y. Okubo, K. Matsuura, A. Osada, Y. Nakamura, and A. Noguchi, All-microwave manipulation of superconducting qubits with a fixed-frequency transmon coupler, Phys. Rev. Lett. 130[, 260601 \(2023\).](https://doi.org/10.1103/PhysRevLett.130.260601)
- <span id="page-28-8"></span>[65] F. Motzoi, J. M. Gambetta, P. Rebentrost, and F. K. Wilhelm, Simple pulses for elimination of leakage in weakly nonlinear qubits, Phys. Rev. Lett. 103[, 110501 \(2009\).](https://doi.org/10.1103/PhysRevLett.103.110501)
- <span id="page-28-9"></span>[66] E. Lucero, J. Kelly, R. C. Bialczak, M. Lenander, M. Mariantoni, M. Neeley, A. D. O'Connell, D. Sank, H. Wang, M. Weides, J. Wenner, T. Yamamoto, A. N. Cleland, and J. M. Martinis, Reduced phase error through optimized control of a superconducting qubit, [Phys. Rev. A](https://doi.org/10.1103/PhysRevA.82.042339) 82[, 042339 \(2010\).](https://doi.org/10.1103/PhysRevA.82.042339)
- <span id="page-28-10"></span>[67] D. C. McKay, C. J. Wood, S. Sheldon, J. M. Chow, and J. M. Gambetta, Efficient Z gates for quantum computing, [Phys.](https://doi.org/10.1103/PhysRevA.96.022330) Rev. A 96[, 022330 \(2017\)](https://doi.org/10.1103/PhysRevA.96.022330).
- <span id="page-28-11"></span>[68] V. V. Sivak, A. Eickbusch, H. Liu, B. Royer, I. Tsioutsios, and M. H. Devoret, Model-free quantum control with reinforcement learning, Phys. Rev. X 12[, 011059 \(2022\)](https://doi.org/10.1103/PhysRevX.12.011059).
- <span id="page-28-13"></span>[69] M. Takita, A. W. Cross, A. D. Córcoles, J. M. Chow, and J. M. Gambetta, Experimental demonstration of fault-tolerant state preparation with superconducting qubits, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.119.180501) 119[, 180501 \(2017\)](https://doi.org/10.1103/PhysRevLett.119.180501).

- <span id="page-28-14"></span>[70] M. A. Rol, F. Battistel, F. K. Malinowski, C. C. Bultink, B. M. Tarasinski, R. Vollmer, N. Haider, N. Muthusubramanian, A. Bruno, B. M. Terhal, and L. DiCarlo, Fast, high-fidelity conditional-phase gate exploiting leakage interference in weakly anharmonic superconducting qubits, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.123.120502) 123[, 120502 \(2019\)](https://doi.org/10.1103/PhysRevLett.123.120502).
- <span id="page-28-15"></span>[71] C. J. Wood and J. M. Gambetta, Quantification and characterization of leakage errors, [Phys. Rev. A](https://doi.org/10.1103/PhysRevA.97.032306) 97, 032306 [\(2018\).](https://doi.org/10.1103/PhysRevA.97.032306)
- <span id="page-28-16"></span>[72] A. G. Fowler, M. Mariantoni, J. M. Martinis, and A. N. Cleland, Surface codes: Towards practical large-scale quantum computation, Phys. Rev. A 86[, 032324 \(2012\).](https://doi.org/10.1103/PhysRevA.86.032324)
- <span id="page-28-17"></span>[73] S. B. Bravyi and A. Y. Kitaev, Quantum codes on a lattice with boundary, [arXiv:quant-ph/9811052](https://arXiv.org/abs/quant-ph/9811052).
- <span id="page-28-18"></span>[74] E. Dennis, A. Kitaev, A. Landahl, and J. Preskill, Topological quantum memory, [J. Math. Phys. \(N.Y.\)](https://doi.org/10.1063/1.1499754) 43, 4452 [\(2002\).](https://doi.org/10.1063/1.1499754)
- <span id="page-28-19"></span>[75] D. C. McKay, S. Filipp, A. Mezzacapo, E. Magesan, J. M. Chow, and J. M. Gambetta, Universal gate for fixed-frequency qubits via a tunable bus, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.6.064007) 6[, 064007 \(2016\)](https://doi.org/10.1103/PhysRevApplied.6.064007).
- <span id="page-28-20"></span>[76] A. Javed and J.-B. Sun, An investigation of structural phase transformation and electrical resistivity in Ta films, [Appl.](https://doi.org/10.1016/j.apsusc.2010.08.023) Surf. Sci. 257[, 1211 \(2010\).](https://doi.org/10.1016/j.apsusc.2010.08.023)
- <span id="page-28-21"></span>[77] G. Dolan, Offset masks for lift-off photoprocessing, [Appl.](https://doi.org/10.1063/1.89690) Phys. Lett. 31[, 337 \(1977\).](https://doi.org/10.1063/1.89690)
- <span id="page-28-22"></span>[78] T. Roy, S. Kundu, M. Chand, A. Vadiraj, A. Ranadive, N. Nehra, M. P. Patankar, J. Aumentado, A. Clerk, and R. Vijay, Broadband parametric amplification with impedance engineering: Beyond the gain-bandwidth product, [Appl.](https://doi.org/10.1063/1.4939148) Phys. Lett. 107[, 262601 \(2015\).](https://doi.org/10.1063/1.4939148)
- <span id="page-28-23"></span>[79] R. Gordon, C. Murray, C. Kurter, M. Sandberg, S. Hall, K. Balakrishnan, R. Shelby, B. Wacaser, A. Stabile, J. Sleight et al., Environmental radiation impact on lifetimes and quasiparticle tunneling rates of fixed-frequency transmon qubits, [Appl. Phys. Lett.](https://doi.org/10.1063/5.0078785) 120, 074002 (2022).
- <span id="page-28-24"></span>[80] F. Yan, S. Gustavsson, A. Kamal, J. Birenbaum, A. P. Sears, D. Hover, T. J. Gudmundsen, D. Rosenberg, G. Samach, S. Weber et al., The flux qubit revisited to enhance coherence and reproducibility, Nat. Commun. 7[, 12964 \(2016\).](https://doi.org/10.1038/ncomms12964)
- <span id="page-28-25"></span>[81] J. M. Gambetta, C. E. Murray, Y.-K.-K. Fung, D. T. McClure, O. Dial, W. Shanks, J. W. Sleight, and M. Steffen, Investigating surface loss effects in superconducting transmon qubits, [IEEE Trans. Appl. Supercond.](https://doi.org/10.1109/TASC.2016.2629670) 27, 1 [\(2016\).](https://doi.org/10.1109/TASC.2016.2629670)
- <span id="page-28-26"></span>[82] Y. Sunada, S. Kono, J. Ilves, S. Tamate, T. Sugiyama, Y. Tabuchi, and Y. Nakamura, Fast readout and reset of a superconducting qubit coupled to a resonator with an intrinsic Purcell filter, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.17.044016) 17, 044016 (2022).
- <span id="page-28-27"></span>[83] E. Magesan, J. M. Gambetta, and J. Emerson, Scalable and robust randomized benchmarking of quantum processes, Phys. Rev. Lett. 106[, 180504 \(2011\).](https://doi.org/10.1103/PhysRevLett.106.180504)
- <span id="page-28-28"></span>[84] P. J. J. O'Malley et al., Qubit metrology of ultralow phase noise using randomized benchmarking, [Phys. Rev. Appl.](https://doi.org/10.1103/PhysRevApplied.3.044009) 3, [044009 \(2015\).](https://doi.org/10.1103/PhysRevApplied.3.044009)
- <span id="page-28-30"></span><span id="page-28-29"></span>[85] V. Sivak, quantum-control-rl, [https://github.com/v-sivak/](https://github.com/v-sivak/quantum-control-rl) [quantum-control-rl](https://github.com/v-sivak/quantum-control-rl).
- [86] J. Schulman, F. Wolski, P. Dhariwal, A. Radford, and O. Klimov, Proximal policy optimization algorithms, [arXiv:](https://arXiv.org/abs/1707.06347) [1707.06347.](https://arXiv.org/abs/1707.06347)

- <span id="page-29-0"></span>[87] D. Greenbaum, Introduction to quantum gate set tomography, [arXiv:1509.02921](https://arXiv.org/abs/1509.02921).
- <span id="page-29-1"></span>[88] J. M. Chow, J. M. Gambetta, A. D. Córcoles, S. T. Merkel, J. A. Smolin, C. Rigetti, S. Poletto, G. A. Keefe, M. B. Rothwell, J. R. Rozen, M. B. Ketchen, and M. Steffen, Universal quantum gate set approaching fault-tolerant thresholds with superconducting qubits, [Phys. Rev. Lett.](https://doi.org/10.1103/PhysRevLett.109.060501) 109[, 060501 \(2012\).](https://doi.org/10.1103/PhysRevLett.109.060501)
- <span id="page-29-2"></span>[89] G. C. Knee, E. Bolduc, J. Leach, and E. M. Gauger, Quantum process tomography via completely positive and tracepreserving projection, Phys. Rev. A 98[, 062336 \(2018\)](https://doi.org/10.1103/PhysRevA.98.062336).
- <span id="page-29-3"></span>[90] K. Gulshen, J. Combes, M. P. Harrigan, P. J. Karalekas, M. P. da Silva, M. S. Alam, A. Brown, S. Caldwell, L. Capelluto, G. Crooks, D. Girshovich, B. R. Johnson, E. C. Peterson, A. Polloreno, N. C. Rubin, C. A. Ryan, A. Staley, N. A. Tezak, and J. Valery, Forest benchmarking: QCVV using PyQuil, [https://tex.stackexchange.com/questions/](https://tex.stackexchange.com/questions/468623/indicating-joint-first-authorship-through-special-markup-in-biblatex-biber) [468623/indicating-joint-first-authorship-through-special](https://tex.stackexchange.com/questions/468623/indicating-joint-first-authorship-through-special-markup-in-biblatex-biber)[markup-in-biblatex-biber.](https://tex.stackexchange.com/questions/468623/indicating-joint-first-authorship-through-special-markup-in-biblatex-biber)
- <span id="page-29-4"></span>[91] G. Catelani, J. Koch, L. Frunzio, R. J. Schoelkopf, M. H. Devoret, and L. I. Glazman, Quasiparticle relaxation of superconducting qubits in the presence of flux, [Phys. Rev.](https://doi.org/10.1103/PhysRevLett.106.077002) Lett. 106[, 077002 \(2011\)](https://doi.org/10.1103/PhysRevLett.106.077002).

- <span id="page-29-5"></span>[92] C. Müller, J. H. Cole, and J. Lisenfeld, Towards understanding two-level-systems in amorphous solids: insights from quantum circuits, [Rep. Prog. Phys.](https://doi.org/10.1088/1361-6633/ab3a7e) 82, 124501 [\(2019\).](https://doi.org/10.1088/1361-6633/ab3a7e)
- <span id="page-29-6"></span>[93] J. Braumüller, L. Ding, A. P. Vepsäläinen, Y. Sung, M. Kjaergaard, T. Menke, R. Winik, D. Kim, B. M. Niedzielski, A. Melville, J. L. Yoder, C. F. Hirjibehedin, T. P. Orlando, S. Gustavsson, and W. D. Oliver, Characterizing and optimizing qubit coherence based on SQUID geometry, [Phys. Rev.](https://doi.org/10.1103/PhysRevApplied.13.054079) Appl. 13[, 054079 \(2020\).](https://doi.org/10.1103/PhysRevApplied.13.054079)
- <span id="page-29-7"></span>[94] L. H. Pedersen, N. M. Møller, and K. Mølmer, Fidelity of quantum operations, [Phys. Lett. A](https://doi.org/10.1016/j.physleta.2007.02.069) 367, 47 (2007).
- <span id="page-29-8"></span>[95] M. A. Nielsen and I. L. Chuang, Quantum Computation and Quantum Information (Cambridge University Press, Cambridge, England, 2010).

Correction: The third sentence of the abstract was erroneously altered during the production of proofs and has been rectified.