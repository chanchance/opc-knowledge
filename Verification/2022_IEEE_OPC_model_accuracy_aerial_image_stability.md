# Improving OPC Model Accuracy and Stability with Aerial Image Contribution

## 메타데이터
- **저자**: (상세 저자 목록은 IEEE Xplore 원문 참조)
- **연도**: 2022
- **게재지**: IEEE Conference Publication (ASMC 또는 ESSDERC 계열 추정)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9972264

## 핵심 요약
모델 기반 OPC에서 OPC 모델의 정확도와 안정성이 모델 캘리브레이션 과정에 크게 의존한다는 점을 출발점으로, 에어리얼 이미지(aerial image) 기여를 OPC 모델 캘리브레이션에 추가함으로써 모델 정확도와 안정성을 동시에 개선하는 방법론을 제안한 논문.

## 주요 기여
1. **에어리얼 이미지 기여 통합**: OPC 모델 캘리브레이션에서 에어리얼 이미지 정보를 추가 입력으로 활용하여 모델 예측 정확도 향상
2. **모델 안정성 개선**: 캘리브레이션 데이터 변동에 대한 모델 강인성(robustness) 향상
3. **정확도-안정성 동시 최적화**: 기존 방법이 정확도와 안정성 간 트레이드오프를 갖는 문제를 에어리얼 이미지 기여로 완화
4. **OPC 모델 캘리브레이션 방법론 개선**: 기존 1D CD 측정 중심 캘리브레이션에 2D 에어리얼 이미지 정보를 보완적으로 통합

## 검증 방법론
- 에어리얼 이미지 기여 포함/미포함 OPC 모델의 캘리브레이션 잔차(RMSE) 비교
- 다양한 패턴 유형(L/S, contact, line-end)에서 모델 예측 정확도 평가
- 캘리브레이션 데이터 셋 변화에 대한 모델 안정성(stability) 측정
- 실제 웨이퍼 CD 측정 대비 모델 예측 오차 분포 비교

## OPC 툴 구현 관련성
- SKOPC의 OPC 모델 캘리브레이션 모듈에서 에어리얼 이미지를 보조 캘리브레이션 지표로 추가할 때 참조
- `2006_Ban_OPC_verification_accuracy_2D_wafer_image.md`의 2D 이미지 기반 모델링 아이디어를 에어리얼 이미지로 확장하는 후속 연구
- OPC 모델의 안정성 지표(stability metric)를 캘리브레이션 보고서에 포함하는 기준 제공

## 태그
`Verification`, `IEEE`, `OPC Model`, `Calibration`, `Aerial Image`, `Accuracy`, `Stability`, `CD`
