# Qiskit Pulse 종합 정리

> **논문**: Thomas Alexander et al., "Qiskit pulse: programming quantum computers through the cloud with pulses"
> **저널**: Quantum Science and Technology **5**, 044006 (2020)
> **기관**: IBM Quantum (Watson, Tokyo, Zürich)

---

## 1. 전체 흐름: 회로 → 펄스 컴파일 파이프라인

### 추상화 계층 구조

```
[사용자]
   ↓  QuantumCircuit (게이트 수준)
[Qiskit Terra 트랜스파일러]
   ↓  OpenQASM (네이티브 게이트 집합으로 최적화)
[Qiskit Pulse 스케줄러]
   ↓  Pulse Schedule (시간·채널 배치)
[OpenPulse 백엔드]
   ↓  AWG/디지타이저 제어 신호
[양자 하드웨어]
```

- 회로 모델: 게이트 순서만 중요, 절대 시간 무관
- 펄스 모델: **절대 시간 + 채널 동기화** 필수
- 스케줄러 기본 정책: **as-late-as-possible** (T₁, T₂ 감쇠 최소화)

---

## 2. Qiskit Pulse 프로그래밍 모델

### 2.1 Pulse (펄스)

복소수 진폭 시계열 [d₀, ..., d_{n-1}], 최대 단위 노름.
실제 출력 신호:

$$D_j = \operatorname{Re}\left[e^{i2\pi f j \, dt + \phi} \, d_j\right]$$

- `f`: 변조 주파수 (반송파), `φ`: 위상
- `dt`: 사이클 타임 (ibmq_almaden: **0.222 ns**)
- 샘플 수가 곧 펄스 지속 시간 (단위: dt의 정수 배)

**파라메트릭 펄스** 예시:

```python
from qiskit.pulse.pulse_lib import Gaussian
gaussian_pulse = Gaussian(duration=128, amp=0.2, sigma=16)
```

주요 펄스 형태:
| 이름 | 용도 |
|------|------|
| Gaussian | 단일 큐빗 회전 |
| GaussianSquare | CR 게이트 (평탄 구간 + Gaussian 에지) |
| DRAG | 단일 큐빗 게이트 (누설 억제) |

### 2.2 Channels (채널)

하드웨어 신호선 추상화. 채널마다 독립 FIFO 큐.

| 채널 | 별칭 | 역할 |
|------|------|------|
| `DriveChannel(i)` | d_i | 큐빗 i 구동 (공명 주파수) |
| `MeasureChannel(i)` | m_i | 큐빗 i 측정 자극 |
| `ControlChannel(i)` | u_i | 2큐빗 게이트 등 임의 제어 |
| `AcquireChannel(i)` | a_i | 측정 신호 수집 (ADC) |

- `PulseChannel`: DriveChannel, MeasureChannel, ControlChannel의 부모 클래스
- 각 채널은 독립적인 주파수 `f`와 위상 `φ`를 추적 → **Virtual Z-gate** 구현 가능

> 회로 모델과 달리 채널은 물리 큐빗 특성에 의존하므로 **서로 교환 불가**.

### 2.3 Instructions (명령)

| 명령 | 피연산자 | 설명 |
|------|----------|------|
| `Play(pulse, channel)` | 펄스, PulseChannel | 파형 출력 |
| `Delay(duration, channel)` | 정수, Channel | 대기 |
| `ShiftPhase(phase, channel)` | float, PulseChannel | 위상 누적 (지속 시간 0) |
| `SetFrequency(freq, channel)` | float, PulseChannel | 주파수 설정 (지속 시간 0) |
| `Acquire(duration, channel, register)` | 정수, AcquireChannel, 레지스터 | 데이터 수집 |

- 모든 명령은 **결정론적 지속 시간** → 컴파일 시점에 절대 시각 확정 (하드 실시간)
- 다중 채널 의존 명령: 모든 피연산자 채널이 준비될 때까지 스톨

### 2.4 Schedule (스케줄)

```python
sched = Schedule(name='prepare_1_measure')
sched += Play(x180_pulse, DriveChannel(0))
sched += Acquire(duration, AcquireChannel(0), MemorySlot(0))
```

고전 기본 블록(basic block)과 동일한 개념.
`draw()` 메서드로 시각화 가능.

---

## 3. Cross-Resonance (CR) 게이트 물리

### 3.1 기본 원리

CR 게이트: **제어 큐빗**을 **타겟 큐빗의 공명 주파수**로 구동.
→ 유효 ZX 상호작용 해밀토니안 유도.

두 트랜스몬 시스템의 유효 CR 해밀토니안 (2차 섭동론):

$$\overline{H}_{CR} = \frac{Z \otimes B}{2} + \frac{I \otimes C}{2}$$

