# 섹션 III: Noise, Decoherence, 오류 완화
**논문:** 1904.06560v5 — A quantum engineer's guide to superconducting qubits

---

## 개요

초전도 qubit을 실제로 작동시킬 때 가장 근본적인 문제는 **noise** 와 **decoherence** 이다. qubit 제어 장비나 양자 프로세서 주변 환경에서 발생하는 무작위적이고 통제 불가능한 물리적 과정들이 noise의 원천이 되어, qubit의 양자 상태를 무너뜨리고 게이트 연산의 충실도(fidelity)를 저하시킨다.

이 섹션에서는 초전도 회로에서의 noise와 decoherence의 기초 이론을 소개하고, 특정 유형의 noise를 완화하기 위한 coherent 제어 방법을 다룬다.

---

## A. Noise의 유형

### 개요: 열린 계와 닫힌 계

**닫힌 계(closed system)** 에서는 qubit의 동역학이 결정론적이다. 즉, 초기 상태와 Hamiltonian을 알면 미래의 어떤 시점에서도 qubit 상태를 정확히 예측할 수 있다.

그러나 실제 qubit은 **열린 계(open system)** 이다. qubit은 환경의 통제 불가능한 자유도(uncontrolled degrees of freedom)와 상호작용하며, 이것이 바로 **noise(fluctuations)** 이다. 시간이 지남에 따라 qubit 상태는 예측에서 점점 멀어지고, 결국 양자 정보가 소실된다.

Noise는 크게 두 가지 유형으로 분류된다.

---

### 1. 체계적 Noise (Systematic Noise)

체계적 noise는 **추적 가능한 고정된 제어 오류 또는 판독 오류**에서 비롯된다.

**예시:** qubit에 180도 회전(X_π 펄스)을 가하려 했는데, 제어 필드가 정확히 조정되지 않아 매번 같은 양만큼 과회전(over-rotation) 또는 과소회전(under-rotation)이 발생하는 경우.

**핵심 특성:**
- 동일한 오류가 매번 반복된다.
- 다양한 제어 시퀀스에서 사용될 때 마치 무작위 noise처럼 보일 수 있다. (펄스가 다른 횟수, 다른 순서로 적용되기 때문에)
- 그러나 근본적으로는 **결정론적(deterministic)** 오류이다.
- 원인을 찾으면 **올바른 교정(calibration)** 이나 하드웨어 개선으로 수정 가능하다.

---

### 2. 확률적 Noise (Stochastic Noise)

확률적 noise는 qubit에 coupling된 파라미터들의 **무작위 요동(random fluctuations)** 에서 비롯된다.

**주요 예시:**
- 제어선(control lines)에 있는 50Ω 저항의 thermal noise (Johnson noise): 전압 및 전류 요동이 발생하며, noise 전력은 온도와 대역폭에 비례한다.
- qubit 제어 펄스에 사용되는 발진기(oscillator)의 amplitude noise 또는 phase noise.
- 금속 표면, 기판 표면, 금속-기판 계면, 기판 내부에서의 무작위적인 전기·자기장 요동.

이러한 요동들이 qubit 파라미터에 알 수 없고 통제 불가능한 변동을 일으켜 **qubit decoherence**를 야기한다.

---

### 3. Noise 강도와 Qubit 민감도

Qubit이 noise에 영향을 받는 정도는 두 가지 요인에 의해 결정된다:

1. **qubit에 가해지는 noise의 양**: 재료 과학, 제조(fabrication), 제어 전자 장치, 극저온 공학의 문제.
2. **qubit의 noise 민감도(susceptibility)**: qubit 설계의 문제.

Qubit은 한 유형의 noise에 덜 민감하도록 설계할 수 있지만, 그 대가로 다른 유형의 noise에 더 민감해질 수 있다. 따라서 재료 과학, 제조 공학, 전자 설계, 극저온 공학, qubit 설계 모두가 높은 coherence를 달성하는 데 역할을 한다.

**Noise coupling 방식:** Noise는 qubit 양자화 축을 기준으로 **longitudinal(종방향)** 또는 **transverse(횡방향)** 으로 coupling된다. 이를 시각화하는 도구가 Bloch sphere이다.

---

## B. Noise와 Decoherence의 모델링

### 1. Bloch Sphere 표현

Bloch sphere는 2준위계(qubit)의 양자 상태를 표현하는 단위 구이다. (Fig. 4 참조)

#### 상태 표현

Qubit 상태 |ψ⟩ = α|0⟩ + β|1⟩를 Bloch sphere에서 극각(polar angle) θ와 방위각(azimuthal angle) φ로 표현하면:

$$|\psi\rangle = \cos\frac{\theta}{2}|0\rangle + e^{i\phi}\sin\frac{\theta}{2}|1\rangle \qquad \text{(Eq. 37)}$$

**관례:**
- 북극(north pole): |0⟩ 상태 (편극 p = +1)
- 남극(south pole): |1⟩ 상태 (편극 p = -1)
- z축: **longitudinal axis(종방향 축)** — qubit 양자화 축, Hamiltonian의 σ_z 항에 해당
- x-y 평면: **transverse plane(횡방향 평면)** — Hamiltonian의 σ_x, σ_y 항에 해당

