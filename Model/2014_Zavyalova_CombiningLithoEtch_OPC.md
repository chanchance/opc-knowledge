# Combining Lithography and Etch Models in OPC Modeling

## 메타데이터
- **저자**: Lena V. Zavyalova, Lan Luan, Hua Song, Thomas Schmoeller, James P. Shiely
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII, 905222
- **DOI/URL**: https://doi.org/10.1117/12.2049003

## 핵심 요약
리소그래피 모델과 에치 모델을 OPC 모델링에서 결합하는 방법론을 연구한다. 레지스트(리소그래피) 모델로 노광 후 패턴 변화를 보정하고, 에치 모델로 에치 공정 효과를 추가 보정하는 순차적·통합적 교정 접근법을 제시한다.

## 주요 기여
1. 리소그래피 효과와 에치 효과를 순차적·단계적으로 모델링하는 표준 방법론 확립
2. 현상 후 레지스트 패턴 변화와 에칭 후 패턴 변화의 분리 모델링
3. 두 공정 효과의 통합 OPC 모델 교정 최적화
4. 리소그래피-에치 결합 모델의 OPC 정확도 향상 정량화
5. 풀칩 OPC 흐름에서 에치 모델 통합의 실용적 가이드라인

## 모델 수식/아키텍처
- **단계별 모델 구조**:
  1. 리소그래피 모델: AI(x,y) → CD_resist (광학 + 레지스트 모델)
  2. 에치 모델: CD_resist + pitch, density → CD_wafer (에치 컴팩트 모델)
- **에치 컴팩트 모델**: CD_etch = CD_resist + B_etch(CD, pitch, density)
- 결합 교정: 리소그래피 파라미터와 에치 파라미터 동시 또는 순차 최적화
- 에치 커널: 에치 편향의 근거리 및 원거리 환경 밀도 의존성 포착

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (리소그래피 + 에치 결합 모델)

## OPC 툴 구현 관련성
- SKOPC 모델 교정 파이프라인의 리소그래피-에치 결합 모델 구현 기반
- 에치 보정 모듈 설계 시 리소그래피 모델과의 결합 방식 참조
- 산업 표준 OPC 흐름(Calibre, Tachyon)의 에치 모델 통합 방식과 일치
- `2023_Sungauer_EtchModel_Curvilinear_OPC.md` 등 후속 연구의 기반 논문

## 태그
`Model`, `Etch`, `Lithography`, `Combined`, `OPC`, `Calibration`, `FullChip`, `SPIE`
