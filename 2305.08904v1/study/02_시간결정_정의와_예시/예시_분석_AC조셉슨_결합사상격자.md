# 예시 분석: AC 조셉슨 효과와 결합 사상 격자

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.II.A — Examples and Counterexamples
**작성일:** 2026-03-03
**목적:** 논문의 구체적 예시를 통해 DTC 판별 기준을 적용하는 연습

---

## 목차

1. [AC 조셉슨 효과: 왜 DTC가 아닌가](#1-ac-조셉슨-효과-왜-dtc가-아닌가)
2. [결합 사상 격자(Coupled Map Lattice)](#2-결합-사상-격자coupled-map-lattice)
3. [Kicked Ising 모형: DTC의 원형](#3-kicked-ising-모형-dtc의-원형)
4. [예시 비교표](#4-예시-비교표)
5. [핵심 통찰 정리](#5-핵심-통찰-정리)

---

## 1. AC 조셉슨 효과: 왜 DTC가 아닌가

### 1-1. AC 조셉슨 효과 기본

조셉슨 접합에 DC 전압 $V$를 가하면 접합 위상 $\phi$가 일정한 속도로 변한다:

$$\dot{\phi} = \frac{2eV}{\hbar} = \frac{2\pi V}{\Phi_0}$$

이로 인해 AC 전류가 발생:

$$I(t) = I_c \sin(\phi(t)) = I_c \sin\left(\frac{2eV}{\hbar}t + \phi_0\right)$$

주파수: $\omega_{AC} = 2eV/\hbar$

### 1-2. 왜 DTC가 아닌가?

| 판별 기준 | AC 조셉슨 |
|-----------|----------|
| 자발적 대칭 깨짐? | ❌ — 외부 $V$가 주파수를 **강제(force)**함 |
| 강성(rigidity)? | ❌ — $V$ 바꾸면 주파수도 연속적으로 변함 |
| 외부 구동 없이 진동? | ❌ — $V=0$이면 진동 없음 |

> **결론:** AC 조셉슨은 외부에서 강제된 진동이지, 대칭의 자발적 깨짐이 아니다. DTC의 판별 기준인 *자발성*을 충족하지 못한다.

---

## 2. 결합 사상 격자(Coupled Map Lattice)

### 2-1. 모형 정의

각 사이트 $i$에서 이산 시간 사상(map) $f$:

$$x_i(n+1) = f(x_i(n)) + \text{coupling to neighbors}$$

예: 텐트 사상(tent map) 또는 로지스틱 사상의 격자 버전.

### 2-2. 이 모형에서의 진동

카오틱한 단일 사이트 사상도 격자에 결합시키면 공간-시간 패턴이 형성될 수 있다.

```
사이트 i:  ... +0.8, -0.8, +0.8, -0.8 ...  (주기 2 진동)
사이트 i+1: ... -0.8, +0.8, -0.8, +0.8 ...  (반대 위상)
```

### 2-3. DTC 여부 검토

이런 격자의 $2T$ 진동이 DTC인지 판단하려면:
- $N \to \infty$ 극한에서 진동이 살아남는가?
- 파라미터 변화에 강성이 있는가?
- 소음(noise)에 강인한가?

---

## 3. Kicked Ising 모형: DTC의 원형

### 3-1. 모형

1D Ising 스핀 체인을 주기 $T$로 킥(kick)하는 Floquet 모형:

$$U(T) = \exp\left(-i\theta\sum_i \sigma_i^x\right) \cdot \exp\left(-i\sum_i J_{ij}\sigma_i^z\sigma_j^z\right)$$

- 첫 번째 항: 모든 스핀을 $\theta$만큼 회전 (킥)
- 두 번째 항: Ising 상호작용

### 3-2. 완벽한 킥 ($\theta = \pi$)

$$U_0 = \exp\left(-i\frac{\pi}{2}\sum_i \sigma_i^x\right)$$

이것은 모든 스핀을 정확히 뒤집는다: $\sigma_i^z \to -\sigma_i^z$

따라서 초기 상태 $|\uparrow\uparrow\cdots\rangle$에서:

```
n=0: |↑↑↑↑↑⟩
n=1: |↓↓↓↓↓⟩  (킥)
n=2: |↑↑↑↑↑⟩  (킥)
n=3: |↓↓↓↓↓⟩  ...
```

완벽한 $2T$ 진동. 그러나 이것은 너무 단순 — 정확한 $\theta = \pi$ 에서만 작동.

### 3-3. 불완전한 킥 ($\theta = \pi + \epsilon$) + MBL

MBL(다체 국소화)이 있으면 $\epsilon \neq 0$이어도 $2T$ 진동이 유지됨!

```
θ = π:      ▔▁▔▁▔▁  (정확한 flip, 자명)
θ = π+ε:   ▔▁▔▁▔▁  (MBL이 보호, 비자명 DTC!)
θ = π+0.5: ▔▁▔╲     (너무 큰 오차, DTC 붕괴)
```

이것이 MBL-DTC의 핵심이다.

---

## 4. 예시 비교표

| 현상 | 주기 진동? | 자발적? | 강성? | DTC? |
|------|-----------|---------|-------|------|
| AC 조셉슨 | ✓ | ❌ (강제) | ❌ | ❌ |
| 단순 공진 | ✓ | ❌ | ❌ | ❌ |
| 결합 사상 격자 | ✓ | 조건부 | 조건부 | 조건부 |
| Kicked Ising + MBL | ✓ | ✓ | ✓ | ✓ |

---

## 5. 핵심 통찰 정리

> **자발성의 중요성:** 외부에서 $2T$ 주기 신호를 넣어 $2T$ 응답을 얻는 것은 DTC가 아니다. DTC는 구동이 $T$ 주기인데 시스템이 *스스로* $2T$를 선택하는 것이다.

> **강성의 중요성:** 파라미터를 변화시켜도 $2T$ 진동이 "잠겨(locked)" 있어야 한다. 이것이 DTC를 단순 공진과 구별한다.

> **예시의 교훈:** 시간 주기 진동 자체는 흔하지만, DTC의 엄밀한 기준(자발성 + 강성 + 열역학적 안정성)을 모두 만족하는 경우는 특별한 물리 메커니즘이 필요하다.

---

## 참고

- 이전 파일: `formal_definition_학습노트.md`
- 다음 Unit: `../03_고전_Floquet_.../Floquet_Hamiltonian_기초.md`
- 관련 개념: Kicked rotor, Floquet 위상, Ising 모형
- 논문 참조: Sec.II.A, Fig.2
