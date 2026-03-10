# 섹션 II: 양자회로 설계 (Engineering Quantum Circuits) — 상세 설명

**논문:** 1904.06560v5 (초전도 qubit 리뷰, Krantz et al.)
**대상:** 물리/공학 대학원생
**작성:** Claude Sonnet 4.6

---

## 개요

이 섹션은 초전도 회로를 기반으로 한 양자 시스템을 어떻게 **의도적으로 설계(engineer)** 할 수 있는지를 다룬다. 핵심 qubit 구조들을 살펴보면서, qubit transition frequency, anharmonicity, 노이즈 민감도를 회로 구조와 소자 파라미터 선택을 통해 어떻게 조절할 수 있는지 설명한다. 또한 개별 양자 시스템들 사이의 상호작용을 어떻게 설계하는지도 다룬다.

---

## 1. quantum harmonic oscillator (QHO)에서 transmon qubit까지

### 1.1 시작점: Schrödinger equation과 Hamiltonian

모든 양자역학적 시스템은 **시간 의존 Schrödinger equation**을 따른다:

$$\hat{H}|\psi(t)\rangle = i\hbar \frac{\partial}{\partial t}|\psi(t)\rangle$$

- $|\psi(t)\rangle$: 시간 $t$에서의 시스템 상태 (양자 상태 벡터)
- $\hbar = h/2\pi$: 환산 플랑크 상수
- $\hat{H}$: 시스템의 **총 에너지**를 기술하는 Hamiltonian 연산자

이 방정식의 공식 해는:

$$|\psi(t)\rangle = e^{-i\hat{H}t/\hbar}|\psi(0)\rangle$$

**직관적 이해:** Hamiltonian을 알면 시스템의 시간 발전을 완전히 기술할 수 있다. 초전도 qubit 연구에서 첫 번째 작업은 항상 회로의 Hamiltonian을 유도하는 것이다.

---

### 1.2 고전적 LC 회로와 Lagrangian-Hamiltonian formalism

초전도 qubit을 이해하는 출발점은 **선형 LC resonator** (그림 1(a) 참조)다. 이 회로에서 에너지는 두 형태로 진동한다:
- **전기 에너지** (capacitor C에 저장) → 운동 에너지에 대응
- **자기 에너지** (inductor L에 저장) → 위치 에너지에 대응

회로 소자의 에너지는 전압 $V(t')$와 전류 $I(t')$의 곱을 시간 적분하여 구한다:

$$E(t) = \int_{-\infty}^{t} V(t')I(t')dt'$$

#### generalized coordinate: flux

고전역학의 Lagrange-Hamilton formalism을 회로에 적용하려면 **generalized coordinate**가 필요하다. 여기서는 **flux**를 선택한다:

