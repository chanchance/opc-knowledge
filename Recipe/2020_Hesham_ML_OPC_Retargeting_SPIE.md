# Implementing Machine Learning for OPC Retargeting

## 메타데이터
- **저자**: Hesham Abdelghany, Kevin Hooker, Marco Guajardo, Chia-Chun Lu
- **연도**: 2020
- **게재지**: Proc. SPIE 11328, Design-Process-Technology Co-optimization for Manufacturability XIV, 113281D
- **DOI/URL**: https://doi.org/10.1117/12.2552402

## 핵심 요약
리소그래피 타겟 데이터에서 OPC 마스크 설계를 생성하는 학습 기반 방법을 제시한다. 리소그래피 타겟 데이터와 OPC 처리된 마스크 쌍을 학습 데이터로 사용하여, 계산 비용이 낮은 방식으로 OPC retargeting을 수행한다. advanced node 제조 테스트 케이스에서 정확도 및 OPC TAT(Turn-Around Time) 개선 효과를 검증한다.

## 주요 기여
1. **ML 기반 OPC Retargeting**: 리소그래피 타겟 → OPC 마스크 직접 예측하는 학습 모델
2. **학습 데이터 구성**: (리소그래피 타겟, OPC 마스크) 쌍으로 supervised learning
3. **낮은 계산 비용**: 기존 iterative OPC 대비 추론 단계에서 크게 빠른 처리
4. **학습 데이터 요구량 분석**: 생산 수준 OPC 안정성 달성을 위한 데이터 양과 다양성 실험
5. **Advanced Node 검증**: 실제 제품 레이아웃에서 정확도 및 TAT 이점 확인

## Recipe/Flow 상세
- **ML OPC Retargeting 플로우**:
  1. **학습 데이터 생성**:
     - 기존 OPC 도구로 다양한 레이아웃 처리 → (타겟, OPC 마스크) 쌍 수집
     - 레이아웃 다양성: 고립/밀집, 2D 패턴, 다양한 CD 범위 포함
  2. **특징 추출**:
     - 타겟 레이아웃의 국소 패턴 특징 (주변 밀도, CD, 방향 등)
     - Polar Fourier 또는 CNN 기반 특징 표현
  3. **ML 모델 학습**:
     - 입력: 리소그래피 타겟 레이아웃
     - 출력: OPC 마스크 segment displacement (보정량)
  4. **추론 (OPC Retargeting)**:
     - 새 레이아웃에 학습된 모델 적용 → 즉시 OPC 마스크 생성
  5. **Post-verification**: 생성된 마스크 시뮬레이션 검증
- **학습 데이터 실험**: 데이터 양 및 다양성에 따른 OPC 안정성 변화 분석
- **적용 노드**: Advanced node (7nm/5nm급)
- **평가 지표**: EPE, OPC TAT, 학습 데이터 요구량

## OPC 툴 구현 관련성
- SKOPC GNN-OPC 모듈의 학습 데이터 구성 전략 참고
- ML 기반 segment displacement 예측 구조 (`gnn_opc.py` 유사)
- OPC TAT 단축을 위한 ML 추론 단계 적용 방법
- 제품 레이아웃 대상 학습 데이터 다양성 확보 전략

## 태그
`MachineLearning`, `OPC`, `Retargeting`, `TAT`, `AdvancedNode`, `SupervisedLearning`, `SPIE`, `2020`
