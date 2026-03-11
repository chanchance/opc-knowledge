# True Process Variation Aware Optical Proximity Correction with Variational Lithography Modeling and Model Calibration

## 메타데이터
- **저자**: Peng Yu, Sean X. Shi, David Z. Pan
- **연도**: 2007
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS (JM3), Volume 6, Issue 3
- **DOI/URL**: https://doi.org/10.1117/1.2752814
- **인용수**: 100+

## 핵심 요약
공정 변동(Process Variation)을 인식하는 OPC 프레임워크를 제안한 논문. 기존 OPC 모델은 단일 공정 조건(nominal)에서만 보정을 수행했으나, 이 연구는 변동 가능한 리소그래피 조건(포커스 변화, 노광량 변화)을 동시에 고려하는 변동적 리소그래피 모델링(Variational Lithography Modeling)을 도입했다. 모델 보정(calibration)과 OPC 최적화를 통합하여 공정 윈도우(process window) 전반에 걸쳐 안정적인 패턴 형성을 달성한다.

## 주요 기여
- 공정 변동(초점/노광량)을 고려하는 변동적 리소그래피 모델 수립
- 변동 인식 OPC(VA-OPC) 알고리즘 개발: 다중 공정 조건에서 EPE 최소화
- 광학 모델과 레지스트 모델의 통합 보정(calibration) 방법론 제안
- 공정 윈도우 분석(PWA)과 OPC의 결합 프레임워크 구축

## 모델 아키텍처/수식
변동적 리소그래피 모델의 핵심은 Taylor 전개를 이용한 공정 변동 선형 근사:

```
I(x; Δf, ΔE) ≈ I₀(x) + (∂I/∂f)·Δf + (∂I/∂E)·ΔE
```

여기서:
- I₀(x): 명목 조건(nominal)에서의 이미지 강도
- Δf: 초점 오차 (defocus)
- ΔE: 노광량 오차 (dose error)
- ∂I/∂f, ∂I/∂E: 각각 초점 및 노광량에 대한 이미지 강도 편미분 (선형 근사 커널로 사전 계산)

OPC 목적함수:
```
minimize Σᵢ Σⱼ [EPEᵢ(fⱼ, Eⱼ)]²
subject to mask manufacturability constraints
```
여기서 j는 다양한 공정 조건(초점, 노광량 조합)을 인덱싱.

레지스트 모델: Variable Threshold Resist Model (VTRM)
```
CD = f(I_max, slope, threshold)
threshold = a·I_max + b·slope + c
```

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 PWO(공정 윈도우 최적화) 모듈에 직접 적용 가능. 변동 인식 OPC를 구현하려면 nominal 모델 외에 초점/노광량 편미분 커널을 추가로 보정해야 한다. `skopc/pwo/` 모듈에서 다중 공정 조건 시뮬레이션 시 이 접근법을 참조. 특히 공정 윈도우(process window) 평가 시 Taylor 근사 기반 변동 예측은 계산 효율을 크게 높인다.

## 참고문헌 (핵심)
- Cobb, N. and Zakhor, A., "Fast sparse aerial image calculations for OPC," SPIE 2621 (1995)
- Granik, Y., "Fast pixel-based mask optimization for inverse lithography," JM3 5(4) (2006)
- Pati, Y. et al., "Phase-shifting masks for microlithography: automated design and mask requirements," JOSA A 11(9) (1994)
- Smith, B.W. et al., "Comparative study of lithographic process modeling," SPIE 1674 (1992)

## 태그
`Model`, `OPC`, `ProcessVariation`, `Calibration`, `VariationalLithography`, `ProcessWindow`, `EPE`, `VTR`, `OpticalModel`, `ResistModel`
