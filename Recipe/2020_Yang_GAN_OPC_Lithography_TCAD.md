# GAN-OPC: Mask Optimization with Lithography-Guided Generative Adversarial Nets

## 메타데이터
- **저자**: Haoyu Yang, Shuhe Li, Zihao Deng, Yuzhe Ma, Bei Yu, Evangeline F.Y. Young
- **연도**: 2018 (DAC 발표), 2020 (IEEE TCAD 확장)
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 39, No. 10, pp. 2822-2834 (2020); 최초 발표 DAC 2018
- **DOI/URL**: https://ieeexplore.ieee.org/document/8823939
- **인용수**: ~120

## 핵심 요약
리소그래피 시뮬레이터를 가이던스로 활용하는 GAN(Generative Adversarial Network) 기반 OPC 마스크 최적화 방법론인 GAN-OPC를 제안한다. 타겟 회로 패턴에서 최적 마스크로의 직접 매핑을 학습하는 생성기(generator)를 ILT와 결합하여 사전 훈련하고, 리소그래피 시뮬레이터를 판별기(discriminator)로 활용하여 준최적 마스크를 생성한다. 표준 OPC 이터레이션 수를 크게 줄이면서 동등하거나 우수한 마스크 품질을 달성한다.

## 주요 기여
1. 리소그래피 시뮬레이터 가이드 GAN을 OPC 마스크 합성에 최초 적용
2. ILT 사전 훈련으로 GAN 수렴 안정화 및 초기화 개선
3. 준최적 마스크 직접 생성으로 표준 OPC 이터레이션 수 대폭 감소
4. CUHK-Bei Yu 그룹의 공개 데이터셋 (~4000 설계) 기여

## Recipe/Process Flow 상세

### GAN-OPC 프레임워크
```
표준 GAN 구조:
  생성기(G): 잠재 벡터 → 합성 이미지
  판별기(D): 진짜/가짜 분류
  학습: 생성기와 판별기 간 min-max 게임

GAN-OPC 맞춤 구조:
  생성기(G): 타겟 패턴 → 마스크 (타겟-마스크 매핑 학습)
  판별기/가이던스:
    방법 1: 별도 판별기 (진짜 OPC 결과 vs. GAN 생성 마스크)
    방법 2: 리소그래피 시뮬레이터 (마스크 → 웨이퍼 이미지 품질)

  핵심 아이디어:
    G(target) = mask ≈ optimal_OPC_mask(target)
    훈련 후: 새 타겟 → G로 직접 준최적 마스크 생성
```

### ILT 사전 훈련 (Pre-training)
```
GAN 직접 훈련의 문제:
  - 마스크 공간 고차원 → 훈련 불안정
  - 최적 마스크 ground truth 부족

ILT 사전 훈련 전략:
  1단계: ILT로 각 타겟에 대한 기준 마스크 생성
    M_ILT = argmin ||I(M) - I_target||² + λ||M||

  2단계: 지도학습으로 G 사전 훈련
    G를 (target, M_ILT) 쌍으로 훈련
    → G가 ILT 마스크 근사 학습

  3단계: GAN 파인 튜닝
    G를 리소그래피 가이던스로 최적화
    → ILT보다 향상된 마스크 생성

사전 훈련 이점:
  - 훈련 안정성 향상
  - 더 빠른 수렴
  - 지역 최솟값 회피
```

### 리소그래피 가이던스 학습
```
손실 함수:
  L_total = L_pixel + λ_litho × L_litho + λ_GAN × L_GAN

  L_pixel: 마스크 픽셀 레벨 유사도 (MSE)
  L_litho: 리소그래피 시뮬레이션 기반 EPE 손실
    L_litho = ||I(G(target)) - I_target||²
  L_GAN: 표준 GAN adversarial 손실

리소그래피 시뮬레이터 통합:
  - 미분 가능한 리소그래피 시뮬레이터 필요
    → PyTorch 기반 Hopkins 광학 모델 + 레지스트 모델
    → 역전파 가능 → G의 그래디언트 직접 계산

마스크 이진화:
  G 출력: 연속 [0,1] → 이진 마스크 변환
  방법: Hard sigmoid + STE (Straight-Through Estimator)
  또는 sigmoid relaxation
```

### 마스크 생성 및 OPC 통합
```
추론 단계:
  새 타겟 패턴 → G(target) → 준최적 초기 마스크
  → 표준 OPC로 잔여 보정 (소수 이터레이션)

성능 비교:
  GAN-OPC 단독: 준최적 마스크, OPC 없이
  GAN-OPC + 표준 OPC (3-5 iter): 최고 품질
  표준 OPC (10-15 iter): 기준

GAN-OPC 장점:
  - 초기 마스크 품질: ILT와 유사하거나 향상
  - 추론 속도: ms 수준 (ILT의 수천 배 빠름)
  - OPC 이터레이션 감소 → 전체 TAT 단축
```

### 공개 데이터셋 기여
```
GAN-OPC 데이터셋:
  GitHub: github.com/phdyang007/GAN-OPC
  규모: ~4000 설계 클립
  형식: 타겟 패턴 + 최적 마스크 (GT) 쌍
  용도: ML-OPC 연구의 표준 벤치마크

후속 연구에 활용:
  - DevelSet, Neural-ILT, CF-ILT 등 많은 후속 ML-OPC 연구
  - OpenILT 플랫폼에 통합
```

### 성능 결과
```
마스크 품질 (L2 norm, EPE):
  GAN-OPC: ILT 대비 동등하거나 개선
  특히 복잡한 2D 패턴에서 우수

런타임:
  ILT: 클립당 수 초~수 분
  GAN-OPC 추론: ms 수준 (~1000× 빠름)
  GAN-OPC + 3 OPC iter: 표준 OPC 10 iter보다 빠름
```

## OPC 툴 구현 관련성
- **SKOPC GNN-OPC 대안**: `skopc/modeling/gnn/` GNN 대신 GAN-OPC 아키텍처로 마스크 직접 생성
- **미분 가능 시뮬레이터**: `skopc/core/litho_engine.py`를 PyTorch 자동 미분으로 래핑 (L_litho 계산)
- **OpenILT 연동**: GAN 사전 훈련에 openilt_adapter.py의 ILT 결과 활용
- **공개 데이터셋**: GAN-OPC 데이터셋으로 SKOPC ML 모델 초기 훈련 가능

## 참고문헌
- IEEE TCAD 39(10), 2822-2834 (2020); DAC 2018
- 저자 소속: CUHK (Bei Yu group)
- 관련: GAN-based SRAF generation (TCAD 2020) — 동일 그룹
- 관련: DevelSet: Deep Neural Level Set for mask optimization (ICCAD 2021)
- 관련: Neural-ILT: reformulating ILT as neural network (ICCAD 2020)

## 태그
`Recipe`, `IEEE`, `TCAD`, `GAN`, `ML-OPC`, `MaskOptimization`, `GenerativeAdversarialNetwork`, `ILT`, `DeepLearning`, `CUHK`, `BeiYu`, `DAC`, `2020`