**물리적 의미:**
- 순수 상태(pure state)의 Bloch 벡터는 구의 표면에 위치한다 (|α|² + |β|² = 1).
- 혼합 상태(mixed state)는 구의 내부에 위치한다 (|a⃗| < 1).

#### Density Matrix 표현

Bloch 벡터 a⃗을 이용한 density matrix:

$$\rho = \frac{1}{2}(I + \vec{a} \cdot \vec{\sigma}) = \begin{pmatrix} |\alpha|^2 & \alpha\beta^* \\ \alpha^*\beta & |\beta|^2 \end{pmatrix} \qquad \text{(Eqs. 38-40)}$$

여기서 I는 항등 행렬, σ⃗ = [σ_x, σ_y, σ_z]는 Pauli matrix 벡터이다.

- **순수 상태:** Tr(ρ²) = 1
- **혼합 상태:** 0 ≤ Tr(ρ²) < 1

#### Rotating Frame

정지 기준틀에서 Bloch 벡터는 qubit 주파수 (E₁-E₀)/ℏ로 z축 주위를 세차 운동한다. 시각화의 편의를 위해, x-y 축도 함께 qubit 주파수로 회전하는 **rotating frame** 을 사용하면, Bloch 벡터는 정지해 보인다.

---

### 2. Bloch-Redfield Decoherence 모델

Bloch-Redfield 모델은 qubit에 약하게 coupling된 noise 원천들이 짧은 상관 시간(short correlation times)을 갖는다는 가정 하에 성립한다. 이 조건에서 relaxation 과정은 두 가지 비율로 특성화된다.

#### 기본 Relaxation Rate 정의

$$\Gamma_1 \equiv \frac{1}{T_1} \qquad \text{(longitudinal relaxation rate, Eq. 41)}$$

$$\Gamma_2 \equiv \frac{1}{T_2} = \frac{\Gamma_1}{2} + \Gamma_{\varphi} \qquad \text{(transverse relaxation rate, Eq. 42)}$$

여기서 Γ_φ는 pure dephasing rate이다.

> **중요:** Γ₂가 두 비율의 합으로 쓰이는 것은 각 감쇠 함수가 지수함수적(exponential)임을 가정한다. 이는 Lorentzian 형태의 noise 스펙트럼, 예를 들어 높은 주파수 차단이 있는 white noise에서 성립한다.

#### Bloch-Redfield Density Matrix

초기 상태 |ψ⟩ = α|0⟩ + β|1⟩에 대한 시간 발전 density matrix:

$$\rho_{\rm BR} = \begin{pmatrix} 1 + (|\alpha|^2 - 1)e^{-\Gamma_1 t} & \alpha \beta^* e^{i\delta\omega t} e^{-\Gamma_2 t} \\ \alpha^* \beta e^{-i\delta\omega t} e^{-\Gamma_2 t} & |\beta|^2 e^{-\Gamma_1 t} \end{pmatrix} \qquad \text{(Eq. 44)}$$

**각 항의 물리적 의미:**
- `exp(-Γ₁t)`: longitudinal 감쇠 함수 — qubit 집단(population)의 relaxation
- `exp(-Γ₂t)`: transverse 감쇠 함수 — coherence의 소실
- `exp(iδωt)`: 의도적 위상 누적 — qubit 주파수 ω_q와 rotating frame 주파수 ω_d의 차이 δω = ω_q - ω_d
- t >> T₁, T₂ 극한에서: 왼쪽 위 행렬 원소 → 1 (모든 집단이 기저 상태로 relaxation), 나머지 → 0

---

## C. Longitudinal Relaxation (T₁)

### 물리적 의미

Longitudinal relaxation rate Γ₁은 qubit 양자화 축(z축) 방향의 탈편극화(depolarization)를 기술한다. "energy decay" 또는 "energy relaxation"이라고도 한다.

**Bloch sphere에서의 직관 (Fig. 4(b)):**
- p = +1 (북극): 완전히 기저 상태 |0⟩
- p = -1 (남극): 완전히 들뜬 상태 |1⟩
- p = 0 (구의 중심): 완전히 탈편극화된 혼합 상태

### 원인: Transverse Noise

Longitudinal relaxation은 **transverse noise** 에 의해 야기된다. 즉, x 또는 y축을 통해 qubit에 coupling되는 noise이다. 이는 상호작용 Hamiltonian의 비대각 원소(off-diagonal elements)가 |0⟩과 |1⟩ 상태 사이의 전이를 유도하기 때문이다.

### Up-rate와 Down-rate

$$\Gamma_1 \equiv \frac{1}{T_1} = \Gamma_{1\downarrow} + \Gamma_{1\uparrow} \qquad \text{(Eq. 45)}$$

- **Γ₁↓**: down-rate — |1⟩ → |0⟩ relaxation (에너지 방출)
- **Γ₁↑**: up-rate — |0⟩ → |1⟩ 들뜸 (에너지 흡수)

**볼츠만 균형(detailed balance):**
$$\Gamma_{1\uparrow} = e^{-\hbar\omega_q / k_B T} \Gamma_{1\downarrow}$$

**초전도 qubit의 실제 조건:**
- Qubit 주파수: ω_q/2π ≈ 5 GHz
- 작동 온도: T ≈ 20 mK (희석 냉동기)
- 이 조건에서 ℏω_q >> k_BT이므로, 볼츠만 인자 exp(-ℏω_q/k_BT)로 up-rate Γ₁↑가 지수적으로 억제된다.
- **결과:** qubit은 자발적으로 에너지를 차가운 환경으로 방출하지만, 환경이 qubit을 들뜨게 하는 경우는 극히 드물다.

