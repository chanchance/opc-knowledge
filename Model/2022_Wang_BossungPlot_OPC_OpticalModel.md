# Utilizing Bossung Plot to Calibrate OPC Optical Model

## 메타데이터
- **저자**: Jian Wang
- **연도**: 2022
- **게재지**: IEEE Conference Publication (ICCAD 2022 관련)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9856895/

## 핵심 요약
Bossung plot을 이용한 OPC 광학 모델 캘리브레이션 방법론을 제안한다. 기존의 RMS(Root Mean Square) 기반 merit function 대신 Bossung curve의 유사도를 기준으로 광학 모델 파라미터를 탐색함으로써 디포커스 조건에서의 예측 정확도를 향상시킨다.

## 주요 기여
- Bossung plot 기반 merit function 연구: RMS, GRADIENT, FOCUS CENTER 세 가지 비교
- Bossung curve를 2차 함수(quadratic function)로 피팅하여 중심 포커스와 기울기를 OPC 모델 탐색 지표로 활용
- 기존 RMS 기반 최적화보다 Bossung plot 유사도 기반 최적화가 defocus 조건 예측에 더 우수함을 실험으로 입증
- 14nm 노드 케이스에 적용하여 검증

## 모델 수식/아키텍처
- Bossung curve: CD vs. focus 관계를 quadratic으로 피팅 → CD(f) = a·f² + b·f + c
- Merit function 후보:
  - RMS: 전통적 CD 매칭 오차
  - GRADIENT: Bossung curve 기울기 매칭
  - FOCUS CENTER: 최적 포커스 위치 매칭
- 광학 모델 파라미터(σ, NA, aberration 등)를 Bossung plot 유사도 기준으로 탐색

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 광학 모델 캘리브레이션 단계에서 merit function 선택에 직접 적용 가능
- 디포커스 조건에서의 모델 예측 안정성 향상에 기여
- SKOPC Modeling 모듈의 캘리브레이션 흐름에서 Bossung curve 기반 검증 지표로 활용 가능

## 태그
`Model`, `IEEE`, `Optical Model`, `Calibration`, `Bossung Plot`, `Defocus`, `OPC`
