# Intelligent Model-Based OPC

## 메타데이터
- **저자**: W.C. Huang, C.M. Lai, B. Luo, C.K. Tsai, M.H. Chih, C.W. Lai, C.C. Kuo, R.G. Liu, H.T. Lin
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX, 615436
- **DOI/URL**: https://doi.org/10.1117/12.657792
- **인용수**: ~60

## 핵심 요약
단일 은닉층 신경망을 이용해 레이아웃 세그먼트의 OPC 바이어스를 예측하여 모델 기반 OPC를 가속화하는 초기 신경망 기반 OPC 연구. 세그먼트 길이와 제어 포인트에서의 강도를 특성으로 학습하여 최적 RMS 오차 1.29nm를 달성하고 OPC 이터레이션을 27.0% 감소시킨다.

## 주요 기여
1. 최초의 신경망 기반 OPC 바이어스 예측 방법론 (초기 연구)
2. 세그먼트 길이와 강도 기반 신경망 피처 설계
3. 학습된 초기 바이어스로 OPC 이터레이션 27% 감소
4. 최적 RMS 오차 1.29nm 달성

## Recipe/Process Flow 상세

### 신경망 기반 OPC 바이어스 예측
```
기존 Model-Based OPC:
- 초기 바이어스: 0 또는 경험값
- 이터레이션 1~N: EPE 기반 반복 보정
- 수렴: 8~12 이터레이션 필요

지능형 OPC (신경망 초기화):
- 신경망으로 초기 바이어스 예측 (OPC 시작 전)
- 예측된 바이어스로 시작 → 이터레이션 감소
```

### 신경망 구조
```
입력 피처:
  x1 = 세그먼트 길이 (segment length)
  x2...xN = 제어 포인트에서의 광학 강도 (intensities at control points)

신경망:
  입력층: N 노드
  은닉층: M 노드 (단일 은닉층)
  출력층: 1 노드 (OPC 바이어스 예측값)

활성화 함수: sigmoid (은닉층), linear (출력층)

훈련:
  Ground Truth: 수렴된 OPC 결과의 최종 바이어스
  손실: MSE(예측 바이어스, 실제 바이어스)
  알고리즘: Backpropagation
```

### 훈련 데이터 구성
```
패턴 유형: 1D 라인-스페이스 (다양한 pitch/CD)
피처 추출:
  - 각 세그먼트에서 제어 포인트 강도 계산
  - 광학 모델 (Hopkins) 기반 강도 계산
레이블: 수렴된 OPC 최종 세그먼트 바이어스
훈련/테스트 분리로 일반화 성능 검증
```

### 성능 결과
```
RMS 오차: 1.29 nm (최적)
이터레이션 감소: 27.0%
  기존: 8~12 이터레이션
  신경망 초기화: ~6~9 이터레이션
런타임 절감: 이터레이션 감소에 비례
```

### 역사적 의의
- 2006년 발표 — GAN-OPC(2020), DiffOPC(2024) 등 현대 ML-OPC의 원시 선구 연구
- 단순한 단층 신경망으로도 OPC 초기화 개선 가능함을 최초 입증
- "세그먼트 강도 피처" 개념은 이후 GNN-OPC의 노드 피처 설계에 영향

## OPC 툴 구현 관련성
- **SKOPC GNN-OPC 역사적 배경**: `skopc/modeling/gnn/` ResGNN의 이론적 원점
- **세그먼트 피처 설계**: 강도 기반 세그먼트 피처는 현대 GNN 노드 피처의 전신
- **이터레이션 초기화**: 신경망 예측 초기값으로 수렴 가속은 현재도 유효한 전략
- **TSMC 출처**: 대만 TSMC 연구팀의 초기 ML-OPC 적용 사례

## 참고문헌
- Proc. SPIE 6154, Optical Microlithography XIX (2006)
- 저자 소속: TSMC (Taiwan Semiconductor Manufacturing Company)
- 특허: US20070143234A1 — Method and system for intelligent model-based OPC
- 관련: GNN-OPC (skopc/modeling/gnn/), GAN-SRAF(2020)

## 태그
`Recipe`, `SPIE`, `NeuralNetwork`, `ModelBasedOPC`, `BiasPredictor`, `IterationReduction`, `HistoricalReference`, `TSMC`, `EarlyML-OPC`
