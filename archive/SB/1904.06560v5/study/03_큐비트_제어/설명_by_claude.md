# 섹션 IV: Qubit Control — 상세 설명

**논문:** A quantum engineer's guide to superconducting qubits (arXiv: 1904.06560v5)
**대상:** 물리/공학 대학원생

---

## 목차

1. [개요: 왜 qubit 제어를 공부하는가?](#1-개요)
2. [고전 논리 gate와 양자 논리 gate 비교](#2-고전-vs-양자-gate)
3. [Single-qubit gate: capacitive coupling을 통한 X, Y 제어](#3-single-qubit-gate)
4. [Rotating frame 유도](#4-rotating-frame-유도)
5. [Virtual Z gate](#5-virtual-z-gate)
6. [DRAG 방식](#6-drag-방식)
7. [Two-qubit gate: tunable qubit에서의 iSWAP](#7-iswap-gate)
8. [Two-qubit gate: CPHASE gate](#8-cphase-gate)
9. [Microwave만을 이용한 gate: bSWAP, MAP, RIP](#9-microwave-전용-gate)
10. [Tunable coupling](#10-tunable-coupling)
11. [핵심 요약](#11-핵심-요약)

---

## 1. 개요

이 섹션은 **초전도 qubit을 실제로 어떻게 조작하여 양자 알고리즘을 실행하는가**를 다룬다. 논문의 논의는 현재 가장 널리 사용되는 **transmon** 계열의 초전도 qubit에 집중되어 있지만, 원리는 모든 종류의 초전도 qubit에 적용된다.

### 계산 기저 (Computational Basis) 규약

이 섹션 전체에서 사용하는 규약:

- 계산 기저: $\{|0\rangle, |1\rangle\}$
  - $|0\rangle$: $\sigma_z$의 $+1$ 고유상태 (Bloch sphere의 북극)
  - $|1\rangle$: $\sigma_z$의 $-1$ 고유상태 (Bloch sphere의 남극)

- $x$축 주위 각도 $\theta$ 회전 연산자:

$$X_{\theta} = R_X(\theta) = e^{-i\frac{\theta}{2}\sigma_x} = \cos(\theta/2)\mathbb{1} - i\sin(\theta/2)\sigma_x \quad \text{(식 62)}$$

- 약어: **X** = $\pi$ 회전 (즉, $X_\pi$), **Y** = $Y_\pi$, **Z** = $Z_\pi$

**물리적 의미:** qubit 상태는 Bloch sphere 위의 한 점으로 표현되며, single-qubit gate란 이 점을 구의 특정 축 주위로 회전시키는 조작이다.

---

## 2. 고전 vs 양자 gate

### 2-1. 고전 논리 gate

고전 컴퓨터는 **비트(bit)**를 다루는데, 비트는 0 또는 1의 두 값만 가진다. 주요 고전 논리 gate:

| gate | 입력 수 | 동작 | 가역성 |
|------|---------|------|--------|
| NOT | 1 | 0→1, 1→0 | **가역** |
| AND | 2 | 두 입력 모두 1이면 출력 1 | 비가역 |
| OR | 2 | 하나 이상 1이면 출력 1 | 비가역 |
| NAND | 2 | AND의 부정 | 비가역 |
| NOR | 2 | OR의 부정 | 비가역 |
| XOR | 2 | 두 입력이 다르면 1 (패리티 gate) | 비가역 |

**NOT gate는 가역적이지만, 나머지 2입력 gate들은 비가역적**이다. AND gate의 경우 출력 0이 나왔을 때, 입력이 00이었는지 01이었는지 10이었는지 알 수 없기 때문이다. 정보가 소실된다.

**Universal gate set:** 임의의 논리 연산을 수행할 수 있는 최소한의 gate 조합. 예를 들어 NAND 하나만으로도 universal gate set이 된다.

### 2-2. Single-qubit 양자 gate

Fig. 9에 제시된 주요 single-qubit gate:

| gate | 행렬 표현 | 물리적 의미 |
|------|-----------|------------|
| **I** | $\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$ | 아무 조작 없음 |
| **X** | $\begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$ | $x$축 주위 $\pi$ 회전; 고전 NOT의 양자 버전 |
| **Y** | $\begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}$ | $y$축 주위 $\pi$ 회전 |
| **Z** | $\begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$ | $z$축 주위 $\pi$ 회전; 상대 위상 반전 |
| **S** | $\begin{pmatrix} 1 & 0 \\ 0 & e^{i\pi/2} \end{pmatrix}$ | $z$축 주위 $\pi/2$ 회전 |
| **T** | $\begin{pmatrix} 1 & 0 \\ 0 & e^{i\pi/4} \end{pmatrix}$ | $z$축 주위 $\pi/4$ 회전 |
| **H** (하다마드) | $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$ | $x$-$z$ 대각선 축 주위 $\pi$ 회전; superposition 상태 생성 |

### 2-3. Two-qubit 양자 gate

Fig. 10에 제시된 주요 two-qubit gate:

**CNOT gate** (Controlled-NOT):

$$U_{\mathsf{CNOT}} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{bmatrix} = |0\rangle\langle 0| \otimes \mathbb{1} + |1\rangle\langle 1| \otimes \mathsf{X} \quad \text{(식 63)}$$

**물리적 의미:** 제어 qubit(control qubit)이 $|1\rangle$일 때만 표적 qubit(target qubit)에 X gate(비트 플립)를 적용한다. 제어 qubit이 $|0\rangle$이면 아무 일도 일어나지 않는다.

**CPHASE gate** (Controlled-Phase 또는 CZ):

$$U_{\mathsf{CPHASE}} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \end{bmatrix} = |0\rangle\langle 0| \otimes \mathbb{1} + |1\rangle\langle 1| \otimes \mathsf{Z} \quad \text{(식 64)}$$

**물리적 의미:** 두 qubit이 모두 $|1\rangle$ 상태일 때만 위상 $-1 = e^{i\pi}$이 적용된다. 다른 상태들($|00\rangle$, $|01\rangle$, $|10\rangle$)은 변하지 않는다. CPHASE는 어느 qubit이 제어이고 어느 것이 표적인지 구별이 없어 대칭적으로 그릴 수 있다.

**CNOT와 CPHASE의 관계:**

$$U_{\mathsf{CNOT}} = (\mathbb{1} \otimes \mathsf{H}) \, U_{\mathsf{CPHASE}} \, (\mathbb{1} \otimes \mathsf{H}) \quad \text{(식 65)}$$

이는 $\mathsf{HZH} = \mathsf{X}$ 라는 항등식에서 나온다. 즉, 표적 qubit에 하다마드 gate를 앞뒤로 적용하면 CPHASE가 CNOT로 변환된다.

### 2-4. 고전 vs 양자 gate의 핵심 차이점

1. **가역성:** 양자 gate는 **모두 가역적**이다. 이는 unitary 연산 $U$에 대해 $U^\dagger U = \mathbb{1}$이기 때문이다. 반면 고전의 AND, OR 등은 비가역적이다.

2. **Superposition과 quantum entanglement:** 양자 gate는 superposition 상태와 quantum entanglement 상태를 생성할 수 있다. CNOT를 $\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)_A \otimes |0\rangle_B$에 적용하면:

$$U_{\mathsf{CNOT}}|\psi\rangle = \frac{1}{\sqrt{2}}\left(|0\rangle_A|0\rangle_B + |1\rangle_A|1\rangle_B\right) \quad \text{(식 69)}$$

이는 Bell state로, 순수한 양자역학적 quantum entanglement 상태이다.

3. **회로 방향:** 양자 회로는 왼쪽에서 오른쪽으로 읽지만, 수식 계산은 오른쪽에서 왼쪽으로 적용한다:

$$|\psi_{\rm out}\rangle = U_n \cdots U_1 U_0 |\psi_{\rm in}\rangle \quad \text{(식 71)}$$

### 2-5. Universal quantum gate set

임의의 single-qubit 회전 + 하나의 quantum entanglement two-qubit gate = universal gate set.

실용적으로 많이 쓰이는 universal gate set:

$$\mathcal{G}_0 = \{ \mathsf{X}_{\theta}, \mathsf{Y}_{\theta}, \mathsf{Z}_{\theta}, \mathsf{Ph}_{\theta}, \mathsf{CNOT} \} \quad \text{(식 72)}$$

이론적으로 중요한 이산 universal gate set ("Clifford + T"):

$$\mathcal{G}_1 = \{\mathsf{H}, \mathsf{S}, \mathsf{T}, \mathsf{CNOT}\} \quad \text{(식 73)}$$

**Solovay-Kitaev 정리:** $\mathcal{G}_1$의 이산 gate set만으로도 임의의 single-qubit gate를 오차 $\epsilon$으로 근사하는 데 $\mathcal{O}(\log^c(1/\epsilon))$번의 gate로 충분하다. 즉, 이론적으로 이산 gate만으로 보편성이 달성된다.

**Native gate:** 각 하드웨어 아키텍처마다 Hamiltonian에서 자연스럽게 나오는 "고유 gate"가 있다. 초전도 qubit에서는 $X_\theta$, $Y_\theta$, $Z_\theta$가 microwave 구동으로 native하게 구현되고, two-qubit gate는 이후 섹션에서 다루는 iSWAP, CPHASE, CR gate 등이 native gate다.

---

## 3. Single-qubit gate

### 3-1. Capacitive coupling의 물리

Fig. 12: microwave 구동선(drive line)이 capacitor $C_d$를 통해 transmon qubit에 결합된 회로.

회로 Hamiltonian (양자화 전):

$$H = \frac{\tilde{Q}(t)^2}{2C_{\Sigma}} + \frac{\Phi^2}{2L} + \frac{C_{\rm d}}{C_{\Sigma}} V_{\rm d}(t) \tilde{Q} \quad \text{(식 75)}$$

여기서:
- $C_{\Sigma} = C + C_d$: 접지 기준 전체 capacitance
- $\tilde{Q} = C_\Sigma \dot{\Phi} - C_d V_d(t)$: 재정규화된 전하 변수
- $V_d(t)$: 구동선의 시간 의존 전압

약한 결합 가정($\tilde{Q} \approx \hat{Q}$) 후:

$$H = H_{\rm LC} + \frac{C_{\rm d}}{C_{\Sigma}} V_{\rm d}(t) \hat{Q} \quad \text{(식 76)}$$

전하 연산자를 생성/소멸 연산자로 표현:

$$\hat{Q} = -iQ_{\rm zpf}(a - a^\dagger) \quad \text{(식 77)}$$

여기서 $Q_{\rm zpf} = \sqrt{\hbar/2Z}$는 **영점 전하 요동(zero-point charge fluctuation)**이고 $Z = \sqrt{L/C}$는 회로 임피던스다.

따라서 LC oscillator + 구동 Hamiltonian:

$$H = \omega\left(a^\dagger a + \frac{1}{2}\right) - \frac{C_{\rm d}}{C_{\Sigma}} V_d(t) \, i Q_{\rm zpf} (a - a^\dagger) \quad \text{(식 78)}$$

**최저 전이만 고려 (2레벨 근사):** $a \to \sigma^-$, $a^\dagger \to \sigma^+$ 치환 후:

$$H = \underbrace{-\frac{\omega_{\mathbf{q}}}{2}\sigma_z}_{H_0} + \underbrace{\Omega V_{\mathbf{d}}(t)\sigma_y}_{H_{\mathbf{d}}} \quad \text{(식 79)}$$

여기서:
- $\Omega = (C_d/C_\Sigma)Q_{\rm zpf}$: 결합 강도 (회로 파라미터로 결정됨)
- $\omega_q = (E_1 - E_0)/\hbar$: qubit 전이 주파수
- $H_0$: qubit 자유 Hamiltonian
- $H_d$: 구동 Hamiltonian

**물리적 해석:** microwave 구동은 capacitor를 통해 qubit의 전하에 결합하며, 이 전하 연산자가 $\sigma_y$ 형태로 나타난다. 즉, 구동은 qubit 상태를 $y$축 주위로 회전시키는 효과를 갖는다 (rotating frame에서는 $x$ 또는 $y$축 모두 가능).

---

## 4. Rotating frame 유도

### 4-1. 왜 rotating frame이 필요한가?

Qubit 주파수 $\omega_q$는 수 GHz에 달한다. 이 주파수로 빠르게 회전하는 위상을 따라가며 계산하면 매우 복잡하다. **Rotating frame** 또는 **interaction frame**으로 변환하면 빠르게 진동하는 항들이 사라지고, 느린 구동 동역학만 남는다.

### 4-2. Rotating frame 변환

$|0\rangle = [1, 0]^T$ 초기 상태에서 $|\psi_0\rangle = (1,1)^T/\sqrt{2}$의 시간 진화:

$$|\psi_0(t)\rangle = e^{-iH_0 t}|\psi_0\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} e^{i\omega_q t/2} \\ e^{-i\omega_q t/2} \end{pmatrix} \quad \text{(식 80)}$$

$\langle\sigma_x\rangle = \cos(\omega_q t)$: qubit 주파수로 빠르게 진동한다.

Rotating frame 변환 연산자: $U_{\rm rf} = e^{iH_0 t}$

새 상태: $|\psi_{\rm rf}(t)\rangle = U_{\rm rf}|\psi_0\rangle$

슈뢰딩거 방정식에서 rotating frame의 유효 Hamiltonian (식 83):

$$\widetilde{H} = i\dot{U}_{\rm rf}U_{\rm rf}^\dagger + U_{\rm rf}H_0 U_{\rm rf}^\dagger$$

$H_0$ 자체를 변환하면 $\widetilde{H}_0 = 0$ (rotating frame에서 자유 Hamiltonian이 사라진다). 구동 Hamiltonian의 rotating frame 표현:

$$\widetilde{H}_{\rm d} = \Omega V_{\rm d}(t)\left(\cos(\omega_q t)\sigma_y - \sin(\omega_q t)\sigma_x\right) \quad \text{(식 84)}$$

### 4-3. IQ 변조와 rotating wave approximation (RWA)

구동 전압의 일반적인 형태:

$$v(t) = s(t)\sin(\omega_d t + \phi) \quad \text{(식 85)}$$

여기서:
- $s(t)$: 무차원 포락선(envelope) 함수 (AWG로 생성)
- $\omega_d$: 구동 주파수
- $\phi$: 위상

IQ 성분 정의:
- $I = \cos(\phi)$: in-phase 성분
- $Q = \sin(\phi)$: quadrature 성분

Rotating frame에서 구동 Hamiltonian을 전개하면 $\omega_q + \omega_d$ 항과 $\omega_q - \omega_d$ 항이 나타난다. **Rotating wave approximation (RWA):** 빠르게 진동하는 $\omega_q + \omega_d$ 항들은 시간 평균이 0이므로 무시한다. 남는 항:

$$\widetilde{H}_{\rm d} = -\frac{\Omega}{2} V_0 s(t) \begin{pmatrix} 0 & e^{i(\delta\omega t + \phi)} \\ e^{-i(\delta\omega t + \phi)} & 0 \end{pmatrix} \quad \text{(식 91)}$$

여기서 $\delta\omega = \omega_q - \omega_d$는 qubit 주파수와 구동 주파수의 차이(detuning)이다.

### 4-4. 공명 구동: X, Y gate

구동 주파수가 qubit 주파수와 정확히 일치할 때 ($\delta\omega = 0$):

$$\widetilde{H}_{\rm d} = -\frac{\Omega}{2} V_0 s(t) \left( I \sigma_x + Q \sigma_y \right) \quad \text{(식 92)}$$

- **I 성분** ($\phi = 0$, in-phase pulse): $\sigma_x$ 방향 회전 → **X gate**
- **Q 성분** ($\phi = \pi/2$, quadrature pulse): $\sigma_y$ 방향 회전 → **Y gate**

**물리적 의미:** microwave pulse의 위상만 바꾸면 회전 축을 x에서 y로 바꿀 수 있다. 이것이 IQ 변조의 핵심이다.

Unitary 연산자 (in-phase pulse):

$$U_{\rm rf,d}^{\phi=0}(t) = \exp\left(\frac{i}{2}\Omega V_0 \int_0^t s(t')dt' \cdot \sigma_x\right) \quad \text{(식 93)}$$

이를 **Rabi driving**이라 한다. 회전각:

$$\Theta(t) = -\Omega V_0 \int_0^t s(t') dt' \quad \text{(식 94)}$$

**$\pi$ pulse 구현:** $\Theta(t) = \pi$가 되도록 $V_0$와 $s(t)$를 조절하면 X gate($\pi$ 회전)가 구현된다.

Gate 시퀀스와 파형의 관계:

$$U_k \cdots U_1 U_0 = \mathcal{T}\prod_{n=0}^k e^{\left[-\frac{i}{2}\Theta_n(t)(I_n\sigma_x + Q_n\sigma_y)\right]} \quad \text{(식 95)}$$

**Fig. 13 설명:** 실험 셋업에서는 위상 잡음이 낮은 microwave 발진기(Local Oscillator, LO)와 임의파형발생기(AWG)를 IQ 믹서로 결합하여 정확한 주파수와 위상의 pulse를 생성한다. AWG에서 저주파 성분 $\omega_{\rm AWG}$를 발생시키고 LO 주파수를 $\omega_{\rm LO} + \omega_{\rm AWG} = \omega_d$가 되도록 설정하여 원하는 qubit 주파수의 pulse를 만든다. 여러 AWG 주파수를 혼합하면 동시에 여러 qubit을 제어할 수 있다(주파수 다중화).

---

## 5. Virtual Z gate

### 5-1. 아이디어: 위상 변환 = Z 회전

식 (92)에서 X 회전과 Y 회전의 차이는 오직 **위상 $\phi$**에 있다. 위상을 $\phi \to \phi + \pi/2$로 바꾸면:
- $I \to Q$, $Q \to -I$
- X 회전이 Y 회전으로 바뀐다 (부호 포함)

이것은 $Z_\pi$ 회전이 X, Y 회전에 미치는 효과와 동일하다:
- $Z_\pi X_\pi = iY_\pi$
- $Z_\pi Y_\pi = -iX_\pi$

### 5-2. 수식적 유도

위상 $\phi_0$만큼 오프셋된 pulse $X_\theta^{(\phi_0)}$ (I 채널을 사용하지만 회전 축이 x에서 $\phi_0$만큼 기울어진 경우)를 $X_\theta$ 다음에 적용하면:

$$X_\theta^{(\phi_0)} X_\theta = e^{-i\frac{\theta}{2}(\cos(\phi_0)\sigma_x + \sin(\phi_0)\sigma_y)} X_\theta \quad \text{(식 96)}$$

$$= \mathsf{Z}_{-\phi_0} \mathsf{X}_\theta \mathsf{Z}_{\phi_0} \mathsf{X}_\theta \quad \text{(식 97)}$$

즉, **AWG 신호의 위상 오프셋 $\phi_0$는 $Z_{\phi_0}$ 회전을 삽입하는 것과 동일**하다!

### 5-3. Virtual Z gate의 실용성

원래 gate 시퀀스:

$$\cdots - U_i - Z_{\theta_0} - U_{i+1} - Z_{\theta_1} - U_{i+2} - \cdots \quad \text{(식 98)}$$

Virtual Z gate를 사용하면 이를 다음과 같이 재구성할 수 있다:

$$\cdots - U_i - U_{i+1}^{(\theta_0)} - U_{i+2}^{(\theta_0+\theta_1)} - \cdots \quad \text{(식 99)}$$

이후 pulse들의 위상만 소프트웨어로 조정하면 별도의 물리적 Z pulse 없이 Z 회전을 구현한다.

**Virtual Z gate의 장점:**
1. **추가 pulse 불필요:** Z gate에 해당하는 별도의 microwave pulse가 없다
2. **Gate time = 0:** 소프트웨어 위상 조정이므로 실질적인 gate time이 없다
3. **완벽한 gate fidelity = 1:** 물리적 오차 없음
4. **측정은 $z$축 기준:** 최종 Z 회전은 측정 결과에 영향이 없으므로 무시 가능

### 5-4. 완전한 single-qubit gate 집합

임의의 single-qubit 연산 (전역 위상 제외):

$$U(\theta, \phi, \lambda) = \mathsf{Z}_{\phi-\frac{\pi}{2}} \mathsf{X}_{\frac{\pi}{2}} \mathsf{Z}_{\pi-\theta} \mathsf{X}_{\frac{\pi}{2}} \mathsf{Z}_{\lambda-\frac{\pi}{2}} \quad \text{(식 100)}$$

**핵심:** $X_{\pi/2}$ 물리 pulse 하나와 virtual Z gate들의 조합만으로 임의의 single-qubit gate를 구현할 수 있다! 예를 들어 하다마드 gate:

$$H = Z_{\pi/2} X_{\pi/2} Z_{\pi/2}$$

Z들이 virtual이므로, 하다마드 gate는 사실상 $X_{\pi/2}$ pulse 하나로 구현된다.

---

## 6. DRAG 방식

### 6-1. 문제: 약한 anharmonicity와 leakage error

식 (79)에서 transmon의 최저 2레벨만 고려했지만, 실제 transmon은 약한 anharmonicity $|\alpha| \approx 200$–$300$ MHz를 갖는 다레벨 시스템이다. $|1\rangle \to |2\rangle$ 전이 주파수는:

$$\omega_q^{1\to 2} = \omega_q + \alpha \quad (\alpha < 0)$$

로 $\omega_q$와 $|\alpha|$만큼 떨어져 있다.

**Fig. 14 설명:** 짧은 가우시안 pulse는 넓은 스펙트럼 폭을 가진다. 표준 편차 $\sigma$ = 1, 2, 5 ns의 가우시안 pulse의 푸리에 변환(스펙트럼)을 보면, 짧을수록 $\omega_q^{1\to 2}$ 주파수에서도 상당한 스펙트럼 성분이 있다.

두 가지 오차 효과:
1. **Leakage error:** $|1\rangle$ 상태에 있는 qubit이 $\pi$ pulse 중에 $|2\rangle$로 여기될 수 있다. $|0\rangle$에서도 $|1\rangle$을 거쳐 $|2\rangle$로 직접 여기될 수 있다.
2. **Phase error:** 구동이 있는 동안 $|1\rangle$과 $|2\rangle$ 레벨 사이에 반발(repulsion)이 생겨 $\omega_q^{0\to 1}$이 변한다 (ac-Stark 이동). 결과적으로 $|0\rangle$과 $|1\rangle$ 사이에 상대 위상이 누적된다.

### 6-2. DRAG 해법

DRAG (Derivative Reduction by Adiabatic Gate) 방식: Q 채널에 추가 신호를 인가하여 두 오차를 동시에 억제한다.

파형 수정:

$$s(t) \to s'(t) = \begin{cases} s(t) & \text{I 채널} \\ \lambda \frac{\dot{s}(t)}{\alpha} & \text{Q 채널} \end{cases} \quad \text{(식 101)}$$

- $\lambda$: 무차원 스케일링 파라미터
- $\dot{s}(t)$: 원래 포락선의 시간 미분
- $\alpha$: anharmonicity (음수)

**최적 파라미터:**
- $\lambda = 0.5$: phase error 최소화에 최적
- $\lambda = 1.0$: leakage error 최소화에 최적
- $\lambda = 0$: DRAG 없음 (원래 가우시안 pulse)

두 오차를 동시에 최소화하려면 주파수 detuning 파라미터 $\delta f$를 추가 도입:

$$s'_{\delta f}(t) = s'(t) e^{i2\pi\delta ft} \quad \text{(식 102)}$$

$\lambda$는 leakage error 최소화로 선택하고, $\delta f$로 phase error를 별도 보정한다. 실제로는 randomized benchmarking과 단발 측정을 조합하여 최적 $\lambda$를 실험적으로 결정한다.

**결과:** 현대 DRAG pulse를 사용한 single-qubit gate fidelity: $F_{1\rm qb} \gtrsim 0.99$ (99% 이상).

---

## 7. iSWAP gate

### 7-1. 배경: Two-qubit gate의 분류

섹션 IV C에서 언급한 바와 같이, 초전도 qubit의 two-qubit gate는 크게 두 계열로 나뉜다:
1. **국소 자기장 제어** (tunable qubit): iSWAP, CPHASE
2. **Microwave 전용** (고정 주파수 qubit): CR gate, bSWAP, MAP, RIP

### 7-2. iSWAP unitary 유도

섹션 II에서 나온 두 qubit 상호작용 Hamiltonian (식 32):

$$H_{\rm qq} = g\,\sigma_{y1} \otimes \sigma_{y2} \quad \text{(식 103)}$$

여기서 $g$는 결합 강도. 이를 생성/소멸 연산자로 다시 쓰면:

$$H_{\rm qq} = -g\left([\sigma^+ - \sigma^-] \otimes [\sigma^+ - \sigma^-]\right) \quad \text{(식 106)}$$

전개하면 $\sigma^+\sigma^+$, $\sigma^-\sigma^-$ (빠르게 진동), $\sigma^+\sigma^-$, $\sigma^-\sigma^+$ (느리게 진동) 항이 나온다. **RWA 적용** (빠른 항 무시):

$$H_{\rm qq} = g\left(e^{i\delta\omega_{12}t}\sigma^+\sigma^- + e^{-i\delta\omega_{12}t}\sigma^-\sigma^+\right) \quad \text{(식 107)}$$

여기서 $\delta\omega_{12} = \omega_{q1} - \omega_{q2}$.

**공명 조건:** qubit 1의 flux를 조절하여 $\omega_{q1} = \omega_{q2}$로 만들면 ($\delta\omega_{12} = 0$):

$$H_{\rm qq} = g(\sigma^+\sigma^- + \sigma^-\sigma^+) = \frac{g}{2}(\sigma_x\sigma_x + \sigma_y\sigma_y) \quad \text{(식 108)}$$

**물리적 해석:**
- $\sigma^+\sigma^-$: qubit 1의 여기(excitation)가 소멸되고 qubit 2에서 생성 → 에너지 교환(swap)
- $\sigma^-\sigma^+$: 반대 방향 교환
- 이 XY interaction은 두 qubit 사이의 여기를 앞뒤로 교환시킨다

XY interaction의 unitary:

$$U_{qq}(t) = e^{-i\frac{g}{2}(\sigma_x\sigma_x + \sigma_y\sigma_y)t} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos(gt) & -i\sin(gt) & 0 \\ 0 & -i\sin(gt) & \cos(gt) & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \quad \text{(식 109)}$$

시간 $t' = \pi/(2g)$에서:

$$U_{qq}\left(\frac{\pi}{2g}\right) = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 0 & -i & 0 \\ 0 & -i & 0 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \equiv i\mathsf{SWAP} \quad \text{(식 110)}$$

**물리적 의미:** qubit 1이 $|1\rangle$, qubit 2가 $|0\rangle$이면, iSWAP 후 qubit 1은 $|0\rangle$, qubit 2는 $-i|1\rangle$ 상태가 된다. 여기가 교환되면서 위상 인자 $-i = e^{-i\pi/2}$가 붙는다. 이것이 "i"SWAP의 "i"이다.

시간 $t'' = \pi/(4g)$에서: $\sqrt{i\mathsf{SWAP}}$ gate (식 111). 이를 이용하면 $|01\rangle + i|10\rangle$ 형태의 Bell state를 생성할 수 있다.

### 7-3. iSWAP 동작 원리 (Fig. 15)

**Fig. 15 설명:**
- (a): 두 transmon qubit의 에너지 스펙트럼을 qubit 1의 flux 함수로 표시. 두 에너지 준위가 교차하는 지점 (avoided crossing)이 iSWAP 동작점 $\Phi_{i\rm SWAP}$.
- (b): $|10\rangle$ 상태를 준비한 후 flux를 iSWAP 동작점으로 이동하고 시간 $\tau$ 대기. 여기가 두 qubit 사이를 왔다 갔다 한다.
- (c): $\Phi_{i\rm SWAP}$에서의 확률 진동. $\tau = \pi/(2g)$에서 완전한 iSWAP가 일어난다.

**Single-qubit phase 처리:**

Flux를 이동시키는 동안 각 qubit은 추가적인 동적 위상을 얻는다:

$$\theta_z = \int_0^\tau dt\,(\omega_q - \omega(t)) \quad \text{(식 112)}$$

이 위상은 virtual Z gate를 이후 pulse에 적용하거나, flux 파형을 적절히 설계하여 위상이 정확히 상쇄되도록 해서 제거한다.

### 7-4. 결합 강도와 설계 파라미터

버스 resonator를 통한 간접 결합:

$$g_{\rm q\text{-}r\text{-}q} = \frac{g_1 g_2(\Delta_1 + \Delta_2)}{2\Delta_1\Delta_2} \quad \text{(식 104)}$$

직접 capacitive coupling:

$$g_{\rm q\text{-}q} = \frac{1}{2}\sqrt{\omega_{q1}\omega_{q2}}\frac{C_{q\text{-}q}}{\sqrt{C_{q\text{-}q}+C_1}\sqrt{C_{q\text{-}q}+C_2}} \quad \text{(식 105)}$$

전형적인 iSWAP 결합 강도: $g/(2\pi) = 5$–$40$ MHz.

**실용적 장점:** 결합 강도 $g$와 qubit 주파수를 알면 iSWAP gate time $\tau = \pi/(2g)$을 fabrication 전에 시뮬레이션으로 예측할 수 있다. 실제 측정값은 전자기 시뮬레이션 결과와 매우 잘 일치한다.

### 7-5. iSWAP의 응용

iSWAP 하나로는 CNOT를 만들 수 없다. CNOT는 iSWAP 두 개와 single-qubit gate들로 구현된다 (식 113):

$$\mathsf{CNOT} = [\text{single-qubit gate들}] \cdot i\mathsf{SWAP} \cdot [\text{single-qubit gate들}] \cdot i\mathsf{SWAP}$$

그럼에도 iSWAP는 특정 입력 상태에 대해 CNOT와 유사한 동작을 효율적으로 수행할 수 있다. 또한 XY interaction(식 108)은 양자 시뮬레이션에서 Heisenberg Hamiltonian의 일부를 직접 구현할 수 있어 유용하다:

$$H_{\rm Heisenberg} = J_x\sigma_x\sigma_x + J_y\sigma_y\sigma_y + J_z\sigma_z\sigma_z \quad \text{(식 114)}$$

---

## 8. CPHASE gate

### 8-1. 아이디어: 더 높은 에너지 준위 활용

iSWAP 유도에서는 qubit의 최저 2레벨만 고려했다. 하지만 transmon은 음의 anharmonicity($\alpha \approx -E_C$)를 가지는 다레벨 시스템이다. 이 더 높은 준위가 CPHASE gate를 자연스럽게 만들어낸다.

CPHASE gate 목표:

$$U_{\mathsf{CPHASE}} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \end{bmatrix} \quad \text{(식 115)}$$

$|11\rangle$ 상태에만 $-1 = e^{i\pi}$ 위상을 적용해야 한다.

### 8-2. 2여기(Two-Excitation) 서브공간의 스펙트럼

두 transmon qubit 시스템의 두 여기 서브공간 Hamiltonian (식 116):

$$H_{2\text{ex}} = \begin{bmatrix} E_{00} & 0 & 0 & 0 & 0 & 0 \\ 0 & E_{01} & g & 0 & 0 & 0 \\ 0 & g & E_{10} & 0 & 0 & 0 \\ 0 & 0 & 0 & E_{11} & \sqrt{2}g & \sqrt{2}g \\ 0 & 0 & 0 & \sqrt{2}g & E_{02} & 0 \\ 0 & 0 & 0 & \sqrt{2}g & 0 & E_{20} \end{bmatrix}$$

여기서 $E_{nm} = E_n^{q1}(\Phi_1) + E_m^{q2}(\Phi_2)$이고, $|02\rangle, |20\rangle \leftrightarrow |11\rangle$ 전이는 $\sqrt{2}g$로 스케일된다 (광자 수가 더 많아서).

**Fig. 16 설명:**
- (a): flux 변화에 따른 스펙트럼. $\Phi_{i\rm SWAP}$에서 $|01\rangle \leftrightarrow |10\rangle$ 피해 교차점, 그보다 먼저 (음의 anharmonicity 때문에) $\Phi_{\rm CPHASE}$에서 $|11\rangle \leftrightarrow |20\rangle$ 피해 교차점이 나타난다.
- (b): $|11\rangle \leftrightarrow |20\rangle$ 피해 교차점 확대. 파라미터 $\zeta$는 $|11\rangle$이 $|01\rangle + |10\rangle$에 비해 획득하는 추가 위상률을 나타낸다.

### 8-3. Adiabatic 궤적을 통한 CPHASE 구현

$|11\rangle$을 준비하고 flux를 $\Phi_{\rm CPHASE}$ 근처로 천천히(adiabatic하게) 이동 후 되돌아오면, 계산 기저에서의 unitary:

$$U_{\rm ad} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & e^{i\theta_{01}(\ell)} & 0 & 0 \\ 0 & 0 & e^{i\theta_{10}(\ell)} & 0 \\ 0 & 0 & 0 & e^{i\theta_{11}(\ell)} \end{bmatrix} \quad \text{(식 117)}$$

각 상태 $|ij\rangle$이 획득하는 위상:

$$\theta_{ij}(\ell(\tau)) = \int_0^\tau dt\,\omega_{ij}[\ell(t)] \quad \text{(식 118)}$$

**핵심 파라미터 $\zeta$:**

$$\zeta = \omega_{11} - (\omega_{01} + \omega_{10}) \quad \text{(식 119)}$$

$\zeta$는 $|20\rangle$ 상태와의 반발로 인해 $|11\rangle$이 $|01\rangle + |10\rangle$에 비해 추가로 획득하는 위상률이다.

**$\pi$ 위상 조건:** 궤적 $\ell_\pi$를 설계하여:

$$\int_0^\tau \zeta(\ell_\pi(t))dt = \pi = \theta_{11}(\ell_\pi) - (\theta_{01}(\ell_\pi) + \theta_{10}(\ell_\pi)) \quad \text{(식 120)}$$

이 조건을 만족하면:

$$U_{\rm ad} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & e^{i\theta_{01}} & 0 & 0 \\ 0 & 0 & e^{i\theta_{10}} & 0 \\ 0 & 0 & 0 & e^{i(\pi + \theta_{01} + \theta_{10})} \end{bmatrix} \quad \text{(식 121)}$$

Virtual Z gate 또는 single-qubit pulse로 single-qubit phase $\theta_{01}, \theta_{10}$을 상쇄하면:

$$U_{\rm ad} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \end{bmatrix} = U_{\rm CPHASE} \quad \text{(식 122)}$$

**물리적 직관:** $|11\rangle$ 상태의 에너지는 $|20\rangle$과의 상호작용으로 인해 $|01\rangle$과 $|10\rangle$의 에너지 합보다 더 많이 이동한다 (레벨 반발). 이 차이가 누적되어 정확히 $\pi$가 되도록 flux 파형을 설계하면 CPHASE가 구현된다.

일반화: 임의의 위상 $e^{-i\phi}$에 대한 $\mathsf{CZ}_\phi$ gate:

$$\mathsf{CZ}_\phi = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & e^{-i\phi} \end{bmatrix} = \exp\left[-i\frac{\phi}{4}\left(\sigma_z\otimes\sigma_z - \sigma_z\otimes\mathbb{1} - \mathbb{1}\otimes\sigma_z\right)\right] \quad \text{(식 123)}$$

**해석:** $|20\rangle$ 준위와의 상호작용이 계산 서브공간 내에서 효과적인 $\sigma_z\otimes\sigma_z$ 결합을 만들어낸다.

### 8-4. CPHASE의 성능과 응용

**궤적 최적화:** 피해 교차점 크기 $g/(2\pi) \approx 20$ MHz에 대해 경험적 최소 gate time은 $2\pi/g \approx 50$ ns. Martinis-Geller 분석: Slepian 파형을 이용한 최적 궤적 $\ell_\pi^*$으로 non-adiabatic 오차를 최소화.

**핵심 성과:**
- Barends et al.: $\mathcal{F}_{\rm CPHASE} = 0.9944$, $\tau = 43$ ns (interleaved RB 측정)
- Kelly et al.: 수치 최적화로 $\mathcal{F} = 0.993$ 달성

**오류 수정과의 연결:** CPHASE gate fidelity $\mathcal{F} > 0.99$는 **surface code의 fault-tolerance threshold ~1%**를 넘는 것으로, quantum error correction (QEC) 기반 양자 컴퓨팅에서 매우 중요한 이정표다. 이 임계값을 넘으면 이론적으로 qubit을 더 추가할수록 논리 오류율이 낮아지는 오류 억제가 가능하다.

**양자 시뮬레이션 응용 (Hubbard 모델):**

두 페르미온 모드의 Hubbard Hamiltonian:

$$H_{\rm Hubbard} = -t(b_1^\dagger b_2 + b_2^\dagger b_1) + Ub_1^\dagger b_1 b_2^\dagger b_2 \quad \text{(식 126)}$$

Jordan-Wigner 변환 후 Pauli operator로:

$$H = \frac{t}{2}(\sigma_x\otimes\sigma_x + \sigma_y\otimes\sigma_y) + \frac{U}{4}(\sigma_z\otimes\sigma_z + \sigma_z\otimes\mathbb{1} + \mathbb{1}\otimes\sigma_z) \quad \text{(식 127, 128)}$$

$\mathsf{CZ}_\phi$를 이용하여 $U_{ZZ}(\phi) = \exp\left[-i\frac{\phi}{2}\sigma_z\otimes\sigma_z\right]$ 생성 가능 (식 129).

**주파수 혼잡 문제와 gmon:** 여러 qubit이 있을 때, 한 qubit의 주파수를 변화시키면 다른 qubit의 주파수와 겹칠 위험이 있다 ("frequency crowding"). Chen et al.의 "gmon" 디바이스는 qubit 결합을 on/off 비율 ~1000으로 제어하여 이 문제를 해결, $\mathcal{F} = 0.9907$ 달성.

---

## 9. Microwave 전용 gate

Tunable qubit에서의 gate(iSWAP, CPHASE)는 flux 제어가 필요하여 새로운 잡음 채널(flux 잡음)이 도입된다. Microwave 전용 gate는 이 문제를 피한다. 대신 고정 주파수 qubit은 더 긴 수명($T_1$)을 갖는다.

### 9-1. CR gate (Cross-Resonance gate)

**원리:**

두 qubit(주파수 $\omega_{q1}$, $\omega_{q2}$, detuning $\Delta_{12} = \omega_{q1} - \omega_{q2}$, 결합 $g \ll \Delta_{12}$) 시스템에서 **qubit 1을 qubit 2의 주파수로 구동**하면 (Fig. 17), Schrieffer-Wolff 변환 후 dressed state 기저에서:

$$H_{d,1} = \Omega V_{d1}(t)\left(\sigma_x\otimes\mathbb{1} + \nu_1^-\mathbb{1}\otimes\sigma_x + \mu_1^-\sigma_z\otimes\sigma_x\right) \quad \text{(식 131)}$$

여기서:

$$\mu_i^\pm = \pm\frac{g}{\Delta_{12}}\frac{\alpha_i}{(\alpha_i \mp \Delta_{12})} \quad \text{(식 133)}$$

$$\nu_i^\pm = \pm\frac{g}{\Delta_{12}}\frac{\mp\Delta_{12}}{(\alpha_i \mp \Delta_{12})} \quad \text{(식 134)}$$

Qubit 2 입장에서 qubit 1 구동이 $\nu_1^-\mathbb{1}\otimes\sigma_x$ (single-qubit 회전)와 $\mu_1^-\sigma_z\otimes\sigma_x$ **(제어된 회전)** 두 항으로 분해된다.

Qubit 2의 Rabi 진동 주파수:

$$\Omega_{\rm QB2}^{\rm Rabi} = \Omega V_{d1}\left(\nu_1^- + z_1\mu_1^-\right) \quad \text{(식 135)}$$

여기서 $z_1 = \langle\sigma_z\mathbb{1}\rangle$은 qubit 1의 상태에 의존한다.

**물리적 의미:** qubit 1의 상태($|0\rangle$ vs $|1\rangle$)에 따라 qubit 2의 Rabi 주파수가 달라진다. 즉, qubit 1이 제어, qubit 2가 표적인 조건부 회전이 일어난다. CR gate는 $\mathsf{ZX}_\theta$ gate라고도 불린다.

**Fig. 17 설명:**
- (c): qubit 1이 $|0\rangle$일 때 (위 패널)와 $|1\rangle$일 때 (아래 패널) qubit 2의 Rabi 진동이 다른 주파수를 보인다.
- (d): 두 경우의 (z,y) 평면에서의 각도 차이. 약 200 ns에서 $\pi$ 위상 차이가 달성된다.

CR gate의 unitary:

$$U_{\mathsf{CR}_\theta} = e^{-\frac{i}{2}\theta\sigma_z\otimes\sigma_x} = \begin{bmatrix} \cos\frac{\theta}{2} & -i\sin\frac{\theta}{2} & 0 & 0 \\ -i\sin\frac{\theta}{2} & \cos\frac{\theta}{2} & 0 & 0 \\ 0 & 0 & \cos\frac{\theta}{2} & i\sin\frac{\theta}{2} \\ 0 & 0 & i\sin\frac{\theta}{2} & \cos\frac{\theta}{2} \end{bmatrix} \quad \text{(식 136)}$$

CNOT 구현 (single-qubit gate 추가):

$$\mathsf{CNOT} = Z_{\pi/2} \cdot \mathsf{CR}_{-\pi/2} \cdot X_{\pi/2} \cdot X_{\pi/2} \quad \text{(대략, 위상 제외)}$$

**Echo CR (eCR) 및 Active Cancellation Echo CR (aceCR):**
- Qubit 1을 비공명으로 구동하면 ac-Stark 이동이 생겨 $\sigma_z\mathbb{1}$ 항이 추가된다.
- 이 원치 않는 항들을 "echo" 기법으로 제거 → $\mathcal{F}_{\rm eCR} = 0.9347$
- 능동 상쇄 추가 (aceCR): $\tau = 160$ ns, $\mathcal{F}_{\rm aceCR} = 0.991$ (surface code threshold 초과)

**CR gate의 특성:**
- 고정 주파수 qubit 사용 → flux 잡음 없음, 더 긴 수명
- Gate time: 초기 300–400 ns → 현재 ~160 ns
- 항상 켜진 결합(always-on coupling): single-qubit 제어와 two-qubit 결합 사이의 트레이드오프 존재
- IBM Quantum Experience의 native two-qubit gate

**양자 시뮬레이션 응용:** CR Hamiltonian($\sigma_z\otimes\sigma_x$)은 XY나 ZZ 형태가 아니지만, 변분 양자 고유값 분해기(VQE)를 통해 H₂, LiH, BeH₂ 분자의 바닥상태 에너지 계산에 활용되었다.

### 9-2. bSWAP gate

**원리:** $|00\rangle \leftrightarrow |11\rangle$ 전이를 직접 구동한다 (Fig. 18 참조).

보통 이 전이의 행렬 원소는 결합 강도의 3차로 매우 작다. 하지만 **두 qubit의 detuning이 anharmonicity와 같을 때** ($\Delta_{12} = |\alpha|$) 전이율이 향상된다.

두 qubit의 중간 주파수 근처에서 구동하면 (Schrieffer-Wolff 변환 여러 번 적용):

$$U = U_{b\rm SWAP}(\theta, \phi) \cdot U_{ZZ} \cdot U_{IZ-ZI} \quad \text{(식 138)}$$

$$U_{b\rm SWAP}(\theta, \phi) = \begin{bmatrix} \cos\theta & 0 & 0 & -ie^{-i2\phi}\sin\theta \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ -ie^{-i2\phi}\sin\theta & 0 & 0 & \cos\theta \end{bmatrix} \quad \text{(식 139)}$$

$U_{ZZ}$와 $U_{IZ-ZI}$는 $U_{b\rm SWAP}$과 교환하므로 후처리로 제거 가능. 유효 Rabi 주파수:

$$\Omega_B = \frac{-2g\Omega^2(-g\gamma\alpha_\Sigma + \gamma^2\alpha_2(\alpha_1+\Delta_{12}) + \alpha_1(\alpha_2-\Delta_{12}))}{(\alpha_1+\Delta_{12})(\alpha_2-\Delta_{12})\Delta_{12}^2} \quad \text{(식 140)}$$

**특징:**
- $\theta = \pi/4$, $\phi = 0$: $|00\rangle \to \frac{1}{\sqrt{2}}(|00\rangle + i|11\rangle)$ Bell state 직접 생성 ($\sqrt{b\rm SWAP}$ gate)
- 이온 트랩의 Mølmer-Sørensen gate의 초전도 qubit 유사체
- $\mathcal{F}_{b\rm SWAP} = 0.90$ (긴 고출력 pulse에 의한 dephasing이 주요 오차 원인)

### 9-3. MAP (Microwave-Activated CPHASE) gate

**원리:** CPHASE와 유사하게 계산 외부 준위를 이용하되, flux 조절 없이 microwave로 구현.

두 고정 주파수 qubit의 주파수를 **$|12\rangle$과 $|03\rangle$ 레벨이 공명**하도록 설계(제작). 이 공명이 $|02\rangle\leftrightarrow|01\rangle$과 $|12\rangle\leftrightarrow|11\rangle$ 전이의 분리를 만든다. $|n2\rangle\leftrightarrow|n1\rangle$ 전이 근방에서 구동하면 유효 $\sigma_z\otimes\sigma_z$ 상호작용 생성:

$$U_{\mathsf{MAP}} = \exp\left[-i\frac{\pi}{4}\sigma_z\otimes\sigma_z\right] \quad \text{(식 141)}$$

$\mathcal{F}_{\mathsf{MAP}} = 0.87$, $\tau_{\rm MAP} = 514$ ns.

**단점:** 여러 qubit으로 확장 시 더 높은 에너지 준위의 정밀한 매칭이 필요하고, 다른 모드와의 불필요한 결합 회피가 어려워진다.

### 9-4. RIP (Resonator Induced Phase) gate

**원리:** 두 고정 주파수 qubit을 버스 resonator에 멀리 결합시킨다. Resonator에 비공명 pulse를 adiabatic하게 인가 후 제거하면 resonator는 원래 상태로 돌아오지만, qubit들은 상태 의존적 위상을 획득한다.

$$U_{\mathsf{rRIP}} = \exp\left[-i\dot{\theta}\sigma_z\otimes\sigma_z\,t\right] \quad \text{(식 142)}$$

결합률:

$$\dot{\theta} \propto \underbrace{\left(\frac{|\Omega V_d|}{2\Delta_{\rm cd}}\right)^2}_{\bar{n}} \frac{\chi}{\Delta_{\rm cd}} \quad \text{(식 143)}$$

여기서 $\bar{n}$은 resonator의 평균 광자 수, $\chi$는 dispersive shift, $\Delta_{\rm cd}$는 구동-resonator detuning.

**RIP gate의 장점:** qubit 주파수 차이에 크게 민감하지 않아 큰 주파수 차이를 가진 qubit 쌍에도 적용 가능.

Paik et al. 실험 (3D transmon, 4 qubit): 4 qubit을 동일 버스에 연결하고, refocused RIP (rRIP) 기법으로 원치 않는 4-qubit 상호작용을 제거. 주파수 차이 0.38–1.8 GHz의 qubit 쌍들에서 $\mathcal{F} = 0.96$–$0.98$, $\tau = 285$–$760$ ns 달성.

**Fig. 18 설명:** iSWAP, bSWAP, CPHASE, MAP gate가 각각 두 결합 qubit의 어떤 에너지 준위를 이용하는지 도식으로 표시. iSWAP는 $|01\rangle\leftrightarrow|10\rangle$, CPHASE는 $|11\rangle\leftrightarrow|20\rangle$, bSWAP는 $|00\rangle\leftrightarrow|11\rangle$, MAP는 더 높은 $|12\rangle$, $|03\rangle$ 준위를 이용한다.

---

## 10. Tunable Coupling

### 10-1. 두 가지 구현 방식

Flux로 제어 가능한 효과적 결합 $\tilde{g}$를 만들어 "parametric gate"를 구현:

**(i) 결합 강도 직접 조절:**
$$g \to g(\Phi(t))$$

**(ii) 결합 요소의 공진 주파수 조절:**
$$\omega_{\rm coupler} \to \omega_{\rm coupler}(\Phi(t))$$
고정된 $g$를 갖지만 결합 요소의 주파수를 조절하여 유효 시간 의존 결합 파라미터 실현.

결합 요소를 qubit들의 주파수 차에 해당하는 주파수로 구동하면 quantum entanglement gate가 구현된다.

### 10-2. 실험 성과

**방식 (ii): Parametric 구동 iSWAP**

두 고정 주파수 qubit 사이의 flux tunable coupler를 parametric 구동:
- $\mathcal{F}_{i\rm SWAP} = 0.9823$ (interleaved RB), $\tau = 183$ ns

**bSWAP parametric 구동:**
두 고정 주파수 transmon을 연결하는 flux tunable transmon의 flux를 두 qubit의 합 주파수로 구동:
- bSWAP (및 iSWAP) gate 시연 성공
- 고정 주파수 qubit만의 구현보다 상당히 빠른 gate time

**Hybrid approach (tunable + 고정 qubit):**
별도의 coupler 없이 항상 켜진 capacitive coupling + 하나의 tunable qubit. Tunable qubit의 주파수를:
- $|01\rangle\leftrightarrow|10\rangle$ 전이 주파수로 변조 → iSWAP
- $|11\rangle\leftrightarrow|02\rangle$ 전이 주파수로 변조 → CPHASE

결과:
- $\mathcal{F}_{i\rm SWAP} = 0.94$ ($\tau = 150$ ns)
- $\mathcal{F}_{\rm CPHASE}^{02} = 0.93$ ($\tau = 210$ ns)
- $\mathcal{F}_{\rm CPHASE}^{20} = 0.88$ ($\tau = 290$ ns, CPHASE 방향에 따라 약간의 비대칭성)

이 gate 구조를 이용하여 4-qubit GHZ 상태 ($\mathcal{F}_{4\text{-qubit GHZ}} = 0.79$), 19 qubit을 이용한 비지도 학습(데이터 군집화) hybrid quantum-classical 알고리즘도 시연.

---

## 11. 핵심 요약

### Single-qubit gate

| 방법 | 물리 메커니즘 | 특징 |
|------|-------------|------|
| X, Y 회전 | Microwave capacitive coupling, IQ 변조 | 위상으로 축 선택, AWG로 각도 제어 |
| Virtual Z gate | AWG 위상 소프트웨어 조정 | Gate time 0, gate fidelity 1 |
| DRAG | Q 채널에 $\dot{s}(t)/\alpha$ 추가 | Leakage 및 phase error 억제, $F \gtrsim 0.99$ |

### Two-qubit gate 비교

| gate | 제어 방식 | 이용 준위 | Gate time | 최고 gate fidelity |
|------|---------|----------|----------|-----------|
| iSWAP | flux (tunable) | $|01\rangle\leftrightarrow|10\rangle$ | ~50 ns | 0.9823 |
| CPHASE | flux (tunable) | $|11\rangle\leftrightarrow|20\rangle$ | 43 ns | 0.9944 |
| CR gate | microwave | $\sigma_z\otimes\sigma_x$ dressed state | 160 ns | 0.991 |
| bSWAP | microwave | $|00\rangle\leftrightarrow|11\rangle$ | 긴 편 | 0.90 |
| MAP | microwave | $|12\rangle$, $|03\rangle$ 매칭 | 514 ns | 0.87 |
| RIP | microwave (resonator 매개) | dispersive coupling | 285–760 ns | 0.96–0.98 |

### Rotating frame 유도의 핵심 흐름

$$H = H_0 + H_d \xrightarrow{U_{\rm rf} = e^{iH_0 t}} \widetilde{H}_d \xrightarrow{\rm RWA} \widetilde{H}_d^{\rm RWA} = -\frac{\Omega}{2}V_0 s(t)(I\sigma_x + Q\sigma_y)$$

이 단순한 결과가 microwave IQ 변조를 이용한 single-qubit 제어의 이론적 근거이다.

### Universal quantum computation을 위한 최소 요소

$$\underbrace{X_{\pi/2} \text{ 물리 pulse}}_{\text{DRAG 적용}} + \underbrace{\text{Virtual Z gate}}_{\text{소프트웨어}} \xrightarrow{\text{single-qubit}} + \underbrace{\text{iSWAP / CPHASE / CR gate}}_{\text{two-qubit quantum entanglement gate}} \xrightarrow{\text{universal quantum computation}}$$

---

*이 설명은 논문 arXiv:1904.06560v5의 섹션 IV (행 751–1392)를 기반으로 작성되었다.*
