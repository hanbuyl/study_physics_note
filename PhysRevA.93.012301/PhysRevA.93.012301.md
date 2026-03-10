## PHYSICAL REVIEW A **93**, 012301 (2016)

## **Characterizing errors on qubit operations via iterative randomized benchmarking**

Sarah Sheldon, Lev S. Bishop, Easwar Magesan, Stefan Filipp, Jerry M. Chow, and Jay M. Gambetta *IBM T.J. Watson Research Center, Yorktown Heights, New York 10598, USA* (Received 27 April 2015; published 4 January 2016)

With improved gate calibrations reducing unitary errors, we achieve a benchmarked single-qubit gate fidelity of 0*.*9995 ± 0*.*0002 with superconducting qubits in a circuit quantum electrodynamics system. We present a method for distinguishing between unitary and nonunitary errors in quantum gates by interleaving repetitions of a target gate within a randomized benchmarking sequence. The benchmarking fidelity decays quadratically with the number of interleaved gates for unitary errors but linearly for nonunitary errors, allowing us to separate systematic coherent errors from decoherent effects. With this protocol, we show that the fidelity of the gates is not limited by unitary errors.

DOI: [10.1103/PhysRevA.93.012301](http://dx.doi.org/10.1103/PhysRevA.93.012301)

Accurate characterization of control gates is an essential task for developing any quantum computing device. Quantum process tomography (QPT) [\[1–3\]](#page-4-0) has been the standard method for characterizing quantum gates because, ideally, it produces a full reconstruction of the quantum process. In practice, however, QPT suffers from many drawbacks, the most inimical being its exponential scaling in the number of quantum bits (qubits) comprising the system and that it is limited by state preparation and measurement (SPAM) errors. Various methods such as randomized benchmarking (RB) [\[4–7\]](#page-4-0) and gate set tomography (GST) [\[8,9\]](#page-4-0) have recently been developed to help overcome these limitations. RB is both insensitive to SPAM errors and efficient [\[10\]](#page-4-0). However, it only extracts a single piece of information, i.e., the average gate fidelity. GST, on the other hand, helps to overcome limitations from SPAM errors by reconstructing an entire library of gates in a self-consistent manner. The price paid for this self-consistent reconstruction is an even worse scaling than QPT.

As control calibration techniques continue to improve and quantum gates approach the fidelity required for fault-tolerant quantum computation, it becomes both important and difficult to verify the presence of increasingly small errors. Error verification constitutes a critical first step in a debugging routine since different physical mechanisms can lead to different error types. QPT and GST are often poor choices for error verification since they are time consuming and contain so much information that backing out the presence of specific error types on small scales can be a challenge in itself. In addition, SPAM errors in QPT set a lower limit on the detectable error strengths [\[8\]](#page-4-0). At the other end of the spectrum, while standard RB is efficient, the information it contains about the gate is typically not enough to perform any sort of useful error verification. An extension of standard RB, i.e., interleaved randomized benchmarking, consists of interleaving a target gate in a benchmarking sequence and provides bounds on the error for the gate of interest [\[11,12\]](#page-4-0). Interleaved benchmarking can identify gates that are poorly calibrated, but does not reveal if the errors are due to decoherence, over- or under-rotations, or off-resonance effects, among other error types. Thus, fast and reliable routines that determine the presence of specific error types are required. Others have proposed to use RB for measuring the unital part of a quantum map [\[13\]](#page-4-0), correlated errors on a multiqubit space [\[14\]](#page-4-0), metrology of phase noise [\[15\]](#page-4-0), and, recently, the authors of Ref. [\[16\]](#page-5-0) have described an alternative method for measuring unitary errors.

In this paper, we propose and experimentally implement a protocol, largely based on the ideas of RB, that verifies the presence of unitary versus nonunitary errors. More specifically, this method distinguishes unitary errors that are additive, such as over-rotation errors, but does not detect other types of unitary errors. Axes errors, for example, would be undetectable unless converted into an angle error through a combination of gates, as we demonstrate experimentally here. Such additive errors do include many types of calibration errors that would be present in a physical system, so any method capable of detecting such errors has a practical utility in experimental settings.

A major source of unitary errors in transmon qubits originates from the presence of higher levels, which can be removed by the derivative removal via adiabatic gate (DRAG) protocol [\[17\]](#page-5-0). To quantify this error source, we compare experimental randomized benchmarking fidelities for several gate times with two simulations, one assuming a DRAG-corrected pulse shape and the other without DRAG (Fig. [1\)](#page-1-0).

The measurements described here are performed on a two-qubit sample consisting of two transmon qubits coupled by a coplanar waveguide resonator, with independent readout resonators for each qubit. The qubit of interest has a transition frequency of 5*.*0154 GHz and anharmonicity of *δ/*2*π* = −323 MHz. *T*<sup>1</sup> and *T*<sup>2</sup> are 45 ± 6 *μ*s and 53 ± 10 *μ*s, respectively. These characteristic times are the mean values from 500 measurements taken over 14 hours, and the error bars are the standard deviation of this data; each independent experiment is well fit by an exponential decay. The pulses used in the RB sequence are truncated Gaussian pulses having total length equal to four times the standard deviation of the Gaussian and with the DRAG correction applied to the quadrature component.

The weak anharmonicity *δ* of the transmon limits the gate fidelity as 1*/δ*, which can be seen for short gate times in Fig. [1.](#page-1-0) The experimental data falls below the non-DRAG curve (brown dotted line in Fig. [1\)](#page-1-0), showing that we have partially removed unitary errors due to the presence of higher levels in the transmon. At the gate length *tg* = 16*.*7 ns, the error rate corresponds to an average fidelity per gate of 0*.*9995 ± 0*.*0002,

<span id="page-1-0"></span>![](_page_1_Figure_2.jpeg)

FIG. 1. (a) Randomized benchmarking fidelity as a function of gate length. Simulated fidelity with (solid blue line) and without (dotted brown line) a DRAG correction. Experimental data (points) with the highest fidelity of  $0.9995 \pm 0.0002$  occurring at 16.7 ns. Dashed black line: simulated fidelity when all gates are over-rotated by  $\pi/64$  (which would be detectable by IRB). Green dot-dashed line: simulated fidelity with gate-dependent dephasing proportional to the drive amplitude  $\gamma_{\phi} = k\Omega$ . (b) The iterative benchmarking sequence with target gate C repeated n times between random Clifford gates,  $C_i$ . The case n=0 corresponds to a regular randomized benchmarking sequence, as used for the data in (a).

but is not yet limited by  $T_1$  and  $T_2$  with the DRAG correction (blue solid line). With the current of control, we can calibrate pulses to within a factor of four of the limit set by  $T_1$  and  $T_2$ , but it is clear that there are still errors remaining in the system. (The remaining simulations in Fig. 1 will be described later in this text.)

For longer pulses, the fidelity is limited by the finite coherence time of the qubit. The tradeoff between decoherence and unitary errors shown in Fig. 1 is generic across quantum computing hardware. For optimal fidelity, any quantum processor will be operating with fidelity at least partially limited by unitary errors: if this were not the case, then the fidelity could surely be improved by shortening the gate time.

We achieve high-fidelity gates through a set of microwave pulse calibrations, which we describe here before demonstrating our method for detecting errors that remain after calibration. We use single sideband (SSB) modulation of our control pulses and adjust the in-phase quadrature (IQ) mixers (MITEQ IRM0408LC2Q) for the chosen intermodulation frequency (IF) to ensure that only the correct sideband is produced with minimal leakage at the carrier frequency. We then calibrate the in-phase control pulse amplitude and the amplitude of the quadrature component for the DRAG correction. The pulse amplitudes for a  $\pi$  pulse  $(X_{\pi/2})$  and a  $\pi/2$  pulse  $(X_{\pi/2})$  about the x axis are tuned up by repeating the pulses in the sequence  $X_{\pi/2} - (X_{\{\pi,\pi/2\}})^{2n}$  in order to amplify

![](_page_1_Figure_7.jpeg)

FIG. 2. Calibrations of the control pulses: (a) Bloch sphere depiction of the qubit for the first three points of the error amplification sequence given in Eq. (1). (b) The amplitude calibration for a  $X_{\pi/2}$  pulse. The initial guess for the pulse amplitude has some error, which the sequence amplifies so the deviation from 1/2 grows with n, the number of repeated pulses. (c) The calibration of the DRAG parameter performs the  $X_{\pi/2}-X_{-\pi/2}$  sequence while varying  $\lambda$ , the amplitude of the derivative pulse on the quadrature channel. The correct derivative amplitude corresponds to the point where the qubit returns to the ground state.

the errors. The evolution of the qubit's Bloch vector during the first three points of this sequence is depicted in Fig. 2(a).

We correct for over- or under-rotations by fitting to the measured population of the qubit ground state,  $P(|0\rangle)$  [see Fig. 2(b)]. Under the assumption that the error is only an over-or under-rotation, it is simple to derive a fitting formula for the amplitude calibration sequences. The fit function for the  $X_{\pi/2}$  pulse in this sequence is

$$P(|0\rangle) = a + \left[\frac{1}{2}(-1)^n \cos(\pi/2 + 2n\epsilon)\right],\tag{1}$$

where a is left as a fit parameter and goes to 1/2 for perfect  $X_{\pi/2}$  pulses. For  $X_{\pi}$ , the fit function is

$$P(|0\rangle) = a + \left[\frac{1}{2}\cos(\pi/2 + 2n\epsilon)\right]. \tag{2}$$

The angle error  $\epsilon$  found by this fit corresponds to a gate error  $r \approx \epsilon^2/6$ . After fitting the error, we update the pulse amplitude accordingly.

Lastly, we determine the DRAG correction by applying the sequence  $(X_{\pi/2} - X_{-\pi/2})$  while varying the amplitude of the derivative pulse on the quadrature channel [Fig. 2(c)]. The error due to DRAG calibration depends on the square of the Rabi rate,  $\Omega^2$ , and is independent of the sign of the Rabi drive. The DRAG error therefore adds during this calibration sequence, so the final state of the qubit traces a cosine as a function of the derivative amplitude. We select the amplitude that returns the qubit in the ground state,  $|0\rangle$ .

To further characterize the control gates, we have developed an extension to interleaved randomized benchmarking. We repeat a target Clifford n times between the random Clifford gates and measure the fidelity as a function of n repetitions [Fig. 2(b)]. A typical benchmarking sequence consists of a set

<span id="page-2-0"></span>of random Clifford gates that together compose to an identity operation [6]. Under realistic assumptions on the noise, the fidelity between the implementation of this sequence with the identity operation decays exponentially as a function of the number of Clifford gates [10]. When the fidelity decay is averaged over many realizations of the random sequence, the decay constant serves as the single metric for the average noise in the system. If the gate errors are nonunitary, then the fidelity will only depend on the total length of the interleaved segment, and the resulting error per segment will thus be linear with n. If there are unitary errors of an over- or under-rotation type, they will add coherently with n, and the fidelity decay will be quadratic to leading order. To see this, suppose we have a single qubit unitary error of the form

$$U = \exp\left(-i\frac{\epsilon}{2}\hat{r}\cdot\vec{\sigma}\right),\tag{3}$$

where  $\epsilon$ ,  $\hat{r}$ , and  $\vec{\sigma}$  are the error angle, axis of rotation, and vector of Pauli operators, respectively. Assuming  $\epsilon \ll 1$ , we can write  $U^n$  to second order in  $\epsilon$  as

$$U^{n} = 1 - in\frac{\epsilon}{2}\hat{r}\vec{\sigma} - [n(2n-1)]\frac{\epsilon^{2}}{4}(\hat{r}\cdot\vec{\sigma})^{2} + O(\epsilon^{2}).$$
 (4)

The average fidelity F of the error gate compared to the identity is given by  $F = [|\text{tr}(U^n)|^2 + 2]/2$ , and writing F in terms of the benchmarking parameter  $\alpha = 2F - 1$  gives [6]

$$\alpha = 1 - \frac{n(2n-1)\epsilon^2}{3},\tag{5}$$

which shows the quadratic dependence in n. We find using a Kraus operator representation of  $T_1$  and  $T_2$  processes that errors due to decoherence do decay linearly in n to first order. The extracted  $\alpha$  approximated to second order in all errors is

$$\alpha = 1 + 2n\left(-\frac{\epsilon_1}{3} - \frac{\epsilon^2}{6} - \frac{2\epsilon_2}{3} - \frac{2\epsilon_2^2}{3}\right) + 2n^2\left(\frac{\epsilon_1^2}{8} + \frac{\epsilon_1\epsilon_2}{3} + \frac{2\epsilon_2^2}{3} - \frac{\epsilon^2}{6}\right),\tag{6}$$

where  $\epsilon_i = 1 - \exp(t_g/T_i)$  corresponds to a  $T_1$  or  $T_2$  error during a gate of length  $t_g$ , and  $\epsilon$  is an over-rotation error. The  $\epsilon_i^2$  terms are negligible for typical gate and coherence times, on the order of  $10^{-8}$  compared to  $10^{-4}$  for an over-rotation of  $\pi/128$ .

The calibrated pulses are used for iterative randomized benchmarking (IRB), in which we interleave each target sequence zero to 30 times within random sequences of up to 365 Clifford gates [as depicted in Fig. 1(b)]. We average over 35 instances of each sequence and fit the decay to  $A_n\alpha_n^i + B_n$ , where i is the number of Clifford gates and n is the number of interleaved gates. Error bars are given by the 95% confidence interval of this fit.

We perform this protocol with a 16.7 ns gate time [the time producing the minimum error per gate; Fig. 1(a)] and interleave the targets I,  $X_{\pi}$ , and  $X_{\pi/2}$ . For these three gates, the increase in the error per gate,  $r = (1 - \alpha)(1 - 1/d)$ , versus the number of interleaved gates is linear [Fig. 3(a)]. This is consistent with the RB data that suggests the unitary errors at this gate time are small.

![](_page_2_Figure_13.jpeg)

![](_page_2_Figure_14.jpeg)

FIG. 3. Iterative benchmarking data for (a) a 16.7 ns gate and (b) a 10.0 ns gate. The interleaved gates are the identity (blue squares),  $X_{\pi/2}$  (red circles),  $Y_{\pi/2}$  (magenta diamonds), and  $X_{\pi/2}Y_{\pi/2}$  (black stars). The product of r, the error per gate, for  $X_{\pi/2}$  and  $Y_{\pi/2}$  is shown (dashed black stars) for comparison to the  $X_{\pi/2}Y_{\pi/2}$  gate. Also in (a) are interleaved over-rotations on an  $X_{\pi/2}$  by  $\pi/256$  (dotted aqua triangles),  $\pi/128$  (dashed green triangles), and  $\pi/64$  (dot-dashed orange triangles). The error bars here are the 95% confidence interval of the fit to the IRB data averaged over 35 instances.

We then intentionally add over-rotation errors to the  $X_{\pi}$  gate to determine a bound on the sensitivity of this procedure to amplitude errors. We repeat the IRB procedure with the  $X_{\pi/2}$  pulse replaced with  $X_{\pi/2+\epsilon}$ , where  $\epsilon = \{\pi/64, \pi/128, \pi/256\}$ . The  $\pi/64$  and  $\pi/128$  over-rotations lead to fidelities that fall off quadratically and are clearly distinguishable from gates approaching the coherence limit. The  $\pi/256$  appears to have similar errors to the calibrated gates, giving a bound on the sensitivity to over-rotation errors. Note that with infinite  $T_1$ , we could increase the sensitivity of this scheme by repeating a larger number of interleaved gates.

In order to quantify the amount of unitary versus nonunitary errors in the IRB data, we fit the data to both quadratic and linear models. Using the Akaike information criterion (AIC), we determine which model most accurately describes the data [18,19]. The AIC is a useful tool for model selection and has been applied to quantum information previously [20].

TABLE I. AIC values for gates with no over-rotation,  $\pi/256$  over-rotation, and  $\pi/128$  over-rotation for linear and quadratic model functions.

| Fit function    | 0                    | $\pi/256$            | $\pi/128$            |
|-----------------|----------------------|----------------------|----------------------|
| bx + c          | 1                    | $1.3 \times 10^{-3}$ | $2.2 \times 10^{-3}$ |
| $ax^2 + b$      | $2.0 \times 10^{-7}$ | 0.18                 | 1                    |
| $ax^2 + bx + c$ | 0.29                 | 1                    | 0.16                 |

For n data points and k fitting parameters, the AIC is given by

$$C = n \ln \left(\frac{R}{n}\right) + 2k + \frac{2k(k+1)}{n-k-1},\tag{7}$$

where R is the residual sum of squares for the fit. The final term in this expression is a correction under the condition that n < 40k. This correction increases the penalty for overfitting when the sample size is small. We compute the C for three models: linear, quadratic with no linear component, and combined linear and quadratic (see Table I). The relative probability that the ith model is correct is

$$P_i = \exp\left[\frac{1}{2}(C_{\min} - C_i)\right],\tag{8}$$

with  $C_{\rm min}$  the smallest AIC value for the set of models. The model with the best fit to the data will have  $P_i=1$ . We calculate the relative probabilities for the three models for iterative randomized benchmarking data with  $X_{\pi/2}$  pulses with no over-rotation, and with  $\pi/128$  and  $\pi/256$  over-rotations. As detailed in Table I, the calibrated gate with no added error is best fit by a linear model, as expected when there is little unitary error present. The gate with  $\pi/256$  over-rotation is fit best by the combined model. The preferred model according to the AIC for the gate with  $\pi/128$  error is the quadratic model, but this is in part due to the penalty placed on adding extra parameters to the fit function. The fit parameters found for each model are given in Table II.

From this analysis, it follows that a  $\pi/128$  over-rotation is detectable with this method and that consequently coherent rotation errors must be smaller than this value. We therefore simulate RB in the presence of a systematic  $\pi/64$  over-rotation (easily detectable by IRB were it present), demonstrating that

TABLE II. Fit parameters for  $X_{\pi/2}$  gates with zero error, and  $\pi/128$  and  $\pi/256$  over-rotation error using the three models compared using the Akaike information criterion in Table I.

| Error     | Fit function    | а                    | b                    | с                    |
|-----------|-----------------|----------------------|----------------------|----------------------|
| 0         | bx + c          |                      | $4.4 \times 10^{-4}$ | $1.1 \times 10^{-3}$ |
| 0         | $ax^2 + c$      | $1.8 \times 10^{-5}$ |                      | $1.1 \times 10^{-3}$ |
| 0         | $ax^2 + bx + c$ | $0.8 \times 10^{-5}$ | $2.4\times10^{-4}$   | $1.1\times10^{-3}$   |
| $\pi/128$ | bx + c          |                      | $1.6\times10^{-3}$   | $1.1 \times 10^{-3}$ |
| $\pi/128$ | $ax^2 + c$      | $1.1 \times 10^{-4}$ |                      | $1.1 \times 10^{-3}$ |
| $\pi/128$ | $ax^2 + bx + c$ | $1.0\times10^{-4}$   | $1.6\times10^{-4}$   | $1.1\times10^{-3}$   |
| $\pi/256$ | bx + c          |                      | $1.0 \times 10^{-3}$ | $1.1 \times 10^{-3}$ |
| $\pi/256$ | $ax^2 + c$      | $6.0 \times 10^{-5}$ |                      | $1.1 \times 10^{-3}$ |
| $\pi/256$ | $ax^2 + bx + c$ | $4.2\times10^{-5}$   | $3.7\times10^{-4}$   | $1.1\times10^{-3}$   |

this is not sufficient to explain the deviation of the experiment from the simulated RB [dashed black line in Fig. 1(a)]. We conclude that there is an additional source of decoherence that is present under the continuous-driving conditions of an RB experiment. One possible form for such nonunitary error would be a dephasing proportional to the Rabi rate of the drive, as would result from amplitude fluctuations in the local oscillator, an amplifier, or other microwave electronics along the control line. Simulated RB in the presence of such noise (green dot-dashed line) shows reasonable agreement with the experimental data. Drive noise with a 1/f dependence has been measured in flux qubits [21], and such low-frequency noise has been studied in the context of randomized benchmarking [22,23]. As the IRB results for  $X_{\pi/2}$  and  $Y_{\pi/2}$  decay at a similar rate to the identity, however, we suspect that the deviation from the coherence limit is actually due to pulse reflections that add incoherently during the randomized sequence of gates in standard RB. The calibration for  $\pi/2$  compensates for this type of error by repeating the pulse many times, and thus IRB shows no unitary error.

We notice that there is still a deviation from the best fit at the shortest gate time in Fig. 1(a). To understand the origin of this larger error rate, we calibrate gates of length 10 ns and apply IRB. For interleaved I,  $X_{\pi/2}$ , and  $Y_{\pi/2}$ , the iterative benchmarking data appears to decay linearly [Fig. 3(b)]. First, we notice that the error of a  $Y_{\pi/2}$  gate is larger than the  $X_{\pi}/2$ gate error. We attribute this to our calibration procedure, in which the amplitude of the  $Y_{\pi/2}$  is assumed to be equal to the  $X_{\pi/2}$  pulse amplitude, but sampling errors in the pulse generation are not taken into account. Second, when the interleaved sequence is  $X_{\pi/2}Y_{\pi/2}$  (black stars), a larger decay is observed. This cannot be accounted for by multiplying (dashed black stars) the individual errors per gate, r, for the  $X_{\pi/2}$  (red circles) and  $Y_{\pi/2}$  (magenta diamonds) implying an additional error on the  $X_{\pi/2}Y_{\pi/2}$  gate. (Note that, in contrast, no additional error for the  $X_{\pi/2}Y_{\pi/2}$  sequence is observed for the 16.67 ns gate, for which the product of  $X_{\pi/2}$  and  $Y_{\pi/2}$  matches the error for  $X_{\pi/2}Y_{\pi/2}$ .) The  $X_{\pi/2}Y_{\pi/2}$  is not directly calibrated, and the presence of unitary errors here indicates a phase error, despite the fact that SSB modulation ensures the orthogonality of X and Y pulses by imposing a  $\pi/2$ -phase shift on the IF signal.

After identifying the phase error, we have developed an error amplification sequence similar to those of Fig. 2 in order to quantify an X-Y axes error. The sequence is a repetition of  $X_{\pi}Y_{\pi}$  within a Ramsey experiment:

$$X_{\pi/2} - (X_{\pi} - Y_{\pi})^n - Y_{-\pi/2}.$$

The fit function for the error case when X and Y are not orthogonal is the same function as for a  $\pi/2$  amplitude error given in Eq. (1). The gate error measured by this sequence is  $2\epsilon^2/3$ .

We measure this error as a function of the buffer time between pulses for three different pulse lengths, as shown in Fig. 4. The IRB data was taken with a 3.33 ns buffer indicated by the vertical line [with pulse length of 13.33 ns for the data in Fig. 3(a) and 6.67 ns for Fig. 3(b)]. The gate error is  $2 \times 10^{-5}$  for the pulse length corresponding to the 16.67 ns gate and  $3 \times 10^{-3}$  for the 10 ns gate. This is consistent with the IRB data that demonstrate an axis error is present for the 6.67 ns pulse (red squares in Fig. 4) but is not detected for 13.33 ns

<span id="page-4-0"></span>![](_page_4_Figure_2.jpeg)

FIG. 4. The gate error measured as a fit to the error amplification sequence  $X_{\pi/2} - (X_{\pi} - Y_{\pi})^n - Y_{\pi/2}$ . The gate error is plotted vs buffer length for three pulse lengths: 6.67 ns in red squares, 13.33 ns in blue circles, and 20 ns in violet triangles. The buffer length used for the data taken in Fig. 3 was the shortest one shown here, 3.33 ns (indicated by the solid vertical line).

(violet triangles). The gate error decreases as the buffer time is increased until it levels off around 15 ns, at which point the resolution of the fit is not better than  $1\times 10^{-5}$ . Because the error decreases with longer buffer time, it is likely due to distortions that cause successive pulses to overlap when the time between them is insufficient. Note that this effect is not typically considered in RB, in which it is assumed a pulse knows no history of previous pulses in the sequence. This pulse distortion may be alleviated by further pulse shaping (as shown in [24] with pulse distortions on flux qubits) and will be the subject of future investigations.

We have introduced a variation of randomized benchmarking, useful for distinguishing nonunitary from unitary

errors, and have validated this method on a superconducting qubit experiment. IRB will work for most physical unitaries without knowledge of the type of error present. Unitary errors that do not add coherently will not be detected, but many such unitaries, such as axes errors, may be rotated within the IRB protocol to errors that are amplified. Once a unitary error is discovered, one can develop a calibration sequence to reduce the error. The calibration sequences will generally be more experimentally efficient than running the IRB protocol for every gate, but these sequences must be developed independently for each type of error. In contrast, IRB provides a brute-force method for identifying small errors without prior knowledge of the type of error. In this work, we have demonstrated IRB on single-qubit gates, but this brute-force approach may be useful when extended to multiqubit systems. Multiqubit gates could be interleaved in the same way without requiring any additional postprocessing, measurements of correlations, or even single-shot readout as is the case for alternative characterization tools such as gate set tomography.

By pushing gate lengths down and paying careful attention to calibrating the resulting unitary errors, we have achieved a benchmarked single-qubit gate fidelity of 99.95%. The error rate corresponding to this fidelity still deviates from the expected coherence by about a factor of four, but our iterative randomized benchmarking data indicate that we are not limited by unitary errors that add coherently. We now seek to identify sources of nonunitary errors (beyond  $T_1$  and  $T_2$ ) that must be limiting our fidelity at this time.

We acknowledge discussions and contributions from Oliver E. Dial, Matthias Steffen, George A. Keefe, and Mary B. Rothwell. This work was supported by ARO under Contract No. W911NF-14-1-0124.

<sup>[1]</sup> I. L. Chuang and M. A. Nielsen, J. Mod. Opt. **44**, 2455 (1997).

<sup>[2]</sup> J. F. Poyatos, J. I. Cirac, and P. Zoller, Phys. Rev. Lett. 78, 390 (1997).

<sup>[3]</sup> J. M. Chow, J. M. Gambetta, L. Tornberg, J. Koch, L. S. Bishop, A. A. Houck, B. R. Johnson, L. Frunzio, S. M. Girvin, and R. J. Schoelkopf, Phys. Rev. Lett. 102, 090502 (2009).

<sup>[4]</sup> J. Emerson, R. Alicki, and K. Zyczkowski, J. Opt. B 7, S347 (2005).

<sup>[5]</sup> E. Knill, D. Leibfried, R. Reichle, J. Britton, R. B. Blakestad, J. D. Jost, C. Langer, R. Ozeri, S. Seidelin, and D. J. Wineland, Phys. Rev. A 77, 012307 (2008).

<sup>[6]</sup> E. Magesan, J. M. Gambetta, and J. Emerson, Phys. Rev. Lett. 106, 180504 (2011).

<sup>[7]</sup> R. Barends, J. Kelly, A. Veitia, A. Megrant, A. G. Fowler, B. Campbell, Y. Chen, Z. Chen, B. Chiaro, A. Dunsworth, I.-C. Hoi, E. Jeffrey, C. Neill, P. J. J. O'Malley, J. Mutus, C. Quintana, P. Roushan, D. Sank, J. Wenner, T. C. White, A. N. Korotkov, A. N. Cleland, and J. M. Martinis, Phys. Rev. A 90, 030303 (2014).

<sup>[8]</sup> S. T. Merkel, J. M. Gambetta, J. A. Smolin, S. Poletto, A. D. Córcoles, B. R. Johnson, C. A. Ryan, and M. Steffen, Phys. Rev. A 87, 062119 (2013).

<sup>[9]</sup> R. Blume-Kohout, J. King Gamble, E. Nielsen, J. Mizrahi, J. D. Sterk, and P. Maunz, arXiv:1310.4492.

<sup>[10]</sup> E. Magesan, J. M. Gambetta, and J. Emerson, Phys. Rev. A 85, 042311 (2012).

<sup>[11]</sup> E. Magesan, J. M. Gambetta, B. R. Johnson, C. A. Ryan, J. M. Chow, S. T. Merkel, M. P. da Silva, G. A. Keefe, M. B. Rothwell, T. A. Ohki, M. B. Ketchen, and M. Steffen, Phys. Rev. Lett. 109, 080505 (2012).

<sup>[12]</sup> J. P. Gaebler, A. M. Meier, T. R. Tan, R. Bowler, Y. Lin, D. Hanneke, J. D. Jost, J. P. Home, E. Knill, D. Leibfried, and D. J. Wineland, Phys. Rev. Lett. 108, 260503 (2012).

<sup>[13]</sup> S. Kimmel, M. P. da Silva, C. A. Ryan, B. R. Johnson, and T. Ohki, Phys. Rev. X 4, 011050 (2014).

<sup>[14]</sup> J. M. Gambetta, A. D. Córcoles, S. T. Merkel, B. R. Johnson, J. A. Smolin, J. M. Chow, C. A. Ryan, C. Rigetti, S. Poletto, T. A. Ohki, M. B. Ketchen, and M. Steffen, Phys. Rev. Lett. 109, 240504 (2012).

<sup>[15]</sup> P. J. J. O'Malley, J. Kelly, R. Barends, B. Campbell, Y. Chen, Z. Chen, B. Chiaro, A. Dunsworth, A. G. Fowler, I.-C. Hoi, E. Jeffrey, A. Megrant, J. Mutus, C. Neill, C. Quintana, P. Roushan, D. Sank, A. Vainsencher, J. Wenner, T. C. White, A. N. Korotkov, A. N. Cleland, and J. M. Martinis, Phys. Rev. Appl. 3, 044009 (2015).

- <span id="page-5-0"></span>[16] [J. Wallman, C. Granade, R. Harper, and S. T. Flammia,](http://dx.doi.org/10.1088/1367-2630/17/11/113020) New J. Phys. **[17](http://dx.doi.org/10.1088/1367-2630/17/11/113020)**, [113020](http://dx.doi.org/10.1088/1367-2630/17/11/113020) [\(2015\)](http://dx.doi.org/10.1088/1367-2630/17/11/113020).
- [17] F. Motzoi, J. M. Gambetta, P. Rebentrost, and F. K. Wilhelm, [Phys. Rev. Lett.](http://dx.doi.org/10.1103/PhysRevLett.103.110501) **[103](http://dx.doi.org/10.1103/PhysRevLett.103.110501)**, [110501](http://dx.doi.org/10.1103/PhysRevLett.103.110501) [\(2009\)](http://dx.doi.org/10.1103/PhysRevLett.103.110501).
- [18] H. Akaike, in *Selected Papers of Hirotugu Akaike*, Springer Series in Statistics, edited by E. Parzen, K. Tanabe, and G. Kitagawa (Springer, New York, 1998), pp. 199–213.
- [19] K. P. Burnham and D. R. Anderson, *Model Selection and Multimodel Inference: A Practical Information-Theoretic Approach* (Springer-Verlag, Berlin, 2002).
- [20] S. J. van Enk and R. Blume-Kohout, [New J. Phys.](http://dx.doi.org/10.1088/1367-2630/15/2/025024) **[15](http://dx.doi.org/10.1088/1367-2630/15/2/025024)**, [025024](http://dx.doi.org/10.1088/1367-2630/15/2/025024) [\(2013\)](http://dx.doi.org/10.1088/1367-2630/15/2/025024).

- [21] F. Yoshihara, Y. Nakamura, F. Yan, S. Gustavsson, J. Bylander, W. D. Oliver, and J.-S. Tsai, [Phys. Rev. B](http://dx.doi.org/10.1103/PhysRevB.89.020503) **[89](http://dx.doi.org/10.1103/PhysRevB.89.020503)**, [020503](http://dx.doi.org/10.1103/PhysRevB.89.020503) [\(2014\)](http://dx.doi.org/10.1103/PhysRevB.89.020503).
- [22] M. A. Fogarty, M. Veldhorst, R. Harper, C. H. Yang, S. D. Bartlett, S. T. Flammia, and A. S. Dzurak, [Phys. Rev. A](http://dx.doi.org/10.1103/PhysRevA.92.022326) **[92](http://dx.doi.org/10.1103/PhysRevA.92.022326)**, [022326](http://dx.doi.org/10.1103/PhysRevA.92.022326) [\(2015\)](http://dx.doi.org/10.1103/PhysRevA.92.022326).
- [23] J. M. Epstein, A. W. Cross, E. Magesan, and J. M. Gambetta, [Phys. Rev. A](http://dx.doi.org/10.1103/PhysRevA.89.062321) **[89](http://dx.doi.org/10.1103/PhysRevA.89.062321)**, [062321](http://dx.doi.org/10.1103/PhysRevA.89.062321) [\(2014\)](http://dx.doi.org/10.1103/PhysRevA.89.062321).
- [24] S. Gustavsson, O. Zwier, J. Bylander, F. Yan, F. Yoshihara, Y. Nakamura, T. P. Orlando, and W. D. Oliver, [Phys. Rev. Lett.](http://dx.doi.org/10.1103/PhysRevLett.110.040502) **[110](http://dx.doi.org/10.1103/PhysRevLett.110.040502)**, [040502](http://dx.doi.org/10.1103/PhysRevLett.110.040502) [\(2013\)](http://dx.doi.org/10.1103/PhysRevLett.110.040502).