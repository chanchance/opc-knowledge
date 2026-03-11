# RuleLearner: OPC Rule Extraction From Inverse Lithography Technique Engine

## 메타데이터
- **저자**: (IEEE Xplore, 2024 발표)
- **연도**: 2024
- **게재지**: IEEE Journal (IEEE Xplore Document ID: 10753456)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10753456/

## 핵심 요약
ILT(Inverse Lithography Technology) 엔진에서 OPC 규칙(rule)을 자동으로 추출하는 RuleLearner 시스템을 제안한다. 모델 기반 OPC와 SRAF 생성을 위한 종합적인 마스크 최적화 시스템으로, 실제 산업 시나리오에서의 적용성을 검증한다.

## 주요 기여
1. ILT 엔진 결과에서 OPC 규칙을 자동 학습·추출하는 RuleLearner 프레임워크
2. SRAF 생성과 모델 기반 OPC를 통합하는 종합적 마스크 최적화 시스템
3. ILT의 높은 정확도를 OPC 규칙 기반 방법의 빠른 속도와 결합
4. 실제 산업 시나리오에서의 OPC 규칙 추출 및 적용 검증
5. 리소그래피 왜곡 보상을 위한 표준 OPC 실무에의 AI 통합

## 모델 수식/아키텍처
- **RuleLearner 파이프라인**:
  1. ILT 엔진으로 다양한 패턴에 대해 최적화된 마스크 생성
  2. ILT 결과 (target, optimal_mask) 쌍에서 패턴 규칙 학습
  3. ML 모델로 새 패턴에 대한 OPC 규칙 예측 및 적용
- 규칙 표현: 패턴 기하학적 특성(CD, pitch, corner 등) → OPC 이동량
- SRAF 규칙: SRAF 삽입 위치 및 크기 자동 결정
- 학습 알고리즘: 결정 트리, 랜덤 포레스트, 또는 신경망 기반 규칙 추출

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드 (ILT 물리 기반 + ML 규칙 추출)

## OPC 툴 구현 관련성
- SKOPC ILT 모듈과 규칙 기반 OPC의 브리지 기술
- ILT 결과에서 재사용 가능한 OPC 규칙 추출로 런타임 단축
- SRAF 자동 생성 규칙을 ML로 학습하는 참조 아키텍처
- `2024_Yang_ILILT_CurvyMask.md` 등 ILT 연구와 연계하여 규칙화 방향 탐색

## 태그
`Model`, `OPC`, `ILT`, `RuleLearner`, `SRAF`, `ML`, `RuleExtraction`, `MaskOptimization`, `IEEE`