$$B = \omega_{ZI}I + \omega_{ZX}X + \omega_{ZY}Y + \omega_{ZZ}Z$$
$$C = \omega_{IX}X + \omega_{IY}Y + \omega_{IZ}Z$$

이상적 목표: **ZX 항만 남기기**

$$U_{ZX}(\theta_{ZX}) = \exp\!\left(-i\theta_{ZX}\frac{ZX}{2}\right)$$

- `U_ZX(π/2)`: perfect entangler → CNOT과 **국소 등가 (locally equivalent)**
- 나머지 항 (ZI, IX, IY, ZZ 등): 결맞음 오류 → 억제 필요

### 3.2 CR1 vs CR2

| | CR1 | CR2 (에코) |
|--|-----|-----------|
| 구조 | 단일 CR 펄스 | CR⁺ + X₁₈₀ + CR⁻ (에코) |
| 채널 | u₁ | u₁ + d₁ |
| ZI 항 | 크게 남음 | 에코로 거의 소거 |
| IX, IY 항 | 남음 | 에코로 소거 |
| 진폭 (π/2용) | 0.229 ± 0.019 | 0.098 ± 0.005 |

**CR2 스케줄 코드**:
```python
sched = Schedule(name='cr2')
cr_p = GaussianSquare(cr_dur, amp, sigma, square_width)
cr_m = GaussianSquare(cr_dur, -amp, sigma, square_width)
x180 = Drag(pi_dur, pi_amp, pi_sigma, pi_beta)

sched += Play(cr_p, ControlChannel(1))
sched += Delay(t_cr, DriveChannel(1))
sched += Play(x180, DriveChannel(1))
sched += Delay(t_cr, DriveChannel(1))
sched += Delay(t_cr, DriveChannel(1))
sched += Play(x180, DriveChannel(1))
```

### 3.3 위상 보정 (Appendix B)

실온 전자장비 → 큐빗 간 동축 케이블의 전달 함수로 위상 오프셋 φ₀ 발생.
→ ZY 항 유발.

보정 방법:
1. CR2 에코 해밀토니안 근사: `H_CR ≈ Ω(A,φ)(cos φ₀ ZX + sin φ₀ ZY) + ε`
2. A_opt = 0.108로 등중첩 상태 생성
3. Y 기저 측정 신호를 φ로 스윕 → |Tr(σ_y ρ)| 최대화
4. 최적 위상: **φ_opt = −0.166 rad**

---

## 4. QPT + 유효 해밀토니안 추출 방법론

### 4.1 양자 프로세스 단층촬영 (QPT)

d차원 채널 ε에 대한 Choi 행렬:

$$\Lambda_{\mathcal{E}} = \sum_{i=0}^{d-1} |i\rangle\langle i| \otimes \mathcal{E}(|i\rangle\langle i|)$$

실험 설정:
- 입력 상태: |0⟩, |1⟩, (|0⟩+|1⟩)/√2, (|0⟩+i|1⟩)/√2
- 측정 기저: X, Y, Z
- 2큐빗 → 144개 회로, 각 2048 샷
- Qiskit Ignis QPT fitter (최대 우도 추정, CPTP 보장)

### 4.2 Lindblad 초연산자에서 해밀토니안 계수 추출

노이즈 있는 진화를 Lindblad 방정식으로 기술:

$$\frac{d}{dt}\rho = \mathcal{G}(\rho) = \mathcal{L}_H(\rho) + \mathcal{D}(\rho)$$

$$\mathcal{L}_H(\rho) = -i[H, \rho], \quad \mathcal{D}(\rho) = \sum_j \gamma_j\!\left(A_j\rho A_j^\dagger - \tfrac{1}{2}\{A_j^\dagger A_j, \rho\}\right)$$

초연산자 표현 `|ρ⟩⟩ = S_ε|ρ(0)⟩⟩`에서 생성자 추출:

$$S_{\mathcal{G}} = t^{-1}\log(S_{\mathcal{E}})$$

파울리 기저 `B_{ij} = ½ P_i ⊗ P_j`의 직교성을 이용해 계수 추출:

$$\omega_{ij} = \frac{\operatorname{Tr}\!\left[S_{\mathcal{L}_{B_{ij}}}^\dagger S_{\mathcal{G}}\right]}{\|S_{\mathcal{L}_{B_{ij}}}\|}$$

> **핵심**: `S_L`과 `S_D`가 직교 → 해밀토니안 항과 소산 항을 분리해서 추출 가능.

### 4.3 ZX 항 진폭 보정 (Appendix C)

3차 섭동 전개로 ZX 상호작용 강도 피팅:

$$\frac{\omega_{ZX}(\bar{A})}{2} = -\frac{J\lambda\bar{A}}{\Delta}\!\left(\frac{\delta_1}{\delta_1+\Delta}\right) + \frac{J(\lambda\bar{A})^3\delta_1^2(\cdots)}{4\Delta^3(\delta_1+\Delta)^3(\cdots)}$$

