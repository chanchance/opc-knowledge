# Improving OPC Modeling Accuracy with Rigorous and Compact Modeling of Deformation Effects in Photoresists

## 메타데이터
- **저자**: Latinwo, F., Kuechler, B., DeLancey, R., Hong, H., Yang, D. (Synopsys)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II
- **DOI/URL**: https://doi.org/10.1117/12.2660580
- **인용수**: ~10

## 핵심 요약
NTD 레지스트의 화학적·물리적 재료 특성(변형 포함)을 정확하게 모델링하기 위한 리고러스 및 컴팩트 시뮬레이션 방법론을 발전시킨다. NTD 레지스트의 기본 변형·수축 거동이 리고러스 및 컴팩트 시뮬레이터로 포착됨을 보이며, OPC 컴팩트 모델링의 정확도 개선 경로를 제시한다.

## 주요 기여
1. NTD 레지스트 변형 효과의 리고러스 시뮬레이션 → 컴팩트 모델 학습 데이터 생성
2. 리고러스 모델 기반 컴팩트 모델 캘리브레이션 방법론 (실험 데이터 없이)
3. 변형 효과가 OPC 모델 오차에 미치는 계통적 기여 정량화
4. NTD 레지스트 특유 재료 특성(탄성률, 포아송비, 팽윤계수) 민감도 분석
5. OPC + ILT 플로우에서 변형 보정 통합 실용적 가이드

## 모델 수식/아키텍처

**리고러스 변형 시뮬레이션:**
```
Governing equations:
  ∇·σ = 0  (평형)
  σ = E/(1+ν) · [ε + ν/(1-2ν)·tr(ε)·I] - α_th·ΔT·I
  ε = (∇u + ∇uᵀ)/2
```
여기서: E = Young's modulus, ν = Poisson's ratio
α_th = 열팽창(현상 용매 흡수) 등가 계수

**변형에 의한 CD 이동:**
```
ΔCD_deform(x) = 2·|u_x(edge, y=0)|  [엣지 수평 변위]
```

**컴팩트 모델 (리고러스 기반 캘리브레이션):**
```
ΔCD_compact(pattern) = Σ_k c_k · g_k(CD, pitch, H_resist, ...)
캘리브레이션: min_{c} ||ΔCD_rigorous - Σ_k c_k·g_k||²
```

**OPC 정확도 향상:**
```
RMS_without_deform: ~2.0nm  (변형 무시)
RMS_with_compact_deform: ~1.1nm  (45% 향상)
RMS_with_rigorous_deform: ~0.8nm  (60% 향상)
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (변형 컴팩트 모델)
- [ ] ML/DL
- [x] 하이브리드 (리고러스 시뮬레이션 → 컴팩트 모델)

## OPC 툴 구현 관련성
- NTD 레지스트 변형 보정: EUV Via/Contact OPC 필수 고려 사항
- skopc NTD 변형 모듈: 리고러스 시뮬레이터 기반 컴팩트 모델 캘리브레이션
- 리고러스 → 컴팩트 전략: PROLITH/S-Litho로 다양한 패턴 시뮬레이션 → 컴팩트 파라미터 피팅
- 재료 파라미터(E, ν): 나노인덴테이션 실험 또는 문헌값 활용
- Synopsys Proteus 최신 NTD 모델 구현의 이론적 기반

## 참고문헌
- Latinwo, F. et al., "3D NTD resist deformation compact model" (2018)
- Chou, A. et al., "Resist shrinkage: rigorous simulations" (2020)
- Adam, K. et al., "Calibration of physical resist models" (2009)

## 태그
`Model`, `SPIE`, `NTD`, `ResistDeformation`, `RigorousSimulation`, `CompactModel`, `OPC`, `ILT`, `2023`
