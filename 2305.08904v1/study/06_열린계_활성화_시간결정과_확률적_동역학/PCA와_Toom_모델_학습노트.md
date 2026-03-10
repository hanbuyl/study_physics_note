# 확률적 셀룰러 오토마타(PCA)와 Toom 모형: 절대 안정 시간결정

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.V.C-F — Absolutely Stable Time Crystals
**작성일:** 2026-03-03
**목적:** 소산계에서 진정으로 영구적인(absolutely stable) DTC를 구현하는 PCA 모형 이해

---

## 목차

1. [절대 안정 시간결정이란](#1-절대-안정-시간결정이란)
2. [확률적 셀룰러 오토마타(PCA)](#2-확률적-셀룰러-오토마타pca)
3. [Toom 규칙: 2D 안정 자성체](#3-toom-규칙-2d-안정-자성체)
4. [Toom 규칙 + Floquet = 절대 안정 DTC](#4-toom-규칙--floquet--절대-안정-dtc)
5. [양자 버전](#5-양자-버전)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. 절대 안정 시간결정이란

### 1-1. 활성화 TC의 한계

Unit 6의 활성화 TC는 유한 수명:

$$\tau_{DTC} \sim e^{\Delta V/k_BT} \xrightarrow{T\to 0} \infty$$

하지만 어떤 유한 온도에서도 결국 붕괴.

### 1-2. "절대 안정"의 정의

**절대 안정 DTC:** 어떤 잡음(noise) 강도에서도 — 심지어 유한한 잡음이 있어도 — 진정으로 무한한 수명.

$$\tau_{DTC} = \infty \quad \text{for ANY finite noise strength}$$

이것은 고전적 소산계에서 가능한가? **YES, if the right mechanism is present!**

---

## 2. 확률적 셀룰러 오토마타(PCA)

### 2-1. 셀룰러 오토마타(CA) 기본

격자의 각 사이트가 이산 상태를 가지며, 동기적으로 이웃 상태에 따라 업데이트:

```
1D CA 예시 (규칙 110):
이전 상태: 1 1 0 1 0 0 1 1
다음 상태: 0 1 0 1 1 0 1 0  (국소 규칙 적용)
```

### 2-2. 확률적 CA (PCA)

업데이트가 확률적으로 일어남:

$$P(\sigma_i^{t+1} = 1 | \{\sigma_j^t\}_{j \in \mathcal{N}(i)}) = f(\{\sigma_j^t\})$$

여기서 $\mathcal{N}(i)$는 $i$의 이웃 집합.

### 2-3. Ising PCA

가장 단순한 PCA: 다수결(majority rule)에 따라 확률적 업데이트:

$$P(\sigma_i^{t+1} = +1) = \frac{1 + \tanh(\beta \sum_{j \in \mathcal{N}(i)} \sigma_j^t)}{2}$$

- $\beta$ 큼 (낮은 온도): 거의 결정론적, 다수결 규칙
- $\beta$ 작음 (높은 온도): 거의 무작위

---

## 3. Toom 규칙: 2D 안정 자성체

### 3-1. Toom 규칙 정의 (1980)

2D 격자에서 비대칭 다수결 규칙:

$$\sigma_i^{new} = \text{majority}(\sigma_{i}, \sigma_{i+\hat{x}}, \sigma_{i+\hat{y}})$$

즉, 사이트 $i$, 오른쪽 이웃, 위 이웃 — 세 사이트의 다수결.

```
2D 격자:
  ↑
  │  ○ ← 이 세 사이트의 다수결로 ×를 업데이트
  │  ×──○
  └──────→
```

### 3-2. Toom 정리

**Toom 정리:** 2D Toom 규칙 PCA는 임의의 유한 잡음 강도에서도 장시간 강자성 질서를 유지한다.

$$\langle \sigma_i \rangle \neq 0 \quad \text{for any finite noise strength}$$

이것은 1D Ising 모형(잡음에 불안정)과 대조적이다.

### 3-3. 왜 Toom이 안정한가?

핵심: **비대칭 정보 흐름**

Toom 규칙은 정보를 $(+\hat{x}, +\hat{y})$ 방향으로만 전파. 즉, 잡음에 의한 국소 "버블"이 성장하지 않고 이동(drift)하다가 사라진다.

```
버블 성장 (1D):                버블 드리프트 (2D Toom):
  ++++●────++         →          ++●────++  → (drift)
      버블이 자라남                    버블이 이동 후 소멸
```

---

## 4. Toom 규칙 + Floquet = 절대 안정 DTC

### 4-1. 구성 방법

1단계: Toom 규칙 PCA로 안정한 강자성 질서 구현
2단계: 주기 $T$마다 전체 스핀 뒤집기 적용

$$\text{한 주기} = \underbrace{\text{Toom 업데이트}}_{\text{질서 복원}} + \underbrace{\text{전체 flip}}_{\text{대칭 깨짐}}$$

### 4-2. 동작 원리

```
시간 0:   모든 스핀이 +1 (Toom이 유지)
시간 T:   전체 flip → 모든 스핀 -1
시간 2T:  Toom이 -1 상태를 유지 → 전체 flip → +1
시간 3T:  ...
```

결과: $+1/-1$ 상태가 $2T$ 주기로 교대!

### 4-3. 절대 안정성

잡음이 일부 스핀을 뒤집어도 Toom 메커니즘이 즉시 복원:
- 1D: 복원 불가 (잡음 버블 성장)
- 2D Toom: 복원 가능 (버블 드리프트 후 소멸)

따라서 2D Toom DTC는 **어떤 유한 잡음에도 절대 안정**.

---

## 5. 양자 버전

### 5-1. 양자 PCA

고전 PCA의 양자 버전: 각 사이트가 큐비트, 업데이트가 양자 채널.

Lindblad 방정식으로 기술:

$$\mathcal{L}\rho = \sum_k \gamma_k \left(L_k\rho L_k^\dagger - \frac{1}{2}\{L_k^\dagger L_k, \rho\}\right)$$

### 5-2. 양자 Toom DTC

고전 Toom 규칙의 양자 아날로그가 존재하며, 코히어런트(coherent) 구동 + 소산 채널의 조합으로 구현 가능.

**실험 가능성:**
- 초전도 큐비트 격자
- 이온 트랩 2D 배열
- Rydberg 원자 배열

### 5-3. 현황

양자 Toom DTC는 아직 실험적으로 실현되지 않았지만, 이론적으로는 명확히 예측되어 있다.

---

## 6. 핵심 통찰 정리

> **PCA의 강력함:** 소산계에서도 올바른 업데이트 규칙(Toom)을 사용하면 임의의 유한 잡음에서도 안정한 DTC를 구현할 수 있다. 이것은 닫힌계 DTC보다 어떤 면에서는 더 강력하다.

> **Toom 규칙의 비대칭성:** 비대칭 다수결이 정보를 한 방향으로 드리프트시켜 잡음 버블이 자라지 않고 사라지게 한다. 이 비대칭성이 절대 안정성의 핵심이다.

> **열린계 DTC의 결론:** Unit 6 전체를 통해, 열린계(소산 + 잡음)에서 DTC는 활성화 TC(긴 수명)와 절대 안정 TC(무한 수명) 두 형태로 가능함을 보았다. 이것은 닫힌계에서 MBL/Prethermal이 필요했던 것에 대응하는 열린계의 해결책이다.

---

## 참고

- 이전 파일: `activated_time_crystal_학습노트.md`
- 다음 Unit: `../07_전망.../새로운_시간결정_방향.md`
- 관련 개념: 에러 정정(quantum error correction), 위상 자동화(topological automaton)
- 논문 참조: Sec.V.C-F, Toom (1980) 원본 논문
