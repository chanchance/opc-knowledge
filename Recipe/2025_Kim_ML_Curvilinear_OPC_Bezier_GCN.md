# ML-Guided Curvilinear OPC: Fast, Accurate, and Manufacturable Curve Correction

## 메타데이터
- **저자**: Seohyun Kim, Shilong Zhang, Youngsoo Shin (KAIST)
- **연도**: 2025
- **게재지**: IEEE Transactions on Semiconductor Manufacturing, Vol. 38, No. 1, pp. 19–28
- **DOI/URL**: https://ieeexplore.ieee.org/document/10835245/

## 핵심 요약
Curvilinear OPC에서 각 세그먼트를 3차 베지어 곡선으로 모델링하고, 두 개의 머신러닝 모델(MLP + GCN)을 결합하여 정확하고 빠르며 제조 가능한 곡선 보정을 수행하는 방법을 제안한다. VPE(Vertex Placement Error) 예측 및 최소화를 핵심 목표로 하며, 곡률 제약도 동시에 만족시킨다.

## 주요 기여
1. **베지어 기반 CL-OPC**: 각 segment를 cubic Bézier curve로 표현하여 제조 가능한 형상 보장
2. **MLP 엔드포인트 위치 결정**: 이전 반복의 VPE와 국소 광강도 신호를 입력으로 새로운 endpoint 위치 예측
3. **GCN 기반 VPE 예측기**: Graph Convolutional Network로 평균/최대 VPE 출력, 중간 제어점을 gradient descent로 최적화
4. **곡률 제약 통합**: VPE 최소화와 curvature MRC 동시 만족
5. **속도-정확도 균형**: 기존 iterative 방법 대비 빠른 수렴, 제조 가능성 유지

## Recipe/Flow 상세
- **Curvilinear OPC 알고리즘 구조**:
  1. **초기화**: Manhattan OPC 결과를 베지어 곡선으로 변환
  2. **MLP (Endpoint Predictor)**:
     - 입력: 이전 iteration VPE + 국소 광강도 맵
     - 출력: 베지어 endpoint 이동량 (Δx, Δy)
  3. **GCN (VPE Predictor)**:
     - 입력: 현재 베지어 제어점 그래프 구조
     - 출력: 각 제어점의 예상 VPE (평균/최대)
  4. **Gradient Descent 최적화**:
     - GCN 예측 VPE를 목적함수로 중간 제어점 위치 최적화
     - 곡률 제약 (최소 반경) 페널티 항 추가
  5. **수렴 판정**: 전체 EPE < 임계값 또는 최대 iteration 도달
- **대상**: Logic/SRAM 레이어 curvilinear 마스크
- **학습 데이터**: ILT 결과물 + lithography 시뮬레이션 쌍
- **평가 지표**: EPE RMS, 최대 VPE, curvature 위반율, 런타임

## OPC 툴 구현 관련성
- SKOPC GNN-OPC 모듈의 curvilinear 확장 참고 구조
- 베지어 제어점 기반 segment 표현 → `curvilinear_segment.py`
- GCN 기반 VPE 예측기 → SKOPC `gnn/` 모듈과 유사한 아키텍처
- 곡률 제약을 gradient descent 페널티로 구현하는 방법

## 태그
`CurvilinearOPC`, `MachineLearning`, `GCN`, `Bezier`, `VPE`, `Manufacturability`, `IEEE`, `2025`
