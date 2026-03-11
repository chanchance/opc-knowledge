# Resist Shrinkage During Development: Rigorous Simulations and First Compact Model for OPC

## 메타데이터
- **저자**: Chou, A. et al. (KLA / Fraunhofer IISB)
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical and EUV Nanolithography XXXIII
- **DOI/URL**: https://doi.org/10.1117/12.2552527
- **인용수**: ~20

## 핵심 요약
레지스트 현상 과정에서 발생하는 수축(shrinkage) 효과를 리고러스 시뮬레이션으로 분석하고, OPC 적용을 위한 최초의 컴팩트 탄성 모델(Elastic Compact Model, ECM)을 개발한다. SEM 전자빔 유발 수축과 구분되는 현상 유발 레지스트 수축이 CD 및 엣지 배치 오차에 미치는 영향을 정량화하고, 이를 OPC 모델에 통합하는 방법론을 제시한다.

## 주요 기여
1. 현상 유발 레지스트 수축의 리고러스 시뮬레이션 (탄성역학 기반)
2. 임의 2D 레지스트 패턴의 수축 유발 바이어스를 예측하는 ECM(Elastic Compact Model) 최초 개발
3. SEM 수축과 현상 수축의 분리 방법론
4. 레지스트 벽(resist wall)의 기하학적 형상이 수축 바이어스에 미치는 영향 분석
5. OPC 캘리브레이션에서 수축 효과 미고려 시의 계통 오차(systematic error) 정량화

## 모델 수식/아키텍처

**탄성 역학 기반 수축 시뮬레이션:**
```
∇·σ + f = 0   [평형 방정식]
σ = C : ε     [구성 방정식, C = 탄성 텐서]
ε = (1/2)(∇u + ∇uᵀ)  [변형률-변위 관계]
```
u = 변위 벡터 (레지스트 수축으로 인한)
f = 현상 응력 (레지스트 팽윤/수축 구동력)

**현상 유발 응력:**
```
σ_development(x,y) = E_resist · α_swelling · ΔM(x,y)
```
E_resist = 레지스트 탄성 계수
α_swelling = 팽윤 계수
ΔM = 현상 과정에서의 PAC/inhibitor 농도 변화

**ECM (Elastic Compact Model):**
```
CD_shrink = CD_nominal - 2·δ_shrink
δ_shrink = f(CD, pitch, resist_height, resist_modulus, swelling_factor)
```

**수축 바이어스의 패턴 의존성:**
```
δ_shrink(isolated) > δ_shrink(dense)  [고립 패턴에서 수축 더 큼]
δ_shrink ∝ 1/pitch  [피치가 클수록 수축 더 크게 느껴짐]
```

**OPC 캘리브레이션 수축 보정:**
```
CD_corrected = CD_SEM + δ_shrink_SEM + δ_shrink_development
→ 수축 보정 후 데이터로 OPC 모델 캘리브레이션
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (탄성 수축 컴팩트 모델)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 캘리브레이션 시 레지스트 수축 보정을 전처리 단계로 추가
- skopc/modeling/resist_shrinkage.py: ECM 구현
- 수축 효과: 고립 패턴에서 크고 밀집 패턴에서 작음 → 패턴 밀도 의존 바이어스
- EUV/ArF 레지스트 모두에서 현상 수축 효과 존재 (5-30nm CD에서 0.5-3nm 수준)
- CD-SEM 측정값에 수축 보정을 적용한 후 OPC 모델 캘리브레이션

## 참고문헌
- Adam, K. et al., "Calibration of physical resist models" (2009)
- Mack, C.A., "PROLITH comprehensive optical lithography model" (1985)
- Fraunhofer IISB resist simulation papers

## 태그
`Model`, `SPIE`, `ResistShrinkage`, `CompactModel`, `ECM`, `Development`, `OPC`, `Calibration`, `2020`