### T₁ 측정

Fig. 5(a)에 T₁ 측정의 예가 나와 있다:
1. X_π 펄스로 qubit을 들뜬 상태로 준비한다.
2. 시간 τ 동안 자발적으로 기저 상태로 relaxation되도록 둔다.
3. Qubit을 측정한다.
4. 이 과정을 여러 번 반복하여 앙상블 평균을 얻는다.
5. 결과: T₁ = 85 μs의 지수적 감쇠.

> **한 번의 측정은 동전 던지기와 같다:** |0⟩ 또는 |1⟩이 나오지만, 집단의 편극을 추정하려면 많은 횟수를 반복해야 한다.

---

## D. Pure Dephasing (T_φ)

### 물리적 의미

Pure dephasing rate Γ_φ는 Bloch sphere의 x-y 평면에서의 탈편극화를 기술한다. "pure dephasing"이라 부르는 이유는, energy relaxation과 같은 다른 위상 파괴 과정과 구분하기 위해서이다.

### 원인: Longitudinal Noise (Fig. 4(c))

Pure dephasing은 **longitudinal noise** — z축을 통해 qubit에 coupling되는 noise — 에 의해 야기된다. 이러한 longitudinal noise는 qubit 주파수 ω_q를 요동시켜, ω_q가 rotating frame 주파수 ω_d와 달라지게 만든다. 결과적으로 Bloch 벡터가 rotating frame에서 앞뒤로 세차 운동한다.

### 물리적 직관: Bloch 벡터의 부채꼴 펼침 (Fan-out)

동일하게 준비된 여러 Bloch 벡터가 x축을 향하고 있다고 가정하자. 각각의 인스턴스에서 qubit 주파수의 확률적 요동이 서로 다른 세차 주파수를 만들어, x-y 평면에서 Bloch 벡터들이 부채꼴로 펼쳐진다. 시간이 지나면 방위각 φ가 완전히 탈편극화된다.

> **주의:** 이 확률적 효과는 transverse relaxation rate Γ₂에 포함된다. Eq. (44)의 결정론적 항 exp(±iδωt)는 의도적인 detuning을 나타내며, 이것과는 다르다.

### T₁ Relaxation과의 핵심 차이점

| 특성 | Pure Dephasing (T_φ) | Energy Relaxation (T₁) |
|------|---------------------|-----------------|
| 원인 | Longitudinal noise (z축) | Transverse noise (x-y축) |
| 공명 여부 | 비공명: 모든 주파수의 noise | 공명: qubit 주파수의 noise만 |
| 가역성 | 가역적 (원칙적으로) | 비가역적 |
| 에너지 교환 | 없음 (탄성적) | 있음 (비탄성적) |
| 완화 방법 | Dynamical decoupling(DD) 펄스로 "되돌리기" 가능 | 근본적으로 회복 불가능 |

Pure dephasing은 탄성적(elastic) 과정이므로 원칙적으로 **가역적(reversible)** 이다. 즉, 양자 정보를 보존하면서 단위 연산(유니터리 게이트, 예: dynamical decoupling 펄스)으로 되돌릴 수 있다. 반면, 자발적 energy relaxation은 **비가역적(irreversible)** 이다. Qubit이 수많은 통제 불가능한 환경 모드로 에너지를 방출하고 나면, 양자 정보는 사실상 복구 불가능하다.

---

## E. Transverse Relaxation (T₂)

### 물리적 의미

Transverse relaxation rate Γ₂ = Γ₁/2 + Γ_φ는 중첩 상태의 coherence 소실을 기술한다. 예를 들어, (1/√2)(|0⟩ + |1⟩) 상태가 x축을 향하는 경우이다 (Fig. 4(d)).

**두 가지 기여:**
1. **Longitudinal noise** → qubit 주파수를 요동시켜 pure dephasing Γ_φ 유발 (빨간색)
2. **Transverse noise** → 중첩 상태의 들뜬 상태 성분을 relaxation시켜 energy relaxation 기여 Γ₁ (파란색)

Energy relaxation 이벤트 자체도 **위상 파괴 과정(phase-breaking process)** 이다: relaxation이 일어나면 Bloch 벡터는 북극 |0⟩을 향하게 되고, 적도 어느 방향을 향하고 있었는지의 정보, 즉 중첩 상태의 상대적 위상이 소실된다.

**중요 한계:** T₂는 절대로 2T₁보다 커질 수 없다. Pure dephasing이 없다면 T₂의 최댓값은 2T₁이다.

### 측정 방법 1: Ramsey Interferometry — Fig. 5(b)

**프로토콜:**
1. X_π/2 펄스로 Bloch 벡터를 적도(equator)에 위치시킨다.
2. Qubit 주파수와 약간 다른 주파수(δω만큼 detuning)로 구동하면, Bloch 벡터가 rotating frame에서 z축 주위를 δω 속도로 세차 운동한다.
3. 시간 τ 동안 자유 세차 운동.
4. 두 번째 X_π/2 펄스로 Bloch 벡터를 z축으로 사영(project)한다.
5. 앙상블 평균으로 qubit 편극의 τ 의존성을 얻는다.

