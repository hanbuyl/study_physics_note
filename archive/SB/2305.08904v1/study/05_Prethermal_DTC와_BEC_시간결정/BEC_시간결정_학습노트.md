# 보즈-아인슈타인 응축(BEC) 시간결정

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.IV.E — BEC Time Crystal
**작성일:** 2026-03-03
**목적:** 무질서 없이 BEC의 거시적 응축이 DTC를 어떻게 안정화하는지 이해

---

## 목차

1. [BEC의 기본: 거시적 응축](#1-bec의-기본-거시적-응축)
2. [BEC에서의 에르고딕성 깨짐](#2-bec에서의-에르고딕성-깨짐)
3. [BEC 시간결정 모형](#3-bec-시간결정-모형)
4. [실험: 초냉각 원자 실험](#4-실험-초냉각-원자-실험)
5. [BEC DTC vs 다른 DTC 비교](#5-bec-dtc-vs-다른-dtc-비교)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. BEC의 기본: 거시적 응축

### 1-1. 보즈-아인슈타인 응축

보존 입자들이 극저온에서 바닥 상태로 거시적으로 응축:

$$N_0 = N\left[1 - \left(\frac{T}{T_c}\right)^3\right]$$

$T < T_c$에서 $N_0 \sim N$ 개의 입자가 **동일한 단입자 상태**를 점유.

### 1-2. 거시적 파동 함수

BEC는 거시적 파동 함수(order parameter)로 기술:

$$\Psi(\mathbf{r}, t) = \sqrt{n_0}\,e^{i\phi(\mathbf{r},t)}$$

여기서 $n_0$는 응축 밀도, $\phi$는 위상.

| 계 | 특성 |
|----|------|
| 일반 보손 기체 | 각 입자가 다른 상태 → 복잡한 다체 기술 필요 |
| BEC | 모든 입자가 동일 상태 → 단일 파동 함수로 기술 |

---

## 2. BEC에서의 에르고딕성 깨짐

### 2-1. 왜 BEC가 비에르고딕인가

에르고딕 시스템: 충분히 오래 기다리면 모든 미시 상태를 방문.

BEC: 거시적으로 많은 입자($N \gg 1$)가 응축 상태를 점유 중.
- 응축 상태에서 다른 상태로 이탈하려면: $N$개 입자가 동시에 변화
- 이 확률은 $\sim e^{-N}$으로 지수적으로 억제

$$\text{에르고딕성 시간} \sim e^N \xrightarrow{N\to\infty} \infty$$

따라서 열역학적 극한에서 BEC는 진정으로 비에르고딕!

### 2-2. MBL과의 차이

| | MBL | BEC |
|-|-----|-----|
| 메커니즘 | 강한 무질서 → l-bit 보존량 | 거시적 응축 → 집단 운동 |
| 무질서 필요? | 필수 | 불필요 |
| 차원 | 1D에서 확립, 2D 논쟁 | 3D에서도 가능 |
| 온도 의존 | 거의 없음 | $T < T_c$ 필요 |

---

## 3. BEC 시간결정 모형

### 3-1. 두 성분 BEC (Two-Component BEC)

두 내부 상태 $|1\rangle, |2\rangle$를 가진 원자의 BEC:

$$\hat{H} = \int d^3r \left[\sum_{\alpha=1,2} \hat{\Psi}_\alpha^\dagger \left(-\frac{\hbar^2\nabla^2}{2m}\right)\hat{\Psi}_\alpha + g_{12}\hat{\Psi}_1^\dagger\hat{\Psi}_2^\dagger\hat{\Psi}_2\hat{\Psi}_1\right]$$

### 3-2. Gross-Pitaevskii 방정식 (평균장)

BEC의 거시적 파동 함수 $\psi_\alpha$는 GPE를 만족:

$$i\hbar\partial_t\psi_\alpha = \left(-\frac{\hbar^2\nabla^2}{2m} + V_{ext} + g_{\alpha\alpha}|\psi_\alpha|^2 + g_{12}|\psi_{3-\alpha}|^2\right)\psi_\alpha$$

### 3-3. Floquet 구동

주기 $T$로 두 성분 사이의 Rabi 결합을 변조:

$$H_{drive}(t) = \Omega(t)\sum_i (\hat{\sigma}_i^+ + \hat{\sigma}_i^-)$$

$\Omega(t) = \Omega_0$ for $0 < t < T/2$, $= -\Omega_0$ for $T/2 < t < T$ (정사각파).

### 3-4. DTC 질서

적절한 조건에서 BEC의 두 성분이 $2T$ 주기로 교대:

$$n_1(nT) = \begin{cases} N & n \text{ 짝수} \\ 0 & n \text{ 홀수} \end{cases}$$

---

## 4. 실험: 초냉각 원자 실험

### 4-1. Träger et al., PRX 2021

- 시스템: $^{87}$Rb BEC
- 광학 격자에 올려진 두 성분 BEC
- Rabi 구동으로 Floquet 시스템 구현

**결과:**
- 열역학적 극한에 가까운 조건 ($N \sim 10^4$)
- 넓은 구동 파라미터 범위에서 안정적 $2T$ 진동
- 시스템 크기가 클수록 DTC 강도 증가 → 진정한 자발 대칭 깨짐 징후

### 4-2. 실험의 강점

| 특성 | 설명 |
|------|------|
| 열역학적 극한 | $N \sim 10^4$ — 다른 실험보다 훨씬 큰 입자 수 |
| 무질서 없음 | 순수한 BEC 메커니즘 |
| 정밀 제어 | 초냉각 원자 기술의 성숙도 |
| 직접 이미징 | 밀도 분포 공간 분해 측정 가능 |

---

## 5. BEC DTC vs 다른 DTC 비교

| | MBL-DTC | Prethermal-DTC | BEC-DTC |
|-|---------|----------------|---------|
| 무질서 | 필수 | 불필요 | 불필요 |
| 상호작용 | 필요 | 필요 | 필요 |
| 수명 | 이론상 무한 | $\sim e^{c\omega/J}$ | 이론상 무한 |
| 차원 | 1D 확립 | 모든 차원 | 3D 가능 |
| 보호 메커니즘 | l-bit | 사전열화 고원 | 거시적 응축 |
| 실험 입자 수 | ~20-50 큐비트 | ~50 큐비트 | ~10,000 원자 |

> **BEC DTC의 강점:** 가장 많은 입자 수로 구현 가능하며, 무질서 없이도 진정한 열역학적 극한에 가까운 DTC를 실현할 수 있다.

---

## 6. 핵심 통찰 정리

> **BEC의 보호 메커니즘:** 거시적으로 많은 입자가 응축 상태를 점유하므로 이탈 확률이 $e^{-N}$으로 억제된다. 이것이 에르고딕성을 깨뜨리고 DTC를 안정화한다.

> **MBL 대비 BEC의 장점:** BEC는 무질서가 필요 없고, 3D에서도 작동하며, 실험적으로 훨씬 많은 입자 수로 구현 가능하다. 이것이 열역학적 극한에 더 가까운 DTC 증거를 제공한다.

> **DTC 안정화의 보편성:** MBL, 사전열화, BEC는 모두 다른 물리 메커니즘이지만, 공통적으로 에르고딕성을 억제하여 초기 정보 보존 → DTC 안정화라는 동일한 논리를 따른다.

---

## 참고

- 이전 파일: `Floquet_prethermalization_학습노트.md`
- 다음 Unit: `../06_열린계.../open_systems_기초_학습노트.md`
- 관련 개념: GPE, 평균장 이론, 원자-원자 산란 길이
- 논문 참조: Sec.IV.E, Fig.7
