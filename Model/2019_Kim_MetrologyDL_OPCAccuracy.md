# Metrology and Deep Learning Integrated Solution to Drive OPC Model Accuracy Improvement

## 메타데이터
- **저자**: (Samsung / KLA / Synopsys 계열, SPIE 10961 발표)
- **연도**: 2019
- **게재지**: Proc. SPIE 10961, Optical Microlithography XXXII
- **DOI/URL**: https://doi.org/10.1117/12.2516236

## 핵심 요약
계측(metrology) 데이터와 딥러닝을 결합하여 OPC 모델 정확도를 향상시키는 통합 솔루션을 제안한다. 대용량 SEM 컨투어 기반 게이지와 딥러닝을 활용하여 메모리 소자에서 기존 접근 대비 47% 이상 모델 정확도를 개선한다.

## 주요 기여
1. 계측 데이터(대용량 SEM 컨투어 게이지)와 딥러닝의 통합 OPC 모델 개선 방법론
2. 검증 게이지 1,400개 이상에서 기존 대비 47% 이상 모델 정확도 향상
3. 메모리 소자 실제 칩 패턴에서의 성능 검증
4. 딥러닝 기반 계측 데이터 처리로 OPC 모델 교정 데이터 품질 개선
5. 계측 오류 필터링 및 이상치(outlier) 자동 제거를 통한 교정 데이터셋 정제

## 모델 수식/아키텍처
- 딥러닝 계측 처리: SEM 이미지 → 고품질 컨투어 추출 네트워크
- OPC 모델 교정: 정제된 컨투어 게이지로 광학/레지스트 모델 파라미터 최적화
- 이상치 검출: 딥러닝 기반 계측 오류 및 비정상 패턴 자동 식별
- 통합 파이프라인: 대용량 SEM 데이터 → DL 처리 → OPC 모델 재교정

## 모델 유형
- [x] 광학
- [x] 레지스트
- [x] ML/DL
- [x] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 모델 교정 파이프라인에서 딥러닝 기반 계측 데이터 전처리 단계 추가
- 대규모 자동화 계측(e-beam, CD-SEM) 데이터 처리에 DL 통합 방향 제시
- 메모리 소자 풀칩 OPC 모델 정확도 개선의 실증 사례
- 2024_Gan_SEMContour_OPCCalib_FullChip.md와 컨투어 기반 교정 접근법 비교 가능

## 태그
`Model`, `Calibration`, `DeepLearning`, `Metrology`, `SEMContour`, `OPC`, `Memory`, `SPIE`
