# Improving OPC Model Accuracy and Stability with Aerial Image Contribution

## 메타데이터
- **저자**: (IEEE Xplore Document 9972264, 저자 상세 접근 필요)
- **연도**: 2022
- **게재지**: IEEE Conference Publication
- **DOI/URL**: https://ieeexplore.ieee.org/document/9972264/

## 핵심 요약
Model-based OPC의 정확도와 안정성이 모델 캘리브레이션 프로세스에 크게 의존한다는 점에 착안하여, aerial image 기여분을 OPC 모델 캘리브레이션에 추가로 활용함으로써 모델 정확도와 안정성을 개선하는 방법을 제안한다.

## 주요 기여
- OPC 모델 캘리브레이션 시 aerial image 신호를 보조 정보로 활용하는 방법론 제안
- 모델 캘리브레이션 정확도 및 안정성(stability) 동시 향상
- CD-SEM 단독 데이터 대비 aerial image 결합 시 모델 예측 일관성 개선
- 선진 리소그래피 프로세스에서의 적용 가능성 검증

## 모델 수식/아키텍처
- Aerial image 기여: 광학 시뮬레이션에서 얻은 aerial image 신호를 SEM CD 데이터와 결합
- 캘리브레이션 목적함수에 aerial image 매칭 항 추가
- 복합 merit function: w₁·RMS_CD + w₂·RMS_AerialImage

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델 캘리브레이션 루프에서 SEM CD 외에 aerial image 데이터 소스 추가 활용
- SKOPC Modeling 모듈의 캘리브레이션 단계에서 다중 데이터 소스 통합 방향과 일치
- 모델 안정성(stability) 개선은 full-chip OPC 실행 수렴성 향상에 직결

## 태그
`Model`, `IEEE`, `Optical Model`, `Calibration`, `Aerial Image`, `OPC Accuracy`, `Stability`
