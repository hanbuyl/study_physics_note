# 섹션 V: Qubit Readout — 상세 설명

> **논문:** Krantz et al., "A Quantum Engineer's Guide to Superconducting Qubits" (arXiv: 1904.06560v5)
> **대상:** 물리/공학 대학원생
> **목적:** dispersive readout의 이론부터 증폭기 체인까지, qubit readout의 전 과정을 한국어로 체계적으로 설명

---

## 목차

1. [서론: 왜 읽기가 어려운가?](#1-서론)
2. [Dispersive Readout의 물리적 원리](#2-분산-읽기)
3. [Jaynes-Cummings 모델과 Dispersive Limit](#3-jaynes-cummings-모델)
4. [읽기 신호: 진폭과 위상](#4-읽기-신호-진폭과-위상)
5. [IQ Mixer와 복조](#5-iq-믹서와-복조)
6. [Homodyne 복조](#6-호모다인-복조)
7. [Heterodyne 복조](#7-헤테로다인-복조)
8. [약한 측정과 강한 측정: 노이즈의 영향](#8-약한-측정과-강한-측정)
9. [양자 역반응 (Quantum Back-Action)](#9-양자-역반응)
10. [Purcell 효과와 Purcell 필터](#10-purcell-효과와-purcell-필터)
11. [Parametric Amplification: SNR 개선](#11-파라메트릭-증폭)
12. [Josephson Parametric Amplifier (JPA)](#12-josephson-파라메트릭-증폭기-jpa)
13. [Traveling Wave Parametric Amplifier (TWPA)](#13-진행파-파라메트릭-증폭기-twpa)
14. [전체 그림: 읽기 체인의 최적화](#14-전체-그림)

---

## 1. 서론

Qubit readout은 양자 프로세서의 핵심 기능 중 하나이다. 양자 계산이 아무리 정확하게 수행되었더라도, 최종 상태를 정확하게 읽어내지 못하면 결과를 얻을 수 없다. 이상적인 readout은 다음 두 조건을 동시에 만족해야 한다:

- **빠른 읽기**: qubit가 relaxation되기 전에 측정을 완료해야 한다 (τ_ro ≪ T₁).
- **높은 signal-to-noise ratio (SNR)**: 두 qubit 상태 |0⟩과 |1⟩을 통계적으로 명확히 구분할 수 있어야 한다.

Circuit QED 아키텍처에서는 **dispersive readout** 이 표준 방법이다. 이 방법에서는 qubit를 readout resonator에 결합시키고, qubit 상태에 따라 resonator의 공명 주파수가 미세하게 달라지는 효과를 측정한다.

물리적 직관: qubit를 직접 측정하는 대신, qubit가 resonator에 미치는 영향을 측정한다. Resonator는 microwave 신호를 반사/투과시키는 역할을 하므로, 고전적인 microwave 회로 기술로 신호를 처리할 수 있다.

---

## 2. Dispersive Readout

### 기본 개념

양자 측정은 다음의 두 단계로 이해할 수 있다:

1. **얽힘 단계**: qubit(양자 시스템)의 자유도가 측정 프로브(resonator)의 관측량과 얽힌다.
2. **고전적 측정 단계**: 프로브를 고전적으로 측정한다.

Circuit QED에서 이 구조는 Fig. 19(a)에 나타난 것처럼, qubit를 readout resonator에 결합시키는 방식으로 구현된다. Qubit를 직접 건드리지 않고 resonator만을 microwave로 탐침(probe)하여 qubit 상태를 추론한다.

### Dispersive Readout의 장점

Dispersive readout을 사용하면:
- Qubit의 **양자 자유도**가 선형 resonator의 **고전적 응답**으로 매핑된다.
- Readout 최적화 문제가 **microwave 신호의 SNR 최대화** 문제로 변환된다.
- 이상적인 경우, 측정이 **quantum non-demolition (QND)** 조건을 만족한다 — 즉, 측정 행위 자체가 qubit 상태를 파괴하지 않는다.

---

## 3. Jaynes-Cummings 모델

### 전체 Hamiltonian

Qubit-resonator 상호작용은 **Jaynes-Cummings Hamiltonian**으로 기술된다:

$$H_{\rm JC} = \omega_r \left( a^{\dagger} a + \frac{1}{2} \right) + \frac{\omega_q}{2} \sigma_z + g \left( \sigma_+ a + \sigma_- a^{\dagger} \right)$$

각 항의 물리적 의미:

| 항 | 의미 |
|---|---|
| $\omega_r (a^\dagger a + 1/2)$ | Resonator의 에너지 (광자 수 연산자 $a^\dagger a$, 진공 에너지 포함) |
| $\frac{\omega_q}{2}\sigma_z$ | Qubit의 에너지 ($\sigma_z$는 qubit 상태 연산자) |
| $g(\sigma_+ a + \sigma_- a^\dagger)$ | Qubit-resonator 결합: qubit가 흥분하면서 resonator 광자를 흡수하거나, 반대로 resonator 광자를 방출하며 qubit가 탈흥분 |

여기서 $\omega_r$은 resonator 주파수, $\omega_q$는 qubit 주파수, $g$는 coupling rate이다.

### 공진 극한과 Vacuum Rabi Splitting

Detuning $\Delta = |\omega_q - \omega_r| \ll g$ 이면 에너지 준위가 혼성화되고, vacuum Rabi splitting $\sqrt{n} g / \pi$가 열린다. 이 상태에서는 qubit와 resonator 사이에 에너지가 직접 교환된다. 이는 특정 2-qubit 게이트에는 유용하지만, readout에는 적합하지 않다 — qubit 상태 자체가 변하기 때문이다.

### Dispersive Limit

**Dispersive limit**은 $\Delta \gg g, \kappa$ 조건에서 성립한다. 이 조건은 qubit와 resonator가 서로 크게 detuning된 상황이다.

이 극한에서 Hamiltonian을 $g/\Delta$의 2차 섭동이론으로 근사하면:

$$H_{\rm disp} = \left(\omega_r + \chi \sigma_z\right) \left(a^{\dagger} a + \frac{1}{2}\right) + \frac{\tilde{\omega}_q}{2} \sigma_z$$

핵심 파라미터: **dispersive shift**

$$
\chi = \frac{g^2}{\Delta}$$

이 Hamiltonian의 물리적 의미: resonator의 유효 주파수가 qubit 상태에 따라 달라진다.
- Qubit가 $|0\rangle$ (즉 $\sigma_z = -1$): resonator 주파수 = $\omega_r - \chi$
- Qubit가 $|1\rangle$ (즉 $\sigma_z = +1$): resonator 주파수 = $\omega_r + \chi$

→ Fig. 19(b)에서 볼 수 있듯이, 두 qubit 상태에 대해 resonator의 반사 스펙트럼이 $2\chi$만큼 주파수 이동한다. 이것이 dispersive readout의 핵심 원리이다.

### Lamb Shift와 ac-Stark Shift

식 (145)를 다르게 정리하면:

$$H_{\rm disp} = \omega_r \left( a^{\dagger} a + \frac{1}{2} \right) + \frac{1}{2} \left( \omega_q + \underbrace{\frac{g^2}{\Delta}}_{\rm Lamb\;shift} + \underbrace{\frac{2g^2}{\Delta} a^{\dagger} a}_{\rm ac\text{-}Stark\;shift} \right) \sigma_z
$$

- **Lamb shift** ($g^2/\Delta$): resonator 진공 요동에 의해 qubit 주파수가 고정된 양만큼 이동. 실험에서 관측되는 qubit 주파수는 항상 Lamb shift된 주파수이다.
- **ac-Stark shift** ($\frac{2g^2}{\Delta} a^\dagger a$): resonator 내 광자 수에 비례하여 qubit 주파수가 이동. **이것이 실제로 문제가 된다** — resonator 안의 잡음 광자(열광자 또는 readout 펄스 광자)가 qubit 주파수를 요동시켜 **위상 이완(dephasing)**을 일으킨다.

### Transmon Qubit의 경우: Anharmonicity 보정

실제 transmon qubit는 2준위계가 아니라 다준위계이다. Anharmonicity $\alpha = \omega_q^{1\to2} - \omega_q^{0\to1}$을 고려하면 dispersive shift가 수정된다:

$$\chi = \chi_{01} + \frac{\chi_{12}}{2} = -\frac{g_{01}^2}{\Delta} \left( \frac{1}{1 + \Delta/\alpha} \right)$$

- $\chi_{01}$: 0→1 전이에 의한 기여
- $\chi_{12}/2$: 1→2 전이에 의한 기여 (이것이 dispersive shift의 부호와 크기를 결정)

이 식에 따라 Fig. 20에서 볼 수 있듯이:
- $\Delta < 0$ 또는 $\Delta > E_C/h$: $\chi < 0$
- $0 < \Delta < E_C/h$: $\chi > 0$ ("straddling regime")
- Transmon에서는 대개 $\Delta < 0$ (qubit 주파수 < resonator 주파수) 영역을 사용

### Critical Photon Number

Dispersive Hamiltonian(식 145)은 resonator 내 광자 수가 **critical photon number** $n_c \equiv \Delta^2 / (4g^2)$ 이하일 때만 유효하다. 이 값을 초과하면 dispersive 근사가 무너지고, QND 조건도 깨진다. 따라서 readout 펄스 출력을 지나치게 높이면 안 된다.

---

## 4. 읽기 신호: 진폭과 위상

### Dispersive Shift의 효과

Fig. 19(b)와 (c)를 참고하면:
- Resonator의 반사 계수 $S_{11}$의 크기와 위상이 qubit 상태에 따라 달라진다.
- $|0\rangle$과 $|1\rangle$에 대한 resonator 응답이 복소 IQ plane에서 두 점으로 표현된다.
- **최대 상태 구분**은 두 공명 주파수의 중간, $\omega_{\rm RF} = (\omega_r^{|0\rangle} + \omega_r^{|1\rangle})/2$에서 탐침할 때 얻어진다. 이 지점에서는 두 상태의 반사 진폭이 같고, 모든 정보가 **위상**에 담긴다.
- 최적 설계 조건: $\chi = \kappa/2$ (dispersive shift가 resonator 선폭의 절반)

### 신호의 수학적 표현

Readout microwave 신호는:

$$s(t) = A_{\rm RO} \cos(\omega_{\rm RO} t + \theta_{\rm RO})$$

복소 표현:

$$s(t) = {\rm Re}\left\{ A_{\rm RO} e^{j(\omega_{\rm RO} t + \theta_{\rm RO})} \right\}$$

**페이저(phasor) 표현**:

$$s(t) = {\rm Re}\left\{ \underbrace{A_{\rm RO} e^{j\theta_{\rm RO}}}_{\rm phasor} e^{j\omega_{\rm RO} t} \right\}$$

Phasor는 $A_{\rm RO}$와 $\theta_{\rm RO}$를 하나의 복소수로 압축한다.

### IQ 성분

Phasor를 실수부(I)와 허수부(Q)로 분해하면:

$$A_{\rm RO} e^{j\theta_{\rm RO}} = \underbrace{A_{\rm RO} \cos\theta_{\rm RO}}_{I} + j\underbrace{A_{\rm RO}\sin\theta_{\rm RO}}_{Q}$$

Readout의 목표: $I$와 $Q$를 측정하여 진폭 $A_{\rm RO}$와 위상 $\theta_{\rm RO}$를 추출하는 것.

$$A_{\rm RO} \propto \sqrt{I^2 + Q^2}, \quad \theta_{\rm RO} = \arctan(Q/I)$$

---

## 5. IQ Mixer와 복조

### IQ Mixer의 구조

Fig. 21에 IQ mixer의 회로 개략도가 나와 있다. 동작 원리:

1. Readout 신호 $s(t)$가 RF 포트로 들어온다.
2. 기준 국소 발진기(LO) 신호 $y(t) = A_{\rm LO}\cos\omega_{\rm LO}t$가 LO 포트로 들어온다.
3. Mixer 내부에서 신호가 I 경로와 Q 경로로 균등하게 분기된다.
4. Q 경로의 LO 신호는 $\pi/2$ 위상 회전된다.
5. 각 경로에서 신호와 LO를 곱하여 중간 주파수 신호를 만든다.
6. 저역통과 필터(LPF)로 합주파수 성분을 제거하고 차주파수 성분만 남긴다.

### 광학적 유추

Mixer는 광학에서 50:50 빔 분리기(beam splitter) + 광검출기의 조합에 해당한다. 두 전기장 $(E_1 + E_2)^2 = E_1^2 + E_2^2 + 2E_1 E_2$에서 교차항 $2E_1 E_2$가 두 신호의 곱셈에 해당한다.

---

## 6. Homodyne 복조

### 원리

**Homodyne** 측정에서는 LO 주파수를 readout 신호와 정확히 같게 설정한다: $\omega_{\rm LO} = \omega_{\rm RO}$.

혼합 후 저역통과 필터링을 하면 DC 성분이 남는다:

$$I = \frac{1}{T} \int_0^T dt\, s_I(t) y_I(t) = \frac{A_{\rm RO} A_{\rm LO}}{8} \cos\theta_{\rm RO}$$

$$Q = \frac{1}{T} \int_0^T dt\, s_Q(t) y_Q(t) = \frac{A_{\rm RO} A_{\rm LO}}{8} \sin\theta_{\rm RO}$$

이로부터 $A_{\rm RO}$와 $\theta_{\rm RO}$를 복원할 수 있다.

### 중요한 점

글로벌 값 $A_{\rm RO}$나 $\theta_{\rm RO}$ 자체가 아니라, qubit가 $|0\rangle$일 때와 $|1\rangle$일 때의 **차이**가 readout 정보이다. 증폭 이득 $G$와 전파 위상 $\phi$는 qubit 상태와 무관하게 두 경우에 동일하게 적용된다.

### Homodyne의 한계

1. **1/f 노이즈 취약성**: DC로 복조된 신호는 저주파 전자 노이즈에 취약하다.
2. **주파수 분할 다중화(FDM) 불가**: 여러 qubit를 동시에 읽으려면 다른 주파수의 신호를 구분해야 하는데, homodyne은 모든 신호를 DC로 낮춰버리므로 구분이 불가능하다.

---

## 7. Heterodyne 복조

### 원리

**Heterodyne** 방식에서는 LO 주파수를 readout 주파수와 다르게 설정한다:

$$
\omega_{\rm IF} = |\omega_{\rm RO} - \omega_{\rm LO}| > 0$$

여기서 $\omega_{\rm IF}$는 중간 주파수(intermediate frequency, IF)이다.

### 아날로그 복조 단계

Mixing 후 저역통과 필터링하면 IF 신호를 얻는다:

$$I_{\rm IF}(t) = \frac{A_{\rm RO} A_{\rm LO}}{8} \cos(\omega_{\rm IF} t + \theta_{\rm RO})
$$

$$Q_{\rm IF}(t) = \frac{A_{\rm RO} A_{\rm LO}}{8} \sin(\omega_{\rm IF} t + \theta_{\rm RO})$$

$\omega_{\rm IF}$는 ADC로 디지타이즈할 수 있을 정도로 충분히 낮다 (보통 수십 ~ 수백 MHz).

### 디지털 복조 단계

디지타이즈된 신호 $I_{\rm IF}[n]$, $Q_{\rm IF}[n]$에 대해 디지털 복조를 수행:

$$I_{\rm IF}[n] = \frac{A_{\rm RO} A_{\rm LO}}{8} \cos(\Omega_{\rm IF} n + \theta_{\rm RO})$$

$$Q_{\rm IF}[n] = \frac{A_{\rm RO} A_{\rm LO}}{8} \sin(\Omega_{\rm IF} n + \theta_{\rm RO})$$

디지털 복조: 각 샘플에 $\cos(\Omega_{\rm IF} n)$과 $\sin(\Omega_{\rm IF} n)$을 점별 곱한 후 평균:

$$I = \frac{1}{M} \sum_{n_1}^{n_2} I_{\rm IF}[n] \cos[\Omega_{\rm IF} n] = \frac{A_{\rm RO} A_{\rm LO}}{16} \cos\theta_{\rm RO}$$

$$Q = \frac{1}{M} \sum_{n_1}^{n_2} Q_{\rm IF}[n] \sin[\Omega_{\rm IF} n] = \frac{A_{\rm RO} A_{\rm LO}}{16} \sin\theta_{\rm RO}$$

### 복소 IQ Plane에서의 해석

복소 신호 $z_{\rm IF}[n] = I_{\rm IF}[n] + jQ_{\rm IF}[n]$은:

$$z_{\rm IF}[n] = \frac{A_{\rm RO} A_{\rm LO}}{8} e^{j\theta_{\rm RO}} e^{j\Omega_{\rm IF} n}$$

디지털 복조: $z[n] = z_{\rm IF}[n] \cdot e^{-j\Omega_{\rm IF} n}$으로 회전 성분을 제거하면 정적인 phasor가 남는다.

평균값:

$$\bar{z} = \frac{1}{M}\sum_i z[n] = \frac{A_{\rm RO} A_{\rm LO}}{8} e^{j\theta_{\rm RO}}$$

이 평균값이 IQ plane의 한 점으로 나타나며, qubit 상태에 따라 위치가 달라진다 — Fig. 22(c)의 2D 히스토그램이 바로 이것이다.

### Heterodyne의 장점

- **1/f 노이즈 회피**: 신호가 DC가 아닌 중간 주파수에 있어 저주파 노이즈의 영향이 적다.
- **FDM 호환**: 여러 qubit를 각각 다른 주파수로 읽으면, heterodyne 후 각각 다른 $\omega_{\rm IF}^{(i)}$에 위치하여 디지털로 구분 가능하다 (식 157).

---

## 8. 약한 측정과 강한 측정

### 노이즈의 역할

실제 readout에서는 노이즈가 존재하므로, IQ plane에서 각 qubit 상태에 대한 측정 결과가 하나의 점이 아니라 **가우스 분포**로 퍼진다 — Fig. 22(c) 참고.

노이즈의 주요 원인:
1. **Microwave 광자의 양자 노이즈**: 각 광자는 $\hbar\omega/2$의 진공 요동을 가진다.
2. **증폭기 노이즈**: Phase-preserving amplifier는 Heisenberg 불확정성 관계에 의해 최소 $\hbar\omega/2$의 노이즈를 추가한다.
3. **신호 감쇠에 의한 노이즈**: 첫 번째 증폭기 이전의 신호 손실은 노이즈로 나타난다.

이 모든 노이즈가 합쳐져 **시스템 노이즈 온도** $T_{\rm sys}$로 정량화된다.

### SNR과 분리 오류

측정 결과를 복소 평면에서 투영하면, SNR을 다음과 같이 정의할 수 있다:

$$
{\rm SNR} = \frac{\delta\theta}{\Delta\theta_1 + \Delta\theta_0}$$

여기서 $\delta\theta = |\theta_1 - \theta_0|$는 신호(두 상태의 분리), $\Delta\theta_0, \Delta\theta_1$은 각 분포의 너비(노이즈)이다.

분리 오류(separation error):

$$\epsilon_{\rm sep} = \frac{1}{2} {\rm erfc}\left[\frac{{\rm SNR}}{2}\right]
$$

- SNR이 클수록 erfc 함수의 인수가 커지므로 $\epsilon_{\rm sep}$이 작아진다 → 분리 오류 감소.
- Fig. 23에서 시간에 따른 분포 변화를 볼 수 있다: 두 분포의 분리(신호)는 시간에 **선형**으로 증가하고, 각 분포의 폭(노이즈)은 $\sqrt{t}$로 증가한다. 따라서 충분히 긴 시간 동안 측정하면 SNR이 향상된다.

### 약한 측정 vs. 강한 측정

| | SNR | Qubit 정보 | 상태 붕괴 |
|---|---|---|---|
| **약한 측정** | SNR < 1 | 부분적 정보만 획득 | 부분적 붕괴 |
| **강한 측정** | SNR > 1 | 완전한 정보 획득 | 완전한 붕괴 |

**Single-shot readout**: 반복 없이 한 번의 측정으로 qubit 상태를 결정하는 것. 이는 높은 SNR이 필요하며, 통상적으로 parametric amplifier가 필요하다.

### Relaxation 중의 읽기 충실도

측정 중에도 qubit는 relaxation될 수 있다:

$$F(\tau_{ro}) = 1 - e^{-\tau_{ro}/T_1}$$

여기서 $\tau_{ro} = \tau_{rd} + \tau_s/2$는 총 readout 시간 (resonator 링업 지연 + 샘플링 시간의 절반).

높은 충실도를 위해서는 **빠른 readout**($\tau_{ro} \ll T_1$)와 **높은 SNR** 두 조건이 모두 필요하다.

---

## 9. Quantum Back-Action

### QND 측정과 역반응

Dispersive readout은 이상적으로 **QND (quantum non-demolition)** 측정이다. Hamiltonian (식 145)에서 상호작용 항 $\chi \sigma_z a^\dagger a$는 $\sigma_z$와 교환 가능하므로, 측정이 qubit 에너지 고유상태를 바꾸지 않는다.

그러나 현실에서는 다음과 같은 역반응이 존재한다:

1. **측정 역반응(measurement back-action)**: Microwave 측정 그 자체가 qubit 상태를 랜덤하게 교란한다. 이는 양자 역학의 근본적인 성질로, Heisenberg 불확정성에 의해 피할 수 없다. 하지만 QND 조건에서는 역반응이 측정 기저(computational basis)와 정렬되어, 반복 측정에서 같은 결과를 얻을 수 있다.

2. **ac-Stark decay rate 역반응**: Resonator 광자 수 요동이 qubit 주파수를 변동시켜 위상 이완을 일으킨다 (식 147의 ac-Stark shift).

3. **Critical photon number 이상에서의 붕괴**: $n > n_c = \Delta^2/(4g^2)$이면 dispersive 근사가 무너지고 QND 조건이 깨진다.

### 역반응 최소화 전략

- Readout 펄스 출력을 $n_c$ 이하로 유지
- Resonator 열광자를 최소화: 냉각, 필터링, 감쇠
- 종방향 결합(longitudinal coupling) 기반 QND readout (현재 연구 중)

---

## 10. Purcell 효과와 Purcell Filter

### Purcell 효과란?

**Purcell effect**는 주변 전자기 환경에 의해 원자(또는 qubit)의 자발 방출률이 변하는 현상이다. Resonator가 있으면 qubit 공명 주파수 근처에서 상태 밀도(density of states)가 강화되어 relaxation이 빨라진다.

Qubit가 50Ω 환경에 직접 연결된 경우의 기본 decay rate:

$$\gamma_{\rm env}^{\rm Purcell} = \frac{g^2}{\omega}$$

(qubit를 전류원으로 모델링, Fig. 24(a) 참고)

### Resonator 추가 시 Purcell Decay Rate

Qubit와 환경 사이에 resonator를 추가하면 (Fig. 24(b)):

$$\gamma_{\rm res-env}^{\rm Purcell} = \frac{g^2}{\omega_r} \frac{{\rm Re}[Z_r(\omega)]}{Z_0}$$

Resonator의 임피던스 실수부:

$${\rm Re}[Z_r(\omega)] = \frac{Q Z_0}{1 + 2(\Delta/\kappa)^2}$$

#### 공진 조건 ($\Delta = 0$):

$$\gamma_{\rm res-env}^{\rm Purcell} = \frac{g^2}{\omega_r} Q = \frac{g^2}{\kappa}$$

#### Dispersive limit ($\Delta \gg g, \kappa$):

$$\gamma_{\rm res-env}^{\rm Purcell} = \left(\frac{g}{\Delta}\right)^2 \kappa$$

**물리적 직관**: Resonator는 qubit 주파수로부터 detuning된 대역통과 필터처럼 작동한다. Qubit가 resonator 주파수에서 멀리 detuning될수록 resonator가 qubit를 환경으로부터 보호한다.

### 읽기 속도 vs. Purcell 보호의 트레이드오프

빠른 readout을 위해서는:
- $\kappa$를 크게 → resonator 링업 시간 $1/\kappa$ 감소 → 좋음
- $g$를 크게 → dispersive shift $\chi = g^2/\Delta$ 증가 → 좋음

그러나 Purcell 보호를 위해서는:
- $g/\Delta$를 작게 → 식 (178)에서 Purcell decay rate 감소 → 좋음
- $\kappa$를 작게 → 식 (178)에서 Purcell decay rate 감소 → 좋음

이 두 조건이 서로 충돌한다. Qubit $T_1 > 100\,\mu{\rm s}$인 현대 소자에서는 이 트레이드오프가 실제로 병목이 된다.

### Purcell Filter

해결책: resonator와 50Ω 환경 사이에 **Purcell filter**를 삽입한다 (Fig. 24(c-d)).

Purcell filter가 있을 때의 decay rate:

$$\gamma_{\rm res-filter-env}^{\rm Purcell} = \kappa \left(\frac{g}{\Delta}\right)^2 \left(\frac{\omega_q}{\omega_r}\right) \left(\frac{\omega_r}{2Q_F \Delta}\right)$$

여기서 $Q_F$는 Purcell filter의 품질 인수이다.

**Purcell filter의 역할**: Resonator 주파수 $\omega_r$ 근방에서는 통과대역을 열어 빠른 신호 방출을 허용하면서, qubit 주파수 $\omega_q$ 근방에서는 큰 임피던스로 qubit를 환경으로부터 차단한다 (Fig. 24(d)).

**설계 방법들**:
- 사분파장 스터브(quarter-wave stub)
- 저-Q 대역통과 필터 (FDM 호환, 여러 readout resonator를 하나의 증폭기 체인에 연결 가능)
- 계단형 임피던스 필터(stepped-impedance filter)

---

## 11. Parametric Amplification: SNR 개선

### 왜 Parametric Amplifier가 필요한가?

Microwave 광자의 에너지는 광학 광자에 비해 훨씬 작다. 따라서 microwave 단일 광자 검출기를 만들기 어렵고, 증폭기를 사용해야 한다.

**양자 효율**:

$$\eta_{\rm SQL} = \frac{\hbar \omega_{\rm RF}}{k_B T_{\rm sys}}, \quad 0 < \eta_{\rm SQL} < 1$$

이 값이 1에 가까울수록 표준 양자 한계(SQL)에 근접하는 이상적인 측정이다.

**증폭기 체인의 시스템 노이즈 온도** (Friis formula):

$$T_{\rm sys} = T_{N,1} + \frac{T_{N,2}}{G_1} + \frac{T_{N,3}}{G_1 G_2} + \cdots$$

- 첫 번째 증폭기의 노이즈 온도가 시스템 노이즈를 지배한다.
- 만약 첫 증폭기가 HEMT ($T_N \approx 2\,{\rm K}$)이면, 시스템 노이즈는 약 7~10K (약 10~20개의 광자 등가 노이즈) → single-shot readout에 불충분.
- 해결책: 첫 번째 증폭기로 **quantum-limited parametric amplifier**를 사용.

### Quantum-Limited Amplification의 물리적 원리

선형 phase-preserving amplifier에서 입력장 $a_{\rm in}$이 출력장 $a_{\rm out}$으로 이상적으로 변환되면:

$$a_{\rm out} = \sqrt{G} a_{\rm in}$$

그러나 이 관계는 보존 교환 관계 $[a_{\rm out}, a_{\rm out}^\dagger] = 1$을 만족시키지 못한다. Caves' theorem에 따르면, 이를 만족시키기 위해 **idler 모드** $b_{\rm in}$의 진공 요동이 반드시 추가된다:

$$a_{\rm out} = \underbrace{\sqrt{G}\, a_{\rm in}}_{\rm 증폭} + \underbrace{\sqrt{G-1}\, b_{\rm in}^\dagger}_{\rm 추가 idler 노이즈}$$

대 이득($G \gg 1$) 극한에서 추가되는 최소 노이즈는 **반 광자($\hbar\omega/2$)**이다. 이것이 상온 증폭기와 달리 parametric amplifier가 달성하는 "quantum-limited amplification"이다.

### Phase-Preserving vs. Phase-Sensitive Amplification

**Phase-preserving amplification**: 두 직교 성분(I와 Q) 모두 동일하게 증폭. 최소 $\hbar\omega/2$의 노이즈 추가 (Fig. 25(c)).

**Phase-sensitive amplification**: Idler 모드를 $b_{\rm in} = e^{i\phi} a_{\rm in}$으로 설정하면:

$$a_{\rm out} = \underbrace{\sqrt{G}\, a_{\rm in}}_{\rm 증폭} + \underbrace{e^{-i\phi}\sqrt{G-1}\, a_{\rm in}^\dagger}_{\rm 위상 의존 노이즈}$$

펌프 위상 $\phi$를 조절하면 한 직교 성분은 노이즈 없이(표준 양자 한계 이하로) 증폭하고, 다른 성분에는 더 많은 노이즈를 추가할 수 있다. 이를 **squeezing**이라 한다 (Fig. 26).

- **장점**: 원리적으로 하나의 직교 성분을 완벽하게 증폭 가능.
- **단점**: 위상에 민감하므로 지속적인 위상 보정이 필요 → 실용적으로 불편.

Qubit readout에서는 대개 phase-preserving amplification이 실용적으로 더 선호된다.

---

## 12. Josephson Parametric Amplifier (JPA)

### JPA의 기본 원리

**Parametric amplification**의 원리: 입력 **signal** 광자가 강한 **pump** 신호와 비선형 매질을 통해 혼합되면서, pump에서 에너지가 signal 광자로 전환되어 이득이 생긴다.

초전도 회로에서 이 비선형성은 **Josephson junction**에서 제공된다. JPA는 약한 비조화 공진기(slightly anharmonic oscillator)로 만들어진다 (Fig. 27(a)).

**파라메트릭 펌핑**: 계의 운동방정식에서 하나의 파라미터(예: resonator 주파수)를 시간에 따라 변조한다.

### 전류 펌핑 (Four-Wave Mixing)

Hamiltonian:

$$H = \omega_r c^\dagger c + K c^\dagger c^\dagger c c$$

여기서 $K$는 Kerr nonlinearity이다.

**Four-wave mixing 과정**: signal($\omega_s$), idler($\omega_i$), pump 광자 2개($\omega_p$)가 에너지 보존:
$$
\omega_s + \omega_i = 2\omega_p$$

Pump는 resonator 공명 주파수 근방($\omega_p \approx \omega_r$)에 인가된다. Fig. 27(b) 참고.

이 방식의 역사: Yurke에 의해 처음 시연. Josephson Bifurcation Amplifier (JBA, Siddiqi et al.)가 이 원리를 기반으로 하며, qubit 상태를 이중안정 분기점의 두 상태로 매핑하여 single-shot readout을 수행했다.

### 플럭스 펌핑 (Three-Wave Mixing)

SQUID 루프를 통해 자속을 교류로 변조하면 resonator 주파수 $\omega_r(t) = 1/\sqrt{L(t)C}$가 변조된다.

Hamiltonian:

$$H = \omega_r c^\dagger c + K\left(p c^\dagger c^\dagger + p^\dagger c c\right)
$$

여기서 $p$는 플럭스 pump 모드 연산자이다.

**Three-wave mixing 과정**: signal($\omega_s$), idler($\omega_i$), pump($\omega_p$) 하나:
$$\omega_s + \omega_i = \omega_p$$

따라서 $\omega_s \approx \omega_i$ 이면 pump 주파수는 약 $\omega_p \approx 2\omega_r$ — 신호의 두 배. Fig. 27(c) 참고.

### 플럭스 펌핑의 실용적 장점

1. **필터링 용이**: Pump가 신호로부터 크게 detuning되어 있어 (주파수 $2\omega_r$ vs $\omega_r$) 후단 디지타이저에 미치는 영향을 쉽게 필터링할 수 있다.
2. **잡음 차단**: 사분파장 resonator는 $\omega_p \approx 2\omega_r$ 근방에 공진 모드가 없으므로 pump에 의한 잡음 광자 생성이 억제된다.
3. **별도 플럭스 라인**: 추가적인 방향성 결합기(directional coupler)가 필요 없다.

### JPA의 한계

1. **좁은 대역폭**: Resonator 선폭 $\kappa$에 제한됨 (보통 10~50 MHz) → 주파수 다중화 readout에 병목.
2. **낮은 포화 출력**: 소수의 Josephson junction만 사용 → 고차 비선형성에 의해 쉽게 포화 → 동시에 읽을 수 있는 qubit 수 제한.

---

## 13. Traveling Wave Parametric Amplifier (TWPA)

### 왜 TWPA가 필요한가?

JPA의 두 가지 한계(좁은 대역폭, 낮은 포화 출력)를 극복하기 위해 개발된 것이 **traveling wave parametric amplifier (TWPA)**이다.

광학에서 수 킬로미터의 약한 비선형 광섬유를 사용하는 광학 parametric amplifier에서 영감을 얻었다.

### TWPA의 구조

**Josephson TWPA** (Fig. 28(a)):
- 수천 개의 동일한 단위 셀로 구성된 비선형 전송선
- 각 단위 셀: 직렬 Josephson inductor $L_J$(비선형) + 병렬 캐패시터 $C$(선형)
- 특성 임피던스: $Z_0 = \sqrt{L_J/C} \approx 50\,\Omega$

비선형성이 수천 개의 junction에 분산되므로:
- **높은 포화 출력**: 각 junction을 한 번씩만 통과 → 고차 비선형성이 억제됨 → Kerr nonlinearity가 $1/N^2$으로 감소 ($N$: junction 수)
- **넓은 대역폭**: Resonator 없이 전파하는 신호 → resonator 선폭에 제한받지 않음

### Phase Matching 문제

Four-wave mixing 과정에서 에너지 보존은 만족되지만 **phase matching**이 깨질 수 있다:
- 시스템 비선형성
- Signal과 pump 광자 사이의 큰 주파수 차이
→ 이 둘의 위상 속도가 달라 비평탄 이득 프로파일, 이득 감소 발생.

### Resonant Phase Matching (RPM)

해결책: 주기적으로 배치된 LC resonator(phase matching resonator)를 TWPA 단위 셀에 삽입한다 (Fig. 28(a), (d)).

**원리**:
- LC resonator들이 집합적으로 특정 주파수에서 정지 대역(stopband)을 만들어 분산 특성을 변형한다.
- Pump 주파수를 이 공진 주파수 근방(분산 특성이 급변하는 지점 왼쪽)에 설정하면 pump의 파동 벡터가 "운동량 킥"을 받아 signal과 phase matching이 이루어진다.
- Fig. 28(c): phase matching 없이는 비평탄 이득 프로파일, RPM 적용 시 넓은 대역에 걸쳐 평탄한 이득 프로파일이 얻어진다.

**설계 세부 사항**:
- Pump 주파수의 최적값은 pump 출력에 의존한다 (Fig. 28(d) 삽입도).
- 이 기술은 O'Brien et al.에 의해 개발되었으며, Josephson TWPA의 실용화를 이끌었다.

### 비선형성 구현 방식의 다양성

TWPA의 비선형성은 다음 중 하나로 구현할 수 있다:
- **초전도 박막의 운동 인덕턴스 (kinetic inductance)**: NbTiN 등 박막 사용
- **Josephson junction 배열**: 가장 일반적인 접근

또한 SNAIL(Superconducting Nonlinear Asymmetric Inductive eLement) 기반 parametric amplifier(SPA)도 넓은 대역폭과 높은 동적 범위를 보여준 다른 접근이다.

---

## 14. 전체 그림: 읽기 체인의 최적화

### 시스템 설계의 큰 그림

Fig. 19(a)는 대표적인 실험 설정을 보여준다:

1. **신호 생성**: AWG(Arbitrary Waveform Generator)로 readout 펄스 생성
2. **Qubit plane**: Qubit-resonator 시스템 (극저온, ~10 mK)
3. **신호 반사**: $S_{11}$ (반사 계수)
4. **제1 증폭 단계**: JPA 또는 TWPA — quantum-limited amplification (4K 이하)
5. **제2 증폭 단계**: HEMT 증폭기 (~4 K)
6. **복조**: heterodyne mixing — 실온
7. **디지타이즈**: ADC
8. **디지털 신호처리**: 디지털 복조, 상태 분류

### 핵심 설계 파라미터 요약

| 파라미터 | 역할 | 트레이드오프 |
|---|---|---|
| $g$ (coupling rate) | dispersive shift $\chi = g^2/\Delta$ 증가 | 너무 크면 Purcell decay rate 증가 |
| $\kappa$ (resonator 선폭) | readout 속도 향상 | 너무 크면 Purcell decay rate 증가 |
| $\Delta$ (detuning) | Purcell 보호 향상 | 너무 크면 dispersive shift $\chi$ 감소 |
| $n_c = \Delta^2/4g^2$ | QND 조건 유지 한도 | readout 출력 상한 |
| $\chi = \kappa/2$ | 최대 상태 구분 조건 | 최적 탐침 주파수 선택 기준 |

### 각 소자별 역할 요약

| 소자 | 목적 | 위치 |
|---|---|---|
| Readout resonator | Qubit 상태를 microwave 위상/진폭으로 변환 | 극저온 |
| Purcell filter | Qubit Purcell decay rate 억제 + 빠른 readout 호환 | 극저온 |
| JPA / TWPA | Quantum-limited 1차 증폭, SNR 향상 | 극저온 (~4K) |
| HEMT | 2차 증폭 | ~4K |
| IQ mixer | Heterodyne 복조 | 실온 |
| ADC + DSP | 디지털 복조, 상태 분류 | 실온 |

---

## 참고 그림 목록

- **Fig. 19**: (a) Dispersive readout 실험 설정 개략도. (b) 두 qubit 상태에 대한 $|S_{11}|$과 위상 응답. (c) IQ 복소 평면에서의 두 상태.
- **Fig. 20**: (a) detuning $\Delta$에 따른 dispersive shift $\chi$. (b) 음의 detuning 영역 확대.
- **Fig. 21**: IQ mixer 회로 개략도.
- **Fig. 22**: Heterodyne detection 개략도: (a) 아날로그 복조, (b) 샘플링 타이밍, (c) IQ plane 히스토그램.
- **Fig. 23**: 시간에 따른 상태 분포 변화 (약한 측정 → 강한 측정).
- **Fig. 24**: Purcell effect 회로 모델과 Purcell filter 개략도.
- **Fig. 25**: Phase-preserving parametric amplification 개략도.
- **Fig. 26**: Phase-sensitive parametric amplification 개략도.
- **Fig. 27**: JPA 회로 및 펌핑 방식 (four-wave mixing vs. three-wave mixing).
- **Fig. 28**: TWPA 회로 및 resonant phase matching.

---

## 핵심 수식 모음

| 수식 | 내용 | 식 번호 |
|---|---|---|
| $H_{\rm JC}$ | Jaynes-Cummings Hamiltonian | (144) |
| $H_{\rm disp}$ | Dispersive Hamiltonian | (145) |
| $\chi = g^2/\Delta$ | Dispersive shift (2준위 근사) | — |
| $\chi = -g_{01}^2/\Delta \cdot 1/(1+\Delta/\alpha)$ | Dispersive shift (transmon) | (146) |
| $n_c = \Delta^2/(4g^2)$ | Critical photon number | — |
| $s(t) = A_{\rm RO}\cos(\omega_{\rm RO}t+\theta_{\rm RO})$ | Readout 신호 | (148) |
| $F(\tau_{ro}) = 1 - e^{-\tau_{ro}/T_1}$ | Relaxation 중 readout 충실도 | (173) |
| $\gamma_{\rm Purcell} = (g/\Delta)^2\kappa$ | Dispersive limit에서의 Purcell decay rate | (178) |
| $T_{\rm sys} = T_{N,1} + T_{N,2}/G_1 + \cdots$ | 시스템 노이즈 온도 (Friis formula) | (181) |
| $a_{\rm out} = \sqrt{G}a_{\rm in} + \sqrt{G-1}b_{\rm in}^\dagger$ | Quantum-limited amplification 산란 관계 | (184) |
| $\omega_s + \omega_i = 2\omega_p$ | Four-wave mixing 에너지 보존 | — |
| $\omega_s + \omega_i = \omega_p$ | Three-wave mixing 에너지 보존 | — |

---

*이 설명 파일은 1904.06560v5 섹션 V (pp. 41–53)의 내용을 바탕으로 작성되었다.*
