# 다체 국소화(MBL, Many-Body Localization) 기초

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.IV.A — MBL Background
**작성일:** 2026-03-03
**목적:** MBL이 무엇인지, 어떻게 에르고딕성을 깨뜨리는지 이해하기 위한 배경 지식

---

## 목차

1. [Anderson 국소화: 단일 입자](#1-anderson-국소화-단일-입자)
2. [다체 국소화(MBL)로의 확장](#2-다체-국소화mbl로의-확장)
3. [MBL의 특성: l-bit 구조](#3-mbl의-특성-l-bit-구조)
4. [MBL이 ETH를 위반하는 방식](#4-mbl이-eth를-위반하는-방식)
5. [MBL의 한계와 논쟁](#5-mbl의-한계와-논쟁)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. Anderson 국소화: 단일 입자

### 1-1. 기본 개념

무질서한(disordered) 포텐셜에서 입자의 파동 함수가 공간적으로 지수 감소:

$$|\psi(r)| \sim e^{-|r - r_0|/\xi}$$

여기서 $\xi$는 국소화 길이(localization length).

```
무질서 없음:   파동함수가 공간 전체에 퍼짐 (확산)
              ─────────────────────────── →

무질서 있음:   파동함수가 한 곳에 갇힘 (국소화)
                   ╭───╮
              ─────┤   ├───── →  지수적으로 감소
```

### 1-2. Anderson 국소화의 물리

무질서 포텐셜이 인접 에너지 준위들을 다른 공간 위치에 배치 → 준위들이 공간적으로 다른 곳에 있어 직접 결합이 어려움 → 국소화.

---

## 2. 다체 국소화(MBL)로의 확장

### 2-1. 질문: 상호작용이 국소화를 파괴하는가?

단일 입자 국소화는 잘 알려져 있다. 그런데 **입자 간 상호작용**이 있으면?

**직관:** 상호작용 → 한 입자가 다른 국소화된 입자에 "올라타서" 이동 → 국소화 파괴?

**MBL 대답:** 무질서가 충분히 강하면, 상호작용이 있어도 국소화가 유지된다!

### 2-2. 1D Heisenberg 스핀 체인 예시

$$H = \sum_i J \mathbf{S}_i \cdot \mathbf{S}_{i+1} + \sum_i h_i S_i^z$$

여기서 $h_i \in [-W, W]$ 는 무작위 자기장.

- $W \ll J$: 에르고딕 상(ETH 만족, 열화)
- $W \gg J$: MBL 상(ETH 위반, 국소화)

```
에르고딕 상  ←────────┤─────────→  MBL 상
            W/J 작음  임계점  W/J 큼
                   (W/J)_c
```

---

## 3. MBL의 특성: l-bit 구조

MBL 상의 가장 중요한 특성: **국소 보존량(local integrals of motion, l-bits)**의 존재.

### 3-1. l-bit이란?

MBL 상에서 유효 Hamiltonian을 다음과 같이 대각화할 수 있다:

$$H_{MBL} = \sum_i \tilde{h}_i \tau_i^z + \sum_{ij} J_{ij} \tau_i^z \tau_j^z + \sum_{ijk} J_{ijk} \tau_i^z \tau_j^z \tau_k^z + \cdots$$

여기서 $\tau_i^z$ 는 l-bit — 실제 입자 스핀 $\sigma_i^z$의 국소적 변환.

**l-bit의 성질:**
- 모든 $[\tau_i^z, H] = 0$ → 모두 보존량!
- $\tau_i^z$는 위치 $i$ 근방에 지수적으로 국소화됨
- 개수: $N$개 (시스템 크기와 동일)

### 3-2. 물리적 의미

$$N \text{개의 보존량} \Rightarrow \text{적분 가능(integrable)} \Rightarrow \text{비에르고딕}$$

```
일반 카오스 시스템:  보존량 적음 (에너지만) → 에르고딕
MBL 시스템:          보존량 N개 (l-bits) → 완전히 비에르고딕
```

---

## 4. MBL이 ETH를 위반하는 방식

### 4-1. 엔탈피 얽힘(Entanglement) 증가 방식

**에르고딕 계:** 엔탈피 얽힘이 부피 법칙(volume law)으로 증가
$$S \propto V \quad (= L^d \text{ in } d\text{ dimensions})$$

**MBL 계:** 엔탈피 얽힘이 면적 법칙(area law)에 포화
$$S \propto A \quad (= L^{d-1})$$

단, 시간에 따라 *로그적*으로 느리게 증가:
$$S(t) \sim \log(t)$$

### 4-2. 초기 조건의 기억

MBL 계에서는 초기 조건의 정보가 영원히 국소 관측량에 보존됨:

$$\langle \sigma_i^z(t) \rangle \xrightarrow{t\to\infty} \text{초기 조건에 의존하는 값} \neq 0$$

에르고딕 계라면 이 값은 0으로 감쇠.

---

## 5. MBL의 한계와 논쟁

### 5-1. 실험적 한계

- MBL은 이론적으로 1D 시스템에서 잘 확립
- 2D 이상: MBL이 불안정하다는 주장 (rare bath regions)
- 실험에서는 유한 크기 효과로 진정한 MBL인지 확인 어려움

### 5-2. 최근 논쟁

- De Roeck & Huveneers (2017): 2D에서 희귀 열욕(rare thermal inclusions)이 결국 MBL을 파괴
- 그러나 1D에서는 여전히 강력한 증거

### 5-3. 실험 조건

```
실험 시스템:
- 차가운 원자 (cold atoms)
- 이온 트랩 (ion trap)
- 초전도 큐비트 (superconducting qubits)

유한한 실험 시간 안에서는 MBL 효과를 관측 가능
(하지만 진정한 열역학적 극한은 아님)
```

---

## 6. 핵심 통찰 정리

> **MBL = 많은 보존량:** MBL 상에서는 $N$개의 국소 보존량(l-bits)이 존재하여 시스템이 완전히 비에르고딕이 된다. 초기 조건 정보가 영원히 보존된다.

> **MBL + Floquet = DTC 가능:** MBL이 Floquet 가열을 막아 주므로, MBL 시스템에 주기 구동을 가하면 진정한 DTC가 가능해진다.

> **실험적 주의사항:** 실제 실험에서는 유한 크기, 유한 시간 효과로 인해 진정한 MBL-DTC와 단순한 긴 수명 진동을 구별하기 어렵다. 이것이 MBL-DTC 실험 해석의 핵심 논쟁점이다.

---

## 참고

- 이전 Unit: `../03_.../에르고딕성과_시간결정의_적.md`
- 다음 파일: `MBL_DTC_모델과_실험.md`
- 관련 개념: Anderson 국소화, 엔탈피 스펙트럼, 희귀 사건(rare events)
- 논문 참조: Sec.IV.A, Nandkishore & Huse review (2015)
