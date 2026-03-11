# Efficient Resist Modeling and Calibration Using a Wiener–Padé Formulation and Convex Optimizations

## 메타데이터
- **저자**: (ScienceDirect/Optics and Lasers in Technology 게재, 저자 정보 제한적)
- **연도**: 2025
- **게재지/학회**: Optics and Lasers in Technology (ScienceDirect), 2025년 5월
- **DOI/URL**: https://doi.org/10.1016/j.optlastec.2025.112399; https://www.sciencedirect.com/article/pii/S0030399225006139
- **인용수**: 신규 (2025년)

## 핵심 요약
기존 선형 조합(linear combination) 프레임워크를 탈피한 새로운 Wiener–Padé 레지스트 모델과 2단계 볼록 최적화(convex optimization) 기반 보정 전략을 제안한 논문. OPC용 compact 레지스트 모델은 빠르고 정확해야 하지만 기존 모델들은 선형 조합 구조의 한계로 복잡한 비선형 레지스트 거동 재현에 어려움이 있다. Wiener–Padé 모델은 다항식과 유리함수(rational function) 근사의 장점을 결합하여 계산 효율을 유지하면서 적응성을 향상시킨다. 2단계 볼록 최적화 보정은 전역 최적성, 계산 효율, 제약 조건 해법의 장점을 통합한다.

## 주요 기여
- 기존 선형 조합 프레임워크를 벗어난 새로운 Wiener–Padé 레지스트 모델 제안
- 다항식(Wiener) + 유리함수(Padé) 근사의 결합으로 레지스트 비선형성 향상된 표현
- 2단계 이차 볼록 최적화(quadratic convex optimization) 보정 전략
- 과적합(overfitting) 방지 및 ill-conditioned 문제 해결
- Full-chip OPC에 적합한 빠르고 정확한 compact 모델

## 모델 아키텍처/수식
**기존 compact 레지스트 모델의 한계:**

기존 선형 조합 모델 (CM1 형태):
```
CD = a₀ + a₁·NILS + a₂·Ipeak + a₃·NILS² + ...
     (다항식 기저의 선형 조합)
```
한계: 복잡한 레지스트 비선형성 재현에 제한

**Wiener–Padé 모델:**

Padé 유리함수 근사:
```
f_Padé(x) = P_m(x) / Q_n(x)
           = (p₀ + p₁x + ... + pₘxᵐ) / (1 + q₁x + ... + qₙxⁿ)
```

Wiener 시스템 (비선형 입출력 관계):
```
y = f(∫ w(τ)·u(t-τ)dτ)   (선형 필터 + 정적 비선형성)
```

Wiener–Padé 통합 모델:
```
CD(x) = P_m(I_eff(x)) / Q_n(I_eff(x))

I_eff(x) = Σₖ cₖ · (hₖ ⊗ I)(x)   (Wiener 선형 필터링)
```
여기서:
- hₖ: k번째 가우시안/다항식 커널
- P_m, Q_n: m차/n차 다항식 (Padé 분자/분모)
- 파라미터: {cₖ, p₀,...,pₘ, q₁,...,qₙ}

**2단계 볼록 최적화 보정:**

1단계: Padé 분모 고정, 분자 최적화
```
min_{p} Σᵢ (P_m(I_eff,i) - CD_meas,i · Q_n(I_eff,i))²
s.t.  Q_n(I_eff,i) > 0, ∀i   (안정성 제약)
```
→ 이차 볼록 프로그램 (QP): 전역 최적해 보장

2단계: 분자 고정, 분모 재최적화
```
min_{q} Σᵢ (P_m(I_eff,i)/Q_n(I_eff,i) - CD_meas,i)²
s.t.  ||q||₂ ≤ δ  (정규화 제약)
```

**장점:**
- 볼록 문제 → 전역 최적해 보장
- 과적합 방지를 위한 명시적 제약
- ill-conditioned 문제 해결
- 기존 CM1 대비 정확도 향상, 유사한 계산 속도

**성능 비교:**
| 모델 | EPE RMS | 계산 시간 |
|------|---------|----------|
| VTR (기준) | 기준 | 빠름 |
| CM1 | 개선 | 빠름 |
| Wiener–Padé | 최선 | 빠름 |

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 레지스트 모델 고도화에 직접 활용 가능. 현재 SKOPC가 VTR 또는 LPM 기반 레지스트 모델을 사용한다면, Wiener–Padé 모델로 교체하여 비선형 레지스트 거동 재현 정확도를 높일 수 있다. 2단계 볼록 최적화 보정은 `skopc/modeling/` 내 보정 루틴을 scipy.optimize에서 CVXPY(볼록 최적화 라이브러리)로 전환하는 방식으로 구현 가능. EUV 노드에서의 복잡한 레지스트 거동 모델링에 특히 유용.

## 참고문헌 (핵심)
- Cobb, N. and Zakhor, A., "Variable threshold resist model," SPIE 3679 (1999)
- Mack, C.A., "Lumped parameter model for CARs," SPIE 5377 (2004)
- Padé, H., "Sur la représentation approchée d'une fonction," Ann. Sci. ENS (1892)
- Wiener, N., "Nonlinear Problems in Random Theory," MIT Press (1958)

## 태그
`Model`, `OPC`, `ResistModel`, `WienerPade`, `CompactModel`, `CalibrationMethod`, `ConvexOptimization`, `Nonlinear`, `FullChip`, `EPE`, `RationalApproximation`
