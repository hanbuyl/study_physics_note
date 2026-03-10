# 자발적 대칭 깨짐(Spontaneous Symmetry Breaking) 기초

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.I (Introduction) — 배경 지식
**작성일:** 2026-03-03
**목적:** 이산 시간결정을 이해하기 위한 대칭 깨짐 개념 정리

---

## 목차

1. [대칭(Symmetry)이란 무엇인가](#1-대칭symmetry이란-무엇인가)
2. [자발적 대칭 깨짐의 정의](#2-자발적-대칭-깨짐의-정의)
3. [공간 대칭 깨짐의 예시: 결정](#3-공간-대칭-깨짐의-예시-결정)
4. [질서 매개변수(Order Parameter)](#4-질서-매개변수order-parameter)
5. [열역학적 극한과 대칭 깨짐](#5-열역학적-극한과-대칭-깨짐)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. 대칭(Symmetry)이란 무엇인가

물리에서 대칭이란 **어떤 변환을 가해도 시스템의 방정식(Hamiltonian)이 변하지 않는 성질**을 말한다.

| 대칭 종류 | 변환 | 예시 |
|-----------|------|------|
| 공간 병진 대칭 | $\mathbf{r} \to \mathbf{r} + \mathbf{a}$ | 균일한 자유 공간 |
| 회전 대칭 | $\mathbf{r} \to R\mathbf{r}$ | 구형 원자 |
| 시간 병진 대칭 | $t \to t + \tau$ | 시간 독립 Hamiltonian |
| $\mathbb{Z}_2$ 대칭 | $\phi \to -\phi$ | Ising 모형 |

수학적으로 표현하면: 변환 $G$에 대해

$$[H, G] = 0$$

이면 $H$는 $G$ 대칭을 가진다.

---

## 2. 자발적 대칭 깨짐의 정의

> **핵심 질문:** Hamiltonian은 대칭을 가지는데, 왜 바닥 상태(ground state)는 대칭이 없을 수 있는가?

자발적 대칭 깨짐(SSB, Spontaneous Symmetry Breaking)은 다음을 말한다:

- Hamiltonian $H$는 대칭 $G$를 가진다 ($[H, G] = 0$)
- 그러나 시스템의 **바닥 상태** $|\psi_0\rangle$는 $G$ 대칭을 갖지 않는다

$$G|\psi_0\rangle \neq |\psi_0\rangle$$

이것은 Hamiltonian의 대칭이 *자발적으로(spontaneously)* 깨진 것이다.

```
대칭 Hamiltonian
       │
       │  여러 가능한 바닥 상태 중
       │  시스템이 하나를 "선택"
       ↓
비대칭 바닥 상태  ← 대칭이 깨진 것처럼 보임
```

---

## 3. 공간 대칭 깨짐의 예시: 결정

결정(crystal)은 공간 대칭 깨짐의 가장 직관적인 예다.

**고온 액체 상태:**
```
● ● ● ● ●   원자들이 무질서하게 배치
 ● ● ● ● ●  → 공간 병진 대칭 있음
● ● ● ● ●   (어디를 봐도 평균적으로 동일)
```

**저온 결정 상태:**
```
● ○ ● ○ ●   원자들이 주기적으로 배치
○ ● ○ ● ○   → 격자 상수 $a$만큼의 병진만 허용
● ○ ● ○ ●   연속 병진 대칭 → 이산 병진 대칭으로 깨짐
```

Hamiltonian(원자 간 상호작용)은 여전히 연속 공간 병진 대칭을 가지지만,
결정 상태는 그 대칭을 스스로 깨뜨린다.

---

## 4. 질서 매개변수(Order Parameter)

대칭이 깨졌는지를 정량화하는 물리량.

| 상전이 | 질서 매개변수 | 대칭 깨짐 |
|--------|--------------|----------|
| 액체 → 결정 | 밀도 파동 진폭 $\rho_\mathbf{q}$ | 연속 공간 병진 |
| 상자성 → 강자성 | 자화 $\mathbf{M}$ | $\mathbb{Z}_2$ (스핀 뒤집기) |
| 정상 → 초전도 | Cooper 쌍 진폭 $\langle\psi_\uparrow\psi_\downarrow\rangle$ | $U(1)$ 게이지 |

질서 매개변수가 0이면 대칭 유지, 0이 아니면 대칭 깨짐.

---

## 5. 열역학적 극한과 대칭 깨짐

> **중요:** 유한한 크기의 시스템에서는 진정한 SSB가 일어나지 않는다.

이유: 유한 시스템의 진정한 바닥 상태는 대칭의 두 축퇴 상태의 **중첩**이다.

$$|\psi_0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\uparrow\cdots\uparrow\rangle + |\downarrow\downarrow\cdots\downarrow\rangle)$$

그러나 열역학적 극한 $N \to \infty$에서는:
- 두 상태 사이의 터널링이 지수적으로 억제됨 ($\sim e^{-N}$)
- 미소한 외부 섭동(symmetry-breaking field)이 하나를 선택
- 결국 단일 방향의 질서 있는 상태가 안정화됨

```
N = 10:   터널링 빠름 → 중첩 상태 → 대칭 유지
N = 10²³: 터널링 거의 0 → 한쪽 선택 → 대칭 깨짐
```

---

## 6. 핵심 통찰 정리

> **SSB의 본질:** Hamiltonian이 가진 대칭보다 낮은 대칭의 상태를 시스템이 자발적으로 채택하는 현상이다. 열역학적 극한에서 에르고딕성(ergodicity)이 깨지면서 발생한다.

> **결정과 시간결정의 유추:** 공간 결정이 연속 공간 병진 대칭을 이산 대칭으로 깨뜨리듯이, 시간결정(time crystal)은 연속 시간 병진 대칭을 이산 시간 대칭으로 깨뜨리려는 시도다.

---

## 참고

- 다음 파일: `time_translation_symmetry_학습노트.md` (시간 대칭과 그 깨짐)
- 관련 개념: 에르고딕성(ergodicity), 상전이(phase transition), Landau 이론
- 논문 참조: Sec.I 첫 문단, Eq.(1)-(2) 주변 논의
