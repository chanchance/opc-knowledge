# ML-Guided Curvilinear OPC: Fast, Accurate, and Manufacturable Curve Correction

## 메타데이터
- **저자**: (저자명 미확인 - IEEE Xplore 수록)
- **연도**: 2025
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10835245/

## 핵심 요약
곡선형(curvilinear) OPC에서 각 세그먼트는 두 개의 끝점(endpoint)과 두 개의 중간점(intermediate point)으로 정의되는 3차 베지어 곡선(cubic Bézier curve)으로 모델링된다. 기존 단순 휴리스틱은 이 점들의 반복적 보정에 효과적이지 않으므로, 두 가지 머신러닝 모델을 적용하여 정확한 곡선 보정을 달성한다.

## 주요 기여
1. **VPE(Vertex Placement Error) 메트릭 도입**: 표준 맨해튼 OPC의 EPE를 대체하는 곡선형 전용 정확도 지표 정의
2. **MLP 기반 끝점 위치 결정**: 이전 반복의 VPE와 PFT(Pattern Fidelity Target) 신호를 입력으로 새 끝점 위치를 예측하는 MLP 모델
3. **GCN 기반 VPE 예측기**: Graph Convolutional Network를 이용해 레이아웃 클립 전체의 평균/최대 VPE를 예측
4. **곡률 제약 경사 하강**: 새 끝점 고정 후 곡률 제약을 준수하면서 VPE를 최소화하는 중간점 최적화
5. **제조 가능성 확보**: 곡률 제약 통합으로 마스크 제조 적합성 동시 달성

## 검증 방법론
- VPE 지표를 이용한 곡선형 마스크 보정 정확도 평가
- 기존 휴리스틱 기반 곡선형 OPC 대비 VPE 감소율 측정
- 레이아웃 클립 단위의 GCN VPE 예측 정확도 검증
- MRC(Mask Rule Check) 준수 여부로 제조 가능성 확인

## OPC 툴 구현 관련성
- `skopc/modeling/gnn/` GNN-OPC 모듈에 VPE 메트릭과 곡선형 세그먼트 처리 통합 가능
- 곡선형 마스크 OPC 플로우 구현 시 베지어 곡선 기반 세그먼트 표현으로 전환 시 참고
- GCN 기반 VPE 예측기를 OPC 수렴 판단 기준으로 활용 가능
- 제조 가능성 제약을 OPC 최적화 목적 함수에 포함하는 설계 패턴 제공

## 태그
`Verification`, `IEEE`, `TCAD`, `Curvilinear`, `OPC`, `Machine_Learning`, `GCN`, `Bezier`, `VPE`, `Manufacturability`, `2025`
