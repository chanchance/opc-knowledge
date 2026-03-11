# Neural Network Classifier-Based OPC With Imbalanced Training Data

## 메타데이터
- **저자**: (IEEE document 8332490 - 2018 IEEE TCAD)
- **연도**: 2018
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/8332490/
- **인용수**: ~60

## 핵심 요약
신경망 분류기(NNC)를 마스크 바이어스 모델로 활용하는 NNC-OPC 프레임워크를 제안한다. 훈련 세그먼트는 마스크 바이어스 범위에서 불균형(imbalanced)하여 희귀 바이어스 세그먼트의 예측 오차가 크다는 문제를 해결하기 위해 합성 데이터 생성과 클래스 재구성의 두 가지 기법을 제안한다. 회귀 방법 대비 예측 오차 29%, 훈련 시간 80% 감소를 달성한다.

## 주요 기여
1. NNC(Neural Network Classifier)를 OPC 마스크 바이어스 예측 모델로 활용
2. 불균형 훈련 데이터 문제 해결: 합성 데이터 생성(synthetic data generation)
3. 클래스 재구성(class reorganization)으로 분류 정확도 향상
4. 기존 회귀 기반 ML-OPC 대비 예측 오차 29%, 훈련 시간 80% 감소

## Recipe/Process Flow 상세

### NNC-OPC 프레임워크
```
기존 회귀 기반 ML-OPC:
  세그먼트 피처 → 회귀 모델 → 연속적 마스크 바이어스 예측

NNC 기반 OPC (분류 접근):
  세그먼트 피처 → 분류기 → 이산 바이어스 클래스 → 마스크 바이어스

클래스 정의:
  마스크 바이어스 범위를 K개 이산 클래스로 분할
  예: [-20nm, +20nm] → K=40 클래스 (1nm 간격)
```

### 불균형 데이터 문제 및 해결책
```
문제: 불균형 훈련 데이터
────────────────────────
실제 레이아웃에서 마스크 바이어스 분포:
  - 대부분 세그먼트: 중간 바이어스 범위 (빈도 높음)
  - 일부 세그먼트: 극단 바이어스 (빈도 낮음)
  → 빈도 낮은 클래스에서 예측 오차 큼

해결책 1: 합성 데이터 생성 (Synthetic Data Generation)
─────────────────────────────────────────────────────────
- 소수 클래스에서 보간/외삽으로 합성 샘플 생성
- SMOTE(Synthetic Minority Over-sampling TEchnique) 유사 방법
- 클래스 간 샘플 수 균형화

해결책 2: 클래스 재구성 (Class Reorganization)
─────────────────────────────────────────────────
- 유사한 물리적 특성을 가진 클래스를 병합
- 바이어스 범위에 따라 비균일 클래스 간격 설정
  * 중간 바이어스: 좁은 간격 (세밀한 분류)
  * 극단 바이어스: 넓은 간격 (병합)
- 효과적 클래스 수 감소로 훈련 안정성 향상
```

### NNC 아키텍처 및 훈련
```
입력 피처:
  - 세그먼트 길이, 위치
  - 제어 포인트에서의 광학 강도
  - 이웃 세그먼트 정보

신경망:
  - 다층 퍼셉트론 (MLP) 또는 CNN
  - 출력: K개 클래스 소프트맥스 확률

훈련:
  - 교차 엔트로피 손실 (불균형 가중치 적용)
  - 합성 데이터 포함된 균형화된 배치

추론:
  - argmax(softmax) → 예측 클래스 → 마스크 바이어스
```

### 성능 결과
```
기존 회귀 ML-OPC 대비:
  예측 오차 감소: 29%
  훈련 시간 감소: 80%
  이터레이션 감소: 불균형 처리로 수렴 가속

특히 효과적: 극단 바이어스가 필요한 핫스팟 구조
```

## OPC 툴 구현 관련성
- **SKOPC GNN-OPC 확장**: `skopc/modeling/gnn/` ResGNN을 분류기로 변환하거나 불균형 처리 기법 적용 가능
- **훈련 데이터 균형화**: OPC 훈련 데이터 생성 시 바이어스 분포 불균형 처리 필수
- **합성 데이터 전략**: 극단 보정이 필요한 패턴(핫스팟)에 대한 훈련 데이터 증강
- **속도-정확도 균형**: 분류기 기반 접근으로 회귀 대비 훈련 속도 대폭 향상

## 참고문헌
- IEEE TCAD 2018, Document 8332490
- 관련: Intelligent model-based OPC (SPIE 6154, 2006)
- 관련: Subresolution Assist Feature Generation With Supervised Data Learning (IEEE TCAD, 2018)

## 태그
`Recipe`, `IEEE`, `TCAD`, `NeuralNetwork`, `Classifier`, `ImbalancedData`, `SyntheticData`, `ML-OPC`, `MaskBias`, `TrainingData`