피팅 결과: `J = 1.87 ± 0.046 MHz` (CR1), `1.79 ± 0.033 MHz` (CR2)
→ θ_{ZX} = π/2 달성 진폭 역산

---

## 5. CNOT 피델리티 최적화

### 국소 회전 최적화 (Appendix D)

CR 게이트를 CNOT으로 변환: 제어·타겟 각각에 **전·후 단일 큐빗 회전** 적용.
12개 실수 파라미터 Θ를 최적화:

$$F_{\max} = \max_{\Theta} F[\mathcal{E}_{CR}(\bar{A}_{\pi/2}),\, U_{\text{ent}}(\Theta)]$$

$$U_{\text{ent}}(\Theta) = U_{\text{pre}}^\dagger(\Theta)\, U_{\text{ent}}\, U_{\text{post}}^\dagger(\Theta)$$

$$U_{\text{pre}}(\Theta) = U_3(\Theta_0,\Theta_1,\Theta_2) \otimes U_3(\Theta_3,\Theta_4,\Theta_5)$$

### 결과

| 구분 | 최대 이론 피델리티 | RB 측정 피델리티 |
|------|:-----------------:|:---------------:|
| CR1-CNOT | F_max = 0.992 | **F = 0.981** |
| CR2-CNOT | F_max = 0.994 | **F = 0.979** |
| 백엔드 기본 CNOT | — | F = 0.984 |

> 취소 톤(cancellation tone) 없이 **개방 루프 보정만으로** 백엔드 기본값에 필적.

Virtual Z-gate: `ShiftPhase` 명령으로 구현 (지속 시간 0, 소프트웨어 처리).

---

## 6. IQ 측정 및 판별기

### 측정 체인 (3단계)

```
[측정 자극 펄스] → [초전도 공명기]
         ↓
  level-0: raw  — ADC 디지타이징된 시계열 (복소수 벡터)
         ↓  [커널 (박스카 적분기)]
  level-1: kerneled  — IQ 평면의 복소수 점
         ↓  [판별기 (LDA 등)]
  level-2: discriminated  — 비트 {0, 1}
```

- `AcquireChannel` + `Acquire` 명령으로 각 레벨 선택 가능
- 측정 자극 펄스와 Acquire 명령은 **동기 정렬** 필수

### 판별기 예시: 측정 누화(crosstalk) 조사

- ibmq_singapore 큐빗 16, 17 선택
- 4개 보정 스케줄: cal_00, cal_01, cal_10, cal_11
- 두 종류 LDA 판별기 비교:
  - Single: 자기 큐빗 데이터만 사용
  - Both: 4개 스케줄 전체 사용

| 판별기 | Q16 측정 배정 피델리티 | Q17 측정 배정 피델리티 |
|--------|:-------------------:|:-------------------:|
| Single | 89.21% | 91.06% |
| Both | 89.48% | 90.62% |

- Pearson 상관계수 t-검정 (95% 신뢰수준): **유의미한 누화 없음**
- 결론: 누화 없을 때 n큐빗에 2n 보정 스케줄로 충분 (2^n 불필요)

---

## 핵심 수식 모음

| 수식 | 의미 |
|------|------|
| $D_j = \operatorname{Re}[e^{i2\pi fj\,dt+\phi}d_j]$ | 실제 출력 신호 |
| $\overline{H}_{CR} = (Z\otimes B)/2 + (I\otimes C)/2$ | 유효 CR 해밀토니안 |
| $U_{ZX}(\theta) = \exp(-i\theta ZX/2)$ | ZX 회전 게이트 |
| $\Lambda_{\mathcal{E}} = \sum_i|i\rangle\langle i|\otimes\mathcal{E}(|i\rangle\langle i|)$ | Choi 행렬 |
| $S_{\mathcal{G}} = t^{-1}\log(S_{\mathcal{E}})$ | Lindblad 생성자 |
| $\omega_{ij} = \operatorname{Tr}[S_{\mathcal{L}_{B_{ij}}}^\dagger S_{\mathcal{G}}]/\|S_{\mathcal{L}_{B_{ij}}}\|$ | 해밀토니안 계수 추출 |

---

## 더 공부할 것들

- [ ] OpenPulse 명세 ([arXiv:1809.03452](https://arxiv.org/abs/1809.03452))
- [ ] Virtual Z-gate 원리 (McKay et al. PRA 2017, Ref [20])
- [ ] CR 게이트 3차 섭동론 전개 (Sheldon et al. PRA 2016, Ref [24])
- [ ] GRAPE 최적 제어 (Khaneja et al. JMR 2005, Ref [15])
- [ ] 리처드슨 외삽법 (Richardson extrapolation, 에러 완화)
- [ ] IQ 평면에서 LDA 판별기 수학적 배경
