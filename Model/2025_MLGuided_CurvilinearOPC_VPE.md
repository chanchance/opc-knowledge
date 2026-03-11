# ML-Guided Curvilinear OPC: Fast, Accurate, and Manufacturable Curve Correction

## 메타데이터
- **저자**: (IEEE Xplore Document 10835245, 저자 상세 접근 필요)
- **연도**: 2025
- **게재지**: IEEE Journals & Magazine (IEEE Xplore)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10835245/

## 핵심 요약
Curvilinear OPC에서 각 세그먼트를 cubic Bézier 곡선(두 끝점 + 두 중간 제어점)으로 모델링하고, 두 가지 ML 모델(MLP + GCN)을 결합하여 곡선 보정을 정확하고 빠르게, 그리고 제조 가능하게 수행하는 방법을 제안한다. VPE(Vertex Placement Error) 기반 정확도 지표를 활용한다.

## 주요 기여
- Cubic Bézier 곡선 기반 curvilinear OPC 세그먼트 표현
- MLP 모델: 새 끝점(endpoint) 위치 예측 - 이전 반복의 VPE와 PFT(Partial Fourier Transform) 신호를 입력으로 활용
- GCN(Graph Convolutional Network) 기반 VPE 예측기: 레이아웃 clip의 평균/최대 VPE 출력
- Gradient descent 최적화로 중간 제어점 위치 결정 (VPE 최소화 + 곡률 제약)
- 속도, 정확도, 제조성(manufacturability) 3요소 동시 개선

## 모델 수식/아키텍처
- Cubic Bézier 세그먼트: B(t) = (1-t)³P₀ + 3(1-t)²tP₁ + 3(1-t)t²P₂ + t³P₃
- MLP 입력: [VPE_prev, PFT_signals] → 출력: 새 끝점 좌표 (Δx, Δy)
- GCN VPE 예측기: 레이아웃 그래프 표현 → VPE 스칼라 예측
- 중간 제어점 최적화: argmin_{P₁,P₂} [VPE_GCN(P₁,P₂) + λ·curvature_penalty]
- VPE(Vertex Placement Error): EPE 대비 곡선 꼭짓점 배치 오차

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드

## OPC 툴 구현 관련성
- SKOPC의 curvilinear OPC 엔진에서 ML 가속 제어점 최적화 방향 제시
- VPE 기반 정확도 지표는 기존 EPE 대비 곡선 OPC 검증에 더 적합
- GCN 기반 VPE 예측기는 OPC 반복 횟수 감소에 활용 가능
- MLP + GCN 하이브리드 구조의 실용적 curvilinear OPC 가속 참조

## 태그
`Model`, `IEEE`, `Curvilinear OPC`, `Machine Learning`, `GCN`, `MLP`, `VPE`, `Bézier`, `Manufacturable`