**결과:** 감쇠하는 진동. 특성 시간 T₂* = 95 μs.

> **"\*" 표기의 의미:** Ramsey 실험은 비균일 확대(inhomogeneous broadening)에 민감하다. 즉, 1/f noise처럼 한 실험 시도 내에서는 준-정적이지만 시도 사이에서는 변하는 저주파 요동에 매우 민감하다. 이는 해당 N=0 filter function이 0주파수에 집중되어 있기 때문이다.

### 측정 방법 2: Hahn Echo — Fig. 5(c)

Ramsey interferometry와 동일하지만, 자유 발전 시간 중간에 Y_π 펄스를 추가한다.

**원리:** 이 π 펄스가 준-정적인 pure dephasing 기여를 "재집속(refocus)"하여, 비균일 확대 메커니즘에 덜 민감한 T₂E 추정치를 얻는다.

**결과:** T₂E = 120 μs (Ramsey의 T₂* = 95 μs보다 개선됨).

> T₂E가 T₂* > T₂E이므로, 저주파 pure dephasing noise의 일부가 완화되었지만, T₂E가 아직 2T₁ 한계에 도달하지 못했으므로 일부 남아 있다는 의미이다.

---

## F. 1/f Noise에 의한 수정

### 왜 Bloch-Redfield가 항상 성립하지 않는가

초전도 qubit에서 광대역 dephasing noise(예: flux noise, charge noise, 임계전류 noise)는 **1/f noise power spectrum**을 나타내는 경향이 있다. 이 noise는:
- ω = 0 근방에서 특이점(singular)을 가진다.
- 긴 상관 시간을 가진다.
- 일반적으로 Bloch-Redfield 설명에 해당하지 않는다.

따라서 Eq. (44)의 비대각 원소의 감쇠 함수는 일반적으로 비지수함수(non-exponential)이고, 단순한 Eq. (42)는 적용할 수 없다.

### Gaussian 분포 1/f Noise 모델

Qubit이 많은 독립적인 요동체(fluctuators)에 coupling되어 있다고 가정하면, 중심 극한 정리에 의해 통합적으로 **Gaussian distribution** noise를 생성한다. 이 경우:

- **위상 감쇠 함수:** exp[-(t/T_φ,G)²] — 지수함수가 아닌 **Gaussian 함수**
- **T₁ 감쇠 성분은 분리 가능:** T₁ noise는 qubit 주파수 근방에서 규칙적(regular)이기 때문

수정된 density matrix (Eq. 46):

$$\rho = \begin{pmatrix} 1 + (|\alpha|^2 - 1)e^{-\Gamma_1 t} & \alpha \beta^* e^{i\delta\omega t} e^{-\frac{\Gamma_1}{2} t} e^{-\chi_N(t)} \\ \alpha^* \beta e^{-i\delta\omega t} e^{-\frac{\Gamma_1}{2} t} e^{-\chi_N(t)} & |\beta|^2 e^{-\Gamma_1 t} \end{pmatrix}$$

여기서 `exp(-χ_N(t))`는 coherence function으로, 비지수함수적 dephasing을 포함하는 일반화된 pure dephasing을 기술한다. 아래첨자 N은 저주파 noise를 재집속하는 데 사용된 π 펄스의 수를 나타낸다.

**실험 예시 (Fig. 5(d)):**
- Ramsey 데이터에서 T₁ = 85 μs로 exp(-t/2T₁) 성분을 제거하면, 남은 pure dephasing 감쇠 함수는 Gaussian 형태를 취한다: ⟨exp(-χ_N(t))⟩ = exp[-(t/T_φ,G)²], T_φ,G = 98 μs.

> **White dephasing:** 1/f 메커니즘 외에도 판독 resonator의 잔여 photon number fluctuation과 같은 "white" pure dephasing 메커니즘도 존재하며, 이는 지수함수적 감쇠를 만든다.

---

## G. Noise Power Spectral Density (PSD)

### 정의

정류 noise 소스 λ의 noise power spectral density (PSD)는 위너-킨친(Wiener-Khintchine) 정리에 따라 자기상관 함수의 푸리에 변환으로 주어진다:

$$S_{\lambda}(\omega) = \int_{-\infty}^{\infty} d\tau \, \langle \lambda(\tau)\lambda(0)\rangle e^{-i\omega\tau} \qquad \text{(Eq. 47)}$$

- **양측(bilateral) PSD:** 적분 범위가 (-∞, ∞) — 양수 및 음수 주파수 포함
- **단측(unilateral) PSD:** 양수 주파수만 고려 — PSD를 대칭화하여 얻음
- 두 표기법 모두 사용되므로 정의를 확인하고 인수(factor)를 추적해야 한다.

**역푸리에 변환:**

$$c_{\lambda}(\tau) = \frac{1}{2\pi} \int_{-\infty}^{\infty} d\omega \, S_{\lambda}(\omega) e^{i\omega\tau} \qquad \text{(Eq. 48)}$$

τ = 0에서 적분하면 noise의 2차 모멘트(분산, variance)가 얻어진다.

### 고전 vs 양자 Noise PSD

