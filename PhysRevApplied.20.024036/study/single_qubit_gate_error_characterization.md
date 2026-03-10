# 단일 큐비트 게이트 오류 특성화 — 논문 학습 노트

## 참고 논문

| 논문 | 저자 | 학술지 | 연도 |
|---|---|---|---|
| Characterizing errors on qubit operations via iterative randomized benchmarking | Sheldon et al. (IBM) | Phys. Rev. A 93, 012301 | 2016 |
| Calibration of Drive Nonlinearity for Arbitrary-Angle Single-Qubit Gates Using Error Amplification | Lazăr et al. (ETH Zurich) | Phys. Rev. Applied 20, 024036 | 2023 |

---

## 1. 핵심 질문

> **단일 큐비트 게이트에 노이즈가 발생할 경우, coherent error rotation angle을 특정할 수 있는가?**

**결론: 가능하다.** 단, 방법별로 할 수 있는 것과 없는 것이 구분된다.

---

## 2. Coherent Error Rotation Angle을 특정하는 방법

### 2-1. 오류 증폭 시퀀스 (Error Amplification Sequence)

ε을 **직접 수치로 추출**하는 방법.

**시퀀스 구조:**
```
X_π/2 → (X_{π,π/2})^{2n} → 측정
```

**피팅 함수:**

$$P(|0\rangle) = a + \left[\frac{1}{2}(-1)^n \cos\!\left(\frac{\pi}{2} + 2n\epsilon\right)\right] \quad (X_{\pi/2} \text{의 경우})$$

$$P(|0\rangle) = a + \left[\frac{1}{2}\cos\!\left(\frac{\pi}{2} + 2n\epsilon\right)\right] \quad (X_{\pi} \text{의 경우})$$

- n을 늘릴수록 오류 각도 ε이 **2nε로 증폭**되어 피팅으로 정확히 추출 가능
- 추출된 ε과 게이트 오류율의 관계: $r \approx \epsilon^2/6$

### 2-2. IRB (Iterative Randomized Benchmarking)

Coherent 오류의 **존재 여부와 스케일**을 판별하는 방법.

랜덤 Clifford 시퀀스 사이에 타깃 게이트를 n회 반복 삽입하여 피델리티 감쇠 패턴을 분석한다.

| 오류 유형 | 피델리티 감쇠 패턴 | 판별 |
|---|---|---|
| Coherent (unitary) 오류 | n에 대해 **2차(quadratic)** 감소 | ε 존재 |
| Incoherent (decoherence) 오류 | n에 대해 **1차(linear)** 감소 | T₁, T₂ 제한 |

이론적 근거:

$$\alpha = 1 - \frac{n(2n-1)\epsilon^2}{3}$$

모델 선택에는 **AIC(Akaike Information Criterion)** 를 사용하여 선형/2차/혼합 모델 중 최적을 정량적으로 결정한다.

**검출 한계 (Sheldon et al. 실험):**
- π/128 과회전 → 명확히 검출
- π/256 과회전 → 검출 경계 수준

### 2-3. X-Y 축 오류 검출 시퀀스

기본 IRB로 검출되지 않는 위상 오차(축 오류)를 위한 별도 시퀀스:

```
X_π/2 - (X_π - Y_π)^n - Y_{-π/2}
```

게이트 오류: $2\epsilon^2/3$

---

## 3. 두 논문에서 실험적으로 확인된 오류 유형

### Phys. Rev. A 93, 012301 (Sheldon et al., 2016)

#### ① 트랜스몬 상위 준위에 의한 유니터리 오류
- 원인: 약한 비조화성(anharmonicity) δ/2π = −323 MHz
- 특징: 게이트 시간이 짧을수록 1/δ 스케일로 피델리티 저하
- 대응: DRAG 보정으로 부분 제거 가능

#### ② 진폭 오보정 (Over/Under-rotation)
- Coherent 오류 → IRB에서 2차 감쇠로 나타남
- 오류 증폭 시퀀스 보정 후 16.7 ns 게이트에서는 이 오류가 잔존하지 않음을 확인

#### ③ X-Y 축 오류 (위상 오차)
- **10 ns 게이트에서 발견**, 16.67 ns 게이트에서는 미검출
- 발견 계기: X_π/2Y_π/2 시퀀스의 오류가 개별 게이트 오류의 합보다 크게 나타남
- 원인: **펄스 왜곡(pulse distortion)** — 펄스 간격이 짧을 때 앞 펄스가 뒤 펄스에 겹침
- 오류 크기: 10 ns → ~3×10⁻³, 16.67 ns → ~2×10⁻⁵

#### ④ 비유니터리 잔여 오류 (최적화 후 남는 오류)
- 16.7 ns 최적 게이트에서 IRB 선형 감쇠 → coherent 오류 없음 확인
- 그러나 T₁, T₂ 예측값보다 피델리티가 **약 4배** 낮음
- 원인으로 두 가지 가능성 제시:
  - 드라이브 진폭 노이즈 (Rabi rate에 비례하는 dephasing: γ_φ = kΩ)
  - **펄스 반사(pulse reflections)** — RB 시퀀스 중 비간섭적으로 누적 (저자들이 더 유력하게 봄)

**최종 달성 성능:** 단일 큐비트 게이트 충실도 **99.95% (0.9995 ± 0.0002)** at 16.7 ns gate

### Phys. Rev. Applied 20, 024036 (Lazăr et al., 2023)

#### ⑤ 전자 소자에 의한 구동 비선형성 (Drive Nonlinearity)
- 원인: 마이크로파 신호 경로의 전자 부품(앰프, 믹서 등)의 비선형 왜곡
- 특징: π 게이트 기준으로 보정하면 다른 각도의 게이트에서 오차 발생
- 대응: 오류 증폭 기반 보정을 각도별로 독립적으로 적용

---

## 4. 오류 유형 종합 정리

| 오류 유형 | Coherent? | 두드러지는 조건 | 검출 방법 |
|---|---|---|---|
| 상위 준위 오류 | Yes | 짧은 게이트 시간 | RB vs. 시뮬레이션 비교 |
| 진폭 오보정 | Yes | 보정 전 | 오류 증폭 시퀀스 |
| X-Y 축 오류 | Yes | 매우 짧은 게이트 (펄스 겹침) | X_π/2-(X_π-Y_π)^n 시퀀스 |
| 구동 비선형성 | Yes | 임의 각도 게이트 | 오류 증폭 시퀀스 |
| 비유니터리 잔여오류 | No | 최적화 이후 | IRB 선형 감쇠 확인 |

---

## 5. 핵심 인사이트

- 두 논문 모두 **보정 후 남는 주된 한계는 coherent 오류가 아니라 비유니터리 오류**임을 공통적으로 지적한다.
- PhysRevA(2016)의 오류 증폭 기반 보정 방법을 PhysRevApplied(2023)이 임의 각도 게이트로 확장한 후속 연구로 볼 수 있다.
- Coherent 오류는 **오류 증폭으로 증폭 후 피팅**하면 각도 수준으로 정량화할 수 있다.
- 비유니터리 오류와 coherent 오류의 구분은 **IRB의 감쇠 패턴 (2차 vs. 1차)** 으로 판별한다.
