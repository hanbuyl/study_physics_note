### **Calibration of Drive Nonlinearity for Arbitrary-Angle Single-Qubit Gates Using Error Amplification**

Stefania Lazar˘ [,](https://orcid.org/0000-0002-7282-6405) 1,\*,† Quentin Ficheux,1[,†](#page-0-0) Johannes Herrmann,<sup>1</sup> Ants Remm,1 Nathan Lacroi[x](https://orcid.org/0000-0003-2002-9495) , 1 Christoph Hellings [,](https://orcid.org/0000-0002-9929-9684) <sup>1</sup> Francois Swiadek,<sup>1</sup> Dante Colao Zanuz,<sup>1</sup> Graham J. Norris,<sup>1</sup> Mohsen Bahrami Panah,1,2 Alexander Flasby,1,2 Michael Kerschbaum,1,2 Jean-Claude Besse,1,2 Christopher Eichler,<sup>1</sup> and Andreas Wallraff1,2,3

1 *Department of Physics, ETH Zurich, Zurich CH-8093, Switzerland ETH Zurich—PSI Quantum Computing Hub, Paul Scherrer Institute, Villigen CH-5232, Switzerland* 3 *Quantum Center, ETH Zurich, Zurich 8093, Switzerland*

![](_page_0_Picture_4.jpeg)

(Received 6 December 2022; revised 26 June 2023; accepted 31 July 2023; published 15 August 2023)

The ability to execute high-fidelity operations is crucial to scaling up quantum devices to large numbers of qubits. However, signal distortions originating from nonlinear components in the control lines can limit the performance of single-qubit gates. In this work, we use a measurement based on error amplification to characterize and correct the small single-qubit rotation errors originating from the nonlinear scaling of the qubit drive rate with the amplitude of the programmed pulse. With our hardware, and for a 15-ns pulse, the rotation angles deviate by up to several degrees from a linear model. Using purity benchmarking, we find that control errors reach 2 <sup>×</sup> <sup>10</sup>−4, which accounts for half of the total gate error. Using crossentropy benchmarking, we demonstrate arbitrary-angle single-qubit gates with coherence-limited errors of 2 <sup>×</sup> <sup>10</sup>−<sup>4</sup> and leakage below 6 <sup>×</sup> <sup>10</sup>−5. While the exact magnitude of these errors is specific to our setup, the presented method is applicable to most sources of nonlinearity. Our work shows that the nonlinearity of qubit drive line components imposes a limit on the fidelity of single-qubit gates, independent of improvements in coherence times, circuit design, or leakage mitigation when not corrected for.

DOI: [10.1103/PhysRevApplied.20.024036](http://dx.doi.org/10.1103/PhysRevApplied.20.024036)

As quantum processors accommodate an ever larger number of qubits, understanding the errors that limit their performance remains an important task to enable further progress [\[1–](#page-9-0)[3\]](#page-9-1). In particular, errors in single- and twoqubit gates limit the fidelities of quantum error-correction codes [\[4–](#page-9-2)[8\]](#page-9-3), variational quantum algorithms [\[9](#page-9-4)[,10\]](#page-9-5), or digital quantum simulations [\[11](#page-9-6)[–13\]](#page-10-0). These errors can be reduced by increasing the coherence times, but also by mitigating control errors [\[14–](#page-10-1)[19\]](#page-10-2) or by reducing the circuit depth when compiling algorithms with a larger gate set [\[10,](#page-9-5)[20](#page-10-3)[,21\]](#page-10-4).

For superconducting quantum processors, standard gate calibration techniques [\[22–](#page-10-5)[25\]](#page-10-6) assume that the control parameters respond linearly to the control fields. However, commonly used electronic components can introduce nonlinear effects, which result in control errors if unaccounted for. For example, in-phase and quadrature (IQ) mixer imperfections produce spurious frequency components [\[26–](#page-10-7)[28\]](#page-10-8), gain compression in amplifiers saturates the power of control signals [\[29\]](#page-10-9), and saturation of pulsegeneration devices leads to waveform distortions [\[30\]](#page-10-10).

For the past decade, two-qubit gates have imposed the main limitation on superconducting quantum processors [\[2,](#page-9-7)[31\]](#page-10-11). However, considerable efforts in recent years have reduced the errors of two-qubit gates into the range of 10−<sup>3</sup> [\[19](#page-10-2)[,32–](#page-10-12)[36\]](#page-10-13), making their contribution to computation errors comparable to that of single-qubit gates [\[1\]](#page-9-0). Moreover, current algorithms often require a larger number of single-qubit gates than two-qubit gates, especially for dynamical decoupling schemes [\[37](#page-10-14)[,38\]](#page-10-15). Thus, further improvements in the performance of single-qubit gates are needed to enhance the overall fidelity of quantum algorithms.

Arbitrary single-qubit rotation angles are routinely calibrated by assuming that the rotation of the state vector scales linearly with the pulse amplitude [\[22](#page-10-5)[–25\]](#page-10-6). However, nonlinear electronic components in the drive line can produce a deviation from this linear model that leads to rotation errors. So far, few techniques have been developed to compensate for similar imperfections, such as waveform predistortion [\[32](#page-10-12)[,39,](#page-10-16)[40\]](#page-10-17), pulse-shape optimization methods [\[41,](#page-11-0)[42\]](#page-11-1), and correction of drive-pulse amplitudes affected by imperfect signal generation [\[30\]](#page-10-10).

<sup>\*</sup>stefania.lazar@phys.ethz.ch

<span id="page-0-0"></span><sup>†</sup>First two authors contributed equally.

Here, we present an in situ amplification scheme for small rotation errors, which allows us to calibrate coherence-limited arbitrary-angle single-qubit gates on a transmon qubit [43] even in the presence of nonlinearity. With this technique, we correct for residual rotation errors when using pulses with amplitudes approaching the 1-dB compression point of the frequency conversion device in our microwave line, which is nonlinear at high input powers [29]. Using randomized benchmarking [44], purity benchmarking [45], and cross-entropy benchmarking [46], we demonstrate arbitrary-angle 15-ns-long single-qubit gates with coherence-limited performance and with leakage outside the computational subspace below  $6 \times 10^{-5}$ . Importantly, we find that, for short gate duration, coherent errors in the computational subspace caused by nonlinear pulse amplitude distortions are one order of magnitude larger than leakage, imposing a lower bound on the gate error for a given gate duration, independent of improvements in coherence times.

We study the effect described above on two flux-tunable superconducting transmon qubits from two different 17-qubit devices labeled A and B, with similar designs to that discussed in Ref. [7]. The devices are controlled by nominally the same electronics. The measurements presented in Secs. II and V were done on device A, while those discussed in Secs. III and IV were performed on device B (see Appendix A, where we also summarize the device parameters).

## <span id="page-1-0"></span>II. PULSE AMPLITUDE CALIBRATION USING ERROR AMPLIFICATION

Nonlinear components in qubit control lines distort coherent microwave drive pulses, effectively changing the amplitude of the driving field at the qubit frequency in an unintended way [26]. We illustrate this effect in Figs. 1(a) and 1(b), where a pulse produced by the waveform generator with amplitude A (purple) reaches the qubit with an amplitude that shows a reduction from a linear behavior (black and gray lines, respectively). This reduction becomes more pronounced with larger input amplitudes and leads to a rotation angle of the qubit state that is smaller than the targeted one. The pulse distortions introduced by the nonlinearity could be corrected with a sample-bysample nonlinear transformation. However, we show that a simple scaling of the pulse amplitude by the inverse of the response function of the drive line (orange pulses) is enough to mitigate the rotation errors produced by the nonlinearity.

In order to characterize the impact of nonlinearity on the pulse amplitudes, we measure the rotation errors that are introduced by reducing the pulse amplitude proportionally to the amplitude of a  $\pi$  rotation; see the dashed black line in Fig. 1(b). To this end, we use the pulse calibration method based on error amplification described in Refs.

[47–49], which we extend to arbitrary angles. We refer to this technique as an *N*-pulse calibration method.

To calibrate any rotation errors left over from an initial Rabi calibration of a  $\pi$  pulse, we start by initializing the qubit in the superposition state  $|+i\rangle=(|g\rangle+i|e\rangle)/\sqrt{2}$ , and then we apply N repetitions of  $X_{\pi+\varepsilon}$  gates, which have a small error in the rotation angle,  $\varepsilon$ . The pulse sequence is shown above Fig. 1(c). In the ideal case ( $\varepsilon=0$ ), the qubit remains in the equatorial plane of the Bloch sphere, where the ground and excited-state populations are  $p_g=p_e=0.5$ . For imperfect gates ( $\varepsilon\neq0$ ), the rotation errors accumulate to produce a deviation of the excited-state population from 0.5 [see the purple points in Fig. 1(c)]. We ignore any small errors in the initialization pulse as they will not be amplified during the pulse sequence.

We extend the methods in Refs. [47–49] by extracting the rotation error per gate from a fit of the excited-state population of the qubit to a master-equation-based model (see Appendix B). After applying the method to a 32-ns pulse with the amplitude calibrated with a single-pulse Rabi experiment, we find around  $0.9^{\circ}$  of rotation error. This corresponds to around 1.7 mV of amplitude error for a pulse amplitude of 335 mV at the output of the arbitrary waveform generator. We shape the pulse using a Gaussian envelope with standard deviation  $\sigma = 6.4$  ns, which is truncated at  $\pm 2.5\sigma$ . We use a value of  $0.68\sigma$  for the quadrature scaling parameter of the derivative removal by adiabatic gate (DRAG) method [50,51] to cancel the phase errors arising from the ac-Stark shift of the *ef* transition during the drive pulse [52,53].

Repeating the measurement after scaling the pulse amplitude based on the fit result, we are able to reduce the observed rotation errors [see the orange points in Fig. 1(c)]. The small residual oscillations exhibited by the orange points are not caused by rotation errors captured by our model, and could originate, for example, from off-resonant driving by higher harmonic frequency components, or from uncompensated nonlinear distortions of the pulse. The latter effects are beyond the scope of the current work.

To determine the impact of nonlinearity for rotation angles smaller than  $\pi$ , we generalize the technique by using groups of pulses implementing rotation angles that add up to  $\pi$ . The initial pulse amplitude for these gates is obtained from a proportional reduction with respect to the previously calibrated  $\pi$ -pulse amplitude.

To calibrate rotation angles up to  $\pi/2$ , we use a pulse sequence in which each  $\pi$  pulse is split into k repetitions of  $X_{\pi/k+\varepsilon}$  gates; see the pulse sequence above Fig. 1(d). For an  $X_{\pi/2}$  rotation, we find an over-rotation error of around 0.4° when setting the pulse amplitude to half of the amplitude of the  $\pi$  pulse that was already corrected with the N-pulse calibration [purple points and line in Fig. 1(d)]. This value corresponds to an amplitude error of around 0.7 mV.

Similarly, to measure the nonlinearity for rotation angles in the range  $\pi/2$  to  $\pi$ , we apply groups of two X rotations,

<span id="page-2-0"></span>![](_page_2_Figure_2.jpeg)

FIG. 1. (a) A pulse with amplitude A (purple) produced by an ideal waveform generator is distorted by a series of nonlinear components before reaching the quantum system with an amplitude f(A), which is lower than expected. A pulse with amplitude scaled by the inverse response function  $f^{-1}(A')$  ensures that the quantum system is driven with the desired amplitude A'. (b) Schematic example of a nonlinear response function f(A) (solid black line) and the linear dependence (dashed line) assumed when single-qubit rotations are implemented with a linear scaling of the pulse amplitude relative to the amplitude of a  $\pi$  rotation. (c)—(e) Measured excited-state population of the qubit  $(p_e)$  after applying a pulse sequence with N repetitions of the 32-ns gates shown above each panel. At the bottom left, we indicate the rotation errors  $\varepsilon$  extracted from a fit of the data (purple line and points) to a master-equation-based model. The orange points are obtained after correcting the pulse amplitudes based on  $\varepsilon$ . We increment N from 0 to 150 in steps of 5 in (c) and (d), and in steps of 3 in (e). (f) Compressed pulse amplitude A0 as a function of the applied pulse amplitude for a 15-ns gate. The gray line is the expected linear response. (g) Difference between the measured data and the gray line in (f). (h) Same data as in (f) but converted to the calibrated rotation angle  $\theta$  as a function of the pulse amplitude relative to the amplitude of a  $\pi$  rotation. The orange line is a fifth-order odd polynomial fit to the data. (i) Difference between the measured data (black points) and polynomial fit (orange line) in (h) and a linear interpolation between the last data point in (h) and the origin (purple line).

where the first is a previously calibrated  $\pi/k$  gate, and the second is a pulse implementing a rotation of  $\pi - \pi/k + \varepsilon$ , which is to be calibrated [indicated by the colored box in the pulse sequence above Fig. 1(e)]. We perform the calibration for an  $X_{5\pi/6}$  gate with the pulse amplitude set to 5/6 of the  $\pi$ -pulse amplitude that was already corrected with the N-pulse calibration. We find an under-rotation error of around  $-1.0^{\circ}$ , corresponding to an amplitude error of around -1.9 mV.

For both  $X_{\pi/2}$  and  $X_{5\pi/6}$ , the accumulation of rotation errors is prevented by adjusting the pulse amplitude with the value extracted from the corresponding fit (see the orange points). We note that the amplitude of the oscillations shown by the purple points in Figs. 1(d) and 1(e) is captured by our model (see Appendix B).

We reconstruct the nonlinear response curve of the qubit drive line by performing the calibration for 11 distinct rotation angles with a gate duration of 15 ns; see Figs. 1(f) and 1(g). This gate duration corresponds to a  $\pi$ -pulse amplitude of 730 mV at the output of the arbitrary-waveform generator (AWG), which is around 100 mV below the 1-dB compression point of our up-conversion device. Figures 1(h) and 1(i) shows that a simple linear downscaling of the

amplitude with respect to the calibrated  $\pi$ -pulse amplitude introduces a systematic over-rotation error; see the filled purple region in Fig. 1(i). For rotation angles between  $0^{\circ}$  and  $180^{\circ}$ , we model this response with a polynomial correction that preserves the antisymmetry between positive and negative amplitudes:

<span id="page-2-1"></span>
$$\theta(\tilde{A}) = 180^{\circ}(1 + b(\tilde{A}^2 - 1) + a(\tilde{A}^4 - 1))\tilde{A},$$
 (1)

Here,  $\tilde{A}=A/A_{\pi}$  is the pulse amplitude scaled with respect to the amplitude of a  $\pi$  rotation, and a and b are fitting parameters capturing the nonlinearity of the up-conversion circuitry. The degree of the polynomial is chosen heuristically based on the shape of the deviation from the linear scaling shown in Fig. 1(i). Parameters a and b are determined from a fit to the data in Fig. 1(h) (orange line), for which we obtain residuals of the order of 0.2°. In Sec. V, we use the model in Eq. (1) to implement arbitrary rotation angles.

In the specific case of our setup, we identify the frequency up-conversion device as the dominant source of the nonlinear response by comparing the results measured with the *N*-pulse calibration to those obtained by rerouting

the up-converted drive signal directly to the detection electronics at room temperature (see Appendix [C\)](#page-7-0). However, not all the observed nonlinearity is explained by this measurement, indicating some further source of nonlinearity in other parts of the drive line, which could not be avoided by only using this type of calibration. On the other hand, the *N*-pulse calibration method is a calibration tool for the entire microwave drive line that can also be used when the nonlinear distortions have a different origin than that we have identified in our setup.

# <span id="page-3-0"></span>**III. IMPACT OF NONLINEARITY ON SHORT**

**SINGLE-QUBIT GATES** A lower bound on single-qubit gate errors is imposed by the ratio between the gate duration and the coherence time of the system. However, decreasing the gate duration requires an increase in the pulse amplitude. As discussed above, this leads to a larger nonlinear distortion [see Figs. [1\(f\)](#page-2-0) and [1\(g\)\]](#page-2-0), and, hence, more rotation errors if not calibrated out; but also to possible leakage out of the computational subspace.

To quantify the impact of rotation errors produced by drive-line nonlinearity on the performance of single-qubit gates, we measure the total average gate error with randomized benchmarking (RB) [\[44,](#page-11-3)[54](#page-11-12)[,55\]](#page-11-13). In addition, we distinguish between coherent and incoherent errors using purity benchmarking (PB) [\[45](#page-11-4)[,56\]](#page-11-14). Both methods rely on the application of random sequences sampled from the 24 single-qubit Clifford operations, which we decompose into *X* and virtual *Z* gates [\[57\]](#page-11-15). However, for purity benchmarking, we apply the tomography pulses *I* (identity), *X*π/2, and *Y*π/<sup>2</sup> at the end of each sequence to measure the state purity (see the pulse sequence at the top of Fig. [2\)](#page-3-1). We record 4096 acquisitions of each sequence using single-shot readout, and discriminate between the evolution confined to the qubit computational subspace and leakage into the *f* state with an average readout assignment error over the three qutrit states of around 4%. The results are then corrected for readout errors [\[58](#page-11-16)[,59\]](#page-11-17).

We calculate the average *f* -state population for each sequence length and extract the leakage error per gate *L* [Fig. [2\(d\)](#page-3-1) and Appendix [D\]](#page-7-1). To estimate the gate errors within the qubit subspace, we then renormalize the populations of the qubit subspace so that they add up to one. The total gate error *E* [Fig. [2\(a\)\]](#page-3-1) and the incoherent error per gate *E*inc [Fig. [2\(b\)\]](#page-3-1) are extracted independently from the decay of sequence fidelity and state purity, respectively (see Appendix [D\)](#page-7-1). Thus, the difference between *E* and *E*inc provides an estimate of the coherent control errors per gate *E*coh in the computational subspace [Fig. [2\(c\)\]](#page-3-1). We stress that, by renormalizing the qubit subspace before estimating the gate errors, *L* does not contribute to the total gate error *E*.

<span id="page-3-1"></span>![](_page_3_Figure_7.jpeg)

FIG. 2. Single-qubit gate performance extracted from Clifford randomized benchmarking (RB) and purity benchmarking (PB). Top: schematic of a PB sequence with single-qubit gates implemented by linearly scaling the π/2-pulse amplitude with respect to the amplitude of a π rotation (purple), and by calibrating the π/2-pulse amplitude with the *N*-pulse calibration (orange). In both cases, the π pulse is calibrated with the *N*-pulse method. (a) Total gate error *E*, (b) incoherent error per gate *E*inc, (c) coherent error per gate *E*coh, and (d) leakage error per gate *L* of singlequbit gates as a function of gate duration τ (bottom axes) and π-pulse amplitude *A*<sup>π</sup> (top axes). The black line in (b) is a linear fit to the orange data points. Colors have the same meaning as in the sequence schematic.

In Sec. [II](#page-1-0) we found that not correcting for the effects of nonlinearity results in around 1◦ of rotation error for a 32-ns gate, and 3.6◦ when the length is decreased to 15 ns. Here we use a different device (device B) with better coherence and smaller π-pulse amplitude (see Appendix [A\)](#page-6-0) to measure the coherent errors introduced when the π/2-pulse amplitude is scaled linearly relative to the πpulse amplitude (purple points in Fig. [2\)](#page-3-1). By calibrating the π/2-pulse amplitude with the *N*-pulse method (orange), we show that these errors can be mitigated. In both cases, the amplitude of the π pulse is calibrated with the *N*-pulse method. We benchmark the performance of single-qubit gates with lengths ranging from 15 to 40 ns (see the bottom horizontal axis in Fig. [2\)](#page-3-1) using 50 random purity benchmarking sequences of up to 4096 Clifford gates. For each gate length, the pulses are implemented as DRAG pulses with Gaussian envelopes having standard deviations σ ranging from 3 to 8 ns that are truncated at ±2.5σ.

For both implementations of the π/2 pulse, we find an expected linear increase of *E*inc with gate duration; see the black line in Fig. [2\(b\).](#page-3-1) At 20 ns, we observe an increase in the coherent errors when using a linear scaling of the amplitude [Fig. [2\(c\)\]](#page-3-1). This increase becomes more pronounced at 15 ns, where the coherent gate errors account for about half of the total gate error [Fig. [2\(a\)\]](#page-3-1), while the leakage remains comparatively low at around 6 <sup>×</sup> <sup>10</sup>−5. With the *N*-pulse calibration we obtain coherence-limited gate errors for all gate lengths; see the orange points. This indicates that the measured coherent errors originate primarily from the nonlinearity identified in Sec. [II,](#page-1-0) which becomes more pronounced at shorter gate lengths where larger pulse amplitudes are needed to achieve the same rotation (see the top axes in Fig. [2\)](#page-3-1). In our experiment, the coherent errors produced by this effect are up to one order of magnitude larger than leakage into the noncomputational states.

# <span id="page-4-0"></span>**IV. IMPACT OF NONLINEARITY ON**

**ARBITRARY-ANGLE SINGLE-QUBIT GATES** In this section, we show that the *N*-pulse calibration method can be used to implement arbitrary-angle singlequbit gates with coherence-limited performance. Purity benchmarking cannot be used to benchmark arbitraryrotation single-qubit gates, since these gates are not in the Clifford group. Hence, we use cross-entropy benchmarking (XEB) [\[20](#page-10-3)[,46,](#page-11-5)[60\]](#page-11-18) with the pulse sequence shown at the top of Fig. [3.](#page-4-1) Each cycle consists of an *X* rotation of fixed angle θ followed by a virtual *Z*φ*<sup>i</sup>* gate, with φ*<sup>i</sup>* sampled fully randomly from a uniform distribution between 0 and 2π. We generate *K* = 200 random sequences of up to 4096 cycles and measure in the *Z* basis using single-shot readout with 4096 acquisitions.

In cross-entropy benchmarking, the cross-entropy is used as a metric to compare the output qubit-state distribution after *K* random sequences to that calculated assuming ideal gates [\[20\]](#page-10-3). By then fitting the exponential decay of this cross-entropy fidelity versus the number of cycles in the sequence, we extract the average error *E* of the *X*<sup>θ</sup> gate (see Appendix [E\)](#page-8-0). In addition, the ratio of the variance of the measured distribution and that of the Porter-Thomas distribution allows us to extract the average purity of the final qubit state over the distribution of random sequences [\[60\]](#page-11-18). This quantity also decays exponentially with the number of cycles, from which we extract the average incoherent errors per gate, *E*inc. Then we calculate the coherent errors per gate *E*coh as the difference between *E* and *E*inc. Finally, as also done for purity benchmarking, we use the measured *f* -state population to estimate the average leakage error per gate *L*, and renormalize the qubit subspace before estimating the gate errors. Thus, *L* does not contribute to the total gate error *E*.

To minimize the incoherent errors, we choose the shortest, 15-ns gate in Fig. [2,](#page-3-1) which is also maximally sensitive to errors caused by the nonlinearity of the driveline components. We benchmark the performance of *X* rotations with angles π/4, π/3, π/2, 3π/4, 5π/6 using

<span id="page-4-1"></span>![](_page_4_Figure_7.jpeg)

FIG. 3. Characterization of arbitrary-angle single-qubit gates using cross-entropy benchmarking (XEB). Top: illustration of an XEB pulse sequence. For each angle θ, the amplitudes of the *X*<sup>θ</sup> gates are obtained either from a linear scaling with respect to the calibrated amplitude of the *X*<sup>π</sup> gate (purple), or from the *N*-pulse calibration (orange). (a) Total gate error *E*, (b) incoherent error per gate *E*inc, (c) coherent error per gate *E*coh, and (d) leakage error per gate *L* for single-qubit *X*<sup>θ</sup> gates of various rotation angles θ. The black squares in (c) are calculated from the amplitude corrections obtained with the *N*-pulse calibration.

the *N*-pulse calibration method, and obtain coherencelimited gate errors in the computational subspace of around 2.0(1) <sup>×</sup> <sup>10</sup>−<sup>4</sup> for all rotation angles [see the orange points in Fig. [3\(a\)\]](#page-4-1). Thus, we observe no coherent errors within error bars.

For reference, we repeat the measurements for the case where the amplitude is scaled linearly with respect to the calibrated π-pulse amplitude (see the purple points), and we find a dependence of the control errors on the rotation angle [Fig. [3\(c\)\]](#page-4-1), which is similar to the curve in Fig. [1\(i\).](#page-2-0) From the *N*-pulse calibration of each rotation angle performed before the corresponding XEB measurement, we calculate the expected control errors per gate, and find good agreement with the data in Fig. [3\(c\);](#page-4-1) see the open black squares.

With both implementations, the incoherent errors per gate remain constant across all measured angles [Fig. [3\(b\)\]](#page-4-1), as expected for a fixed gate duration. However, the leakage shows a small increase with rotation angle from around <sup>2</sup> <sup>×</sup> <sup>10</sup>−<sup>5</sup> for π/4 to around 6 <sup>×</sup> <sup>10</sup>−<sup>5</sup> at 5π/6 [Fig. [3\(d\)\]](#page-4-1), which is expected as the drive amplitude becomes larger. Nevertheless, the leakage is smaller by one order of magnitude than the coherent errors introduced by the nonlinearity, signaling the latter as the main limitation on overall gate performance.

<span id="page-5-1"></span>![](_page_5_Figure_2.jpeg)

FIG. 4. Cross-entropy benchmarking of random-angle singlequbit *X* rotations. The data points show the sequence fidelity, and the line is an exponential fit to the data. The legend indicates the total gate error obtained when using linear (purple) and polynomial (orange) scaling for calculating the amplitudes of the *X* pulses.

## <span id="page-5-0"></span>**V. CONTINUOUSLY PARAMETERIZED**

**SINGLE-QUBIT GATES** Finally, we show that an individual calibration of the amplitude of every arbitrary-rotation single-qubit gate used in a sequence is not required to achieve coherence-limited gates in our experimental setup. To this end, we implement a continuously parameterized gate set using a polynomial scaling of the pulse amplitude obtained from the fit of the data in Fig. [1\(h\)](#page-2-0) to the model in Eq. [\(1\).](#page-2-1)

To benchmark continuously parameterized single-qubit gates, we replace the fixed-angle *X*<sup>θ</sup> gates in the protocol described in Sec. [IV](#page-4-0) by *X*θ*<sup>i</sup>* gates, where in each cycle, the angles θ*<sup>i</sup>* are sampled fully randomly from a uniform distribution between 0 and π. We use 400 random sequences of up to 2048 cycles, and measure each sequence in the *Z* basis using single-shot readout with 8192 acquisitions. We discriminate between the computational subspace and leakage, and process the data as described in Sec. [IV.](#page-4-0)

When the pulse amplitudes are scaled with the polynomial function, we measure coherence-limited randomangle *<sup>X</sup>* gates with an average error of 8.9(4) <sup>×</sup> <sup>10</sup>−<sup>4</sup> on device A; see the orange data points in Fig. [4](#page-5-1) and the exponential fit (line). With a linear amplitude scaling (purple points and line), we find around 3.8 <sup>×</sup> <sup>10</sup>−<sup>4</sup> of coherent control errors. This number matches the mean value of the gate errors calculated from the rotation errors in Figs. [1\(h\)](#page-2-0) and [1\(i\).](#page-2-0)

In this work, we have presented the *N -pulse calibration* method for pulse amplitudes, which amplifies small rotation errors by the repeated application of gates. Such errors can originate from signal distortions introduced by nonlinear components that are essential for processing microwave signals, such as the frequency up-conversion circuitry used in our experiment. By correcting the rotation errors, we demonstrated—using randomized and purity benchmarking—that this nonlinearity can be the dominant source of single-qubit coherent gate errors, and that the errors produced by the nonlinearity can be up to one order of magnitude larger than leakage into the *f* state. In particular, in our setup using superconducting transmon qubits, we found up to several degrees of over-rotation error for the shortest gates we have investigated (15 ns), which accounts for half the total gate error. Finally, by scaling the pulse amplitude based on a simple polynomial model of the nonlinear response of our control line, we showed that we can implement a continuous family of single-qubit gates with coherence-limited performance for any rotation angle, as characterized with cross-entropy benchmarking.

Our method demonstrates that a sample-by-sample correction of the pulse shape is not needed to mitigate the control errors introduced by the nonlinearity and obtain coherence-limited gates. Moreover, the *N*-pulse technique is an *in situ* calibration measurement that can be used to compensate for most sources of nonlinearity (for example, sources of nonlinearity such as that described in Ref. [\[61\]](#page-11-19) and errors originating from heating of the electronics would need further experimental investigation). However, while our protocol tackles rotation errors, it is not highly sensitive to other types of control errors, such as leakage, crosstalk, or phase errors that may arise from off-resonant driving by spurious frequency components. Nevertheless, similar error amplification techniques, such as those used in Refs. [\[22,](#page-10-5)[62\]](#page-11-20), can be tailored to address these error mechanisms as well.

This work demonstrates that as qubit coherence times improve in the near future, the characterization and mitigation of coherent single-qubit control errors is crucial for further improving the fidelity of these gates. The *N*pulse calibration is an essential step in this direction. Our method is applicable to any quantum computing platform suffering from nonlinear distortions of the drive signals. In particular, the *N*-pulse calibration method is an essential tool for architectures that are compatible with large driving amplitudes, such as superconducting circuits with larger anharmonicity [\[33](#page-10-18)[,63–](#page-11-21)[65\]](#page-11-22).

The authors acknowledge the contributions of Luca Hofele to device calibration and characterization.

The authors acknowledge financial support from the Office of the Director of National Intelligence (ODNI), Intelligence Advanced Research Projects Activity (IARPA), under the U.S. Army Research Office Grant No. W911NF-16-1-0071, from the EU Flagship on Quantum Technology H2020-FETFLAG-2018-03 project 820363 OpenSuperQ, from the National Centre of Competence in Research Quantum Science and Technology (NCCR QSIT), a research instrument of the Swiss National Science Foundation (SNSF), from the SNFS R'equip grant 206021-170731, from the Baugarten Foundation and the ETH Zurich Foundation, from the EU program H2020-FETOPEN project 828826 Quromorphic, and from ETH Zurich. The views and conclusions contained herein are those of the authors and should not be interpreted as necessarily representing the official policies or endorsements, either expressed or implied, of the ODNI, IARPA, or the U.S. Government.

S.L. and Q.F. planned the experiments, and S.L. performed the main experiment and analyzed the data. A.R. and F.S. designed the devices, and D.C., A.R., G.J.N., M.B.P., A.F., M.K., and J.-C.B. fabricated the devices. S.L., C.H., N.L., and A.R., developed the experimental software framework, and S.L. developed the control and calibration software routines used in this work. S.L., A.R., C.H., and J.H. designed and built elements of the room-temperature setup, and S.L., Q.F., N.L., C.H., and J.H. maintained the experimental setup. S.L., Q.F., and N.L. characterized and calibrated the devices and the experimental setup. S.L. prepared the figures for the manuscript, and S.L. and Q.F. wrote the manuscript with inputs from the coauthors. C.E. and A.W. supervised the work.

### <span id="page-6-0"></span>**APPENDIX A: DEVICE PARAMETERS**

In Table I, we summarize the properties of the qubits on the two devices (A and B) with which the experiments

were performed, and indicate for which figure of the main text they were used.

## <span id="page-6-1"></span>APPENDIX B: AMPLITUDE CORRECTION WITH ERROR AMPLIFICATION

The excited-state population of the qubit after the application of a series of N  $\pi$  pulses [see Figs. 1(c)–1(e)] is fitted to a master equation model to extract the error in the rotation angle.

We model our measurement starting from the time-independent Hamiltonian  $H=\Omega\sigma_x/2$  describing rotations around the x axis of the Bloch sphere at the Rabi rate  $\Omega$ . The time evolution of the y and z components of the Bloch vector are captured by the Lindblad equation

<span id="page-6-3"></span>
$$\frac{d\rho(t)}{dt} = -i[H, \rho(t)] + \frac{\Gamma_{\phi}}{2} (\sigma_z \rho(t) \sigma_z - \rho(t)) + \Gamma_1 \left(\sigma_{-} \rho(t) \sigma_{+} - \frac{\sigma_{+} \sigma_{-} \rho(t) + \rho(t) \sigma_{+} \sigma_{-}}{2}\right)$$
(B1)

with  $\sigma_+ = |1\rangle\langle 0|$ ,  $\sigma_- = |0\rangle\langle 1|$ , the energy relaxation rate of the qubit  $\Gamma_1 = 1/T_1$ , and the dephasing rate  $\Gamma_{\phi} = 1/T_2 - 1/(2T_1)$ .

From Eq. (B1), we obtain the time evolution of the Bloch vector components of the qubit state in the y-z plane as [66]

$$\begin{pmatrix} \tilde{y}(t) \\ \tilde{z}(t) \end{pmatrix} = e^{-(3\Gamma_1 + 2\Gamma_\phi)t/4} \begin{pmatrix} \cos(\nu t) + \sin(\nu t)(\Gamma_1 - 2\Gamma_\phi)/4\nu & \sin(\nu t)\Omega/\nu \\ -\sin(\nu t)\Omega/\nu & \cos(\nu t) - \sin(\nu t)(\Gamma_1 - 2\Gamma_\phi)/4\nu \end{pmatrix} \begin{pmatrix} \tilde{y}(0) \\ \tilde{z}(0) \end{pmatrix},$$
 (B2)

where

$$\tilde{y}(t) = y(t) + \frac{2\Omega\Gamma_1}{\Gamma_1(\Gamma_1 + 2\Gamma_\phi) + 2\Omega^2},$$
 (B3)

$$\tilde{z}(t) = z(t) + \frac{\Gamma_1(\Gamma_1 + 2\Gamma_\phi)}{\Gamma_1(\Gamma_1 + 2\Gamma_\phi) + 2\Omega^2},$$
 (B4)

$$\nu = \sqrt{\Omega^2 - \frac{(\Gamma_1 - 2\Gamma_\phi)^2}{16}},\tag{B5}$$

and  $\tilde{y}(0), \tilde{z}(0)$  are the coordinates at the start of the evolution.

We apply Eq. (B2) to the qubit ground state (y(0) = 0, z(0) = -1), and then continue to apply this equation to the qubit state after each pulse in the *N*-pulse calibration measurement. We estimate the final qubit excited-state population as  $p_e = (1 + z(t))/2$ . Denoting the gate duration by  $\tau$ , we express  $\Omega = \alpha \pi/\tau$ , and extract the dimensionless fraction of a  $\pi$  rotation  $\alpha$  from a fit of the measured data to

<span id="page-6-4"></span> $p_e$ . The dephasing time  $T_2$  is also adjusted during the fit to capture the effects of the drive on the qubit dephasing; however, we keep the  $T_1$  time fixed to the experimental values shown in Table I.

<span id="page-6-2"></span>TABLE I. Qubit parameters, and their coherence, drive, and readout properties. The measurements in Figs. 1 and 4 were performed on device A, while those in Figs. 2 and 3 were done on device B.

|                                                     | Device A | Device B |
|-----------------------------------------------------|----------|----------|
| Qubit idle frequency $\omega_O/2\pi$ (GHz)          | 6.257    | 4.640    |
| Qubit anharmonicity $\alpha/2\pi$ (MHz)             | -153     | -183     |
| Lifetime $T_1$ ( $\mu$ s)                           | 12.3     | 60.9     |
| Ramsey decay time $T_2^*$ (µs)                      | 9.86     | 55.3     |
| Echo decay time $T_2^{\rm e}$ ( $\mu$ s)            | 14.7     | 67.3     |
| 15-ns $\pi$ -pulse amplitude $A_{\pi}$ (mV)         | 730      | 235      |
| Three-state readout error $\epsilon_{RO}^{(3)}$ (%) | 3        | 4        |

<span id="page-7-2"></span>![](_page_7_Figure_2.jpeg)

FIG. 5. (a) Simplified schematic of the room-temperature and measurement setups used to operate the qubits. Intermediate frequency pulses are generated with an AWG and up-converted to the gigahertz range using the conversion device indicated in red. This device contains an IQ mixer and an amplifier, and is the main source of nonlinearity in our drive line. We configure a switch to either send the pulses into the dilution refrigerator via the qubit drive line (path 1) or directly into the detection chain consisting of another IQ mixer, which down-converts the pulses into the frequency band of the detection device (path 2). (b) Measured qubit rotation angle as a function of the applied pulse amplitude relative to the  $\pi$ -pulse amplitude. The blue points are measured with the N-pulse calibration via path 1, and the black points are obtained from the amplitudes of the demodulated pulses measured via path 2 and converted to the same units. (c) Difference between the rotation angles in (b) and a linear interpolation between the last point and the origin. The lines in (b) and (c) are fits to the fifth-order polynomial in Eq. (1) of the main text.

Using the found value of  $\alpha$ , we calculate the pulse amplitude as  $A = \alpha A_{\pi}$ , where  $A_{\pi}$  is the amplitude of a  $\pi$  rotation.

# <span id="page-7-0"></span>APPENDIX C: SIGNAL NONLINEARITY DUE TO ELECTRONIC COMPONENTS

The response curves shown schematically in Fig. 1(b) and measured in Figs. 1(f)–1(i) are typical for electronic components such as mixers or amplifiers, which become nonlinear above a certain input power [29].

Here we verify that the nonlinearity observed with the N-pulse calibration originates mostly from the control electronics used for driving the qubits. We perform the measurements on a different setup than those presented in the main text, but with nominally identical control electronics. We use slightly longer 50-ns DRAG pulses, with a  $\sigma = 10$ -ns standard deviation of the Gaussian envelope truncated at  $\pm 2.5\sigma$ . The pulses are generated at an intermediate frequency of -100 MHz before up-conversion to the qubit frequency using a circuit that consists of an IQ mixer and amplifiers [see the red outline in the schematic in Fig. 5(a)]. We choose to either apply the pulses to the qubit and perform the N-pulse calibration [path 1 in Fig. 5(a)] or we directly down-convert the pulses to an intermediate frequency of 200 MHz before detecting the quadratures of the signal (path 2). The signal for path 2 is attenuated by -20 dB to ensure that the down-conversion mixer and subsequent amplifiers are operated in their linear regime. We

then demodulate the signal to dc, filter out spurious frequency components larger than the spectral width of the pulse, and extract the amplitudes of the resulting pulses. These data are then converted to a rotation angle [see the black squares in Fig. 5(b)] for better comparison to the results obtained with the N-pulse calibration via path 1 (blue circles).

We find that the nonlinear scaling of the Rabi angle with the pulse amplitude identified with the N-pulse calibration technique originates mostly from our frequency conversion device; see Fig. 5(c), where we plot the difference between the measured data points in Fig. 5(b) and a linear interpolation between the origin and the last data point. However, the results obtained via path 2 systematically overestimate those measured using the qubit by about  $0.2^{\circ}$  at an amplitude ratio of 0.5, showing that the room-temperature calibration presented here cannot fully replace the *in situ* calibration presented in the main text.

### <span id="page-7-1"></span>APPENDIX D: PURITY BENCHMARKING

In order to distinguish between incoherent and control errors, we use a simple extension of the randomized benchmarking protocol known as purity benchmarking. Purity benchmarking consists of performing tomography of the qubit state vector after each random sequence of Clifford gates [45,56]. This is illustrated by the schematic in Fig. 6(a), where the orange block consists of the single-qubit tomography pulses I (identity),  $X_{\pi/2}$ , and  $Y_{\pi/2}$ . We

<span id="page-8-1"></span>![](_page_8_Figure_2.jpeg)

FIG. 6. RB and PB with the 40-ns single-qubit gate shown in Fig. 2. (a) Schematic illustration of the PB experiment. (b) Average expectation value of the  $\sigma_z$  operator (blue), and the average of the square root of the sequence purity  $\sqrt{\mathcal{P}}$  (orange) as a function of the number of Clifford gates. The lines are fits to the exponential decay functions in Eq. (D2). (c) The f-state population as a function of the number of Clifford gates (points) with a fit to the rate equation (D4) (line). The error bars in (b) and (c) represent one standard deviation of the distribution of outcomes of the random sequences for a fixed number of Clifford gates.

estimate the purity of the state after each random sequence as

$$\mathcal{P} = \langle \sigma_x \rangle^2 + \langle \sigma_y \rangle^2 + \langle \sigma_z \rangle^2, \tag{D1}$$

and compute the mean of this quantity over the random sequences for a fixed number of Clifford gates.

In Fig. 6(b) we show the exponential decay of the  $\langle \sigma_z \rangle$  operator (blue) from the RB measurement of the 40-ns gate in Fig. 2 of the main text calibrated with the *N*-pulse technique. We compare this decay to the decay of  $\langle \sqrt{\mathcal{P}} \rangle$  (orange) from the corresponding PB experiment. In the absence of control errors, the two curves should coincide.

For RB and PB, respectively, we fit to

$$\langle \sigma_z \rangle(m) = A\alpha^m + B,$$
  
 $\langle \mathcal{P} \rangle(m) = A'u^m + B',$ 
(D2)

where m is the number of Clifford gates,  $\alpha$  is the depolarization parameter [44], u is the unitarity [45], and A, A', B, B' are fit parameters capturing state preparation and measurement errors. The total average error per gate and the average incoherent error per gate are then respectively calculated as

$$E = \frac{1 - \alpha}{2N},$$

$$E_{\text{inc}} = \frac{1 - \sqrt{u}}{2N},$$
(D3)

where N = 1.125 is the average number of physical gates per Clifford in the HZ decomposition [57]. The virtual Z

gates are implemented in software by a qubit phase update, and hence it has perfect fidelity. Subtracting these two quantities gives an estimate of the coherent control error per gate,  $E_{\rm coh} = E - E_{\rm inc}$ .

The analysis described above is performed after discriminating between the qubit subspace and leakage, and normalizing the qubit populations so that they add up to one. In Fig. 6(c), we show the average f-state population as a function of the RB sequence length (points). We fit these data to the rate equation [22]

<span id="page-8-3"></span>
$$p_f(m) = \frac{l}{l+s} (1 - e^{-(l+s)m}) + p_0 e^{-(l+s)m},$$
 (D4)

from which we find the average leakage per gate, L = l/N. Here, s is the decay rate into the computational subspace and  $p_0$  is the initial f -state population.

From the data shown in Fig. 6, we extract a leakage rate per gate of around  $1.1(1) \times 10^{-5}$ , and a total average gate error of  $4.4(2) \times 10^{-4}$ , which is limited by decoherence at around  $4.1(1) \times 10^{-4}$ .

### <span id="page-8-0"></span>APPENDIX E: CROSS-ENTROPY BENCHMARKING

To benchmark the performance of gates that do not belong to the Clifford group, such as arbitrary-rotation single-qubit gates, we use the XEB technique [20,46,60]. In the XEB protocol, sequences of random cycles of gates are applied to a system prepared in a chosen state (typically the ground state). The only requirement to take into consideration when choosing the cycle design is that sequences with enough cycles should fully explore the Hilbert space of the system [46].

The average sequence fidelity is estimated by comparing the distribution of measured outcomes  $Q_{\text{meas}}$  to the calculated, ideal distribution  $Q_{\text{ideal}}$  using the cross-entropy as a metric of overlap. The cross-entropy between two distributions Q and R is given by

$$S(Q,R) = -\sum_{i} q_{i} \ln(r_{i}), \tag{E1}$$

<span id="page-8-2"></span>where  $q_i$ ,  $r_i$  are samples from distributions Q, R. For a fixed number of cycles, we estimate the average XEB sequence fidelity of a distribution of random sequence outcomes as [20]

$$F_{\text{XEB}} = \frac{S(Q_{\text{incoh}}, Q_{\text{ideal}}) - S(Q_{\text{meas}}, Q_{\text{ideal}})}{S(Q_{\text{incoh}}, Q_{\text{ideal}}) - S(Q_{\text{ideal}}, Q_{\text{ideal}})}.$$
 (E2)

Here,  $Q_{\rm incoh}$  is the incoherent distribution where all the bit strings have an equal probability of  $1/2^n$  (with n=1 for one qubit), and  $Q_{\rm meas}$  and  $Q_{\rm ideal}$  are the measured and calculated distributions of probabilities  $(p_g,p_e)_i$  describing the qubit state at the end of each random sequence i.

To constrain  $F_{\text{XEB}}$  between 0 and 1, we normalize  $Q_{\text{incoh}}$ ,  $Q_{\text{meas}}$ , and  $Q_{\text{ideal}}$  by the total number of random sequences for a fixed number of cycles.

From the variance of the measured probability distribution, we also estimate the average purity of the final qubit state as [60]

$$\mathcal{P} = \frac{\text{Var}(Q_{\text{meas}})}{\text{Var}(Q_{\text{PT}})},\tag{E3}$$

where  $Var(Q_{PT}) = (2^n - 1)/(2^{2n}(2^n + 1))$  is the variance of the Porter-Thomas distribution, with n = 1 for a single qubit.

The points in Fig. 7(a) show the exponential decays of the XEB fidelity (blue) and the square root of the sequence purity (orange) for the purple point in Fig. 3 of the main text, corresponding to an X gate of angle  $5\pi/6$ . The lines are fits to

$$F_{\text{XEB}}(m) = A \left( 1 - \frac{2^n}{2^n - 1} E \right)^m + B,$$

$$\sqrt{\mathcal{P}}(m) = A' \left( 1 - \frac{2^n}{2^n - 1} E_{\text{inc}} \right)^m + B',$$
(E4)

from which we estimate the total average errors per cycle E, and the average incoherent errors per cycle  $E_{\rm inc}$ . Here m is the number of cycles, and A, A', B, B' are fit parameters capturing the state preparation and measurement errors. We then calculate the amount of coherent control errors per cycle as  $E_{\rm coh} = E - E_{\rm inc}$ . Since both cycle designs chosen for this work (see Figs. 3 and 4) contain only one physical gate, E,  $E_{\rm inc}$ , and  $E_{\rm coh}$  quantify the average errors per gate. From the data set in Fig. 7(a), we find a total average gate error of  $6.3(3) \times 10^{-4}$ , with a contribution from decoherence errors of  $5.6(2) \times 10^{-4}$ , giving around  $8(3) \times 10^{-5}$  control errors.

The analysis described above is performed after discriminating between the qubit subspace and leakage, and normalizing the qubit populations so that they add up to one. In Fig. 7(b), we show the average f -state population (points) as a function of the XEB sequence length, and a fit to the rate equation in Eq. (D4) (line), from which we extract an average leakage rate per gate of around  $9.5(7) \times 10^{-5}$ .

- <span id="page-9-0"></span>[1] A. Blais, A. L. Grimsmo, S. M. Girvin, and A. Wallraff, Circuit quantum electrodynamics, Rev. Mod. Phys. **93**, 025005 (2021).
- <span id="page-9-7"></span>[2] M. Kjaergaard, M. E. Schwartz, J. Braumüller, P. Krantz, J. I.-J. Wang, S. Gustavsson, and W. D. Oliver, Superconducting qubits: Current state of play, Annu. Rev. Condens. Matter Phys. 11, 369 (2020).

<span id="page-9-9"></span>![](_page_9_Figure_12.jpeg)

FIG. 7. XEB with the 15-ns single-qubit  $X_{5\pi/6}$  gate shown in Fig. 6. (a) Average XEB sequence fidelity  $F_{\rm XEB}$  (blue) and the square root of the average sequence purity  $\sqrt{\mathcal{P}}$  (orange) as a function of the number of cycles. The lines are fits to the exponential decay functions in Eq. (E4). (b) The f-state population as a function of the number of cycles (points) with a fit to the rate equation (D4) (line). The error bars represent one standard deviation of the distribution of outcomes of the random sequences for a fixed number of cycles.

- <span id="page-9-10"></span><span id="page-9-1"></span>[3] G. Wendin, Quantum information processing with superconducting circuits: A review, Rep. Prog. Phys. **80**, 106001 (2017).
- <span id="page-9-2"></span>[4] J. Kelly, *et al.*, State preservation by repetitive error detection in a superconducting quantum circuit, Nature **519**, 66 (2015).
- [5] C. K. Andersen, A. Remm, S. Lazar, S. Krinner, N. Lacroix, G. J. Norris, M. Gabureac, C. Eichler, and A. Wallraff, Repeated quantum error detection in a surface code, Nat. Phys. 16, 875 (2020).
- [6] J. F. Marques, B. M. Varbanov, M. S. Moreira, H. Ali, N. Muthusubramanian, C. Zachariadis, F. Battistel, M. Beekman, N. Haider, W. Vlothuizen, A. Bruno, B. M. Terhal, and L. DiCarlo, Logical-qubit operations in an error-detecting surface code, Nat. Phys. 18, 80 (2021).
- <span id="page-9-8"></span>[7] S. Krinner, N. Lacroix, A. Remm, A. D. Paolo, E. Genois, C. Leroux, C. Hellings, S. Lazar, F. Swiadek, J. Herrmann, G. J. Norris, C. K. Andersen, M. Müller, A. Blais, C. Eichler, and A. Wallraff, Realizing repeated quantum error correction in a distance-three surface code, Nature 605, 669 (2022).
- <span id="page-9-3"></span>[8] Z. Chen, *et al.*, Exponential suppression of bit or phase errors with cyclic error correction, Nature **595**, 383 (2021).
- <span id="page-9-4"></span>[9] A. Kandala, A. Mezzacapo, K. Temme, M. Takita, M. Brink, J. M. Chow, and J. M. Gambetta, Hardware-efficient variational quantum eigensolver for small molecules and quantum magnets, Nature **549**, 242 (2017).
- <span id="page-9-5"></span>[10] N. Lacroix, C. Hellings, C. K. Andersen, A. Di Paolo, A. Remm, S. Lazar, S. Krinner, G. J. Norris, M. Gabureac, J. Heinsoo, A. Blais, C. Eichler, and A. Wallraff, Improving the Performance of Deep Quantum Optimization Algorithms with Continuous Gate Sets, PRX Quantum 1, 020304 (2020).
- <span id="page-9-6"></span>[11] Y. Salathé, M. Mondal, M. Oppliger, J. Heinsoo, P. Kurpiers, A. Potočnik, A. Mezzacapo, U. Las Heras, L. Lamata, E. Solano, S. Filipp, and A. Wallraff, Digital Quantum Simulation of Spin Models with Circuit Quantum Electrodynamics, Phys. Rev. X 5, 021027 (2015).

- [12] R. Barends, *et al.*, Digitized adiabatic quantum computing with a superconducting circuit, Nature **534**[, 222 \(2016\).](https://doi.org/http://dx.doi.org/10.1038/nature17658)
- <span id="page-10-0"></span>[13] F. Arute, *et al.*, Observation of separated dynamics of charge and spin in the Fermi-Hubbard model, [ArXiv:2010.07965](https://arxiv.org/abs/2010.07965) (2020).
- <span id="page-10-1"></span>[14] D. C. McKay, S. Sheldon, J. A. Smolin, J. M. Chow, and J. M. Gambetta, Three-Qubit Randomized Benchmarking, Phys. Rev. Lett. **122**[, 200502 \(2019\).](https://doi.org/10.1103/PhysRevLett.122.200502)
- [15] K. Rudinger, T. Proctor, D. Langharst, M. Sarovar, K. Young, and R. Blume-Kohout, Probing Context-Dependent [Errors in Quantum Processors,](https://doi.org/10.1103/PhysRevX.9.021045) Phys. Rev. X **9**, 021045 (2019).
- [16] M. Sarovar, T. Proctor, K. Rudinger, K. Young, E. Nielsen, and R. Blume-Kohout, Detecting crosstalk errors in quantum information processors, Quantum **4**[, 321 \(2020\).](https://doi.org/10.22331/q-2020-09-11-321)
- [17] D. C. McKay, A. W. Cross, C. J. Wood, and J. M. Gambetta, Correlated randomized benchmarking, [ArXiv:2003.02354](https://arxiv.org/abs/2003.02354) (2020).
- [18] S. Krinner, S. Lazar, A. Remm, C. Andersen, N. Lacroix, G. Norris, C. Hellings, M. Gabureac, C. Eichler, and A. Wallraff, Benchmarking Coherent Errors in Controlled-[Phase Gates Due to Spectator Qubits,](https://doi.org/10.1103/PhysRevApplied.14.024042) Phys. Rev. Appl. **14**, 024042 (2020).
- <span id="page-10-2"></span>[19] R. Barends, *et al.*, Diabatic Gates for Frequency-Tunable [Superconducting Qubits,](https://doi.org/10.1103/PhysRevLett.123.210501) Phys. Rev. Lett. **123**, 210501 (2019).
- <span id="page-10-3"></span>[20] B. Foxen, *et al.*, Demonstrating a Continuous Set of Two-[Qubit Gates for Near-Term Quantum Algorithms,](https://doi.org/10.1103/physrevlett.125.120504) Phys. Rev. Lett. **125**, 120504 (2020).
- <span id="page-10-4"></span>[21] J. Herrmann, S. M. Llima, A. Remm, P. Zapletal, N. A. McMahon, C. Scarato, F. Swiadek, C. K. Andersen, C. Hellings, S. Krinner, N. Lacroix, S. Lazar, M. Kerschbaum, D. C. Zanuz, G. J. Norris, M. J. Hartmann, A. Wallraff, and C. Eichler, Realizing quantum convolutional neural networks on a superconducting quantum proces[sor to recognize quantum phases,](https://doi.org/10.1038/s41467-022-31679-5) Nat. Commun. **13**, 4144 (2022).
- <span id="page-10-5"></span>[22] Z. Chen, *et al.*, Measuring and Suppressing Quantum State [Leakage in a Superconducting Qubit,](https://doi.org/10.1103/PhysRevLett.116.020501) Phys. Rev. Lett. **116**, 020501 (2016).
- [23] J. Kelly, P. OMalley, M. Neeley, H. Neven, and J. M. Martinis, Physical qubit calibration on a directed acyclic graph, [ArXiv:1803.03226](https://arxiv.org/abs/1803.03226) (2018).
- [24] P. Krantz, M. Kjaergaard, F. Yan, T. P. Orlando, S. Gustavsson, and W. D. Oliver, A quantum engineer's guide to superconducting qubits, [Appl. Phys. Rev.](https://doi.org/10.1063/1.5089550) **6**, 021318 (2019).
- <span id="page-10-6"></span>[25] Y. Xu, G. Huang, J. Balewski, R. K. Naik, A. Morvan, B. Mitchell, K. Nowrouzi, D. I. Santiago, and I. Siddiqi, Automatic qubit characterization and gate optimization with qubic, [ArXiv:2104.10866](https://arxiv.org/abs/2104.10866) (2021).
- <span id="page-10-7"></span>[26] J. Herrmann, C. Hellings, S. Lazar, F. Pfäffli, F. Haupt, T. Thiele, D. C. Zanuz, G. J. Norris, F. Heer, C. Eichler, and A. Wallraff, Frequency up-conversion schemes for controlling superconducting qubits, [ArXiv:2210.02513](https://arxiv.org/abs/2210.02513) (2022).
- [27] S. W. Jolin, R. Borgani, M. O. Tholén, D. Forchheimer, and D. B. Haviland, Calibration of mixer amplitude and phase [imbalance in superconducting circuits,](https://doi.org/10.1063/5.0025836) Rev. Sci. Instrum.
- <span id="page-10-8"></span>**91**, 124707 (2020). [28] Y. Xu, G. Huang, D. I. Santiago, and I. Siddiqi, Radio frequency mixing modules for superconducting qubit room

- [temperature control systems,](https://doi.org/10.1063/5.0055906) Rev. Sci. Instrum. **92**, 075108 (2021).
- <span id="page-10-9"></span>[29] J. C. Pedro, D. E. Root, J. Xu, and L. C. Nunes, in *Nonlinear Circuit Simulation and Modeling: Fundamentals for Microwave Design*, The Cambridge RF and Microwave Engineering Series (Cambridge University Press, Cambridge, United Kingdom, 2018) p. 1.
- <span id="page-10-10"></span>[30] K. R. Chaves, X. Wu, Y. J. Rosen, and J. L. DuBois, Nonlinear signal distortion corrections through quantum sensing, [Appl. Phys. Lett.](https://doi.org/10.1063/5.0035712) **118**, 014001 (2021).
- <span id="page-10-11"></span>[31] J. M. Gambetta, J. M. Chow, and M. Steffen, Building logical qubits in a superconducting quantum computing system, [npj Quantum Inf.](https://doi.org/10.1038/s41534-016-0004-0) **3**, 2 (2017).
- <span id="page-10-12"></span>[32] V. Negirneac, H. Ali, N. Muthusubramanian, F. Battistel, R. Sagastizabal, M. S. Moreira, J. F. Marques, W. J. Vlothuizen, M. Beekman, C. Zachariadis, N. Haider, A. Bruno, and L. DiCarlo, High-Fidelity Controlled-*z* Gate with Maximal Intermediate Leakage Operating at the Speed [Limit in a Superconducting Quantum Processor,](https://doi.org/10.1103/PhysRevLett.126.220502) Phys. Rev. Lett. **126**, 220502 (2021).
- <span id="page-10-18"></span>[33] Q. Ficheux, L. B. Nguyen, A. Somoroff, H. Xiong, K. N. Nesterov, M. G. Vavilov, and V. E. Manucharyan, Fast Logic with Slow Qubits: Microwave-Activated Controlled-*<sup>Z</sup>* [Gate on Low-Frequency Fluxoniums,](https://doi.org/10.1103/PhysRevX.11.021026) Phys. Rev. X **11**, 021026 (2021).
- [34] Y. Sung, L. Ding, J. Braumüller, A. Vepsäläinen, B. Kannan, M. Kjaergaard, A. Greene, G. O. Samach, C. McNally, D. Kim, A. Melville, B. M. Niedzielski, M. E. Schwartz, J. L. Yoder, T. P. Orlando, S. Gustavsson, and W. D. Oliver, Realization of High-Fidelity CZ and *ZZ*-Free iSWAP Gates with a Tunable Coupler, Phys. Rev. X **11**[, 021058 \(2021\).](https://doi.org/10.1103/PhysRevX.11.021058)
- [35] A. Kandala, K. X. Wei, S. Srinivasan, E. Magesan, S. Carnevale, G. A. Keefe, D. Klaus, O. Dial, and D. C. McKay, Demonstration of a High-Fidelity CNOT Gate for Fixed-Frequency Transmons with Engineered *ZZ* Suppression, Phys. Rev. Lett. **127**[, 130501 \(2021\).](https://doi.org/10.1103/PhysRevLett.127.130501)
- <span id="page-10-13"></span>[36] K. X. Wei, E. Magesan, I. Lauer, S. Srinivasan, D. F. Bogorin, S. Carnevale, G. A. Keefe, Y. Kim, D. Klaus, W. Landers, N. Sundaresan, C. Wang, E. J. Zhang, M. Steffen, O. E. Dial, D. C. McKay, and A. Kandala, Quantum crosstalk cancellation for fast entangling gates and improved multi-qubit performance, [ArXiv:2106.00675](https://arxiv.org/abs/2106.00675) (2021).
- <span id="page-10-14"></span>[37] J. Bylander, S. Gustavsson, F. Yan, F. Yoshihara, K. Harrabi, G. Fitch, D. G. Cory, Y. Nakamura, Jaw-Shen Tsai, and W. D. Oliver, Noise spectroscopy through dynamical [decoupling with a superconducting flux qubit,](https://doi.org/doi:10.1038/nphys1994) Nat. Phys. **7**, 565 (2011).
- <span id="page-10-15"></span>[38] H. Y. Carr and E. M. Purcell, Effects of diffusion on free precession in nuclear magnetic resonance experiments, Phys. Rev. **94**[, 630 \(1954\).](https://doi.org/10.1103/PhysRev.94.630)
- <span id="page-10-16"></span>[39] S. Gustavsson, O. Zwier, J. Bylander, F. Yan, F. Yoshihara, Y. Nakamura, T. P. Orlando, and W. D. Oliver, Improving Quantum Gate Fidelities by Using a Qubit to Measure [Microwave Pulse Distortions,](https://doi.org/http://link.aps.org/doi/10.1103/PhysRevLett.110.040502) Phys. Rev. Lett. **110**, 040502 (2013).
- <span id="page-10-17"></span>[40] M. A. Rol, L. Ciorciaro, F. K. Malinowski, B. M. Tarasinski, R. E. Sagastizabal, C. C. Bultink, Y. Salathe, N. Haandbaek, J. Sedivy, and L. DiCarlo, Time-domain characterization and correction of on-chip distortion of

- control pulses in a quantum processor, Appl. Phys. Lett. **116**, 054001 (2020).
- <span id="page-11-0"></span>[41] M. Werninghaus, D. J. Egger, F. Roy, S. Machnes, F. K. Wilhelm, and S. Filipp, Leakage reduction in fast superconducting qubit gates via optimal control, npj Quantum Inf. 7, 14 (2021).
- <span id="page-11-1"></span>[42] J. Singh, R. Zeier, T. Calarco, and F. Motzoi, Compensating for non-linear distortions in controlled quantum systems, ArXiv:2210.07833 (2022).
- <span id="page-11-2"></span>[43] J. Koch, T. M. Yu, J. Gambetta, A. A. Houck, D. I. Schuster, J. Majer, A. Blais, M. H. Devoret, S. M. Girvin, and R. J. Schoelkopf, Charge-insensitive qubit design derived from the Cooper pair box, Phys. Rev. A 76, eid 042319 (2007).
- <span id="page-11-3"></span>[44] E. Magesan, J. M. Gambetta, and J. Emerson, Scalable and Robust Randomized Benchmarking of Quantum Processes, Phys. Rev. Lett. **106**, 180504 (2011).
- <span id="page-11-4"></span>[45] J. Wallman, C. Granade, R. Harper, and S. T. Flammia, Estimating the coherence of noise, New J. Phys. 17, 113020 (2015).
- <span id="page-11-5"></span>[46] S. Boixo, S. V. Isakov, V. N. Smelyanskiy, R. Babbush, N. Ding, Z. Jiang, M. J. Bremner, J. M. Martinis, and H. Neven, Characterizing quantum supremacy in near-term devices, Nat. Phys. 14, 595 (2018).
- <span id="page-11-6"></span>[47] S. Asaad, C. Dickel, N. K. Langford, S. Poletto, A. Bruno, M. A. Rol, D. Deurloo, and L. DiCarlo, Independent, extensible control of same-frequency superconducting qubits by selective broadcasting, Npj Quantum Inf. 2, 16029 (2016).
- [48] S. Sheldon, L. S. Bishop, E. Magesan, S. Filipp, J. M. Chow, and J. M. Gambetta, Characterizing errors on qubit operations via iterative randomized benchmarking, Phys. Rev. A 93, 012301 (2016).
- <span id="page-11-7"></span>[49] J. M. Chow, Ph.D. thesis, Yale University, 2010.
- <span id="page-11-8"></span>[50] F. Motzoi, J. M. Gambetta, P. Rebentrost, and F. K. Wilhelm, Simple Pulses for Elimination of Leakage in Weakly Nonlinear Qubits, Phys. Rev. Lett. 103, eid 110501 (2009).
- <span id="page-11-9"></span>[51] J. M. Gambetta, F. Motzoi, S. T. Merkel, and F. K. Wilhelm, Analytic control methods for high-fidelity unitary operations in a weakly nonlinear oscillator, Phys. Rev. A 83, 012308 (2011).
- <span id="page-11-10"></span>[52] J. M. Chow, L. DiCarlo, J. M. Gambetta, F. Motzoi, L. Frunzio, S. M. Girvin, and R. J. Schoelkopf, Optimized driving of superconducting artificial atoms for improved single-qubit gates, Phys. Rev. A 82, 040305 (2010).
- <span id="page-11-11"></span>[53] J. M. Martinis and M. R. Geller, Fast adiabatic qubit gates using only  $\sigma_z$  control, Phys. Rev. A **90**, 022307 (2014).
- <span id="page-11-12"></span>[54] E. Magesan, J. M. Gambetta, B. R. Johnson, C. A. Ryan, J. M. Chow, S. T. Merkel, M. P. da Silva, G. A. Keefe, M. B.

- Rothwell, T. A. Ohki, M. B. Ketchen, and M. Steffen, Efficient Measurement of Quantum Gate Error by Interleaved Randomized Benchmarking, Phys. Rev. Lett. **109**, 080505 (2012).
- <span id="page-11-13"></span>[55] J. M. Epstein, A. W. Cross, E. Magesan, and J. M. Gambetta, Investigating the limits of randomized benchmarking protocols, Phys. Rev. A 89, 062321 (2014).
- <span id="page-11-14"></span>[56] G. Feng, J. J. Wallman, B. Buonacorsi, F. H. Cho, D. K. Park, T. Xin, D. Lu, J. Baugh, and R. Laflamme, Estimating the Coherence of Noise in Quantum Control of a Solid-State Qubit, Phys. Rev. Lett. 117, 260501 (2016).
- <span id="page-11-15"></span>[57] D. C. McKay, C. J. Wood, S. Sheldon, J. M. Chow, and J. M. Gambetta, Efficient *Z* gates for quantum computing, Phys. Rev. A **96**, 022330 (2017).
- <span id="page-11-16"></span>[58] R. C. Bialczak, M. Ansmann, M. Hofheinz, E. Lucero, M. Neeley, A. D. O'Connell, D. Sank, H. Wang, J. Wenner, M. Steffen, A. N. Cleland, and J. M. Martinis, Quantum process tomography of a universal entangling gate implemented with Josephson phase qubits, Nat. Phys. 6, 409 (2010).
- <span id="page-11-17"></span>[59] P. Magnard, P. Kurpiers, B. Royer, T. Walter, J.-C. Besse, S. Gasparinetti, M. Pechal, J. Heinsoo, S. Storz, A. Blais, and A. Wallraff, Fast and Unconditional All-Microwave Reset of a Superconducting Qubit, Phys. Rev. Lett. 121, 060502 (2018).
- <span id="page-11-18"></span>[60] F. Arute, *et al.*, Quantum supremacy using a programmable superconducting processor, Nature **574**, 505 (2019).
- <span id="page-11-19"></span>[61] I. N. Hincks, C. E. Granade, T. W. Borneman, and D. G. Cory, Controlling Quantum Devices with Nonlinear Hardware, Phys. Rev. Appl. 4, 024012 (2015).
- <span id="page-11-20"></span>[62] E. Lucero, J. Kelly, R. C. Bialczak, M. Lenander, M. Mariantoni, M. Neeley, A. D. O'Connell, D. Sank, H. Wang, M. Weides, J. Wenner, T. Yamamoto, A. N. Cleland, and J. M. Martinis, Reduced phase error through optimized control of a superconducting qubit, Phys. Rev. A 82, 042339 (2010).
- <span id="page-11-21"></span>[63] A. Somoroff, Q. Ficheux, R. A. Mencia, H. Xiong, R. V. Kuzmin, and V. E. Manucharyan, Millisecond coherence in a superconducting qubit, ArXiv:2103.08578 (2021).
- [64] F. Liu, M. Chen, C. Wang, S. Li, Z. Shang, C. Ying, J. Wang, C. Peng, X. Zhu, C. Lu, and J. Pan, Quantum design for advanced qubits, ArXiv:2109.00994 (2021).
- <span id="page-11-22"></span>[65] E. Hyyppä, et al., Unimon qubit, Nat. Commun. 13, 6895 (2022).
- <span id="page-11-23"></span>[66] Q. Ficheux, S. Jezouin, Z. Leghtas, and B. Huard, Dynamics of a qubit while simultaneously monitoring its relaxation and dephasing, Nat. Commun. 9, 1926 (2018).