# Optimal OPC Model Selection with SEM Image Contours

## 메타데이터
- **저자**: Zheng 등 (Zheng, Zhang 포함)
- **연도**: 2022
- **게재지**: 2022 International Workshop on Advanced Patterning Solutions (IWAPS), IEEE
- **DOI/URL**: https://ieeexplore.ieee.org/document/9972274/

## 핵심 요약
SEM 이미지에서 추출된 컨투어를 이용하여 가장 신뢰할 수 있는 OPC 모델을 선택하는 새로운 방법을 제안한다. Calibre SEMSuite™로 추출한 웨이퍼 SEM 이미지 컨투어와 다양한 OPC 모델로부터 생성된 시뮬레이션 컨투어를 다차원 비교하여 최적 모델을 결정론적으로 선택한다.

## 주요 기여
1. **SEM 컨투어 기반 모델 선택**: 웨이퍼 SEM 이미지 컨투어를 기준으로 OPC 모델 후보를 평가하여 실제 인쇄 패턴을 가장 잘 모사하는 모델 선택
2. **다차원 비교 및 최종 랭킹 스코어**: 여러 품질 차원(dimension)에서 가중치 적용 비교 후 종합 랭킹 스코어 산출로 결정론적 모델 선택
3. **Calibre SEMSuite 통합**: 기존 OPC 워크플로우 툴과의 통합을 고려한 실용적 구현
4. **모델 선택 객관성**: 전문가 주관적 판단 배제, 정량적 기준에 의한 자동화된 모델 선택 가능

## 검증 방법론
- 웨이퍼 SEM 이미지 컨투어와 여러 OPC 모델 시뮬레이션 컨투어 간 다차원 정량 비교
- 랭킹 스코어에 따른 모델 선택 결과의 검증 게이지 EPE 성능 확인
- 선택된 모델의 다양한 패턴 조건에서의 예측 정확도 평가

## OPC 툴 구현 관련성
- `skopc/modeling/` 의 Evaluation 모듈에 SEM 컨투어 기반 모델 선택 기능 통합 가능
- 다중 OPC 모델 후보를 자동 평가하고 최적 모델을 선택하는 모델 관리 시스템 설계에 참고
- 모델 캘리브레이션 후 자동화된 QA(Quality Assurance) 단계로 통합 가능
- 랭킹 스코어 산출 알고리즘은 `skopc/modeling/` 내 모델 비교 유틸리티 개발에 활용

## 태그
`Verification`, `IEEE`, `IWAPS`, `OPC_Model`, `SEM_Contour`, `Model_Selection`, `Calibre`, `2022`
