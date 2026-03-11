# Co-Optimization of Optical and Resist Models in the OPC Modeling Process Using In-House Genetic Algorithm

## 메타데이터
- **저자**: Lee, S. et al. (Samsung Electronics)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, Optical and EUV Nanolithography XXXVI
- **DOI/URL**: https://doi.org/10.1117/12.2657959
- **인용수**: ~10

## 핵심 요약
OPC 모델링 과정에서 광학 파라미터와 레지스트 파라미터를 순차적으로 최적화하는 기존 방법 대신, 유전 알고리즘(Genetic Algorithm, GA)으로 두 모델 파라미터를 동시에 공동 최적화(co-optimization)하는 방법을 제안한다. 광학-레지스트 모델 파라미터 간 상관관계를 활용한 전역 최적화로 기존 순차적 최적화 대비 모델 정확도를 향상시킨다.

## 주요 기여
1. 광학 파라미터 + 레지스트 파라미터 동시 공동 최적화 (GA 기반)
2. 순차적 최적화 대비 전역 최적해 도달 가능성 향상
3. 광학-레지스트 파라미터 상관관계 분석 및 가이드라인 제시
4. 인하우스 GA 구현으로 OPC 모델 캘리브레이션 파이프라인 통합
5. 실제 EUV/ArF 레이어에서 모델 정확도 향상 실증

## 모델 수식/아키텍처

**OPC 모델 파라미터 공간:**
```
θ = [θ_optical, θ_resist]
θ_optical = [NA, σ_inner, σ_outer, illumination_shape, aberrations...]
θ_resist = [c_0, c_1, ..., c_K]  (CM1/VTRE 계수)
```

**캘리브레이션 목적함수:**
```
L(θ) = (1/N) Σ_i (CD_sim(θ, pattern_i) - CD_meas,i)²
```

**기존 순차 최적화:**
```
Step 1: θ_optical* = argmin L(θ_optical; θ_resist_fixed)
Step 2: θ_resist* = argmin L(θ_resist; θ_optical_fixed = θ_optical*)
→ 국소 최적해에 갇힐 위험
```

**GA 동시 공동 최적화:**
```
Population: {θ^(1), θ^(2), ..., θ^(P)}  (P = 50-200 개체)
Selection: tournament / roulette wheel
Crossover: θ_child = α·θ_parent1 + (1-α)·θ_parent2
Mutation: θ_child_k += N(0, σ_mutation)
Fitness: f = 1 / (1 + L(θ))
Evolution: G = 100-500 세대
```

**광학-레지스트 상관관계:**
```
Corr(NA, c_threshold) ~ -0.7  (NA 증가 → threshold 감소)
Corr(σ, c_loading) ~ +0.5    (sigma 증가 → loading 계수 증가)
→ 순차 최적화 시 이 상관관계 무시 → 준최적해
```

## 모델 유형
- [x] 광학 모델 (공동 최적화)
- [x] 레지스트 모델 (공동 최적화)
- [x] ML/DL (진화 알고리즘)
- [x] 하이브리드 (물리 모델 + GA 최적화)

## OPC 툴 구현 관련성
- skopc 캘리브레이션 엔진에 GA 옵션 추가: 광학+레지스트 동시 최적화
- GA 계산 비용: 순차 대비 ~P×G 배 → 병렬 처리 필수
- 현실적 적용: GPU 병렬 공중상 계산 + GA 최적화 루프
- 광학 파라미터가 고정되지 않은 경우(신규 스캐너 세팅)에 특히 유용
- GA 외 대안: CMA-ES, Bayesian Optimization 등도 적용 가능

## 참고문헌
- Adam, K. et al., "Calibration of physical resist models" (2009)
- Zuniga, C. et al., "CM1 standard process model" (2007)
- Huang, Y.-H. et al., "Effective OPC model calibration using ML" (2022)

## 태그
`Model`, `SPIE`, `CoOptimization`, `GeneticAlgorithm`, `OPCCalibration`, `OpticalModel`, `ResistModel`, `GlobalOptimization`, `2023`
