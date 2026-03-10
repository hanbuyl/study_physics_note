# 시간 병진 대칭과 이산 시간결정 개론

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.I — Introduction
**작성일:** 2026-03-03
**목적:** 논문 도입부의 핵심 논의 — 시간 대칭 깨짐이 왜 특별하고 어려운가

---

## 목차

1. [시간 병진 대칭(Time Translation Symmetry)](#1-시간-병진-대칭time-translation-symmetry)
2. [연속 시간결정은 왜 불가능한가](#2-연속-시간결정은-왜-불가능한가)
3. [이산 시간결정(Discrete Time Crystal)의 아이디어](#3-이산-시간결정discrete-time-crystal의-아이디어)
4. [Floquet 시스템: 주기적 구동](#4-floquet-시스템-주기적-구동)
5. [DTC의 정성적 특성](#5-dtc의-정성적-특성)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. 시간 병진 대칭(Time Translation Symmetry)

시간 독립 Hamiltonian은 **연속 시간 병진 대칭**을 가진다:

$$H(t) = H \quad \Rightarrow \quad t \to t + \tau \text{ 에 대해 불변}$$

이것은 에너지 보존 법칙의 근원이다 (Noether 정리).

| 대칭 | 보존량 |
|------|--------|
| 공간 병진 | 선운동량 $\mathbf{p}$ |
| 회전 | 각운동량 $\mathbf{L}$ |
| **시간 병진** | **에너지 $E$** |

---

## 2. 연속 시간결정은 왜 불가능한가

> **Watanabe-Oshikawa 정리 (2015):** 평형 상태(equilibrium)에서는 연속 시간 병진 대칭을 깨는 상전이가 존재하지 않는다.

**직관적 이유:**

시간 독립 Hamiltonian의 에너지 고유 상태는 시간에 따라 오직 위상 인자만 변한다:

$$|\psi(t)\rangle = e^{-iEt/\hbar} |E\rangle$$

이것은 관측 가능한 물리량(밀도, 상관함수 등)에서 시간 의존성을 만들지 **않는다**:

$$\langle O \rangle(t) = \langle E | e^{iEt/\hbar} \hat{O} e^{-iEt/\hbar} | E \rangle = \langle E | \hat{O} | E \rangle = \text{const}$$

따라서 평형에서 관측 가능한 양의 진정한 시간 결정 질서는 없다.

---

## 3. 이산 시간결정(Discrete Time Crystal)의 아이디어

**핵심 우회:** 평형에서의 시간 독립 Hamiltonian이 아니라, **주기적으로 구동되는(periodically driven) Floquet 시스템**을 사용한다.

```
연속 시간 대칭 (H 시간 독립):  불가능
         ↓
이산 시간 대칭 (H 주기 T):     가능!
```

주기 $T$로 구동되는 시스템은 이산 시간 병진 대칭을 가진다:

$$H(t+T) = H(t)$$

이 대칭을 **2배 주기로** 깨뜨리는 것이 이산 시간결정(DTC)이다:

$$\text{구동 주기} = T \quad \Longrightarrow \quad \text{응답 주기} = 2T$$

---

## 4. Floquet 시스템: 주기적 구동

주기 $T$로 구동되는 시스템의 진화 연산자:

$$U(T) = \mathcal{T}\exp\left(-\frac{i}{\hbar}\int_0^T H(t)\,dt\right)$$

이것을 **Floquet 연산자**라 부른다. 한 주기 후의 상태:

$$|\psi((n+1)T)\rangle = U(T) |\psi(nT)\rangle$$

DTC에서는 어떤 초기 상태 $|\psi_0\rangle$에 대해:

$$|\psi(nT)\rangle = \begin{cases} |\psi_A\rangle & n \text{ 짝수} \\ |\psi_B\rangle & n \text{ 홀수} \end{cases}$$

즉, 시스템이 $2T$ 주기로 진동한다.

```
구동 신호:   ▔▁▔▁▔▁▔▁  (주기 T)
시스템 응답: ▔▔▁▁▔▔▁▁  (주기 2T)  ← 대칭 깨짐!
```

---

## 5. DTC의 정성적 특성

DTC가 되려면 단순한 공진이나 일시적 진동과 달리:

| 특성 | 설명 |
|------|------|
| **강성(Rigidity)** | 구동 파라미터를 조금 바꿔도 $2T$ 진동이 유지됨 |
| **자발성(Spontaneity)** | 외부에서 $2T$ 신호를 넣지 않아도 스스로 $2T$ 진동 |
| **열역학적 극한** | 무한한 시스템 크기 $N \to \infty$ 에서도 유지 |
| **안정성** | 단순 과도 응답(transient)이 아닌 오래 지속되는 질서 |

> **핵심:** 이것이 일반적인 공진(resonance)과 구별되는 점이다. 공진은 파라미터에 정확히 맞아야 하지만, DTC는 파라미터 범위에 걸쳐 강성을 가진다.

---

## 6. 핵심 통찰 정리

> **왜 시간 대칭 깨짐이 어려운가:** 평형계에서 에너지 고유 상태는 관측 가능량에서 시간 의존성을 만들지 않는다. Watanabe-Oshikawa 정리는 이 불가능성을 증명한다.

> **우회 전략:** 이산 시간 대칭만을 가진 Floquet 시스템($H(t+T)=H(t)$)을 쓰면, 그 이산 대칭을 또다시 $2T$ 주기로 깨뜨리는 DTC가 원리상 가능해진다.

> **논문의 핵심 질문:** 어떤 물리적 메커니즘이 이 $2T$ 진동을 장시간 안정하게 유지시키는가? — 이것이 이 논문 전체의 주제다.

---

## 참고

- 이전 파일: `symmetry_breaking_기초.md`
- 다음 Unit: `02_시간결정_정의와_예시/formal_definition_학습노트.md`
- 관련 개념: Floquet 이론, 에르고딕성, Noether 정리
- 논문 참조: Sec.I, Eq.(1)-(2), Watanabe & Oshikawa, PRL 114, 251603 (2015)
