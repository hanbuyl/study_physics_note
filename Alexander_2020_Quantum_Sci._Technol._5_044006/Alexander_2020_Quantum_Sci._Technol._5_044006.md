![](_page_0_Picture_1.jpeg)

![](_page_0_Picture_2.jpeg)

#### **PAPER • OPEN ACCESS**

# Qiskit pulse: programming quantum computers through the cloud with pulses

To cite this article: Thomas Alexander et al 2020 Quantum Sci. Technol. 5 044006

View the [article online](https://doi.org/10.1088/2058-9565/aba404) for updates and enhancements.

# You may also like

- [Intermediate-temperature topological](https://iopscience.iop.org/article/10.1088/2058-9565/ae2d8d) [Uhlmann phase on IBM quantum](https://iopscience.iop.org/article/10.1088/2058-9565/ae2d8d) [computers](https://iopscience.iop.org/article/10.1088/2058-9565/ae2d8d) -
- Christopher Mastandrea, Costin Iancu, Hao Guo et al.
- [Benchmarking near-term devices with](https://iopscience.iop.org/article/10.1088/2058-9565/aba038) [quantum error correction](https://iopscience.iop.org/article/10.1088/2058-9565/aba038) James R Wootton -
- [Suppressing quantum errors by noise](https://iopscience.iop.org/article/10.1088/2058-9565/ae05c4)[aware circuit design](https://iopscience.iop.org/article/10.1088/2058-9565/ae05c4) Yi Hu, Congcong Zheng, Xiaojun Wang et al. -

![](_page_0_Figure_12.jpeg)

![](_page_1_Picture_4.jpeg)

#### **OPEN ACCESS**

#### **RECEIVED**

7 February 2020

**REVISED**

# 13 April 2020

**ACCEPTED FOR PUBLICATION** 8 July 2020

#### **PUBLISHED**

18 August 2020

Original content from this work may be used under the terms of the Creative Commons [Attribution 4.0 licence.](https://creativecommons.org/licenses/by/4.0/)

Any further distribution of this work must maintain attribution to the author(s) and the title of the work, journal citation and DOI.

![](_page_1_Picture_16.jpeg)

#### <span id="page-1-1"></span>**PAPER**

# Qiskit pulse: programming quantum computers through the cloud with pulses

**Thomas Alexander**[1,4,](#page-1-0)[5](#page-1-1) **[,](https://orcid.org/0000-0003-3452-0082) Naoki Kanazawa**[2,4](#page-1-0) **, Daniel J Egger**[3](#page-1-0) **, Lauren Capelluto**[1](#page-1-0) **, Christopher J Wood**[1](#page-1-0) **, Ali Javadi-Abhari**[1](#page-1-0) **and David C McKay**[1](#page-1-0)

- <span id="page-1-0"></span><sup>1</sup> IBM Quantum, T.J. Watson Research Center, Yorktown Heights, NY 10598, USA
- <sup>2</sup> IBM Quantum, IBM Research Tokyo, 19-21 Nihonbashi Hakozaki-cho, Chuo-ku, Tokyo, 103-8510, Japan
- <sup>3</sup> IBM Quantum, IBM Research Zürich S¨aumerstrasse 4, 8803 Rüschlikon, Switzerland
- <sup>4</sup> These two authors contributed equally.
- <sup>5</sup> Author to whom any correspondence should be addressed.

**E-mail: [talexander@ibm.com](mailto:talexander@ibm.com)**

**Keywords:** QASM, quantum computing, pulse, gate calibration, quantum programming, state discrimination, Qiskit

## **Abstract**

The quantum circuit model is an abstraction that hides the underlying physical implementation of gates and measurements on a quantum computer. For precise control of real quantum hardware, the ability to execute pulse and readout-level instructions is required. To that end, we introduce Qiskit Pulse, a pulse-level programming paradigm implemented as a module within Qiskit-Terra [\[1\]](#page-16-0). To demonstrate the capabilities of Qiskit Pulse, we calibrate both un-echoed and echoed variants of the cross-resonance entangling gate with a pair of qubits on an IBM Quantum system accessible through the cloud. We perform Hamiltonian characterization of both single and two-pulse variants of the cross-resonance entangling gate with varying amplitudes on a cloud-based IBM Quantum system. We then transform these calibrated sequences into a high-fidelity CNOT gate by applying pre and post local-rotations to the qubits, achieving average gate fidelities of *F* = 0.981 and *F* = 0.979 for the un-echoed and echoed respectively. This is comparable to the standard backend CNOT fidelity of *FCX* = 0.984. Furthermore, to illustrate how users can access their results at different levels of the readout chain, we build a custom discriminator to investigate qubit readout correlations. Qiskit Pulse allows users to explore advanced control schemes such as optimal control theory, dynamical decoupling, and error mitigation that are not available within the circuit model.

# **1. Introduction**

In quantum computing, information is stored and processed according to the laws of quantum mechanics [\[2\]](#page-16-1). The primary quantum programming paradigm is the circuit model. In this model, the underlying dynamics of the physical system implementing the quantum computer are abstracted as a sequence of unitary gate operations and projective measurements applied to a set of qubits. Gates manipulate the states of qubits, while measurements extract classical information in the form of bit-strings, which encode the outcome of projective measurements of the qubits in a particular measurement basis.

Qiskit is an open-source quantum computing framework designed to enable research on near-term quantum computers and their applications. It provides tools for creating, manipulating and running quantum programs on quantum systems independent of their underlying technology and architecture. The standard programming abstraction for a quantum circuit is a quantum assembly language (QASM) such as OpenQASM [\[3\]](#page-16-2) which Qiskit supports [\[1\]](#page-16-0) and many similar languages that have been described in the literature [\[4,](#page-16-3) [5\]](#page-16-4). However, hardware is not capable of natively implementing quantum instructions and must compose these operations from the classical stimulus available to control hardware.

At the hardware level the time-dependent dynamics of a quantum system interacting with applied control fields is described by its Hamiltonian and the Schrödinger equation. Through careful engineering of applied classical control fields a quantum system may be steered through a desired unitary evolution [\[6\]](#page-16-5). Superconducting transmon qubits, for example, encode a qubit in a non-linear oscillator formed by a parallel circuit consisting of a Josephson junction and capacitor, and may be manipulated by applying shaped microwave control pulses [\[7\]](#page-16-6). Implementing the quantum circuit model on such an architecture requires compiling circuit instructions to a set of microwave control instructions, or pulses, which enact the desired state-transformations and/or measurements.

In the circuit domain, an atomic circuit instruction is agnostic to its pulse-level implementation on hardware. Extracting the highest performance out of quantum hardware requires the ability to craft a pulse-level instruction schedule, which cannot be done within the standard circuit model. To enable pulse-level programming an instruction set, OpenPulse [\[8\]](#page-16-7), was developed to describe quantum programs as a sequence of pulses, scheduled in time. We present within this paper a Python implementation of OpenPulse, *Qiskit Pulse* which adds to the Qiskit compilation pipeline the capability to schedule a quantum circuit into a pulse program intermediate representation, perform analysis and optimizations, and then compile to OpenPulse object code to execute on a quantum system.

The various hardware architectures used for current-day quantum computing systems creates a need for a pulse-level instruction set that may address most platforms at an abstract level, compatible with both commercial off-the-shelf and proprietary control instruments, including arbitrary waveform generators (AWG), signal generators, filters, amplifiers and digitizers [\[9\]](#page-16-8). To program such systems at the pulse-level in a *hardware independent* manner requires the user-level instruction set to be target-compiled to the underlying system hardware components, each of which may have a unique instruction set and programming model. Recent efforts to construct microarchitectures that conform to classical computer engineering paradigms [\[10–](#page-16-9)[12\]](#page-16-10) have programming semantics closely tied to the underlying microarchitecture. Compiling directly from the circuit model to target hardware obfuscates the underlying pulses that manipulate the hardware removing a powerful degree of control.

With Qiskit Pulse we enable the development of a common and reusable suite of technology-independent quantum control techniques [\[6\]](#page-16-5) that operate at the level of analog stimulus which may be remotely retargeted to cloud-based quantum computing systems.

*Paper outline*—in section [2](#page-2-0) we present our pulse programming model. We demonstrate the capabilities of Qiskit Pulse in section [3](#page-6-0) where we show Hamiltonian characterization of the two-qubit cross-resonance interaction, and calibration of a high-fidelity entangling gate, on a cloud-based quantum computer available on the IBM Quantum Experience. We discuss how the readout of quantum computers is incorporated in Qiskit Pulse in section [4](#page-9-0) and conclude in section [5.](#page-11-0) The source code and data for the experiments within this paper has been made available online [\[13\]](#page-16-11).

# <span id="page-2-0"></span>**2. Qiskit Pulse programming model**

In the standard quantum circuit model, the time elapsed between operations is irrelevant as long as the order of non-commuting gates is preserved [\[14\]](#page-16-12). However, when controlling quantum hardware at the pulse level, properly timing and synchronizing instructions is crucial for accurately enacting quantum operations. For instance, users may create new gate definitions, characterize and correct for crosstalk on neighboring qubits, implement optimal control techniques such as GRAPE [\[15\]](#page-16-13) or mitigate errors through Richardson extrapolation [\[16–](#page-16-14)[18\]](#page-16-15).

We envision that a classical microprocessor with an embedded *pulse coprocessor* will be responsible for controlling and measuring the quantum device. Within this work we only focus on describing a virtual execution model and limited set of instructions for the pulse coprocessor which can be compiled to the instruction set architecture (ISA) of the underlying control hardware. Qiskit Pulse's position in the predicted quantum computing compilation pipeline is demonstrated in figure [1.](#page-3-0) We expect that as quantum hardware continues to be refined these abstractions will be extended.

Qiskit Pulse provides an open source, front-end implementation of the OpenPulse interface [\[8\]](#page-16-7). Third parties can fully integrate with Qiskit Pulse by implementing their own Qiskit provider [\[1\]](#page-16-0) which is responsible for translating Qiskit Pulse programs to executable programs on the provider-specific hardware which might include components such as AWGs and digitizers. Qiskit Pulse programs are composed of *pulses*, *channels*, and *instructions* which we present in the following subsections.

# **2.1. Pulses**

A *pulse* is a *time-series* of complex-valued amplitudes with a maximum unit norm, [*d*0, ... , *dn*−1]. Each *dj*, *j* ∈ {0, ... , *n* − 1}, is called a *sample*. Every system specifies a cycle-time of d<sup>t</sup> which is the finest time-resolution exposed on the pulse coprocessor, and is typically defined by the sample rate of the coprocessor's waveform generators. Each sample in a pulse is output for one cycle, a *timestep*. All pulse

![](_page_3_Figure_3.jpeg)

<span id="page-3-0"></span>**Figure 1.** The envisioned quantum program representations and their associated lowering compilation procedures. QASM programs may be built and optimized with information of the system topology, native gates, and error rates, and then are *scheduled* into pulse programs by using calibrated native gate definitions. Pulse programs are compiled to a processor-specific ISA through a target code generation procedure. The typical user is expected to program at the circuit level, whereas Qiskit Pulse enables advanced users to control at the pulse level.

durations and timesteps are defined and discretized dimensionlessly with respect to  $\mathtt{d}t$ . The ideal output signal has amplitude

$$D_j = \operatorname{Re}\left[e^{i2\pi f j dt + \phi} d_j\right] \tag{1}$$

<span id="page-3-1"></span>at time j dt, where f and  $\phi$  are a modulation frequency and a phase. The pulse samples describe only the envelope of the produced signal which are then mixed up in hardware with a carrier signal defined by a frequency and a phase. To reduce encoding sizes we also allow hardware providers to define parametric pulse shapes. For example, one parametric pulse supported by IBM backends and made available through the Pulse library is the Gaussian pulse. It takes three parameters: an integer duration in terms of dt, a complex amplitude amp, and standard deviation sigma. This parametric pulse can be instantiated within Qiskit in the following way:

```
from qiskit.pulse.pulse_lib import Gaussian

duration = 128

amp = 0.2

sigma = 16

gaussian_pulse = Gaussian(duration, amp, sigma)
```

#### 2.2. Channels

Hardware components are modeled with Channels. Channels label signal lines that either transmit or receive signals between the control electronics and the quantum device. Each channel executes instructions from a first-in, first-out (FIFO) queue as outlined in subsection 2.3.

Channels are constrained at target code generation time to target hardware components, e.g., an AWG. The calibrated parameters of a channel, such as its frequency, and the pulses played on that channel, depend on the physical properties of the targeted qubit. Therefore, channels are not interchangeable at the pulse abstraction layer, i.e. permuting channels over qubits will not give equivalent results. This highlights another difference between circuit and pulse instructions, the parameters of gates in a quantum circuit do not depend on the physical properties of the targeted qubits. The qubits in a quantum circuit can therefore be interchanged without affecting the computational result as long as the topology of the device is taken into account and gate imperfections are ignored.

There are several different channel types, and each may support a different instruction set. A summary of channels and their descriptions is provided in table 1. The channel type, and thus the supported instructions, is determined by the effect of the channel on the quantum device. For example, a PulseChannel models the output of a control field  $\alpha_k(t)$  in a system Hamiltonian  $H(t) = H_{\rm sys} + \sum_k \alpha_k(t) H_k$  which is composed of time-independent system and time-dependent control terms. The Hamiltonian term for a given channel,  $\hat{H}_k$  in general may be arbitrary, but is typically associated with the subtype of the respective pulse channel that is assigned at system configuration time.

The sub-types of PulseChannels are DriveChannels, MeasureChannels, and ControlChannels. Each pulse channel maintains an instruction writeable frequency f and phase  $\phi$ , which modify the channel output as per equation (1). Tracking the phase in this way enables the implementation of *virtual* Z-gates [19, 20]. Qubit drive and readout pulses are respectively assigned to DriveChannels and MeasureChannels, see e.g., the drive pulses on drive channels  $d_0$  and  $d_1$  in figure 2. Their index is trivially mapped to the address of the target qubit. The ControlChannel

<span id="page-4-1"></span>**Table 1.** A summary of channels and the pulse instructions that are defined on them. Note that the DriveChannel, MeasureChannel, and ControlChannel are subtypes of PulseChannel, whereas the AcquireChannel, which cannot transmit stimulus pulses, is not. In the near term it is expected that the instruction set below will continue to be expanded.

| Channel        | Alias                                                           | Description                                                                                                                       |  |  |
|----------------|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|--|--|
| PulseChannel   | —                                                               | sub-types are DriveChannel, MeasureChannel and ControlChannel.<br>Generic transmit channel used to manipulate the quantum system. |  |  |
| DriveChannel   | di                                                              | Transmit channel connected to qubit i, with signals typically modulated at a<br>frequency in resonance with qubit i.              |  |  |
| MeasureChannel | mi                                                              | Transmit channel connected to the readout component of qubit i.                                                                   |  |  |
| ControlChannel | ui                                                              | Transmit channel with signals typically associated with arbitrary interaction<br>terms in the Hamiltonian.                        |  |  |
| AcquireChannel | ai                                                              | Receive channel connected to the readout component of qubit i, capable of<br>digitizing and acquiring data.                       |  |  |
| Instruction    | Operands                                                        | Description                                                                                                                       |  |  |
| Play           | pulse: Pulse,<br>channel: PulseChannel                          | Output the waveform described by pulse on the channel.                                                                            |  |  |
| Delay          | duration: int,<br>channel: Channel                              | Idle the channel for the given duration.                                                                                          |  |  |
| ShiftPhase     | phase: float,<br>channel: PulseChannel                          | Shift the phase of the channel by phase radians.                                                                                  |  |  |
| SetFrequency   | frequency: float,<br>channel: PulseChannel                      | Set the frequency of the channel to frequency Hz.                                                                                 |  |  |
| Acquire        | duration: int,<br>channel:AcquireChannel,<br>register: Register | Trigger the channel to collect data for the given duration, and<br>store the measurement result in a register.                    |  |  |

implements any remaining control fields, such as coupler drives or two-qubit drives as depicted by <sup>u</sup><sup>2</sup> in figure [2.](#page-5-0) The backend hardware may choose to map multiple PulseChannels to the same control unit in the system, which enables tracking a unique phase for each channel. For example, in the IBM Quantum systems used to perform the experiments within this paper, every DriveChannel may share an AWG with multiple ControlChannels, each of which have a frequency and phase adjusted to track that of their respectively coupled qubits, enabling the implementation of two-qubit gates as demonstrated in section [3.](#page-6-0)

The AcquireChannel is used to communicate to the system when qubit readout data must be acquired. It is not associated with a control term in the Hamiltonian and does not output stimulus to the quantum system. Data collected on these channels are used to determine the qubit state, see section [4](#page-9-0) for more details.

For convenience we alias drive, measurement, control and acquisition channels as {*d*0, ... , *dn*q−1}, {*m*0, ... , *mn*q−1}, {*u*0, ... , *un*u−1}, and {*a*0, ... , *an*q−1} respectively, where *n*<sup>q</sup> is the number of qubits and *n*<sup>u</sup> is the number of arbitrary control channels of the system.

## <span id="page-4-0"></span>**2.3. Instructions and execution model**

Instructions may be scheduled on Channels to manipulate the quantum system. Pulse instructions have as operands channels and instruction-dependent constants. All pulse instructions have a fixed, deterministic duration, which may be specified either implicitly or explicitly. Instructions are executed with an *allocation* and *trigger* timing model in which instructions are loaded into a FIFO queue unique to each channel and then execution is initialized synchronously across all channels with an external trigger signal. Consequently the absolute start and end of every pulse instruction may be scheduled at compile-time across channels with hard real-time deadlines relative to the external trigger signal. Instructions may have multiple channels as operands causing an execution dependency. In this case channels stall execution until all operand channels are available. We now outline the different types of instructions, which are summarized in table [1.](#page-4-1)

Every channel supports a Delay instruction which has as operands a duration which is specified as a number of cycles, and a target channel. The channel will idle for the duration of the instruction.

The Play instruction allows users to play a pulse on a target PulseChannel with a frequency and phase set with the ShiftPhase and SetFrequency instructions. The ShiftPhase instruction has an implicit duration of zero and accepts an input float phase and PulseChannel. The instruction

![](_page_5_Figure_3.jpeg)

<span id="page-5-0"></span>**Figure 2.** (a) Qiskit code to construct a quantum circuit that prepares and measures a Bell state and then schedules the circuit to produce an equivalent pulse schedule. Here, <sup>h</sup> is a Hadamard gate, cx a CNOT gate and backend is a description of a quantum system received from a hardware provider. (b) and (c) Visualization of the mapping between circuit instructions (b) and the composite pulse sequences that will implement the circuit elements (c). Pulse envelopes filled with bright and dark colors respectively represent the real (in-phase) and imaginary (quadrature-phase) components of the input control waveform. The circular arrows represent a phase shift. The gray shadow on <sup>a</sup>0 and <sup>a</sup>1 indicates the data acquisition trigger for the ADC which is synchronized with the measurement stimulus pulse. These mappings are automatically provided by the hardware backend, but may be overridden by the user as we demonstrate in section [3.](#page-6-0) The scheduler will align the gates in time according to the selected scheduling policy.

will shift the phase φ of the target channel by phase radians. This relative shift persists on the channel from the time of the instruction, allowing the phase of a channel to be accumulated throughout an experiment. The SetFrequency instruction has an implicit duration of zero and accepts an input float frequency and a PulseChannel. This instruction will set the frequency *f* of all proceeding pulses on the target channel to frequency Hz. Like any other instruction, SetFrequency can be used on a single channel multiple times within a schedule, subject to the instantaneous bandwidth of the hardware. It can therefore be used, for example, to measure the anharmonicity of a transmon qubit.

The Acquire instruction has as operands a duration, an AcquireChannel, and a classical register in which to store the observed result. This instruction signals to the measurement unit to begin acquiring data, and for how long. Each Acquire instruction should align with a corresponding measurement stimulus Play instruction to induce a measurement of the target qubit. An acquisition channel outputs an unsigned integer value <sup>N</sup> into the result register. For the standard two-level qubit, this will be a single bit {0, 1}1.

If a measurement stimulus pulse measures multiple qubits, as is typical for multiplexed measurement schemes [\[21,](#page-16-18) [22\]](#page-16-19), an acquisition instruction must be synchronously scheduled for each of the measured qubits. In hardware, each AcquireChannel is constrained to a measurement chain which usually includes data acquisition, filtering, kerneling, and state discrimination. To accommodate the heterogeneous readout schemes encountered in hardware we defined three levels of readout data and how to convert between them, see section [4.](#page-9-0)

The set of operations in Qiskit Pulse should have sufficient generality to program a pulse coprocessor for an arbitrary quantum computing system in the time-domain and be embedded within a larger instruction

set that might include both classical control flow and a traditional gate-level description of a quantum program with instructions being implemented by a lowering procedure to pulse instructions. The benefit of this approach is that a single software stack may provide the middle-end for the rapidly developing heterogeneous quantum computing platforms.

## **2.4. The pulse schedule**

The pulse Schedule is the representation of a pulse program in Qiskit Pulse and is an ordered collection of scheduled pulse instructions. The pulse schedule is equivalent to a basic block [\[23\]](#page-16-20) in a classical computation with deterministic instruction durations. To construct a pulse schedule Instructions may be appended as demonstrated in the example below, which prepares qubit 0 in the |1 state and then measures it:

### **2.5. Scheduling**

Quantum circuits and pulse schedules are both representations of a quantum program. The Qiskit *transpiler* optimizes quantum circuits according to the properties of the targeted quantum system such as the device topology, the native gate set, and the gate fidelities. A *scheduler* compiles a circuit program to a pulse program, as depicted in figure [1.](#page-3-0) Scheduling requires system dependent information, most notably the definitions of the native gates in terms of scheduled pulse instructions. The scheduler therefore requires a quantum circuit to be transpiled to the native gate set of the target system prior to scheduling. Furthermore, during scheduling it is crucial to maintain the relative timing of groups of pulse instructions calibrated to implement an element of the native gate set. For instance, the cross-talk cancellation tone of a cross-resonance gate applied to the target qubit must be aligned with the pulse that drives the control qubit at the frequency of the target qubit [\[24\]](#page-16-21).

The input circuit provides only implicit topological timing constraints, which allows the scheduler to arbitrarily resolve the remaining free time-alignment parameters in the output schedule. The scheduler's behavior in resolving free parameters is set by specifying a *scheduling method* or *policy*. By default the Qiskit scheduler follows an 'as-late-as-possible' scheduling method [\[1\]](#page-16-0). This will schedule individual gates as late as possible while minimizing the deadtime between instructions on the same channel. This scheduling routine mitigates *T*<sup>1</sup> and *T*2-decay errors by maximizing the time that qubits will spend in their initial ground state prior to the first pulse, while also minimizing the time between the last pulse and the measurement. Figure [2](#page-5-0) provides a code snippet for scheduling a quantum circuit into a pulse schedule using Qiskit, and visually demonstrates the correspondence between the circuit instructions input to the scheduler and the calibrated output pulse sequences. This output is easily generated for both the QuantumCircuit and Schedule with the draw method.

<span id="page-6-0"></span>Qiskit Pulse users may create pulse programs to replace the default pulse programs of the native gate set provided by the backend and pass them as an argument to the scheduler. This gives users low level control over the gate definitions used at scheduling time. They may specify their own scheduling policies to dynamically aggregate gates and generate composite pulse sequences such as would be required to implement the compilation techniques described by Shi *et al* [\[25\]](#page-16-22).

![](_page_7_Figure_3.jpeg)

<span id="page-7-0"></span>Figure 3. CNOT pulse Schedules implemented with the CR gates obtained with local fidelity optimization. Local operations are realized by  $X_{\pi/2}^{\pm}$  pulses with three virtual-Z gates before and after the CR gates on the DriveChannels  $d_0$  and  $d_1$ . The CR1 and CR2 gate are surrounded by red boxes. (a) CR1-based CNOT gate composed of a single CR pulse  $CR_{\pi/2}$  on the ControlChannel  $u_1$ . (b) CR2-based CNOT gate composed of two CR pulses  $CR_{\pi/4}^{\pm}$  on  $u_1$  with echo pulses  $X_{\pi}^{+}$  applied on  $d_1$ . Measurement and acquisition pulses are not shown. The numbers below the channel aliases show the amplitude scaling factor used for plotting. The 12 circular arrows topped by floating point numbers represent phase shifts in units of radians and each phase shift corresponds to an optimization parameter  $\Theta_i$ . Note that the phase shifts on  $u_1$  match those used in  $d_0$  to synchronize the frame of both channels; they are automatically inserted by the pulse scheduler.

#### 3. Demonstration of a cross-resonance entangling gate

To highlight how Qiskit Pulse can enable tasks that cannot be done in the circuit model we perform standard quantum process tomography (QPT) [26] of both echoed and un-echoed cross-resonance (CR) [27] pulses for *varying amplitudes* on a cloud-based quantum computer. We use the tomography data to calculate the coefficients of the effective CR Hamiltonian as a function of the pulse amplitude, and show how to implement a high-fidelity controlled-NOT (CNOT) gate based on the calibrated CR pulse.

#### 3.1. The cross-resonance interaction

The CR gate is a microwave-only two-qubit entangling gate for fixed-frequency dispersively coupled qubits [27]. It is physically realized by driving the control qubit with microwave pulses at the frequency of the target qubit to stimulate the evolution of an effective ZX interaction Hamiltonian, where Z and X are the Pauli-Z and X operators of the driven control qubit and the target qubit, respectively.

![](_page_8_Figure_3.jpeg)

<span id="page-8-1"></span>**Figure 4.** Process tomography circuits for the  $\mathcal{E}_{CR}(A)$  pulse embedded as a user-defined custom gate.

The two-transmon system driven by the CR pulse is described by a time-dependent Hamiltonian  $H_{\rm CR}(t)$  which, in the absence of noise, results in the unitary evolution  $U_{\rm CR}$ . We can approximate the evolution as being generated by a time-independent Hamiltonian  $\overline{H}_{\rm CR}$  using the perturbative method presented in reference [28] which showed good agreement with experimental results for single-pulse and echoed CR gates [24]. This technique approximates the time-dependent control qubit drive pulse with a constant amplitude pulse and block-diagonalizes the resulting Hamiltonian to second order. Using this approach the CR evolution is approximated by  $U_{\rm CR} \approx \exp\left(-it_{\rm CR}\,\overline{H}_{\rm CR}\right)$  where

<span id="page-8-2"></span>
$$\overline{H}_{CR} = \frac{Z \otimes B}{2} + \frac{I \otimes C}{2}$$

$$B = \omega_{ZI}I + \omega_{ZX}X + \omega_{ZY}Y + \omega_{ZZ}Z$$

$$C = \omega_{IX}X + \omega_{IY}Y + \omega_{IZ}Z.$$
(2)

If the ZX term could be isolated, the resulting unitary gate would be a two-qubit rotation

<span id="page-8-0"></span>
$$U_{\rm ZX}(\theta_{\rm ZX}) = \exp\left(-\mathrm{i}\theta_{\rm ZX}\frac{ZX}{2}\right),$$
 (3)

where the rotation angle  $\theta_{ZX}$  depends on the strength and duration of the pulse applied to the control qubit. The unitary gate  $U_{ZX}(\pi/2)$  is a *perfect entangler*—it can be used to generate a maximally entangled state from a separable input state and is locally equivalent to a CNOT gate [29]. Therefore, combined with arbitrary single-qubit operations, it is sufficient for universal quantum computation.

The terms in addition to  $\omega_{ZX}ZX$  in  $\overline{H}_{CR}$  lead to coherent errors and divergences from the ideal target unitary in equation (3). Characterizing the strength of these terms and designing pulse sequences that suppress them is necessary to create high fidelity entangling operations. The standard techniques used to suppress these terms are multi-pulse echos and cancellation tones [24].

#### 3.2. Constructing and calibrating a cross-resonance gate

The experiments presented within this section are executed on the twenty-qubit IBM Quantum system ibmq\_almaden to take advantage of higher resolution waveforms with a cycle-time dt = 0.222 ns afforded by infrastructure under test on that system at the time of writing. We use qubit 1 and qubit 0 as the control and target qubits, respectively. The resonance frequency and anharmonicity of the control qubit are  $f_1=4.972$  GHz and  $\delta_1=-319.7$  MHz, and  $f_0=4.857$  GHz and  $\delta_0=-320.2$  MHz for the target qubit.

We implement both a single-pulse (CR1), and an echoed two-pulse (CR2) variant of the CR gate without a cross-talk cancellation tone on the target qubit [30]. The CR pulse envelope is a GaussianSquare pulse, i.e. a square pulse with Gaussian-shaped rising and falling edges. The pulse has a square amplitude A, a phase  $\phi = -0.166$  rad, discussed in appendix B, and a total duration  $t_{\rm CR} = 848$  dt = 184.4 ns. The square portion of the pulse has a duration of 720 dt and the Gaussian rising and falling edges last 64 dt and have a 32 dt standard deviation. The pulse duration is chosen so that a  $\pi/2$  rotation angle can be achieved within the weak driving regime.

The CR1 sequence is a single CR pulse on the ControlChannel  $u_1$ , see figure 3(a). The CR2 sequence consists of two CR pulses with opposite phases on  $u_1$ , and two additional single-qubit pulses on the DriveChannel  $d_1$ , one after each CR pulse, see figure 3(b). This echo sequence refocuses unwanted terms in the interaction Hamiltonian [24]. The following code exemplifies how to build the CR2 schedule in Qiskit Pulse.

```
# Create a pulse schedule
sched = Schedule(name='cr2')

# Create pulse objects for the echoed CR gate
cr_p = GaussianSquare(cr_dur, amp, sigma, square_width)
cr_m = GaussianSquare(cr_dur, -amp, sigma, square_width)
x180 = Drag(pi_dur, pi_amp, pi_sigma, pi_beta)

# Assemble the schedule
sched += Play(cr_p, ControlChannel(1))
sched += Delay(t_cr, DriveChannel(1))
sched += Play(x180, DriveChannel(1))
sched += Delay(t_cr, DriveChannel(1))
sched += Delay(t_cr, DriveChannel(1))
sched += Play(x180, DriveChannel(1))
```

#### 3.3. Quantum process tomography of the CR gate

To study the dynamics of the CR pulse, we perform standard QPT [26] of the CR1 and CR2 pulse sequences for a range of CR pulse amplitudes using the tomography module of Qiskit Ignis [31]. Given a d-dimensional noisy quantum channel  $\mathcal{E}$ , QPT reconstructs the Choi-matrix  $\Lambda_{\mathcal{E}}$  which is the positive-semidefinite matrix defined by  $\Lambda_{\mathcal{E}} \equiv \sum_{i=0}^{d-1} |i\rangle\langle i| \otimes \mathcal{E}(|i\rangle\langle i|)$  [32].

The QPT circuits, shown in figure 4, use the single-qubit gates  $\{U_i^{\text{prep}}\}_{i=0}^3$  and  $\{U_i^{\text{meas}}\}_{i=0}^2$  to prepare the required input states and measurement bases, respectively. We prepare each qubit in the states  $|0\rangle, |1\rangle, \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle), \frac{1}{\sqrt{2}}(|0\rangle + i|1\rangle)$  and measure in the X, Y and Z bases. Our amplitude-dependent CR pulse is inserted into the QPT circuits in figure 4 as a custom gate that the Qiskit pulse scheduler maps to a pulse program, see appendix A.1. Each of the 144 two-qubit QPT pulse schedules is executed 2048 times to estimate the measurement outcome probabilities of each qubit. The details of the readout process are presented in section 4. We correct for measurement errors using the readout error mitigation techniques [33] implemented in Qiskit Ignis. Readout error mitigation for two qubits requires four additional schedules which were interleaved with the QPT schedules. The reconstructed Choi-matrix  $\mathcal{E}_{CR}(A)$  for the noisy gate was obtained from the convex-optimization QPT fitter in Qiskit Ignis for each value of the CR pulse amplitude A. This fitter uses maximum likelihood estimation to find the completely-positive trace-preserving process that is most likely to fit the measured data after correction for readout errors.

We use the fitted Choi-matrices  $\mathcal{E}_{CR}(A)$  to compute estimates of the coefficients of the effective CR Hamiltonian in equation (2). The method is described in appendix C. We then fit these coefficients to a third order model to find the CR pulse amplitude that implements a  $\theta_{ZX} = \pi/2$  rotation, see appendix C. The estimated amplitudes, marked by the stars in figure 5, were  $0.229 \pm 0019$  and  $0.098 \pm 0005$  for CR1 and CR2, respectively.

#### <span id="page-9-1"></span>3.4. Optimizing CNOT fidelity with local operations

To estimate the highest fidelity of a maximally entangling gate that the CR gate can be transformed into, we optimize the average gate fidelity F over all single-qubit pre and post-rotation angles  $\Theta$  on both the control and target qubits, see appendix D. The optimized fidelities for the measured CR1 and CR2 process maps are  $F_{\text{max}} = 0.992$  and  $F_{\text{max}} = 0.994$ .

We then use the Qiskit transpiler and pulse scheduler to optimize and build a CNOT gate from the calibrated CR gate and the device-calibrated single-qubit gates [34] which implement the optimal local rotation parameters  $\Theta$  from equation (D1). The optimized CNOT schedules are shown in figure 3. The average gate fidelities of the calibrated CNOT gates are measured with randomized benchmarking (RB) [35]. The details of the pulse program applying the local rotations and setting up the RB measurements are given in appendix A.2. The RB experiments estimate an average gate fidelity of F = 0.981 and F = 0.979 for the CR1 and CR2 gates, respectively. These fidelities are comparable to the measured fidelity of F = 0.984 for the standard CNOT gate provided by <code>ibmq\_almaden</code> which is implemented using a highly-tuned calibration process including an echo sequence, cancellation tone, and closed-loop amplitude calibration [24]. It is worth noting that the CNOT gates demonstrated in this paper have no cancellation tone and all parameters are obtained with open-loop calibration. In the same way, we can create custom basis gates which may enable hardware-efficient implementations of quantum algorithms.

#### <span id="page-9-0"></span>4. Readout at the pulse level

Readout is the process through which the qubit state is projected onto  $|0\rangle$  or  $|1\rangle$  and a corresponding classical bit is obtained. This process is modeled by a readout chain in which the observed signal undergoes

![](_page_10_Figure_3.jpeg)

<span id="page-10-0"></span>**Figure 5.** CR Hamiltonian coefficients reconstructed following the procedure described in appendix [C,](#page-14-1) plotted against the time-averaged CR pulse amplitude *A*. The blue solid lines are the fits to the third order expansion of the CR Hamiltonian in equation [\(C6\)](#page-15-2). The rotation angle is estimated by θ = *n*CRω*ijt*CR where *n*CR is the number of CR pulses. Star-shaped markers indicate operating points of CNOT gates. (a) Measured coefficients of the CR1 sequence. The *ZI* coefficient is several orders of magnitude larger than other Hamiltonian terms and is displayed with a 1/100 scale in (a) whereas in (b) it is approximately zeroed by the echo pulse in CR2 and is therefore not scaled.

a series of successive transformations. Qiskit Pulse supports returning the output data of each measurement layer to the programmer. The lowest level accessible to the user, level-zero or *raw* data, typically corresponds to a digitized time-series signal. A kernel method applied to the signal data removes its time dependency and results in a complex value which encodes the qubit state (level-one *kerneled* data). Finally, the classified qubit state (level-two *disciminated* data), is obtained by applying a discriminator to the kerneled data. For a superconducting qubit processor, the time traces are complex vectors representing the digitized readout signals reflected or transmitted from the readout resonators [\[9\]](#page-16-8). The kernel method, such as the boxcar integrator used within this paper, outputs points in the IQ plane which a discriminator may use to classify the qubit's state.

Qiskit users are now able to retrieve data from different levels in the readout-chain by specifying the readout data-level, i.e., zero, one, or two. For example, users of IBM Quantum processors may request the kerneled data in the form of IQ points so that they may implement their own discriminator. To be sure, Qiskit users that do not wish to implement their own kernels and discriminators can request level-two data using the built-in readout scheme. The readout methodology that we implemented reflects the typical data flow during readout in hardware and should allow users to test novel readout schemes [\[36\]](#page-16-33) as well as accommodate different quantum computing architectures.

Aside from counting qubit states, discriminators may also be used to infer properties of the system and benchmark it. We illustrate this by investigating spurious correlations in the qubit readout of the IBM Quantum system ibmq\_singapore selected based on its availability at the time of the experiment. From ibmq\_singapore we randomly selected qubits 16 and 17 to study as they are a neighboring pair of qubits on the chip. Kerneled data was measured for four calibration schedules, named cal\_ij with *i*, *j* ∈ {0, 1}. Here, to prepare the state |*ij* a π-pulse is applied to qubit *i* if *i* = 1 and simultaneously to qubit *j* if *j* = 1. The single-qubit pulses are followed by the measurement stimulus pulses and acquisition instructions for all qubits. For each qubit we fit two discriminators based on linear discriminant analysis [\[36\]](#page-16-33). For qubit *i*, one discriminator is fitted to a subset of the calibration data in which the other qubit is always in state |0, shown in figure [6,](#page-11-1) while the other discriminator is fitted using all four calibration schedules. We expect that the discriminator that uses all the calibration data will perform best if there is measurement cross-talk. The fidelities of the fitted discriminators, shown in table [2,](#page-11-2) suggest that there is no significant cross-talk between the qubits that we measured. This is verified by *t*-tests on sixteen Pearsons'

![](_page_11_Figure_3.jpeg)

<span id="page-11-1"></span>**Figure 6.** IQ data and the decision boundary for the discriminators of qubits 16, shown in (a), and 17, shown in (b), that use only the IQ data of their respective qubit.

<span id="page-11-2"></span>Table 2. The measurement assignment fidelity  $F_a = 1 - (Pr[0|1] + Pr[1|0])/2$  of the four discriminators [36]. For example, the Single-Q16 discriminator was fitted with the calibration schedules  $cal_00$  and  $cal_01$  while the discriminator Both-Q16 was fitted with all four calibration schedules:  $cal_00$ ,  $cal_01$ ,  $cal_110$  and  $cal_111$ . The confidence intervals were obtained using Jeffreys interval at a 95% confidence level.

|           |        | Qubit discriminated       |                           |
|-----------|--------|---------------------------|---------------------------|
|           |        | Q16                       | Q17                       |
| Data used | Single | $89.21^{+1.78}_{-2.00}\%$ | $91.06^{+1.42}_{-1.65}\%$ |
|           | Both   | $89.48^{+1.26}_{-1.38}\%$ | $90.62^{+1.05}_{-1.16}\%$ |

correlation coefficients  $r_j(ES_{i,X}, GS_{i,Y})$  between  $ES_{i,X}$  and  $GS_{i,Y}$  which correspond to the  $X, Y \in \{I, Q\}$  data of qubit i in state  $j \in \{0, 1\}$  when the other qubit is in the excited state  $(ES, i.e., |1\rangle)$  and ground state  $(GS, i.e., |0\rangle)$ , respectively. These correlation coefficients are sensitive to cross-talk between the two qubits. With 1024 degrees of freedom, i.e., measurement shots, we do not observe any statistically significant correlation at the 95% confidence level. This implies that it is sufficient to fit discriminators using only a ground and excited reference schedule for each qubit and consequently only 2n calibration schedules are required for n qubits when there is no cross-talk rather than the  $2^n$  calibration schedules that would be required with all-to-all measurement crosstalk.

#### <span id="page-11-0"></span>5. Conclusions and future work

Rapid development in quantum computing has led to publicly available quantum computers with an increasing number of qubits, improved connectivity, and greater control. Prior to this work, publicly available quantum programming frameworks for cloud-based quantum computers have been at the relatively high-level of the circuit model, or implementation-specific, thus limiting their application. In the near-term, pulse-level control is desired to extract as much quantum volume as possible from the hardware by experimenting with novel control and characterization schemes [37–39].

We have introduced Qiskit Pulse, an implementation of the virtual pulse-level programming model, OpenPulse [8]. We have demonstrated that the Qiskit circuit scheduler can target pulse instructions and that physical superconducting qubit hardware can interpret these instructions to execute useful programs. By embedding our pulse programming instruction set in Qiskit we have integrated gate-level quantum programs and classical pulse stimulus, exposing a new level of hardware control to Qiskit users. The benefit that pulse control provides quantum programmers was demonstrated by calibrating a cross-resonance pulse on a cloud-based quantum computer and embedding it as a gate within the standard circuit programming model.

Giving users pulse-level access to current-day quantum computers will allow them to explore techniques such as error mitigation and dynamical decoupling schemes that cannot be investigated at the circuit level. In the future we will explore embedding the pulse programming model as a coprocessor within a classical virtual ISA that supports arithmetic and control-flow [\[40\]](#page-17-0). We will also investigate extensions to the pulse programming model such as defining special purpose registers to track phase across multiple channels which would reduce the number of required PulseChannels and enable simpler tracking of shared phase for composite gates. These capabilities will be used to explore the implementation of active error-correcting codes, and promising variational quantum–classical algorithms such as the variational quantum eigensolver [\[41–](#page-17-1)[43\]](#page-17-2).

# **Acknowledgments**

We thank Blake Johnson for insightful discussions. We thank Andrew Wack and John Lemek for providing system access and deployments.

# **Appendix A. Programming with Qiskit pulse**

# <span id="page-12-0"></span>**A.1. Performing quantum process tomography**

The code example below demonstrates how the QPT schedules for the CR1 used in section [3](#page-6-0) are created with Qiskit Pulse.

The above example uses the mock backend FakeAlmaden for IBM Quantum system ibmq\_almaden which can be substituted for the real backend.

The pulse envelope of the CR1 cr1\_pulse is created with a flat-topped Gaussian pulse. The pulse schedule sched of CR1 is then added to the basis\_gates and the circuit instruction to pulse schedule mapping inst\_map for qubits one and zero with the name cr1. The basis\_gates defines a list of primitive circuit instructions available in the system and the inst\_map defines a lookup table of calibrated pulse schedules for each basis gate on each qubit. The circuit object of the CR1 sequence is created with

a custom gate cr1\_gate. The QPT circuits are then assembled by calling the process\_tomography\_ circuits function in Qiskit-Ignis. This appends state preparation circuits and measurement circuits before and after the circuit. The returned qpt\_circuits is a list of quantum circuits containing each possible combination of input states and measurement bases. The qpt\_circuits are then mapped to the backend in question by Qiskit's transpiler, taking into account the extended set of basis\_gates. Finally, we call the pulse scheduler with the custom inst\_map containing CR1 to create the QPT pulse schedules. The QPT program for the CR2 sequence is created with the same procedure.

#### <span id="page-13-0"></span>**A.2. Performing randomized benchmarking**

The code example below demonstrates how the standard RB schedules with the CR1–CNOT used in section [3.4](#page-9-1) are created in the qiskit pulse module.

As shown in section A.1, the pulse schedules are programmed with the aid of the QuantumCircuit class to apply device calibrated single-qubit gates around the CR1 pulse sequence abstracted by cr1\_gate. The local rotation parameters can be obtained by the optimization routine shown in section D. It should be noted that in a standard two-qubit RB sequence the CNOT gate can assign both qubit 0 and 1 as a control qubit. Beacuse the CNOT gate is not identical under the exchange of the control and the target qubits, we need to prepare pulse schedules for both qubit arrangements. Then, the default CNOT instruction in the inst\_map is overwitten by the pulse schedules based on the calibrated CR1 sequence. Finally, the RB circuits are generated by a call to the randomized\_benchmarking\_seq function in Qiskit-Ignis. The returned rb\_circuits\_seeds is a list of RB circuits for each random seed. These RB circuits are then independently transpiled and scheduled to create RB pulse programs. The RB programs for the CR2 sequence are created with the same procedure.

# <span id="page-14-0"></span>Appendix B. Cross resonance phase calibration

In the twenty-qubit IBM Quantum system  $ibmq_almaden$ , microwave pulses programmed with Qiskit Pulse are generated by waveform generators at room temperature and travel through coaxial cables to the qubits [44]. The transfer function between the room temperature electronics and the qubits can cause a phase offset  $\phi_0$  in equation (1) resulting in an error in the rotation axis of the target qubit. The Hamiltonian may therefore have an unwanted ZY interaction term which we eliminate by adjusting the phase of CR pulse  $\phi$ . We perform this calibration with the CR2 schedule since its time-independent Hamiltonian, which we approximate by

$$\overline{H}_{CR} \simeq \Omega(A, \phi) (\cos \phi_0 ZX + \sin \phi_0 ZY) + \varepsilon,$$
 (B1)

has fewer terms than the CR1 Hamiltonian due to the echo. Here,  $\Omega$  is the strength of the CR drive as a function of its amplitude A and its phase  $\phi$  while  $\varepsilon$  represents the small interaction terms which are not fully refocused by the echo sequence.

First, we initialize the qubit in the  $|00\rangle$  state. We sweep the amplitude A and measure the target qubit in the Pauli-Z basis to find the pulse amplitude  $A_{\rm opt}=0.108$  which creates an equal superposition of  $|0\rangle$  and  $|1\rangle$ . If the offset  $\phi_0$  is zero this transformation is a  $\pi/2$ -rotation around the X-axis so that the target qubit, measured in the Y-basis, yields  ${\rm Tr}(\hat{\sigma_y}\rho)=\pm 1$  with the sign depending on the state of the control qubit. We thus measure the readout signal at  $A_{\rm opt}$  in the Y-basis for both initial states of the control qubit  $|10\rangle$  and  $|00\rangle$ , while sweeping the phase  $\phi$ . The calibrated phase that maximizes  $|{\rm Tr}(\hat{\sigma_y}\rho)|$  is  $\phi_{\rm opt}=-0.166$  rad.

### <span id="page-14-1"></span>Appendix C. Effective Hamiltonian estimation and amplitude calibration

We use the fitted Choi-matrices  $\mathcal{E}_{CR}(A)$  to compute estimates of the coefficients of the effective CR Hamiltonian in equation (2). Since a real CR pulse will have noise the resulting process is not unitary. Noisy quantum evolution for a time-independent Hamiltonian in the presence of Markovian noise may be described by the *Lindblad equation*  $\frac{d}{dt}\rho(t) = \mathcal{G}(\rho)$  with the Lindblad generator

$$\mathcal{G}(\rho) = \mathcal{L}_H(\rho) + \mathcal{D}(\rho) \tag{C1}$$

$$\mathcal{L}_{H}(\rho) = -i[H, \rho] \tag{C2}$$

$$\mathcal{D}(\rho) = \sum_{j} \gamma_{j} \left( A_{j} \rho A_{j}^{\dagger} - \frac{1}{2} \{ A_{j}^{\dagger} A_{j}, \rho \} \right), \tag{C3}$$

where the operator  $\mathcal{L}$  is the generator of the unitary evolution, and  $\mathcal{D}$  is the generator of the non-unitary dissipative evolution. As with unitary evolution, the Lindblad equation can be solved as a matrix differential equation obtaining  $|\rho(t)\rangle\rangle = S_{\mathcal{E}}|\rho(0)\rangle\rangle$ , where  $|A\rangle\rangle$  denotes a *column-vectorized* matrix A, and  $S_{\mathcal{E}} = \exp(tS_{\mathcal{G}})$  is the *superoperator* representation of quantum process  $\mathcal{E}$  [32].

For a Hamiltonian H we note that the operators  $B_{ij} = \frac{1}{2}P_i \otimes P_j$ , with  $P_i$  are single-qubit Pauli operators and define an orthonormal basis for two-qubit operators—i.e.  $\text{Tr}[B_{ij}B_{kl}^{\dagger}] = \delta_{ik}\delta_{jl}$ . Hence for a Hamiltonian given by  $H = \sum_{ij} \omega_{ij}B_{ij}$ , we can extract the coefficients via  $\omega_{ij} = \text{Tr}[B_{ij}^{\dagger}H]$ . The superoperator for the Hamiltonian component of  $\mathcal{G}$  is given by

$$S_{\mathcal{L}_H} = -i(\mathbb{I} \otimes H - H^T \otimes \mathbb{I}). \tag{C4}$$

We can use the fact that the superoperators of the Hamiltonian basis term  $S_{\mathcal{L}_{B_{ij}}}$  are also an orthogonal (but not-normalized) basis for  $S_{\mathcal{L}_{H}}$ , and importantly, are orthogonal to the dissipative part of the generator

 $(\text{Tr}[S_{\mathcal{L}_{B_{ij}}}^{\dagger}S_{\mathcal{D}}]=0)$  when the dissipator only involves Pauli and  $T_1$  and  $T_2$  relaxation terms. This allows us to extract the coefficients from the Lindblad superoperator generator as

<span id="page-15-3"></span>
$$\omega_{ij} = \frac{\text{Tr}\left[S_{\mathcal{L}_{B_{ij}}}^{\dagger} S_{\mathcal{G}}\right]}{\|S_{\mathcal{L}_{B_{ii}}}\|}.$$
 (C5)

To compute the superoperator generator  $S_G$ , we first obtain the Choi-matrix estimate for a channel  $\mathcal{E}$  from QPT and then convert it to the superoperator representation  $S_{\mathcal{E}}$ . For additional details on the superoperators and converting between superoperators and the Choi-matrix representation obtained from tomography see [32]. Next, we take the matrix logarithm to obtain the generator  $S_G = t^{-1} \log(S_{\mathcal{E}})$  from which we estimate  $\omega_{ij}$  for our two-qubit system using equation (C5). The process fidelities of the estimated CR Hamiltonian using this technique and the experimentally obtained Choi-matrix are 99.4% and 98.6% on average for CR1 and CR2 experiments, respectively.

We find that as predicted only the terms ZX, ZY, ZZ, ZI, IX, IY, and IZ, shown in figure 5, are significant for CR1 and CR2 while all other remaining Pauli terms are negligible. In both CR sequences the ZY term is suppressed by the calibrated CR phase  $\phi_{\rm opt}$  and a monotonic increase of the desired ZX term is observed as the pulse amplitude A increases. The CR1 pulse without echoing has large contributions from the IX, IY and ZI terms, see figure 5(a). Such unwanted interactions, except for ZZ, are removed by the echo sequence in CR2, compare figures 5(a) and (b). The effect of these unwanted interactions can be reduced by applying single-qubit gates before and after the CR pulse to correct for local coherent errors as discussed in section 3.4.

We now find the CR pulse amplitude that creates a maximum entangling gate, i.e.  $\theta_{ZX}=\pi/2$  in equation (3). Due to the Gaussian edges of our CR pulses we relate the drive strength  $\Omega$  to the time-averaged pulse amplitude  $\overline{A}$  through a linear response  $\Omega=\lambda\overline{A}$ . The measured ZX interaction strengths are fit by the third order expansion of the CR Hamiltonian [28]

<span id="page-15-2"></span>
$$\frac{\omega_{ZX}(\overline{A})}{2} = -\frac{J\lambda\overline{A}}{\Delta} \left(\frac{\delta_1}{\delta_1 + \Delta}\right) + \frac{J(\lambda\overline{A})^3 \delta_1^2 (3\delta_1^3 + 11\delta_1^2 \Delta + 15\delta_1 \Delta^2 + 9\Delta^3)}{4\Delta^3 (\delta_1 + \Delta)^3 (\delta_1 + 2\Delta)(3\delta_1 + 2\Delta)}$$
(C6)

where J is the coupling strength,  $\delta_1$  is the anharmonicity of the control qubit, and  $\Delta$  is the frequency difference between the control and target qubits. In this model, we have a pair of fit parameters J and  $\lambda$ . The coupling strength obtained from the fit was  $J=1.87\pm0.046\,\mathrm{MHz}$  and  $1.79\pm0.033\,\mathrm{MHz}$  for the CR1 and CR2 data, respectively. The  $\lambda$  coefficient was  $-271.2\pm12.2\,\mathrm{MHz}$  and  $-288.9\pm10.2\,\mathrm{MHz}$  for the CR1 and CR2 data, respectively. These fit parameters are independent of the pulse sequences and both results almost agree within the error range. The small mismatch between the fit values may be caused by imperfections in the Hamiltonian reconstructed from the tomography data. These fit curves yield the controlled rotation angle as a function of the CR pulse amplitude  $\theta_{ZX}(\overline{A}) = n_{CR}\omega_{ZX}(\overline{A})t_{CR}$  where  $n_{CR}=1$  for CR1 and  $n_{CR}=2$  for CR2. Finally, we can find the pulse amplitudes  $\overline{A}$  for  $\theta_{ZX}=\pi/2$ . The estimated amplitudes were respectively 0.229  $\pm$  0019 and 0.098  $\pm$  0005 for CR1 and CR2. These are marked by the stars in figure 5. Due to the nonlinearity between the ZX term and the average pulse amplitude  $\overline{A}$ , see equation (C6), the estimated drive amplitude of CR1 is slightly larger than double the drive amplitude of CR2.

#### <span id="page-15-0"></span>Appendix D. Optimizing CNOT fidelity with local operations

To estimate the highest fidelity of a maximally entangling gate that the CR gate can be transformed into, we optimize the average gate fidelity *F* over all single-qubit pre and post-rotations on both the control and target qubits:

$$F_{\text{max}} = \max_{\Theta} F[\mathcal{E}_{\text{CR}}(\overline{A}_{\pi/2}), U_{\text{ent}}(\Theta)]$$
 (D1)

<span id="page-15-1"></span>where the optimization is over 12 real parameters for the four parameterized  $U_3(\Theta_i, \Theta_j, \Theta_k)$  rotations in SU(2):

$$\begin{split} U_{\text{ent}}(\Theta) &= U_{\text{pre}}^{\dagger}(\Theta)U_{\text{ent}}U_{\text{post}}^{\dagger}(\Theta), \\ U_{\text{pre}}(\Theta) &= U_{3}(\Theta_{0},\Theta_{1},\Theta_{2}) \otimes U_{3}(\Theta_{3},\Theta_{4},\Theta_{5}), \\ U_{\text{post}}(\Theta) &= U_{3}(\Theta_{6},\Theta_{7},\Theta_{8}) \otimes U_{3}(\Theta_{9},\Theta_{10},\Theta_{11}). \end{split}$$

The ideal unitary matrix for the cross-resonance perfect-entangler is  $U_{\text{ent}} = ZX(\pi/2)$  and for the CNOT gate is  $U_{\text{ent}} = CX$ . This optimization aims to remove the effect of locally correctable coherent errors. It will,

however, underestimate the error of the transformed CR gate as it neglects errors in the single-qubit gates. The optimized fidelities for the measured CR1 and CR2 process maps are *F*max = 0.994 and *F*max = 0.998.

# **ORCID iDs**

Thomas Alexander <https://orcid.org/0000-0003-3452-0082>

# **References**

- <span id="page-16-0"></span>[1] Aleksandrowicz G *et al* 2019 *Qiskit: An Open-Source Framework for Quantum Computing*
- <span id="page-16-1"></span>[2] Nielsen M A and Chuang I L 2000 *Quantum Computation and Quantum Information* (Cambridge: Cambridge University Press)
- <span id="page-16-2"></span>[3] Cross A W, Bishop L S, Smolin J A and Gambetta J M 2017 Open quantum assembly language (arXiv[:1707.03429\)](https://arxiv.org/abs/1707.03429)
- <span id="page-16-3"></span>[4] Isaac C 2005 Qasm2circ <https://media.mit.edu/quanta/qasm2circ/>
- <span id="page-16-4"></span>[5] Khammassi N, Guerreschi G G, Ashraf I, Hogaboam J W, Almudever C G and Bertels K 2018 cQASM v1.0: towards a common quantum assembly language (arXiv[:1805.09607\)](https://arxiv.org/abs/1805.09607)
- <span id="page-16-5"></span>[6] Glaser S J *et al* 2015 Training schrödinger's cat: quantum optimal control *Eur. Phys. J.* D **[69](https://doi.org/10.1140/epjd/e2015-60464-1)** [279](https://doi.org/10.1140/epjd/e2015-60464-1)
- <span id="page-16-6"></span>[7] Koch J *et al* 2007 Charge-insensitive qubit design derived from the cooper pair box *Phys. Rev.* A **[76](https://doi.org/10.1103/physreva.76.042319)** [042319](https://doi.org/10.1103/physreva.76.042319)
- <span id="page-16-7"></span>[8] McKay D C *et al* 2018 Qiskit backend specifications for OpenQASM and OpenPulse experiments (arXiv[:1809.03452\)](https://arxiv.org/abs/1809.03452)
- <span id="page-16-8"></span>[9] Krantz P, Kjaergaard M, Yan F, Orlando T P, Gustavsson S and Oliver W D 2019 A quantum engineer's guide to superconducting qubits *Appl. Phys. Rev.* **[6](https://doi.org/10.1063/1.5089550)** [021318](https://doi.org/10.1063/1.5089550)
- <span id="page-16-9"></span>[10] Fu X *et al* 2017 An experimental microarchitecture for a superconducting quantum processor *Proceedings of the 50th Annual IEEE/ACM International Symposium on Microarchitecture, MICRO-50 '17* (New York: ACM) pp 813–25
- [11] Butko A, Michelogiannakis G, Williams S, Iancu C, Donofrio D, Shalf J, Carter J and Siddiqi I 2019 Understanding quantum control processor capabilities and limitations through circuit characterization (arXiv[:1909.11719\)](https://arxiv.org/abs/1909.11719)
- <span id="page-16-10"></span>[12] Ryan C A, Johnson B R, Rist´e D, Donovan B and Ohki T A 2017 Hardware for dynamic quantum computing *Rev. Sci. Instrum.* **[88](https://doi.org/10.1063/1.5006525)** [104703](https://doi.org/10.1063/1.5006525)
- <span id="page-16-11"></span>[13] Alexander T, Kanazawa N, Egger D J, Capelluto L, Wood C J, Javadi-Abhari A and McKay D 2020 Notebooks and data for 'Qiskit-Pulse: programming quantum computers through the cloud with pulses' <https://doi.org/10.5281/zenodo.3751565>
- <span id="page-16-12"></span>[14] Metodi T S, Thaker D D, Cross A W, Chong F T and Chuang I L 2006 Scheduling physical operations in a quantum information processor *Quantum Information and Computation IV* vol 6244 (International Society for Optics and Photonics) [62440T](https://doi.org/10.1117/12.666419)
- <span id="page-16-13"></span>[15] Khaneja N, Reiss T, Kehlet C, Schulte-Herbrüggen T and Glaser S J 2005 Optimal control of coupled spin dynamics: design of NMR pulse sequences by gradient ascent algorithms *J. Magn. Reson.* **[172](https://doi.org/10.1016/j.jmr.2004.11.004)** [296–305](https://doi.org/10.1016/j.jmr.2004.11.004)
- <span id="page-16-14"></span>[16] Temme K, Bravyi S, Jay M and Gambetta 2017 Error mitigation for short-depth quantum circuits *Phys. Rev. Lett.* **[119](https://doi.org/10.1103/physrevlett.119.180509)** [180509](https://doi.org/10.1103/physrevlett.119.180509)
- [17] Richardson L F and Arthur Gaunt J 1927 VIII. The deferred approach to the limit *Phil. Trans. R. Soc.* A **[226](https://doi.org/10.1098/rsta.1927.0008)** [299–361](https://doi.org/10.1098/rsta.1927.0008)
- <span id="page-16-15"></span>[18] Kandala A, Temme K, C´orcoles A D, Mezzacapo A, Chow J M and Gambetta J M 2019 Error mitigation extends the computational reach of a noisy quantum processor *Nature* **[567](https://doi.org/10.1038/s41586-019-1040-7)** [491–5](https://doi.org/10.1038/s41586-019-1040-7)
- <span id="page-16-16"></span>[19] Lurie D J 1969 Numerical design of composite radiofrequency pulses *J. Magn. Reson.* **[70](https://doi.org/10.1016/0022-2364(86)90359-8)** [11–20](https://doi.org/10.1016/0022-2364(86)90359-8)
- <span id="page-16-17"></span>[20] McKay D C, Wood C J, Sheldon S, Chow J M and Gambetta J M 2017 Efficient *Z* gates for quantum computing *Phys. Rev.* A **[96](https://doi.org/10.1103/physreva.96.022330)** [022330](https://doi.org/10.1103/physreva.96.022330)
- <span id="page-16-18"></span>[21] Jeffrey E *et al* 2014 Fast accurate state measurement with superconducting qubits *Phys. Rev. Lett.* **[112](https://doi.org/10.1103/physrevlett.112.190504)** [190504](https://doi.org/10.1103/physrevlett.112.190504)
- <span id="page-16-19"></span>[22] Heinsoo J *et al* 2018 Rapid high-fidelity multiplexed readout of superconducting qubits *Phys. Rev. Appl.* **[10](https://doi.org/10.1103/physrevapplied.10.034040)** [034040](https://doi.org/10.1103/physrevapplied.10.034040)
- <span id="page-16-20"></span>[23] Cooper K and Torczon L 2003 *Engineering a Compiler* 1st edn (San Mateo, CA: Morgan Kaufmann)
- <span id="page-16-21"></span>[24] Sheldon S, Magesan E, Chow J M and Gambetta J M 2016 Procedure for systematically tuning up cross-talk in the cross-resonance gate *Phys. Rev.* A **[93](https://doi.org/10.1103/physreva.93.060302)** [060302](https://doi.org/10.1103/physreva.93.060302)
- <span id="page-16-22"></span>[25] Shi Y, Leung N, Gokhale P, Rossi Z, Schuster D I, Hoffmann H and Chong F T 2019 Optimized compilation of aggregated instructions for realistic quantum computers *Proceedings of the Twenty-Fourth International Conference on Architectural Support for Programming Languages and Operating Systems, ASPLOS '19* (Providence, RI: Association for Computing Machinery) pp 1031–44
- <span id="page-16-23"></span>[26] Mohseni M, Rezakhani A T and Lidar D A 2008 Quantum-process tomography: resource analysis of different strategies *Phys. Rev.* A **[77](https://doi.org/10.1103/physreva.77.032322)** [032322](https://doi.org/10.1103/physreva.77.032322)
- <span id="page-16-24"></span>[27] Chow J M *et al* 2011 Simple all-microwave entangling gate for fixed-frequency superconducting qubits *Phys. Rev. Lett.* **[107](https://doi.org/10.1103/physrevlett.107.080502)** [080502](https://doi.org/10.1103/physrevlett.107.080502)
- <span id="page-16-25"></span>[28] Magesan E and Gambetta J M 2018 Effective Hamiltonian models of the cross-resonance gate *Phys. Rev.* A **[101](https://doi.org/10.1103/PhysRevA.101.052308)** [052308](https://doi.org/10.1103/PhysRevA.101.052308)
- <span id="page-16-26"></span>[29] Zhang J, Vala J, Sastry S and Birgitta Whaley K 2003 Geometric theory of nonlocal two-qubit operations *Phys. Rev.* A **[67](https://doi.org/10.1103/physreva.67.042313)** [042313](https://doi.org/10.1103/physreva.67.042313)
- <span id="page-16-27"></span>[30] Willsch D, Nocon M, Jin F, De Raedt H and Michielsen K 2017 Gate-error analysis in simulations of quantum computers with transmon qubits *Phys. Rev.* A **[96](https://doi.org/10.1103/physreva.96.062302)** [062302](https://doi.org/10.1103/physreva.96.062302)
- <span id="page-16-28"></span>[31] IBM Qiskit Ignis 2019 <https://github.com/Qiskit/qiskit-ignis>(accessed: 2019–12-31)
- <span id="page-16-29"></span>[32] Wood C J, Biamonte J D and Cory D G 2015 Tensor networks and graphical calculus for open quantum systems *Quantum. Inf. Comput.* **[15](https://doi.org/10.26421/QIC15.9-10)** [0759–811](https://doi.org/10.26421/QIC15.9-10)
- <span id="page-16-30"></span>[33] Dewes A, Ong F R, Schmitt V, Lauro R, Boulant N, Bertet P, Vion D and Esteve D 2012 Characterization of a two-transmon processor with individual single-shot qubit readout *Phys. Rev. Lett.* **[108](https://doi.org/10.1103/physrevlett.108.057002)** [057002](https://doi.org/10.1103/physrevlett.108.057002)
- <span id="page-16-31"></span>[34] The general single-qubit gate is built from a pair of π/2-pulses with three virtual *Z*-gates with rotation angles Θ*i*, Θ*j*, and Θ*k*
- <span id="page-16-32"></span>[35] Magesan E, Gambetta J M and Joseph E 2011 Scalable and robust randomized benchmarking of quantum processes *Phys. Rev. Lett.* **[106](https://doi.org/10.1103/physrevlett.106.180504)** [180504](https://doi.org/10.1103/physrevlett.106.180504)
- <span id="page-16-33"></span>[36] Magesan E, Gambetta J M, C´orcoles A D and Chow J M 2015 Machine learning for discriminating quantum measurement trajectories and improving readout *Phys. Rev. Lett.* **[114](https://doi.org/10.1103/physrevlett.114.200501)** [200501](https://doi.org/10.1103/physrevlett.114.200501)
- <span id="page-16-34"></span>[37] Bishop L, Bravyi S, Cross A W, Gambetta J M and Smolin J A 2017 Quantum volume [http://book.itep.ru/depository/quant\\_](http://book.itep.ru/depository/quant_comp/quant_volume.pdf) [comp/quant\\_volume.pdf](http://book.itep.ru/depository/quant_comp/quant_volume.pdf)
- <span id="page-16-35"></span>[38] White G A L, Hill C D and Hollenberg L C L 2019 Performance optimisation for drift-robust fidelity improvement of two-qubit gates (arXiv[:1911.12096\)](https://arxiv.org/abs/1911.12096)

- [39] Werninghaus M, Egger D J, Roy F, Machnes S, Wilhelm F K and Filipp S 2020 Leakage reduction in fast superconducting qubit gates via optimal control (arXiv[:2003.05952\)](https://arxiv.org/abs/2003.05952)
- <span id="page-17-0"></span>[40] Adve V, Lattner C, Brukman M, Shukla A and Gaeke B 2003 LLVA: a low-level virtual instruction set architecture *Proceedings of the 36th Annual IEEE/ACM International Symposium on Microarchitecture, MICRO* vol 36 (Washington, DC: IEEE Computer Society) p 205
- <span id="page-17-1"></span>[41] Noh K and Chamberland C 2019 Fault-tolerant bosonic quantum error correction with the surface-GKP code *Phys. Rev.* A **[101](https://doi.org/10.1103/PhysRevA.101.012316)** [012316](https://doi.org/10.1103/PhysRevA.101.012316)
- [42] Kandala A, Mezzacapo A, Temme K, Takita M, Brink M, Chow J M and Gambetta J M 2017 Hardware-efficient variational quantum eigensolver for small molecules and quantum magnets *Nature* **[549](https://doi.org/10.1038/nature23879)** [242–6](https://doi.org/10.1038/nature23879)
- <span id="page-17-2"></span>[43] Ganzhorn M *et al* 2019 Gate-efficient simulation of molecular eigenstates on a quantum computer *Phys. Rev. Appl.* **[11](https://doi.org/10.1103/physrevapplied.11.044092)** [044092](https://doi.org/10.1103/physrevapplied.11.044092)
- <span id="page-17-3"></span>[44] Krinner S, Simon S, Kurpiers P, Paul M, Heinsoo J, Keller R, Luetolf J, Eichler C and Wallraff A 2019 Engineering cryogenic setups for 100-qubit scale superconducting circuit systems *EPJ Quantum Technol.* **[6](https://doi.org/10.1140/epjqt/s40507-019-0072-0)** [2](https://doi.org/10.1140/epjqt/s40507-019-0072-0)