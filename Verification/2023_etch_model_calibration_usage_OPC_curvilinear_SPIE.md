# Etch Model Calibration and Usage in OPC Flow for Curvilinear Layouts

## 메타데이터
- **저자**: Elodie Sungauer, Laurent Depre, Raphael La Greca
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124951H (2023년 4월 28일)
- **DOI/URL**: https://doi.org/10.1117/12.2657676

## 핵심 요약
곡선형(curvilinear) 패턴에 적합한 OPC 플로우를 ASML Tachyon OPC+ 플랫폼으로 구현하면서, 에치(etch) 모델 캘리브레이션 방법론, 모델 기반 에치 바이어스 보정(etch bias correction) 구현, 전반적인 OPC 성능을 제시한다. 기존 맨해튼 패턴 기반 에치 모델을 곡선형 패턴으로 확장하는 과정의 도전과 해결책을 다룬다.

## 주요 기여
1. **곡선형 전용 에치 모델 캘리브레이션**: 곡선형 마스크 패턴에서의 에치 바이어스를 정확하게 모델링하는 캘리브레이션 방법론 확립
2. **Tachyon OPC+ 기반 구현**: ASML의 Tachyon OPC+ 플랫폼에서 곡선형 레이아웃 OPC 플로우 실용화
3. **모델 기반 에치 바이어스 보정**: OPC 플로우 내에서 에치 바이어스를 모델 기반으로 보정하는 통합 구현
4. **전반적 OPC 성능 평가**: 에치 모델 통합 후 곡선형 OPC의 종합 성능 분석

## 검증 방법론
- 곡선형 패턴에서의 에치 모델 캘리브레이션 정확도(RMSE) 평가
- 에치 보정 포함/미포함 OPC 결과의 웨이퍼 CD/EPE 비교
- Tachyon OPC+ 플로우에서의 런타임 및 정확도 균형 분석

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 에치 모델 모듈을 곡선형 패턴으로 확장할 때 핵심 참고 자료
- `2021_Hooker_ML_etch_model_OPC_ILT.md`, `2022_Shi_deep_learning_etch_model_OPC_accuracy.md`와 연계하여 곡선형 에치 모델 개발 전략 수립
- 곡선형 OPC 플로우에서 에치 모델 보정을 OPC 루프에 통합하는 아키텍처 설계 참고
- `recipes/example_euv.yaml` 등 EUV 레시피의 에치 보정 파라미터 설정 기준으로 활용

## 태그
`Verification`, `SPIE`, `Etch_Model`, `Curvilinear`, `OPC`, `Calibration`, `Tachyon`, `EUV`, `2023`
