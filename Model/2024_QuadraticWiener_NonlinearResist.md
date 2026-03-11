# Efficient Nonlinear Resist Modeling by Combining and Cascading Quadratic Wiener Systems

## 메타데이터
- **저자**: (Optics & Laser Technology 게재, 저자 정보 제한적)
- **연도**: 2024
- **게재지/학회**: Optics & Laser Technology (ScienceDirect), December 2024
- **DOI/URL**: https://doi.org/10.1016/j.optlastec.2024.111773; https://www.sciencedirect.com/article/pii/S0030399224017730
- **인용수**: 신규 (2024년)

## 핵심 요약
다단계(multi-stage) 계단식(cascaded) 이차 Wiener 모델 네트워크를 이용한 포괄적인 비선형 레지스트 모델링 솔루션을 제안한 논문. 레지스트 노광 및 현상 공정의 복잡한 비선형 물리화학 반응을 빠르고 정확하게 모델링하는 것이 핵심 과제다. 고유값 분해(eigendecomposition) 기반 시뮬레이션 가속 방법과 사영 Landweber 방법(projected Landweber method) 기반 효율적 모델 보정 방법을 함께 제안한다. 단일 단계와 다단계 Wiener 모델 모두 산업 표준을 충족하며, 다단계가 모든 면에서 우수한 성능을 보인다.

## 주요 기여
- 다단계 계단식 이차 Wiener 모델 네트워크로 레지스트 비선형성 정밀 모델링
- 고유값 분해 기반 시뮬레이션 가속 방법
- 사영 Landweber 방법 기반 효율적 모델 보정
- 단일/다단계 Wiener 모델 비교: 다단계가 모든 지표에서 우수
- 산업 표준 OPC 정확도 달성 입증

## 모델 아키텍처/수식
**Wiener 시스템 기본 구조:**
```
Input → [Linear Filter H] → [Static Nonlinearity f] → Output
y = f(H * u)    (선형 필터 + 정적 비선형성)
```

**이차 Wiener 시스템 (Quadratic Wiener):**
```
y = Σₙ Σₘ hₙₘ · uₙ · uₘ + Σₙ hₙ · uₙ + h₀
   (2차 Volterra 급수의 Wiener 표현)
```
행렬 표현:
```
y = u^T · H₂ · u + h₁^T · u + h₀
H₂: 2차 커널 행렬 (대칭)
h₁: 선형 커널 벡터
```

**단일 단계 이차 Wiener 모델:**
```
I_eff(x) = Σₙ Σₘ H₂(n,m) · I(xₙ) · I(xₘ)  (비선형 이미지 합성)
CD(x) = a · I_eff(x) + b    (선형 출력)
```

**다단계 계단식 구조 (Multi-stage Cascaded):**
```
Stage 1: I₁ = W₁(I_aerial)  (1차 이차 Wiener)
Stage 2: I₂ = W₂(I₁)        (2차 이차 Wiener)
...
Stage K: Iₖ = Wₖ(Iₖ₋₁)
Output: CD = linear(Iₖ)
```
각 단계가 레지스트 공정의 한 단계를 모델링:
- Stage 1: 광자 흡수 + 이차 반응
- Stage 2: PEB 확산 비선형성
- Stage 3: 현상 비선형성

**고유값 분해 기반 시뮬레이션 가속:**
H₂의 고유값 분해:
```
H₂ = V · Λ · V^T   (대칭 행렬 분해)
y = Σₙ λₙ · (V_n^T · u)²   (n개 고유 모드)
```
계산 복잡도: O(N²) → O(N·K)  (K = 유지 고유 모드 수, K << N)

**사영 Landweber 보정 (Projected Landweber):**
```
θₜ₊₁ = P_C(θₜ - α · ∇_θ ||y_pred(θ) - y_meas||²)
P_C: 제약 집합 C로의 사영 (물리적 제약: θ ∈ C)
```
수렴: 볼록 제약 하에서 전역 수렴 보장

**성능:**
| 모델 | EPE RMS | 계산 시간 |
|------|---------|----------|
| 단일 Wiener | 산업 표준 충족 | 빠름 |
| 다단계 Wiener | 모든 지표 최선 | 빠름 |
| VTR (기준) | 기준 | 매우 빠름 |

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 레지스트 모델 고도화에 직접 활용. 현재 VTR/LPM 기반 레지스트 모델을 다단계 이차 Wiener 모델로 업그레이드 시 비선형성 재현 정확도 향상. 사영 Landweber 보정은 물리적 제약(σ_blur > 0 등)을 만족하면서 보정하는 수치적으로 안정적인 방법으로 `skopc/modeling/` calibration 루틴에 참조. 고유값 분해 가속은 numpy/scipy로 구현 가능.

## 참고문헌 (핵심)
- Wiener, N., "Nonlinear Problems in Random Theory," MIT Press (1958)
- Cobb, N. and Zakhor, A., "Variable threshold resist model," SPIE 3679 (1999)
- Mack, C.A., "Lumped parameter model for CARs," SPIE 5377 (2004)
- (이전 논문) "Efficient resist modeling using Wiener–Padé formulation," Opt. Laser Tech. (2025)

## 태그
`Model`, `OPC`, `ResistModel`, `WienerModel`, `Nonlinear`, `Cascaded`, `Quadratic`, `Eigendecomposition`, `LandweberMethod`, `CompactModel`, `Calibration`, `OPC_Accuracy`
