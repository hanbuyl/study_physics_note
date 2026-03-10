# 열린 양자/고전계 기초: Langevin 방정식과 마스터 방정식

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.V — Open Systems: DTC Background
**작성일:** 2026-03-03
**목적:** 소산(dissipation)과 잡음(noise)이 있는 열린계 기술의 기초 이해

---

## 목차

1. [닫힌계 vs 열린계](#1-닫힌계-vs-열린계)
2. [고전 열린계: Langevin 방정식](#2-고전-열린계-langevin-방정식)
3. [양자 열린계: Lindblad 마스터 방정식](#3-양자-열린계-lindblad-마스터-방정식)
4. [소산이 DTC에 미치는 영향](#4-소산이-dtc에-미치는-영향)
5. [비평형 정상 상태(NESS)](#5-비평형-정상-상태ness)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. 닫힌계 vs 열린계

| 특성 | 닫힌계 | 열린계 |
|------|--------|--------|
| 환경 결합 | 없음 | 있음 |
| 에너지 | 보존 | 환경과 교환 |
| Floquet 가열 | 결국 무한 온도 | 소산이 상쇄 가능 |
| 기술 방법 | Schrödinger 방정식 | 마스터 방정식 |
| DTC 가능성 | MBL/Prethermal 필요 | 소산 자체로 안정화 가능! |

> **역설:** 소산(dissipation)은 직관적으로 DTC를 파괴할 것 같지만, 실제로는 DTC를 **안정화**할 수 있다!

---

## 2. 고전 열린계: Langevin 방정식

### 2-1. 기본 방정식

질량 $m$, 위치 $x(t)$의 브라운 입자:

$$m\ddot{x} = F(x) - \gamma\dot{x} + \xi(t)$$

항목:
- $F(x) = -\partial V/\partial x$: 보존력
- $-\gamma\dot{x}$: 마찰(소산)
- $\xi(t)$: 랜덤 힘(백색 잡음)

**요동-소산 정리:**

$$\langle\xi(t)\xi(t')\rangle = 2\gamma k_B T \,\delta(t-t')$$

소산($\gamma$)과 잡음($\xi$)은 항상 쌍으로 온다.

### 2-2. 정상 상태

충분히 오래 기다리면 열적 평형:

$$P_{eq}(x) \propto e^{-V(x)/k_BT}$$

소산이 있으면 시스템이 에너지를 잃고, 잡음이 에너지를 공급하여 균형을 이룬다.

---

## 3. 양자 열린계: Lindblad 마스터 방정식

### 3-1. 밀도 행렬

열린 양자계의 상태는 밀도 행렬 $\rho$로 기술:

$$\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$$

순수 상태: $\rho^2 = \rho$, $\text{Tr}(\rho^2) = 1$
혼합 상태: $\rho^2 \neq \rho$, $\text{Tr}(\rho^2) < 1$

### 3-2. Lindblad 방정식

$$\frac{d\rho}{dt} = -\frac{i}{\hbar}[H, \rho] + \sum_k \gamma_k \left(L_k\rho L_k^\dagger - \frac{1}{2}L_k^\dagger L_k\rho - \frac{1}{2}\rho L_k^\dagger L_k\right)$$

- 첫 번째 항: 유니터리 진화
- 두 번째 항: 소산, $L_k$ = 점프 연산자(jump operator)

**점프 연산자 예시:**
- $L = \sigma^-$: 자발 방출 (excited → ground)
- $L = \sigma^z$: 위상 소멸(dephasing)
- $L = \sigma^+$: 펌핑(ground → excited)

### 3-3. 정상 상태

$d\rho/dt = 0$인 정상 상태 $\rho_{ss}$:

$$\mathcal{L}\rho_{ss} = 0$$

유일한 정상 상태가 있으면 모든 초기 상태가 그것으로 수렴.

---

## 4. 소산이 DTC에 미치는 영향

### 4-1. 두 가지 효과

**효과 1: DTC 파괴**

소산은 코히어런스를 잃게 하여 $2T$ 진동의 진폭을 감쇠시킨다:

$$\langle O(nT)\rangle \sim (-1)^n e^{-n\Gamma} m_0$$

충분히 큰 소산률 $\Gamma$이면 신호가 빠르게 감쇠.

**효과 2: DTC 안정화 (역설적)**

소산이 *올바른* 정상 상태로 시스템을 고정할 수 있다:

```
구동 + 소산:  시스템을 특정 상태로 "펌핑"
             Floquet 가열을 소산이 상쇄
             → 영구적인 비평형 정상 상태로 수렴
             → 그 정상 상태가 DTC 질서를 가질 수 있음
```

### 4-2. 경쟁 조건

소산이 DTC를 안정화할 조건:
1. 소산이 Floquet 가열보다 빠름: $\Gamma > \Gamma_{heat}$
2. 소산의 고정점(attractor)이 DTC 질서를 가짐
3. 잡음이 너무 세지 않음

---

## 5. 비평형 정상 상태(NESS)

### 5-1. 개념

구동(에너지 주입) + 소산(에너지 방출) → 비평형이지만 시간에 따라 변하지 않는 상태.

```
에너지 흐름:
구동 → [시스템] → 환경(소산)
         ↑↓
      비평형 정상 상태
```

열적 평형과의 차이:
- 열적 평형: 구동 없음, 세부 균형(detailed balance) 만족
- NESS: 구동 있음, 세부 균형 위반, 비가역적 에너지 흐름

### 5-2. NESS와 DTC

NESS가 $2T$ 주기성을 가지면 DTC:

$$\rho_{NESS}(t + 2T) = \rho_{NESS}(t)$$

이것은 소산계에서의 DTC 정의 — 일반적으로 열린계 DTC는 진동하는 비평형 정상 상태를 찾는 문제다.

---

## 6. 핵심 통찰 정리

> **소산의 역설:** 소산은 DTC를 파괴하는 것처럼 보이지만, 실제로는 Floquet 가열을 억제하고 시스템을 DTC 질서를 가진 비평형 정상 상태로 유도할 수 있다.

> **Lindblad vs Schrödinger:** 닫힌계(Schrödinger)와 달리, 열린계(Lindblad)에서는 고유 상태가 아닌 고유 채널(Lindblad operator의 고유값)이 동역학을 지배한다.

> **NESS의 역할:** 열린계 DTC는 진동하는 비평형 정상 상태로 귀결된다. 이것이 닫힌계 DTC와의 핵심 개념적 차이다.

---

## 참고

- 이전 Unit: `../05_.../BEC_시간결정_학습노트.md`
- 다음 파일: `activated_time_crystal_학습노트.md`
- 관련 개념: Fokker-Planck 방정식, 양자 궤적(quantum trajectory), 비가역 열역학
- 논문 참조: Sec.V 서두, Lindblad 마스터 방정식 배경
