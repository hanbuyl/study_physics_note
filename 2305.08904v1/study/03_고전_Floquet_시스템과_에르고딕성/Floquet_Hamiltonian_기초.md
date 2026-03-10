# Floquet Hamiltonian 기초: 회전 프레임과 Magnus 전개

**논문:** Zaletel et al., "Colloquium: Quantum and Classical Discrete Time Crystals" (arXiv:2305.08904v1, 2023)
**대응 섹션:** Sec.III — Classical Floquet Systems
**작성일:** 2026-03-03
**목적:** 주기적으로 구동되는 시스템의 유효 정적 Hamiltonian을 이해하기 위한 기초

---

## 목차

1. [주기적 구동과 Floquet 이론](#1-주기적-구동과-floquet-이론)
2. [Floquet 연산자와 준에너지](#2-floquet-연산자와-준에너지)
3. [유효 Floquet Hamiltonian](#3-유효-floquet-hamiltonian)
4. [Magnus 전개](#4-magnus-전개)
5. [회전 프레임 변환](#5-회전-프레임-변환)
6. [핵심 통찰 정리](#6-핵심-통찰-정리)

---

## 1. 주기적 구동과 Floquet 이론

주기 $T$로 구동되는 시스템의 Hamiltonian:

$$H(t) = H(t + T)$$

**Floquet 정리 (Bloch 정리의 시간 버전):**
주기 $T$ 해밀토니안의 해는 다음 형태를 가진다:

$$|\psi(t)\rangle = e^{-i\epsilon t/\hbar} |u(t)\rangle$$

여기서:
- $\epsilon$: 준에너지(quasienergy) — 에너지의 시간 버전
- $|u(t)\rangle = |u(t+T)\rangle$: 주기적 "Floquet 모드"

---

## 2. Floquet 연산자와 준에너지

한 주기 진화 연산자:

$$U_F = U(T, 0) = \mathcal{T}\exp\left(-\frac{i}{\hbar}\int_0^T H(t)\,dt\right)$$

$U_F$의 고유값과 고유벡터:

$$U_F |n\rangle = e^{-i\epsilon_n T/\hbar} |n\rangle$$

준에너지 $\epsilon_n$은 $[-\pi\hbar/T, \pi\hbar/T]$ 범위에서만 정의된다 (Brillouin zone 아날로그).

| 공간 블로흐 이론 | 시간 Floquet 이론 |
|----------------|-----------------|
| 결정 주기 $a$ | 구동 주기 $T$ |
| 공간 파수 $k$ | 준에너지 $\epsilon$ |
| 에너지 밴드 | 준에너지 밴드 |
| $k \in [-\pi/a, \pi/a]$ | $\epsilon \in [-\pi/T, \pi/T]$ |

---

## 3. 유효 Floquet Hamiltonian

$U_F$를 마치 유효 정적 Hamiltonian의 시간 진화처럼 쓸 수 있다:

$$U_F = e^{-iH_F T/\hbar}$$

이것을 **유효 Floquet Hamiltonian** $H_F$라 한다.

$H_F$는 실제 Hamiltonian이 아니라 *유효* Hamiltonian이지만, $t = nT$ 순간의 시간 진화를 정확히 기술한다.

```
실제 시스템:  H(t) (복잡한 시간 의존성)
                │
                │  t = nT 순간만 본다
                ↓
유효 기술:    H_F (정적, 단순)
               e^{-iH_F·nT/ℏ}|ψ₀⟩ = |ψ(nT)⟩
```

---

## 4. Magnus 전개

고주파 구동 ($\omega = 2\pi/T \gg J/\hbar$, $J$ = 상호작용 강도) 극한에서 $H_F$를 체계적으로 구하는 방법.

$$H_F = H_F^{(0)} + H_F^{(1)} + H_F^{(2)} + \cdots$$

첫 몇 항:

$$H_F^{(0)} = \frac{1}{T}\int_0^T H(t)\,dt \quad \text{(시간 평균)}$$

$$H_F^{(1)} = \frac{1}{2i\hbar T}\int_0^T\int_0^{t_1} [H(t_1), H(t_2)]\,dt_2\,dt_1$$

**고주파 극한에서의 특성:**
- $H_F^{(n)} \sim (J/\omega)^n$이므로 $\omega \gg J$면 고차항 무시 가능
- 유효 Floquet Hamiltonian이 잘 정의된 정적 시스템처럼 행동

**고주파 가열 문제:**
그러나 실제로는 Magnus 전개가 발산할 수 있다 — 시스템이 결국 가열되어 무한 온도로 수렴. 이것이 DTC의 적!

---

## 5. 회전 프레임 변환

주기 구동 문제를 단순화하는 핵심 도구.

**예시: 주기 자기장으로 구동되는 스핀**

$$H(t) = \omega_0 \sigma^z + h\cos(\omega t) \sigma^x$$

$\omega_0 \approx \omega$ (공진 근방)에서 회전 프레임 변환:

$$U_{rot}(t) = e^{i\omega t \sigma^z/2}$$

변환된 Hamiltonian (RWA 후):

$$\tilde{H} = \frac{\Delta}{2}\sigma^z + \frac{h}{2}\sigma^x \quad (\Delta = \omega_0 - \omega)$$

이것은 정적 Hamiltonian! 회전 프레임에서 문제가 훨씬 단순해진다.

```
Lab frame:    복잡한 시간 의존 H(t)
                    │
                    │  회전 프레임 변환
                    ↓
Rotating frame: 정적 또는 단순한 H_eff
```

---

## 6. 핵심 통찰 정리

> **Floquet 이론의 핵심:** 주기 구동 시스템을 분석하는 핵심 도구는 한 주기 진화 연산자 $U_F$와 그로부터 정의되는 유효 Floquet Hamiltonian $H_F$다.

> **Magnus 전개의 의의:** 고주파 극한에서 복잡한 시간 의존 문제를 정적 문제로 근사할 수 있다. 하지만 긴 시간에서는 반드시 가열이 일어남을 주의해야 한다.

> **회전 프레임의 힘:** 구동 주파수로 도는 좌표계로 이동하면 시간 의존성이 제거되어 물리가 직관적으로 보인다. Virtual Z-gate (McKay 논문)와 동일한 개념이 DTC 분석에도 사용된다.

---

## 참고

- 이전 Unit: `../02_.../formal_definition_학습노트.md`
- 다음 파일: `parametric_resonance_학습노트.md`
- 관련 개념: Bloch 정리, RWA, Baker-Campbell-Hausdorff 공식
- 논문 참조: Sec.III.A, Eq.(4)-(6)