| 특성 | 고전 Noise | 양자 Noise |
|------|-----------|-----------|
| PSD 대칭성 | **대칭** (자기상관 함수가 실수) | **비대칭** 가능 (연산자 비가환성) |
| 예시 | Johnson noise (thermal noise), 1/f noise | 자발 방출(Nyquist noise) |
| 물리적 해석 | 실수 장의 요동 | 시간 순서 중요 |

**양자 시스템에서의 해석 (Fig. 6 참조):**
- **S(+ω_q):** qubit → 환경으로 에너지 이동 (유도 방출 + 자발 방출 → down-rate Γ₁↓)
- **S(-ω_q):** 환경 → qubit으로 에너지 이동 (흡수 → up-rate Γ₁↑)
- **Nyquist noise:** 차가운 환경으로의 자발 방출. 충분히 낮은 온도 또는 높은 주파수(ℏω > 2k_BT)에서 thermal noise를 지배하는 비대칭 PSD.

> S(ω_q)와 측정된 qubit 감쇠 함수 사이의 연결이 **noise spectroscopy**의 기반을 이룬다.

---

## H. 흔한 Noise의 종류

### 1. Charge Noise

Charge noise는 고체 소자에서 보편적으로 나타난다. 결함이나 전하 트랩(계면 유전체, 접합 터널 장벽, 기판 자체의 결함)에 있는 대전 요동체(charged fluctuators)에서 비롯된다. 이들은 주로 요동하는 two-level system (TLS) 앙상블 또는 벌크 유전 손실로 모델링된다.

**트랜스몬 qubit에서의 영향:**
- 캐패시터 판 사이의 전기장 → 유전 결함에 coupling
- 전기장 변수는 트랜스몬 양자화 축에 **transverse** 이므로, 주로 **energy relaxation (T₁)** 에 기여한다.
- E_J/E_C 비율이 충분히 크지 않은 경우(~60 미만), 트랜스몬 주파수가 광대역 전하 요동에 민감해져 **저주파 charge noise가 longitudinal으로 coupling → pure dephasing (T_φ)** 유발.

**Charge noise PSD:**

$$S_Q(\omega) = A_Q^2 \left(\frac{2\pi \times 1\text{Hz}}{\omega}\right)^{\gamma_Q} \qquad \text{(Eq. 49)}$$

- 준-보편적 값: A²_Q = (10⁻³e)²/Hz (1 Hz에서), γ_Q ≈ 1 (1/f 특성)
- **고주파 영역:** S_Q(ω) = B²_Q[ω/(2π × 1 Hz)] (ohmic noise)
- **1/f → ohmic 전환 주파수:** 보통 ~1 GHz 근방 (샘플마다 다름)

**역사적 맥락:** 초기 charge qubit은 큰 1/f 요동과 불연속적인 전하 오프셋(랜덤 전신 noise 유사)으로 심각하게 제한되었다. 이것이 **용량성 단락 charge qubit(transmon)** 개발의 강력한 동기가 되었으며, transmon은 charge noise에 대한 longitudinal 민감도를 대폭 감소시켰다.

---

### 2. Flux Noise

Flux noise는 초전도 금속 표면에 있는 스핀(자기 쌍극자)의 확률적 뒤집힘(stochastic flipping)에서 비롯된다. 이 스핀들의 무작위 요동이 flux-tunable qubit을 편향시키는 효과적인 자기장에 무작위 요동을 만든다.

**스플릿 트랜스몬에서의 영향:**
- 루프를 통과하는 외부 자기장 → 조셉슨 에너지 E_J를 통해 전이 주파수를 변조
- Flux noise는 트랜스몬에 **longitudinal으로 coupling** → **pure dephasing (T_φ)** 기여
- 예외: φ_e = 0 (1차 자기장 요동 민감도 없음)

**플럭스 qubit에서의 영향:**
- 자속 편향점에 따라, flux noise가 longitudinal (→ T_φ) 또는 transverse (→ T₁ relaxation)으로 coupling 가능

**Flux noise PSD:**

$$S_{\Phi}(\omega) = A_{\Phi}^2 \left(\frac{2\pi \times 1 \text{Hz}}{\omega}\right)^{\gamma_{\Phi}} \qquad \text{(Eq. 50)}$$

- 준-보편적 값: γ_Φ ≈ 0.8-1.0, A²_Φ ≈ (1 μΦ₀)²/Hz
- **주파수 범위:** 밀리헤르츠 이하부터 기가헤르츠 이상까지 확장됨
- 최근 연구에서 1/f flux noise가 qubit 주파수까지 연장될 때 T₁ 메커니즘이 됨을 발견.

**공학적 적용:**
- 낮은 주파수에서의 큰 1/f noise power 가중치 → dynamical decoupling (DD) 기법으로 효과적으로 완화 가능.
- **비대칭 접합 스플릿 트랜스몬:** 대칭 접합에 비해 flux noise 민감도가 낮음 (주파수 조절성은 감소하지만, 일반적으로 가치 있는 절충점).

**미해결 문제:** Flux noise의 정확한 물리적 기원은 아직 불분명하다. 1/f noise가 준-보편적이고 소자와 거의 무관하다는 사실은 공통된 기원을 강하게 시사한다. 최근 연구는 흡착된 분자 산소(adsorbed molecular oxygen)가 원인일 수 있다고 제안한다.

---

### 3. Photon Number Fluctuations

