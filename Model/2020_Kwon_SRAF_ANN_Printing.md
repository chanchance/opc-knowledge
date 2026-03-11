# SRAF Printing Prediction Using Artificial Neural Network

## 메타데이터
- **저자**: Yonghwi Kwon, Jinho Yang, Sungho Kim, Cheolkyun Kim, Youngsoo Shin
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical Microlithography XXXIII, 113270C
- **DOI/URL**: https://doi.org/10.1117/12.2550685

## 핵심 요약
서브해상도 보조 피처(SRAF) 인쇄 여부를 인공 신경망(ANN)으로 빠르고 정확하게 예측하는 ML-SPC(Machine Learning SRAF Printing Check) 방법을 제안한다. 각 SRAF 픽셀과 주변 환경의 극좌표 푸리에 변환 신호 및 국소 레이아웃 밀도를 ANN 입력으로 사용한다.

## 주요 기여
1. ANN 기반 SRAF 인쇄 예측기 ML-SPC 개발
2. 극좌표 푸리에 변환(Polar Fourier Transform) 기반 SRAF 픽셀 특징 추출
3. 국소 레이아웃 밀도(local layout density)를 ANN 입력으로 통합
4. 기존 리소그래피 시뮬레이션 대비 빠른 SRAF 인쇄 위험 예측
5. 메모리 및 로직 레이어에서 ML-SPC 검증

## 모델 수식/아키텍처
- **입력 특징**: Polar Fourier 변환 신호 + 국소 밀도 (각 SRAF 픽셀 기준)
  - r, θ 방향의 푸리에 계수 (패턴 방향 및 주파수 인코딩)
  - 반경 R_1, R_2, R_3 내의 레이아웃 밀도
- **ANN 구조**: 완전 연결 다층 퍼셉트론
  - 출력: SRAF 인쇄 확률 P(print) ∈ [0, 1]
- **판단 임계값**: P > t → SRAF 인쇄 위험 플래그
- 학습 데이터: 리소그래피 시뮬레이션 결과 (인쇄/미인쇄 레이블)

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC SRAF 삽입 모듈에서 SRAF 인쇄 위험 사전 필터링에 활용
- ML 기반 SRAF 체크로 시뮬레이션 기반 검증 대비 런타임 단축
- OPC 검증(verification) 흐름에서 핫스팟 우선 식별 도구로 통합
- `2021_Shin_CompLithoML_KAIST_Review.md`의 ML 리소그래피 응용 예시 중 하나

## 태그
`Model`, `SRAF`, `ANN`, `ML`, `PrintingPrediction`, `OPC`, `Lithography`, `SPIE`