$$\Phi(t) = \int_{-\infty}^{t} V(t')dt'$$

flux는 전압의 시간 적분이다. (전하 $Q$를 사용해도 동등한 결과를 얻는다.)

#### 운동 에너지와 위치 에너지

flux $\Phi$를 이용하면 두 에너지 항을 다음과 같이 표현할 수 있다:

$$\mathcal{T}_C = \frac{1}{2}C\dot{\Phi}^2 \quad \text{(capacitor의 운동 에너지)}$$

$$\mathcal{U}_L = \frac{1}{2L}\Phi^2 \quad \text{(inductor의 위치 에너지)}$$

**직관:** $\dot{\Phi} = V$이므로 $\mathcal{T}_C = \frac{1}{2}CV^2$이 된다. inductor에서는 $\Phi = LI$이므로 $\mathcal{U}_L = \frac{1}{2L}\Phi^2 = \frac{1}{2}LI^2$이다.

#### Lagrangian과 Hamiltonian

Lagrangian은 운동 에너지에서 위치 에너지를 뺀 것이다:

$$\mathcal{L} = \mathcal{T}_C - \mathcal{U}_L = \frac{1}{2}C\dot{\Phi}^2 - \frac{1}{2L}\Phi^2$$

르장드르 변환을 통해 Hamiltonian을 구하려면 **conjugate momentum**을 계산한다. 여기서 conjugate momentum은 capacitor에 충전된 **전하** $Q$이다:

$$Q = \frac{\partial \mathcal{L}}{\partial \dot{\Phi}} = C\dot{\Phi}$$

최종 Hamiltonian은:

$$H = Q\dot{\Phi} - \mathcal{L} = \frac{Q^2}{2C} + \frac{\Phi^2}{2L} \equiv \frac{1}{2}CV^2 + \frac{1}{2}LI^2$$

**해석:** 이 Hamiltonian은 질량 $m = C$, 공진 주파수 $\omega = 1/\sqrt{LC}$인 1차원 harmonic oscillator의 Hamiltonian $H = p^2/2m + m\omega^2 x^2/2$와 정확히 같은 형태다. 즉, LC 회로는 전기적 harmonic oscillator다.

---

### 1.3 양자화: 고전 → 양자역학

고전 좌표를 **양자 연산자**로 승격(promote)시켜 양자역학적 기술로 넘어간다. 고전 포아송 괄호:

$$\{\Phi, Q\} = 1$$

가 양자 교환자 관계로 바뀐다:

$$[\hat{\Phi}, \hat{Q}] = i\hbar$$

이는 위치-운동량 교환자 $[\hat{x}, \hat{p}] = i\hbar$와 완전히 동일한 구조다.

#### 환산 변수 도입

편의상 **환산 flux** $\phi \equiv 2\pi\Phi/\Phi_0$와 **쿠퍼 쌍의 수** $n = Q/2e$를 도입한다. 여기서 $\Phi_0 = h/(2e)$는 초전도 flux quantum이다. 이를 이용하면 LC 회로의 양자 Hamiltonian은:

$$H = 4E_C n^2 + \frac{1}{2}E_L \phi^2$$

여기서:
- $E_C = e^2/(2C)$: **charging energy** — 섬(island)에 쿠퍼 쌍 하나를 추가하는 데 필요한 에너지
- $E_L = (\Phi_0/2\pi)^2/L$: **inductive energy**
- $n$: 섬 위의 초과 쿠퍼 쌍 수 (양자 연산자)
- $\phi$: gauge-invariant phase (inductor에 걸린 환산 flux)
- 교환자 관계: $[\phi, n] = i$

**참고:** 앞의 계수 4는 역사적 이유에서 비롯된 것으로, 원래 단일 전자 시스템에서 정의된 에너지 스케일을 쿠퍼 쌍(2전자) 시스템에 그대로 채택했기 때문이다.

---

### 1.4 quantum harmonic oscillator (QHO)의 energy level 스펙트럼

식 (13)의 Hamiltonian은 **1차원 이차 포텐셜** 속의 입자, 즉 QHO와 동일하다. $\phi$를 위치 좌표로 보면, 포텐셜 에너지는 $\phi^2$에 비례한다 (그림 1(b) 참조). 이 고유치 문제의 해는:

- 무한한 energy eigenstate들: $|k\rangle$, $k = 0, 1, 2, \ldots$
- **등간격 energy level 스펙트럼**: $E_{k+1} - E_k = \hbar\omega_r$

resonant frequency: $\omega_r = \sqrt{8E_L E_C}/\hbar = 1/\sqrt{LC}$

2차 양자화 형식으로 표현하면:

$$H = \hbar\omega_r\left(a^\dagger a + \frac{1}{2}\right)$$

여기서 $a^\dagger$($a$)는 resonator의 단일 여기를 생성(소멸)하는 연산자다.

원래의 연산자들을 사다리 연산자로 표현하면:
- $n = n_\text{zpf} \times i(a - a^\dagger)$
- $\phi = \phi_\text{zpf} \times (a + a^\dagger)$

여기서 $n_\text{zpf} = [E_L/(32E_C)]^{1/4}$와 $\phi_\text{zpf} = (2E_C/E_L)^{1/4}$는 각각 전하와 위상 변수의 **zero-point fluctuation**이다.

**zero-point fluctuation의 의미:** 양자역학적으로 기저 상태에서도 파동함수가 $n$과 $\phi$ 값의 범위에 걸쳐 분포한다. 이를 zero-point fluctuation이라 하며, 이는 고전적으로는 존재하지 않는 순수 양자 효과다.

#### QHO의 근본적 한계

QHO는 qubit으로 사용할 수 없다. 이유는 단순하다: **energy level들이 등간격**이기 때문이다. $|0\rangle \leftrightarrow |1\rangle$ transition을 구동할 때 사용하는 주파수가 $|1\rangle \leftrightarrow |2\rangle$ transition에도 정확히 공명하기 때문에, 계산 부공간($|0\rangle$, $|1\rangle$)만을 선택적으로 다룰 수 없다 (그림 1(b) 참조).

---

### 1.5 Josephson junction: 비선형성의 도입

QHO의 한계를 극복하려면 **anharmonicity**가 필요하다: $\omega_q^{0\to1}$과 $\omega_q^{1\to2}$가 충분히 다르면 두 energy level을 개별적으로 조작할 수 있다.

비선형성을 도입하는 핵심 소자가 **Josephson junction**이다. 이 접합은 비선형이고 손실이 없는 회로 소자로, 초전도 회로의 근간을 이룬다. 선형 inductor를 Josephson junction(비선형 inductor 역할)으로 교체하면 포텐셜 에너지의 형태를 바꿀 수 있다.

#### Josephson equation

Josephson junction의 두 가지 기본 관계식:

$$I = I_c \sin(\phi), \quad V = \frac{\hbar}{2e}\frac{d\phi}{dt}$$

- $I_c$: 임계 전류 (접합이 저항 없이 흘릴 수 있는 최대 전류)
- 첫 번째 식: 전류가 위상의 사인 함수 → **비선형성의 원천**

식 (3)과 (15)를 결합하면 Josephson junction의 포텐셜 에너지가 $-E_J\cos(\phi)$ 형태임을 유도할 수 있다. 따라서 Josephson qubit의 Hamiltonian은:

$$H = 4E_C n^2 - E_J\cos(\phi)$$

여기서:
- $E_C = e^2/(2C_\Sigma)$, $C_\Sigma = C_s + C_J$: 전체 capacitance (shunt capacitance + 접합 자체 capacitance)
- $E_J = I_c\Phi_0/2\pi$: Josephson energy

**핵심 변화:** 포텐셜 에너지가 $\phi^2$ (포물선형)에서 $-E_J\cos(\phi)$ (사인형)으로 바뀐다. 이것이 energy level 스펙트럼을 비등간격으로 만들어 qubit으로 사용 가능하게 한다 (그림 1(d) 참조).

---

### 1.6 transmon qubit: $E_J \gg E_C$ 체제

#### charge dispersion와 $E_J/E_C$ 비율

식 (16)에서 시스템 동역학은 $E_J/E_C$ 비율에 의해 결정된다. 초전도 qubit 커뮤니티는 $E_J \gg E_C$ 설계로 수렴해왔다. 그 이유:

- $E_J \leq E_C$인 경우: qubit이 **charge noise**에 매우 민감해진다 → 높은 결맞음 달성이 어렵다
- 현재 기술로는 Hamiltonian의 inductive(포텐셜) 부분을 설계하는 데 더 유연성이 있다
- $E_J \gg E_C$ 체제에서 charge noise 민감도를 크게 줄일 수 있다

**charge dispersion:** $n = Q/2e$에 의한 energy level의 변동. $E_J/E_C$가 커질수록 charge dispersion은 **지수적으로 감소**한다.

#### transmon 설계

$E_J \gg E_C$를 달성하는 방법: 접합에 **큰 shunt capacitor $C_s \gg C_J$를 병렬 연결**한다. 이렇게 하면 $E_C = e^2/(2C_\Sigma)$가 작아진다. 이 회로가 바로 **transmon** qubit이다.

이 한계에서 초전도 위상 $\phi$는 좋은 양자수(good quantum number)가 된다 — 즉, 파동함수의 $\phi$ 값 분포가 좁다. 낮은 energy eigenstate들은 포텐셜 우물 안에 국소화된다 (그림 1(d) 참조).

#### 코사인 포텐셜의 전개

$\phi$가 작은 경우, 포텐셜 항을 멱급수로 전개할 수 있다:

$$E_J\cos(\phi) = \frac{1}{2}E_J\phi^2 - \frac{1}{24}E_J\phi^4 + \mathcal{O}(\phi^6)$$

- **첫째 항 $\frac{1}{2}E_J\phi^2$**: harmonic oscillator 항 → 이것만 있으면 QHO
- **둘째 항 $-\frac{1}{24}E_J\phi^4$**: 4차 항 → 조화 구조를 깨뜨려 anharmonicity 생성
- 4차 항의 **음의 부호**: anharmonicity $\alpha = \omega_q^{1\to2} - \omega_q^{0\to1}$가 음수임을 의미

#### anharmonicity와 transmon 파라미터

transmon의 anharmonicity: $\alpha = -E_C$

일반적인 설계값:
- anharmonicity: $|\alpha| = 100\text{–}300\ \text{MHz}$
- qubit frequency: $\omega_q = (\sqrt{8E_JE_C} - E_C)/\hbar = 3\text{–}6\ \text{GHz}$
- 에너지 비율: $E_J/E_C \geq 50$ (charge 민감도 억제 충분)

**중요한 트레이드오프:**
- charge 민감도는 $E_J/E_C$ 증가에 따라 **지수적으로 감소** → 좋음
- anharmonicity는 **약한 멱함수**로 감소 → 수용 가능

따라서 두 효과의 균형을 맞추는 최적 설계 구간이 존재한다.

#### Duffing oscillator Hamiltonian

4차항까지 포함하면, QHO eigenstate 기저를 이용해 Hamiltonian이 **Duffing oscillator** 형태가 된다:

$$H = \omega_q a^\dagger a + \frac{\alpha}{2}a^\dagger a^\dagger aa$$

$|\alpha| \ll \omega_q$이므로 transmon은 **weakly anharmonic oscillator (AHO)**다.

높은 energy level ($k \geq 2$) 여기가 억제되면 — 충분한 $|\alpha|$ 또는 DRAG 펄스 등의 강건한 제어 기법으로 — AHO를 2준위계로 단순화할 수 있다:

$$H = \omega_q \frac{\sigma_z}{2}$$

단, 높은 energy level이 물리적으로 존재한다는 사실을 항상 염두에 두어야 한다. 실제로 높은 energy level을 의도적으로 활용하여 더 효율적인 gate operation을 구현하는 경우도 있다.

#### 3D transmon과 전기장 분포 설계

큰 shunt capacitor를 사용하면 charge dispersion을 줄이는 것 외에도, 양자 시스템의 **전기장 분포**를 설계할 수 있다. 3D transmon(2D transmon을 3D 공동에 결합)에서는 두 측면 capacitor 판 사이의 간격을 크게 만들면 전기장이 손실이 많은 계면(금속-기판, 기판-진공 계면)과의 상호작용이 줄어들어 결맞음 시간이 증가한다.

---

## 2. qubit Hamiltonian 설계 (Qubit Hamiltonian Engineering)

### 2.1 주파수 가변 qubit: split transmon

#### 왜 주파수 가변성이 필요한가?

고속 고fidelity gate operation을 구현하려면 **주파수 조절 가능한 qubit**이 필요하다. 예를 들어:
- 두 qubit을 공명 상태로 만들어 에너지를 교환(스왑)해야 할 때
- 유휴 상태(idling)에서는 두 qubit의 상호작용을 최소화해야 할 때

외부 파라미터로 시스템의 자유도에 제어 가능하게 접근해야 한다.

#### dc-SQUID 구조 (그림 2(a) 참조)

가장 널리 사용되는 기법: 단일 Josephson junction을 **두 개의 동일한 접합이 이루는 루프** (dc-SQUID)로 교체한다. SQUID의 두 팔 사이의 간섭 때문에, 루프를 통과하는 magnetic flux를 가하면 두 병렬 접합의 유효 임계 전류를 감소시킬 수 있다.

**fluxoid quantization 조건:**

$$\varphi_1 - \varphi_2 + 2\varphi_e = 2\pi k$$

여기서 $\varphi_e = \pi\Phi_\text{ext}/\Phi_0$. 이 조건으로 자유도 하나를 제거하고 SQUID 루프를 단일 접합으로 취급할 수 있다. 단, $E_J$가 외부 flux $\Phi_\text{ext}$에 의해 조절 가능하다는 중요한 변경이 생긴다.

**split transmon의 Hamiltonian** (상수 무시):

$$H = 4E_C n^2 - \underbrace{2E_J|\cos(\varphi_e)|}_{E_J'(\varphi_e)}\cos(\phi)$$

이 식은 식 (16)과 유사하지만, $E_J$가 $E_J'(\varphi_e) = 2E_J|\cos(\varphi_e)|$로 교체되었다. 유효 Josephson energy $E_J'$는 인가 flux에 대해 $\Phi_0$ 주기로 변하며, 0에서 최대값 $2E_J$까지 변한다. 따라서 **qubit frequency를 $\Phi_\text{ext}$로 주기적으로 조절**할 수 있다 (그림 2(b) 참조).

#### flux noise의 트레이드오프

split transmon은 주파수 가변성을 얻는 대신, **랜덤 flux fluctuation**에 대한 민감도가 생긴다. qubit 스펙트럼의 기울기:

$$
\frac{\partial\omega_q}{\partial\Phi_\text{ext}}$$

가 flux noise 민감도를 1차 근사로 나타낸다. 이 민감도는 $\Phi_\text{ext} = k\Phi_0$ (정수 $k$배의 flux quantum)에서만 0이 된다. 이 점들이 **flux sweet spot**이다.

#### asymmetric split transmon (그림 2(c) 참조)

최근 연구 방향: 두 접합을 **비대칭**으로 만들어 flux noise 민감도를 줄이면서도 충분한 가변성을 유지한다. 접합 비대칭도 $\gamma = E_{J2}/E_{J1}$를 도입하면:

$$H = 4E_C n^2 - \underbrace{E_{J\Sigma}\sqrt{\cos^2(\varphi_e) + d^2\sin^2(\varphi_e)}}_{E_J'(\varphi_e)}\cos(\phi)
$$

여기서 $E_{J\Sigma} = E_{J1} + E_{J2}$, $d = (\gamma-1)/(\gamma+1)$는 접합 비대칭 파라미터.

두 가지 극한:
- **$d = 0$ (대칭)**: $E_J'(\varphi_e) = E_{J\Sigma}|\cos(\varphi_e)|$ → 식 (21)로 환원
- **$|d| \to 1$**: $E_J'(\varphi_e) \to E_{J\Sigma}$ → flux 가변성 소멸, 단일 접합 케이스 (식 16)와 동일

asymmetric split transmon의 이점 (그림 2(d) 참조):
- 전체 주파수 가변 범위에 걸쳐 **flux 민감도가 억제**된다
- cross-resonance gate: 두 qubit 간의 특정 주파수 detuning이 최적, asymmetric split transmon으로 제작 편차를 보정할 수 있는 소폭 조절 범위 확보
- surface code: 단열 CPHASE gate 기반 방식은 qubit 간의 특정 주파수 구성이 필요하며, asymmetric split transmon이 잘 맞는다

---

### 2.2 더 큰 anharmonicity를 향해: flux qubit과 fluxonium

#### split transmon의 한계

대칭/비대칭 split transmon은 단일 접합 버전과 같은 회로 구조(사인형 포텐셜)를 공유한다. 따라서 qubit 특성을 설계할 수 있는 범위가 근본적으로 달라지지 않는다. 특히 **transmon형 qubit의 제한된 anharmonicity**는 본질적으로 높은 energy level로의 잔류 여기를 유발하여 gate operation 성능을 저해한다.

이를 극복하려면 회로에 추가적인 복잡성을 도입해야 한다.

#### flux qubit (그림 2(e) 참조)

**flux qubit**은 qubit 루프에 **3개(또는 4개)의 접합**을 도입한다:
- 한쪽 브랜치: 작은 접합 1개 (Josephson energy $E_J$)
- 다른쪽 브랜치: 더 큰 접합 2개 (크기 비율 $\gamma$, 각각 $\gamma E_J$)

이 추가 접합이 단순히 split transmon에 접합 하나를 더하는 것처럼 보이지만, 사실은 **회로 구조 자체가 바뀌어** 포텐셜 에너지 프로파일이 완전히 달라진다.

각 접합에 위상 변수가 대응되고, fluxoid quantization 조건으로 자유도 하나를 제거한다. 그 결과 2차원 포텐셜 지형이 생기지만, 배열 접합이 더 크다($\gamma > 1$)는 가정 하에 **quasi-1D 근사**를 사용할 수 있다:

$$H \approx 4E_C n^2 - E_J\cos(2\phi + \varphi_e) - 2\gamma E_J\cos(\phi)$$

여기서:
- $\phi$: 두 배열 접합에 걸린 브랜치 위상의 합의 절반 $(\phi_1 + \phi_2)/2$
- $\varphi_e = 2\pi\Phi_\text{ext}/\Phi_0$: 외부 flux
- 둘째 항: 작은 접합 기여
- 셋째 항: 두 배열 접합의 합산 기여 ($2\gamma E_J$)

이 두 항의 합은 단순한 코사인이 아닌 **biharmonic** 형태로, 외부 flux $\varphi_e$와 접합 면적 비율 $\gamma$에 따라 포텐셜 프로파일과 고유상태가 달라진다.

#### flux qubit의 작동점: flux degeneracy point

가장 일반적인 작동점: **$\varphi_e = \pi + 2\pi k$** (반 flux quantum이 루프를 통과할 때). 이 점에서:
- qubit 스펙트럼이 최솟값에 도달
- qubit frequency가 1차 flux noise에 **민감하지 않음** (그림 2(f) 참조)
- 이 점을 **flux degeneracy point**라 하며, flux qubit의 최적 결맞음 시간을 얻는 지점

#### single-well vs. double-well 포텐셜

이 작동점에서 $\gamma$ 값에 따라 포텐셜이 달라진다:

**single-well ($\gamma \geq 2$):**
- transmon과 유사한 특성
- capacitively shunted flux qubit (CSFQ): 이 체제를 탐구, 긴 결맞음과 상당히 높은 anharmonicity 달성
- 중요 차이: CSFQ의 anharmonicity는 **양수** ($\alpha > 0$) — transmon의 음수 anharmonicity와 반대

**double-well ($\gamma < 2$):**
- **persisting-current flux qubit (PCFQ)**
- 직관적 그림: 서로 반대 방향으로 도는 순환 전류 상태가 qubit 자유도를 이룸
- anharmonicity가 transmon이나 CSFQ보다 훨씬 클 수 있음
- transition matrix element $|\langle 1|\hat{n}|0\rangle|$, $|\langle 1|\hat{\phi}|0\rangle|$이 동일한 $E_J/E_C$ 기준 상당히 작아짐 → 더 긴 relaxation time 기대

#### fluxonium qubit (그림 2(g) 참조)

fluxonium은 PCFQ 아이디어의 극단적 확장이다. 배열 Josephson junction의 수를 **수십~수백 개** ($N \sim 100$)로 대폭 늘린다.

quasi-1D 근사를 적용하면, 마지막 항이 $-N\gamma E_J\cos(\phi/N)$가 된다. $N$이 크면 코사인의 인수 $\phi/N$가 충분히 작아지므로 2차 전개로 근사할 수 있다:

$$H \approx 4E_C n^2 - E_J\cos(\phi + \varphi_e) + \frac{1}{2}E_L\phi^2$$

여기서 $E_L = (\gamma/N)E_J$는 접합 배열의 등가 inductance의 inductive energy다. 이 등가 inductance는 값이 매우 크기 때문에 **superinductance**라 불린다.

**포텐셜의 물리적 의미:**
- $\frac{1}{2}E_L\phi^2$: 이차 포텐셜 (우물 형태)
- $-E_J\cos(\phi + \varphi_e)$: 사인형 변조

이 두 항의 경쟁이 풍부한 물리를 만든다:
- **plasmon state:** 같은 우물 안에 국소화된 상태
- **fluxon state:** 서로 다른 우물에 국소화된 상태

$E_J$와 $E_L$의 상대적 크기에 따라 다양한 체제가 나타난다. transition 스펙트럼은 일반적으로 flux qubit과 유사하며 (그림 2(h) 참조), flux sweet spot에서 긴 결맞음과 높은 anharmonicity 모두 기대할 수 있다.

fluxonium은 최근 밀리초 수준의 $T_1$ 시간 달성과 이러한 잘 보호된 qubit에 적용 가능한 새로운 gate 기법 발명으로 큰 주목을 받고 있다.

#### $0\text{-}\pi$ qubit

더 강한 위상학적 노이즈 보호를 갖는 추가 확장이 $0\text{-}\pi$ qubit이다. 단, 외부 요동에 대한 강하게 억제된 민감도는 조작을 어렵게 만드는 트레이드오프가 있다.

---

## 3. interaction Hamiltonian 설계 (Interaction Hamiltonian Engineering)

개별 양자 시스템 간의 얽힘을 생성하려면 두 시스템의 자유도를 연결하는 **interaction Hamiltonian**을 설계해야 한다.

### 3.1 물리적 coupling: capacitive와 inductive

두 coupling된 시스템의 Hamiltonian:

$$H = H_1 + H_2 + H_\text{int}$$

여기서 $H_1$, $H_2$는 개별 양자 시스템의 Hamiltonian이고, $H_\text{int}$는 두 시스템의 변수를 연결하는 interaction Hamiltonian이다. 초전도 회로에서 coupling 에너지의 물리적 형태는 전기장 또는 자기장(또는 그 조합)이다.

#### capacitive coupling — 그림 3(a) 참조

두 회로의 전압 노드 사이에 capacitor를 놓으면:

$$H_\text{int} = C_g V_1 V_2$$

여기서 $C_g$는 coupling capacitance, $V_1$($V_2$)는 연결된 전압 노드의 전압 연산자.

두 transmon qubit을 직접 capacitive coupling하면 ($C_g \ll C_1, C_2$ 한계):

$$H = \sum_{i=1,2}\left[4E_{C,i}n_i^2 - E_{J,i}\cos(\phi_i)\right] + 4e^2\frac{C_g}{C_1 C_2}n_1 n_2$$

마지막 항이 상호작용이다. $V_i = (2e/C_i)n_i$를 사용했다. coupling 에너지는 coupling capacitance와 전압 연산자의 행렬 요소에 의존하며, 섭동 한계 ($C_g \ll C_1, C_2$)에서 쌍선형(bilinear)으로 나타난다.

구현 방법: capacitor 패드 가장자리를 가까이 가져오기만 하면 된다. coupling capacitance는 평면 capacitor 형상과 기판 유전 상수, 접지면 근접도 등 주변 환경에 의해 결정된다.

#### inductive coupling — 그림 3(c) 참조

두 루프가 공유하는 mutual inductance를 통한 coupling:

$$H_\text{int} = M_{12}I_1 I_2$$

여기서 $M_{12}$는 mutual inductance, $I_1$($I_2$)는 각 inductor의 전류 연산자.

두 rf-SQUID형 flux qubit의 완전한 Hamiltonian:

$$H = \sum_{i=1,2}\left[4E_{C,i}n_i^2 - E_{J,i}\cos(\phi_i) + \frac{1}{2}\frac{\Phi_{Li}^2}{L_i(1-K^2)}\right] - M_{12}(1-K^2)\frac{\Phi_{L1}}{L_1(1-K^2)}\frac{\Phi_{L2}}{L_2(1-K^2)}$$

여기서:
- 첫째, 둘째 항: Josephson junction 에너지
- 셋째 항: inductor 에너지
- 넷째 항: mutual coupling 에너지 ($MI_1I_2$ 형태)
- $K$: 무차원 mutual coupling 계수, $M_{12} = K\sqrt{L_1L_2}$로 정의
- $K^2$이 $L_1$, $L_2$, $M_{12}$를 재규격화 → 회로에 의한 부하 효과(loading effect) 반영

fluxoid quantization 조건으로 위상 변수를 이용해 표현하면 (식 30):

$$H = \sum_{i=1,2}\left[4E_{C,i}n_i^2 - E_{J,i}\cos(\phi_i) + \frac{1}{2}\frac{(\Phi_0/2\pi)^2(\phi_i - \phi_{ei})^2}{L_i(1-K^2)}\right] - M_{12}(1-K^2)\frac{(\Phi_0/2\pi)(\phi_1-\phi_{e1})}{L_1(1-K^2)}\frac{(\Phi_0/2\pi)(\phi_2-\phi_{e2})}{L_2(1-K^2)}$$

약결합 한계 $K^2 \ll 1$에서, coupling 항을 Josephson 전류로 근사하면:
$$
M_{12}I_1I_2 \approx M_{12}I_{c1}\sin\phi_1 \cdot I_{c2}\sin\phi_2$$

**kinetic inductance:** mutual inductance를 실현하는 방법 중 하나. 두 루프 회로를 가까이 위치시키거나 겹치게 하면 된다. Josephson junction이나 특정 금속에서 inductance는 기하학적 inductance가 아닌 **kinetic inductance**가 지배적이다. kinetic inductance는 전하 운반체의 관성 질량에서 비롯되며, 초전도체에서만 실용적으로 관찰된다. kinetic inductance의 주요 특징은 통상적인 기하학적 inductance보다 훨씬 큰 값을 가질 수 있다는 것이다.

---

### 3.2 coupling 축: transverse coupling과 longitudinal coupling

물리적 구현 방식과 관계없이, coupling이 시스템 동역학에 미치는 영향은 **개별 시스템의 eigenstate 기저**에서 표현된 형태로 결정된다.

#### transverse coupling

capacitive coupling된 두 transmon qubit (그림 3(a) 참조)을 2차 양자화로 표현하면 (식 27에서):

$$H = \sum_{i \in 1,2}\left[\omega_i a_i^\dagger a_i + \frac{\alpha_i}{2}a_i^\dagger a_i^\dagger a_i a_i\right] - g(a_1 - a_1^\dagger)(a_2 - a_2^\dagger)
$$

여기서 $g$는 coupling 에너지. $V \propto n \propto i(a - a^\dagger)$이므로 원래의 $n_1 n_2$ 항이 이 형태가 된다.

**transverse coupling이라 불리는 이유:** coupling Hamiltonian이 양쪽 oscillator 모두에 대해 비대각 위치에만 0이 아닌 행렬 요소를 갖는다. 즉:
$$
_i\langle k|a_i - a_i^\dagger|k\rangle_i = 0 \quad \text{(임의의 정수 } k, i \in 1,2\text{에 대해)}$$
반면 $_i\langle k \pm 1|a_i - a_i^\dagger|k\rangle_i \neq 0$

높은 energy level ($k \geq 2$)을 무시할 수 있다면, 식 (31)을 다음과 같이 두 스핀 Hamiltonian으로 자를 수 있다:

$$H = \sum_{i \in 1,2}\frac{1}{2}\omega_i\sigma_{z,i} + g\sigma_{y,1}\sigma_{y,2}
$$

이는 exchange interaction으로 coupling된 두 스핀 Hamiltonian이다. 현대 구현에서 가장 일반적으로 사용되며, 다양한 종류의 2-qubit entangling gate를 생성할 수 있다.

**참고:** 보통 interaction 항을 $\sigma_x\sigma_x$로 표현하는 경우가 많다. 여기서 $\sigma_y\sigma_y$를 사용한 것은 임의적 선택이며 동역학을 바꾸지 않는다. 다만 capacitive와 inductive coupling이 모두 있는 경우, $\sigma_x\sigma_x$와 $\sigma_y\sigma_y$ 모두 필요할 수 있다.

#### qubit-resonator transverse coupling (Jaynes-Cummings model) — 그림 3(b) 참조

qubit과 harmonic oscillator 사이의 transverse coupling:

$$H = \frac{1}{2}\omega_q\sigma_z + \omega_r a^\dagger a + g(\sigma_+ a + \sigma_- a^\dagger)$$

여기서:
- $\omega_q$, $\omega_r$: qubit과 resonator frequency
- $\sigma_+ = |0\rangle\langle 1|$: qubit excitation 연산자
- $\sigma_- = |1\rangle\langle 0|$: qubit de-excitation 연산자
- dispersive limit ($g \ll \omega_q, \omega_r$) 가정: 이중 (탈)여기 항($\sigma_+ a^\dagger$ 및 $\sigma_- a$)은 빠르게 진동하여 평균이 0이 됨 (rotating wave approximation, RWA)

이 Hamiltonian은 **원자가 resonant cavity 안에서 상호작용하는 표준 모형**으로 알려져 있다 — cavity quantum electrodynamics (cavity QED). 이것이 회로로 확장된 것이 **circuit quantum electrodynamics (cQED)**다. cQED는 초전도 양자 정보 구조에서 고fidelity readout, cavity bus, 양자 메모리, cat state 양자 계산 등 다양한 응용에 사용된다.

#### resonator를 통한 qubit coupling — 그림 3(b) 참조

qubit-qubit 직접 capacitive coupling의 물리적 분리 한계를 극복하기 위해, **resonator를 중간 coupling 매체**로 사용할 수 있다. 예를 들어, 두 transmon qubit이 공통 resonator에 capacitive coupling되면:

$$H = \sum_{i=1,2}\left(\omega_i a_i^\dagger a_i + \frac{\alpha_i}{2}a_i^\dagger a_i^\dagger a_i a_i\right) + \omega_r a_r^\dagger a_r + g_{1r}(a_1^\dagger a_r + a_1 a_r^\dagger) + g_{2r}(a_2^\dagger a_r + a_2 a_r^\dagger)$$

dispersive limit ($g_{ir} \ll |\omega_i - \omega_r|$)에서, resonator를 적절한 변환과 근사로 처리하면 **resonator가 분리된 시스템**으로 취급되고, 합성 시스템이 transverse coupling된 두 qubit으로 단순화된다 (식 32 참조). 이 방식은 물리적으로 약 1 cm 떨어진 qubit들도 coupling할 수 있어 유용하다.

#### longitudinal coupling

inductive coupling된 두 flux qubit (그림 3(c) 참조)을 생각한다. double-well 포텐셜 (그림 2(g) 참조)에서 우물 사이 장벽이 높으면 energy degeneracy point $\Phi_e = \pi$에서 qubit transition frequency가 지수적으로 작아진다. 이 degeneracy point 근방에서:
- $\sin(\phi)$의 비대각 행렬 요소가 0에 가까움
- 기저 상태와 여기 상태가 서로 다른 우물에 국소화
- $\langle 1|\sin(\phi)|1\rangle - \langle 0|\sin(\phi)|0\rangle \neq 0$

이 경우 Hamiltonian은 다음으로 표현된다:

$$H = \sum_{i=1,2}\frac{1}{2}\omega_i\sigma_{z,i} + g\sigma_{z1}\sigma_{z2}$$

이제 coupling 축이 qubit quantization 축과 **같다** — 이를 **longitudinal coupling**이라 한다.

**longitudinal coupling의 중요성:**
- **에너지 교환 없이** 얽힘을 생성할 수 있다
- **quantum annealing**에 필수적: 어떤 어려운 조합 최적화 문제들이 식 (35)의 Ising Hamiltonian으로 모델링되며, 그 바닥 상태를 찾으면 문제가 풀린다

중간 qubit 모드를 longitudinal coupling의 coupler로도 사용할 수 있다 (그림 3(d) 참조). 추가 rf-SQUID가 coupling을 중개하며, coupling 강도를 coupler SQUID의 flux bias로 조절할 수 있다.

**tunable coupler의 이점:**
- 넓은 범위의 coupling 강도 제공
- 높은 on/off 비율 → gate error rate 감소
- 고fidelity entangling gate 달성의 다양한 방법
- 트레이드오프: 추가 제어 선이 필요

#### 혼합형 coupling: qubit에 longitudinal, resonator에 transverse

순수 transverse/longitudinal coupling 외에도 혼합형 interaction Hamiltonian이 있다:

$$H = \frac{1}{2}\omega_q\sigma_z + \omega_r a^\dagger a + g\sigma_z(a + a^\dagger)$$

이 모형은 qubit에 대해서는 **longitudinal**, harmonic oscillator에 대해서는 **transverse**다. 이를 일반적으로 "longitudinal" coupling이라 부르지만, 오직 한 시스템에 대해서만 longitudinal임을 유의해야 한다.

harmonic oscillator에 대해 물리적으로 순수한 longitudinal coupling을 구현하는 것은 어렵다. E-장($V$)이나 B-장($I$) 모두 harmonic oscillator의 eigenmode에 대해 transverse이기 때문이다. 그러나 transverse 모형(식 33)은 특정 작동 체제에서 longitudinal 모형으로 변환될 수 있다.

#### quantum annealing에서의 응용

quantum annealing 등의 응용에서는 longitudinal coupling($\sigma_z\sigma_z$, 문제 매핑용)과 transverse coupling($\sigma_x\sigma_x$, annealing 성능 향상용) **모두**가 필요하며, 독립적인 제어가 요구된다.

---

## 4. 핵심 개념 정리 및 요약

### 4.1 qubit 설계 계층 구조

| qubit 유형 | 회로 구조 | $E_J/E_C$ | anharmonicity | 주파수 가변성 | 주요 특징 |
|---|---|---|---|---|---|
| QHO (LC 회로) | 선형 L + C | — | 0 (등간격) | — | qubit 불가 |
| Cooper-pair box | 1 JJ + 작은 C | $\lesssim 1$ | 높음 | — | charge noise에 민감 |
| transmon | 1 JJ + 큰 $C_s$ | $\gg 1$ | $-E_C$ (100~300 MHz) | 없음 | 범용, charge noise 강인 |
| split transmon (대칭) | dc-SQUID + 큰 $C_s$ | $\gg 1$ | $-E_C$ | 있음 | flux noise 민감 |
| split transmon (비대칭) | asymmetric SQUID + 큰 $C_s$ | $\gg 1$ | $-E_C$ | 제한적 | flux noise 저감 |
| CSFQ | 3 JJ + 큰 $C_s$ | $\gg 1$ | 양수, 중간 | 부분적 | single-well 체제 |
| PCFQ | 3 JJ | 중간 | 매우 높음 | 부분적 | double-well, 순환 전류 |
| fluxonium | 1 JJ + JJ 배열 ($N \sim 100$) | 중간 | 매우 높음 | flux 의존 | superinductance, ms 수준 $T_1$ |

### 4.2 coupling 방식 비교

| coupling 유형 | 물리적 구현 | Hamiltonian 형태 | 특징 |
|---|---|---|---|
| 직접 capacitive | capacitor $C_g$ | $n_1 n_2 \to \sigma_{y,1}\sigma_{y,2}$ | transverse, 에너지 교환 |
| resonator 매개 capacitive | resonator + $C_g$ | $g_{1r}(a_1^\dagger a_r + \text{h.c.})$ | transverse, 원거리 coupling 가능 |
| 직접 inductive | mutual inductance $M_{12}$ | $I_1 I_2 \to \sigma_{z,1}\sigma_{z,2}$ | longitudinal, 에너지 교환 없음 |
| tunable coupler | rf-SQUID 매개 | 조절 가능 | on/off 비율 높음 |
| 혼합형 | qubit-resonator | $\sigma_z(a + a^\dagger)$ | qubit에 longitudinal, resonator에 transverse |

### 4.3 주요 물리 직관 요약

1. **QHO → transmon:** 선형 inductor를 Josephson junction으로 교체하면 포텐셜이 포물선 → 코사인으로 바뀌어 비등간격 스펙트럼이 생긴다. $E_J \gg E_C$ 체제에서 charge noise 내성이 확보된다.

2. **anharmonicity의 트레이드오프:** $|\alpha| = E_C$이므로, 큰 $C_s$ (작은 $E_C$)는 charge noise 내성은 높이지만 anharmonicity를 줄인다. DRAG 펄스 등의 기법으로 제한된 anharmonicity를 보완한다.

3. **주파수 가변성의 비용:** dc-SQUID로 주파수를 조절하면 flux noise 민감도가 생긴다. asymmetric junction이 이 트레이드오프를 개선한다.

4. **더 많은 접합 = 더 많은 설계 자유도:** 3~4개의 접합(flux qubit)이나 수십~수백 개의 배열(fluxonium)을 사용하면 포텐셜 형태를 근본적으로 바꿀 수 있어 더 높은 anharmonicity와 더 강한 노이즈 보호가 가능하다.

5. **transverse vs. longitudinal coupling:** transverse coupling($\sigma_x\sigma_x$, $\sigma_y\sigma_y$)은 에너지 교환을 통해 얽힘을 생성하며, 범용 gate operation에 활용된다. longitudinal coupling($\sigma_z\sigma_z$)은 에너지 교환 없이 얽힘을 생성하며, quantum annealing 등에서 핵심적이다.

---

*이 설명은 1904.06560v5 논문의 섹션 II (102~418행)를 기반으로 작성되었습니다.*