회로 QED 아키텍처에서 resonator photon number fluctuation은 또 다른 주요 decoherence 원인이다.

**메커니즘:**
- Resonator에 잔류하는 microwave 장이 photon number fluctuation을 가짐.
- 분산 정권(dispersive regime)에서 상호작용 항 χσ_z n을 통해 qubit에 영향을 줌 (섹션 II C 2 참조).
- 이 상호작용은 Stark shift를 만든다: Δ_Stark = 2ηχn̄ (n̄: 평균 photon 수, η = κ²/(κ² + 4χ²))

**분산 한계에서의 pure dephasing rate:**

$$\Gamma_{\phi} = \eta \frac{4\chi^2}{\kappa} \bar{n} \qquad \text{(Eq. 51)}$$

여기서:
- χ: qubit-resonator 분산 coupling 강도
- κ: resonator 감쇠율
- n̄: 평균 photon 수

**Noise PSD (Lorentzian):**

$$S(\omega) = 4\chi^2 \frac{2\eta \bar{n}\kappa}{\omega^2 + \kappa^2} \qquad \text{(Eq. 52)}$$

- κ까지는 사실상 **white noise** 스펙트럼.
- 3dB 차단 주파수는 resonator 감쇠율 κ에 의해 결정됨.

**Noise 원천:** 잔류 photon은 주로 희석 냉동기의 더 높은 온도 단계로부터의 복사(radiation)에서 비롯된다.

> 이 noise는 longitudinal으로 coupling되어 pure dephasing에만 기여한다. 따라서 T₁에는 직접 영향을 주지 않는다.

---

### 4. Quasiparticles

Quasiparticle(짝을 이루지 못한 전자, unpaired electrons)은 초전도 소자의 또 다른 중요한 noise 원천이다.

**영향:**
- Qubit 접합을 통한 quasiparticle 터널링 → **T₁ relaxation** 및 **pure dephasing (T_φ)** 모두 야기 가능
- Qubit 유형, 자속 편향점, 터널링이 발생하는 접합에 따라 다름

**Quasiparticle 밀도 문제:**
- 열역학적으로, 온도가 낮아질수록 quasiparticle 밀도는 지수적으로 억제되어야 한다.
- 그러나 실제로는 약 150 mK 아래에서, 관측된 quasiparticle 밀도(일반적으로 10⁻⁸ ~ 10⁻⁶ 쿠퍼쌍당)가 10 mK의 BCS 이론 예측보다 훨씬 높다.

**초과 Quasiparticle (Excess Quasiparticles)의 원인 (미해결):**
- 비열적 생성 메커니즘의 존재 가능성
- 밀리켈빈 온도에서의 "bottleneck effects"로 인한 재결합율 감소
- 또는 두 가지의 조합

**최신 결과:**
- 오늘날 최첨단 고-coherence 트랜스몬에서 관측된 T₁과 초과 들뜬 상태 집단은 ~10⁻⁷ ~ 10⁻⁶ 쿠퍼쌍당의 준-보편적 밀도를 가진 초과 "뜨거운" 비평형 quasiparticle과 자기 일관적(self-consistent)임.
- Quasiparticle을 일시적으로 펌프해 제거하면 T₁이 개선되고 T₁의 시간 변동성이 감소한다.

---

## I. Qubit-환경 상호작용의 연산자 형태

### 일반 상호작용 Hamiltonian

Qubit 자유도 Ô_q와 noise 원천의 자유도 λ̂ 사이의 상호작용:

$$\hat{H}_{\rm int} = \nu \hat{O}_q \hat{\lambda} \qquad \text{(Eq. 53)}$$

- ν: coupling 강도 (qubit의 환경 요동에 대한 민감도 ∂Ĥ_q/∂λ 관련)
- δλ: noise 환경이 만드는 요동

### T₁과 PSD의 연결

Transverse coupling (Ô_q ~ σ_x 또는 (a + a†)) 시, qubit 주파수의 noise가 상태 전이를 유발한다.

$$\Gamma_1 = \frac{1}{\hbar^2} \left| \langle 0 | \frac{\partial \hat{H}_q}{\partial \lambda} | 1 \rangle \right|^2 S_\lambda(\omega_{\mathbf{q}}) \qquad \text{(Eq. 54)}$$

**물리적 해석:**
- 이 식은 **Fermi's golden rule** 과 동등하다.
- Qubit의 transverse 민감도가 noise power spectral density (PSD)에 의해 구동된다.
- T₁은 qubit 전이 주파수 ω_q에서의 noise PSD에만 의존한다.

**예시 (트랜스몬):** 전하 요동 δλ = δn에 대해, 관련 항은 4E_C(n̂ - n_g)²이고, 민감도는 8E_C n̂이다.

### T_φ와 PSD의 연결

Longitudinal coupling (Ĥ_q ~ σ_z 또는 a†a) 시, noise는 확률적으로 qubit 전이 주파수를 변조하여 중첩 상태에 확률적 위상 발전을 도입한다 → **pure dephasing**.

**중첩 상태의 누적 위상:**

$$\varphi(t) = \int_0^t \omega_q dt' = \langle \omega_q \rangle t + \delta\varphi(t) \qquad \text{(Eq. 55)}$$

**주파수 요동으로 인한 위상 확산:**

