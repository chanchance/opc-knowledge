# Towards Efficient and Accurate Cost Functions for EUVL Stochastic-Aware OPC Correction and Verification

## 메타데이터
- **저자**: Shuling Wang, Azat Latypov, Shumay Shang, Germain Fenger, Chih-I Wei, Xima Zhang
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 1295319 (10 April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010912

## 핵심 요약
EUVL 확률론적 OPC 보정 및 검증을 위한 효율적이고 정확한 비용 함수를 연구한다. 전통적인 이미지 메트릭(NILS) 또는 공정 변동 밴드(PV band) 기반 접근법이 Calibre 확률론적 모델로 계산된 실제 비아 고장 확률을 정확히 예측하는지 광범위한 레이아웃에서 검증한다.

## 주요 기여
1. **확률론적 비용 함수 비교**: 이미지 메트릭(NILS) vs PV band vs 실제 고장 확률 비교
2. **비아 레이어 특화 분석**: 현대 IC 비아 레이어의 다양한 레이아웃에서 검증
3. **OPC 보정 정확도 향상**: 단순화된 메트릭의 예측 정확도 한계 규명
4. **실용적 가이드라인**: 확률론적 인식 OPC를 위한 비용 함수 선택 지침 제공

## 알고리즘/수식
### 비교되는 비용 함수 유형
```
유형 1: 이미지 기반 메트릭
  NILS = CD × d(ln I)/dx |_{edge}
  - 이미지 기울기 기반 대비도 척도
  - 빠른 계산, 확률론적 효과 간접 반영

유형 2: PV Band (공정 변동 밴드)
  PV_band = CD(focus+Δf, dose+Δd) - CD(focus-Δf, dose-Δd)
  - 공정 변동에 대한 CD 민감도
  - 중간 복잡도, 확률론적 효과 부분 반영

유형 3: 실제 고장 확률 (기준)
  P_fail(via) = P(via_open) + P(via_bridge)
  - Calibre 확률론적 모델 기반
  - 가장 정확, 계산 비용 높음

검증 질문:
  NILS 또는 PV_band ∝ P_fail 이 성립하는가?
  → 다양한 레이아웃에서 상관관계 분석
```

### 검증 방법
- 광범위한 비아 레이어 레이아웃 데이터셋 사용
- Calibre 확률론적 모델을 기준(ground truth)으로 사용
- 단순 메트릭과 실제 고장 확률 간 상관계수 계산

## OPC 툴 SMO 구현 관련성
- EUV OPC/SMO 비용 함수 설계의 핵심 참조
- 확률론적 메트릭을 SMO 비용 함수에 통합 시 어떤 근사가 유효한지 가이드
- 비아 레이어 SMO에서 NILS/PV band 기반 최적화의 한계 인식
- SKOPC SMO 모듈의 EUV 비용 함수 설계 시 정확도-속도 트레이드오프 결정에 활용

## 태그
`SMO`, `OPC`, `EUV`, `stochastic`, `cost_function`, `NILS`, `PV_band`, `failure_probability`, `via_layer`, `Calibre`, `SPIE`
