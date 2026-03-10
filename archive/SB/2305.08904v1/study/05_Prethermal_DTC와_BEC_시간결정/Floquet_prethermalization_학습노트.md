# Floquet 사전열화(Prethermalization)와 Prethermal DTC

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.IV.D — Prethermal DTC
**작성일:** 2026-03-03
**목적:** 무질서 없이 고주파 구동만으로 DTC를 구현하는 사전열화 메커니즘 이해

---

## 목차

1. [사전열화란 무엇인가](#1-사전열화란-무엇인가)
2. [Floquet 사전열화의 메커니즘](#2-floquet-사전열화의-메커니즘)
3. [Prethermal DTC 모형](#3-prethermal-dtc-모형)
4. [MBL-DTC와 Prethermal DTC 비교](#4-mbl-dtc와-prethermal-dtc-비교)
5. [실험적 실현](#5-실험적-실현)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. 사전열화란 무엇인가

### 1-1. 개념

빠른 구동 시스템에서, 진정한 열화(thermalization)까지의 시간이 **지수적으로 길어지는** 현상:

$$t^* \sim \tau_0 e^{c\omega/J}$$

여기서:
- $\omega$: 구동 주파수
- $J$: 상호작용 강도 (에너지 스케일)
- $c$: 수치 상수

### 1-2. 직관

```
빠른 구동:  시스템이 에너지를 흡수하려면
            광자 여러 개를 한꺼번에 흡수해야 함
            (고조파 공정, high-order process)
            → 확률 ~ (J/ω)^n → 지수적으로 작음

결과:  t < t* 동안 시스템이 가열되지 않음
       마치 유효 정적 Hamiltonian 아래에 있는 것처럼 행동
```

---

## 2. Floquet 사전열화의 메커니즘

### 2-1. 유효 정적 Hamiltonian

$t < t^*$ 동안, 시스템은 유효 정적 Hamiltonian $D$ 아래에서 진화:

$$e^{-iH_F T} \approx e^{-iDT} \cdot \text{(구동 관련 변환)}$$

$D$는 Magnus 전개의 첫 유한 항으로 근사:

$$D \approx H_F^{(0)} + H_F^{(1)} + \cdots \quad (\omega \to \infty \text{ 극한})$$

### 2-2. 사전열화 상태

$t < t^*$에서 시스템은 $D$의 열적 앙상블로 이완됨:

$$\rho(t) \approx \rho_{D,\beta} = \frac{e^{-\beta D}}{Z_D} \quad \text{for } J/\omega \ll t \ll t^*$$

이것이 "사전열화 상태(prethermal state)".

```
시간 진행:
t = 0     t ~ 1/J           t ~ t*          t → ∞
  │           │                  │              │
초기 상태  → 사전열화 상태  →  가열 시작  →  무한 온도 상태
             (유사 평형)
```

---

## 3. Prethermal DTC 모형

### 3-1. 핵심 아이디어

사전열화 상태가 $D$의 열적 앙상블이라면, $D$에 대칭 깨짐이 있으면 DTC가 가능!

구체적으로:
1. Floquet 연산자를 설계하여 유효 $D$가 강자성(ferromagnetic)을 갖도록
2. 구동 주기 $T$로 전체 스핀을 뒤집는 연산이 포함되도록

### 3-2. 모형 구성

$$U_F = e^{-i\pi\sum_i \sigma_i^x / 2} \cdot e^{-iDT}$$

- 첫 번째 항: 전체 스핀 $\pi$ 뒤집기
- $D$: 강자성 Ising 모형 ($J > 0$)

$$D = -J\sum_i \sigma_i^z \sigma_{i+1}^z + \cdots$$

### 3-3. 메커니즘

1. 낮은 온도에서 $D$의 강자성이 대칭 깨짐: $\langle \sigma^z \rangle \neq 0$
2. 구동의 $\pi$ 뒤집기가 두 번마다 원래 상태로 복귀
3. 결과: $2T$ 주기의 DTC 질서

$$\langle \sigma^z(nT) \rangle = (-1)^n m_0 \quad (t < t^*)$$

### 3-4. 온도 의존성

```
낮은 온도 (β 큼):  강자성 질서 유지 → DTC 존재
                    m₀ ≠ 0

임계 온도:          상전이 (paramagnetic → ferromagnetic)

높은 온도 (β 작음): 상자성 → DTC 없음
                    m₀ = 0
```

---

## 4. MBL-DTC와 Prethermal DTC 비교

| 특성 | MBL-DTC | Prethermal DTC |
|------|---------|----------------|
| 무질서 필요? | 필수 | 불필요 |
| DTC 수명 | 이론적 무한 | $t^* \sim e^{c\omega/J}$ |
| 메커니즘 | l-bit 보호 | 사전열화 고원 |
| 온도 의존 | 거의 없음 | 있음 (임계 온도 존재) |
| 실험 구현 | 무질서 필요, 어려움 | 고주파 구동, 비교적 쉬움 |
| 진정한 열역학적 DTC? | 이론상 가능 | $t^*$ 이후에는 붕괴 |

> **핵심 차이:** MBL-DTC는 영원히 지속되는 진정한 DTC인 반면, Prethermal DTC는 매우 긴 수명을 가지지만 결국 사라진다.

---

## 5. 실험적 실현

### 5-1. Mi et al., Nature 2022 (Google, 다른 해석)

같은 Google 실험을 Prethermal DTC로 해석:
- 고주파 구동: $J \ll \omega$
- 사전열화 시간 $t^*$ 이내에서 강인한 $2T$ 진동
- MBL이 없어도 Prethermal이 설명 가능?

### 5-2. Ye et al., PRX 2021 (이론 예측)

고주파 구동 + 강자성 상호작용만으로 Prethermal DTC 예측.
무질서 없이도 가능함을 이론적으로 증명.

---

## 6. 핵심 통찰 정리

> **사전열화의 힘:** 고주파 구동에서 가열 시간이 지수적으로 길어지므로, 실험적으로 관련 있는 시간 척도에서 무질서 없이도 DTC가 가능하다.

> **MBL vs Prethermal:** MBL-DTC는 원리상 영원하지만 구현이 어렵다. Prethermal DTC는 유한 수명이지만 실험적으로 더 접근하기 쉽다. 이 trade-off가 현실적 실현의 핵심이다.

> **실험 해석 논란:** 많은 DTC 실험들이 MBL 효과인지 Prethermal 효과인지 명확히 구별하기 어렵다. 이것이 현재 분야의 핵심 논쟁이다.

---

## 참고

- 이전 Unit (병렬): `../04_.../MBL_DTC_모델과_실험.md`
- 다음 파일: `BEC_시간결정_학습노트.md`
- 관련 개념: Magnus 전개, 유효 Hamiltonian, 상전이
- 논문 참조: Sec.IV.D, Else et al. PRL 2017