$$\delta\varphi(t) = \frac{\partial\omega_{\mathbf{q}}}{\partial\lambda} \int_0^t \delta\lambda(t')dt' \qquad \text{(Eq. 56)}$$

여기서 ∂ω_q/∂λ = (1/ℏ)|⟨∂Ĥ_q/∂λ⟩|는 qubit의 longitudinal 민감도이다.

**Gaussian 통계 가정 하에서 앙상블 평균:**

$$\langle e^{i\,\delta\varphi(t)}\rangle = e^{-\frac{1}{2}\,\langle\delta\varphi^2(t)\rangle} \equiv e^{-\chi_N(t)} \qquad \text{(Eq. 57)}$$

**Coherence 감쇠 함수:**

$$\langle e^{-\chi_N(\tau)} \rangle = \exp\left[ -\frac{\tau^2}{2} \frac{\partial \omega_{\mathbf{q}}}{\partial \lambda} \int_{-\infty}^{\infty} g_N(\omega, \tau) S(\omega) d\omega \right] \qquad \text{(Eq. 58)}$$

여기서 g_N(ω, τ)는 **filter function** 으로, 제어 시퀀스가 noise PSD에 미치는 효과를 주파수 영역에서 표현한다.

---

## J. Noise Spectroscopy

### 기본 원리

Qubit은 주변 noise 환경에 매우 민감하며, 이 특성을 역으로 활용하여 **noise power spectral density (PSD)를 지도화(map out)** 할 수 있다.

**두 가지 발전 유형:**
1. **자유 발전(free evolution):** 제어 없이 qubit이 자유롭게 발전하는 기간 동안 (매우 짧은 DD 펄스 제외)
2. **구동 발전(driven evolution):** 제어 필드가 qubit에 적용되는 기간 동안

두 유형의 발전 모두 특성화해야 하며, noise PSD가 서로 다를 수 있다.

### 자유 발전 Noise Spectroscopy

**저주파 영역 (서브-밀리헤르츠 ~ ~100 Hz):**
- Ramsey 주파수 자체가 longitudinal noise에 민감하다.
- Ramsey 주파수의 시간 요동을 모니터링하여 noise PSD를 매핑.

**중간 주파수 영역 (0.1 ~ 300 MHz):**
- CPMG dynamical decoupling 시퀀스를 이용하여 좁은 대역 필터를 만든다.
- 자유 발전 시간 τ와 펄스 수 N을 변화시켜 다른 주파수에서 noise를 "샘플링".

**높은 주파수 영역 (1 GHz 이상):**
- T₁ 측정 + Fermi's golden rule → qubit 주파수 이상의 transverse noise 스펙트럼 매핑.

### 구동 발전 Noise Spectroscopy

**Spin-locking 기법:**
- x 또는 y축 방향의 강한 구동이 새로운 qubit 양자화 축을 정의.
- Rabi 주파수(Rabi frequency)가 spin-locking rotating frame에서의 새로운 "qubit 주파수".
- Qubit이 지속적인 구동 필드에 노출되는 동안의 noise 스펙트럼을 추론.

---

## K. Dynamical Decoupling

### Filter Function

Eq. (58)에서 함수 g_N(ω, τ)는 제어 시퀀스가 qubit에 미치는 noise PSD S_λ(ω)의 주파수 영역 filter로 해석할 수 있다 (Fig. 7(a) 참조).

**π 펄스 시퀀스에 대한 일반 filter function (Eq. 59):**

$$g_N(\omega, \tau) = \frac{1}{(\omega \tau)^2} \left| 1 + (-1)^{1+N} \exp(i\omega \tau) + \frac{1}{2} \sum_{j=1}^N (-1)^j \exp(i\omega \delta_j \tau) \cos(\omega \tau_\pi / 2) \right|^2$$

- N: π 펄스의 수
- δ_j ∈ [0,1]: j번째 π 펄스의 정규화된 위치
- τ: 전체 자유 유도 시간
- τ_π: 각 π 펄스의 길이

**핵심 성질:**
- N이 증가할수록(τ 고정), filter function의 피크가 더 높은 주파수로 이동.
- 1/f^α형(α > 0) noise에서, 더 큰 N은 더 작은 통합 noise에 해당한다.
- τ' = τ/N 고정 시 N이 커질수록 filter가 날카로워지고 ω'/2π = 1/2τ'에서 점근적으로 피크.

### Ramsey (N=0) vs Hahn Echo (N=1)

**Ramsey filter function (N=0):**

$$g_0(\omega, \tau) = \operatorname{sinc}^2 \frac{\omega \tau}{2} \qquad \text{(Eq. 60)}$$

- ω = 0에 중심을 둔 sinc 함수.
- 1/f noise에서 최악의 선택: noise가 가장 강한 저주파에서 최대 투과.

**Hahn echo filter function (N=1):**

$$g_1(\omega, \tau) = \sin^2 \frac{\omega \tau}{4} \operatorname{sinc}^2 \frac{\omega \tau}{4} \qquad \text{(Eq. 61)}$$

- 중심이 더 높은 주파수로 이동.
- ω = 0에서 값이 0: 저주파(준-정적) noise에 대한 민감도 없음.
- 1/f noise에서 유리: 더 높은 T₂E 달성.

### CPMG 시퀀스 (Fig. 7(a), (b))

**Carr-Purcell-Meiboom-Gill (CPMG) 시퀀스**는 자유 발전 시간 τ 내에 N개의 균등 간격 π 펄스를 적용한다. 이는 위의 개념을 더 많은 펄스로 확장한 것이다.

**효과:**
- N이 증가할수록 효과적인 T₂ 시간이 증가한다 (Fig. 7(b)).
- 강한 dephasing noise의 영향을 받는 qubit을 2T₁ 한계까지 끌어올릴 수 있다.

**예시 (Fig. 7(b)):**
- 1/f flux noise에 강하게 노출된 flux qubit.
- Ramsey (N=0): T₂ ≈ 300 ns
- Hahn echo (N=1): T₂E ≈ 1.5 μs
- N 증가에 따라 T₂가 점점 2T₁ 한계에 수렴.

### Dynamical Decoupling의 직관

**핵심 아이디어:** "spin echo" 기법에서, π 펄스가 자유 발전을 방해함으로써 저주파 noise에 의한 coherent 위상 분산을 "재집속(refocus)"한다. CPMG와 같은 더 발전된 버전은 다수의 π 펄스로 시스템을 더 자주 방해하여 filter 대역을 더 높은 주파수로 밀어 올린다.

> **1/f noise와 dynamical decoupling의 궁합이 좋은 이유:** 1/f noise는 낮은 주파수에서 power가 집중되므로("준-정적"), 저주파를 차단하는 DD filter가 매우 효과적이다.

---

## L. Noise 완화를 위한 엔지니어링

### 1. 재료 및 제조 개선

- **Charge noise:** 기판 세정, 기판 어닐링, 트렌칭(trenching) 등으로 material defect 수 감소.
- **Flux noise:** 자속 결함의 거동과 특성을 연구하고 광학적 표면 처리로 제거 시도.
- **Quasiparticle:** quasiparticle trap을 회로 설계에 추가하여 quasiparticle 수 감소.

### 2. 설계 개선

- **캐패시터 기하학 변경:** 전기장 모드 부피 증가 → 얇은 유전체 영역에서의 전기장 밀도 감소 → material defect "참여(participation)" 감소 → noise 민감도 감소.
- **비대칭 접합 스플릿 트랜스몬:** flux noise 민감도 낮춤 (주파수 조절성 감소 대가). 단열 CPHASE 게이트와 같은 게이트 방식에서 낮은 dephasing rate → 게이트 충실도 향상.

### 3. Dynamical Error Suppression

Spin echo 기법과 CPMG 시퀀스를 통한 1/f dephasing 완화 (위 섹션에서 상세 설명).

**Quasiparticle의 경우:** π 펄스의 확률적 적용이 quasiparticle을 qubit 영역에서 펌프해 제거 → 더 길고 안정적인 T₁. (이 기법은 coherent 오류가 아닌 incoherent 오류 T₁을 다루므로, dynamical error suppression과는 다른 메커니즘.)

### 4. 극저온 공학

**Photon shot noise의 경우:**
- 크라이오제닉 설정의 감쇠를 최적화하여 소자에 도달하는 thermal photon 플럭스 감소.
- 더 효율적인 열 싱킹으로 크라이오제닉 감쇠기 개선.
- 산란 thermal photon을 흡수하는 흡수성 "검정" 재료 추가.
- 열화를 위한 추가 공동 필터 추가.

---

## 핵심 요약표

| 물리량 | 기호 | 정의 | 원인 | 가역성 |
|--------|------|------|------|--------|
| Longitudinal relaxation 시간 | T₁ | Energy relaxation의 1/e 시간 | Transverse noise (x-y축) | 비가역 |
| Transverse relaxation 시간 | T₂ | Coherence 소실의 1/e 시간 | T₁ + pure dephasing | 부분적 |
| Pure dephasing 시간 | T_φ | 위상 정보 소실 시간 | Longitudinal noise (z축) | 가역 (원칙적으로) |
| Dephasing 시간 (Gaussian) | T_φ,G | 1/f noise에서의 Gaussian 감쇠 | 광대역 저주파 noise | 부분적 |

**Relaxation rate 관계:**

$$\frac{1}{T_2} = \frac{1}{2T_1} + \frac{1}{T_{\varphi}}$$

$$T_2 \leq 2T_1 \quad \text{(항상 성립)}$$

---

## 그림 참조 가이드

| 그림 | 내용 |
|------|------|
| Fig. 4 | Bloch sphere에서의 longitudinal/transverse noise 표현. (a) Bloch sphere, (b) T₁ longitudinal relaxation, (c) T_φ pure dephasing, (d) T₂ transverse relaxation |
| Fig. 5 | T₁, T₂ 측정. (a) T₁ 측정 (T₁=85μs), (b) Ramsey interferometry T₂* 측정 (95μs), (c) Hahn echo T₂E (120μs), (d) Gaussian pure dephasing 성분 분리 |
| Fig. 6 | 대칭 및 비대칭 noise PSD 예시: thermal noise, Nyquist noise, 1/f noise |
| Fig. 7 | Dynamical error suppression. (a) CPMG 시퀀스와 filter function, (b) N 증가에 따른 T₂ 향상 |

---

*이 설명은 논문 1904.06560v5의 섹션 III (pp. 12-22 해당 범위, 라인 419-750)을 기반으로 작성되었다.*
