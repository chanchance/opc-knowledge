# Towards Efficient and Accurate Cost Functions for EUVL Stochastic-Aware OPC Correction and Verification: Via Failure Probability versus Image and Process Variation Band Metrics

## 메타데이터
- **저자**: Shuling Wang, Azat Latypov, Shumay Shang, Germain Fenger, Chih-I Wei, Xima Zhang
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 1295319
- **DOI/URL**: https://doi.org/10.1117/12.3010912

## 핵심 요약
EUV 리소그래피의 확률론적(stochastic) 변동성을 OPC 보정 및 검증 알고리즘에 활용하기 위한 효율적이고 정확한 비용 함수를 연구한 논문. 기존의 이미지 메트릭(NILS, PV band)에 기반한 단순화된 접근법이 via 레이어 레이아웃에서의 stochastic 실패 확률 예측에 얼마나 정확한지 Calibre stochastic 모델로 검증한다.

## 주요 기여
1. **비용 함수 비교**: NILS(Normalized Image Log Slope), PV band 등 이미지 기반 메트릭과 rigorous stochastic via failure probability 계산의 상관관계 분석
2. **다양한 레이아웃 검증**: 현대 IC의 via 레이어에 일반적인 다양한 레이아웃 패턴에 대한 평가
3. **OPC 효율성**: 실패 확률 직접 계산보다 저비용 메트릭이 언제 유효한지 경계 조건 규명
4. **Stochastic-aware OPC 전략**: EUV 공정에서 확률적 결함을 줄이기 위한 OPC 파라미터 튜닝 방향 제시

## Recipe/Flow 상세
- **대상 레이어**: Via/contact 레이어 (EUV 공정)
- **모델**: Calibre stochastic model (rigorous resist model)
- **비용 함수 후보**:
  - Image Log Slope (ILS) / NILS
  - Process Variation (PV) band 파라미터
  - Via failure probability (직접 계산)
- **평가 방법**: 다양한 via 레이아웃에서 각 메트릭과 실제 실패 확률의 상관관계 측정
- **적용 목적**: stochastic-aware OPC correction + post-OPC verification

## OPC 툴 구현 관련성
- EUV 공정 OPC에서 확률론적 모델 통합 방안
- via 레이어 OPC의 비용 함수 설계 지침
- `stochastic_cost_function.py` 구현 시 NILS vs failure probability 트레이드오프 참고
- Calibre nmOPC의 stochastic-aware 모드 동작 원리 이해

## 태그
`Stochastic`, `EUV`, `OPC`, `CostFunction`, `Via`, `SPIE`, `2024`
