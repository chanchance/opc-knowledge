# Accurate Etch Modeling with Massive Metrology and Deep-Learning Technology

## 메타데이터
- **저자**: Lu, Y., Zhao, Y., Li, M. et al. (TSMC / Synopsys)
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical and EUV Nanolithography XXXIII
- **DOI/URL**: https://doi.org/10.1117/12.2552001
- **인용수**: ~45

## 핵심 요약
첨단 노드에서 복잡해진 에칭 거동을 대규모 자동화 메트롤로지 데이터와 딥러닝 기술을 결합하여 정밀하게 모델링하는 방법론을 제시한다. 기존 규칙 기반 OPC 보정의 한계를 극복하기 위해 수만 개의 게이지 측정값을 대규모로 수집하고, 딥러닝 에칭 모델로 복잡한 에칭 패턴 의존 거동을 학습한다. 실제 양산 환경에서 에칭 모델 정확도를 대폭 향상시킴을 실증한다.

## 주요 기여
1. 대규모 자동화 CD-SEM 메트롤로지(수만 개 게이지)를 활용한 에칭 모델 학습 데이터 생성
2. 딥러닝 에칭 모델이 복잡한 비선형 에칭 패턴 의존성 학습
3. 기존 항(term) 기반 에칭 모델 대비 RMS 오차 50% 이상 감소
4. 대규모 데이터 수집을 위한 자동화 메트롤로지 파이프라인 구축
5. 전체 칩 OPC 플로우에서 딥러닝 에칭 모델 통합 가능성 실증

## 모델 수식/아키텍처

**딥러닝 에칭 모델 입력 특성:**
```
x_i = [CD_litho, pitch, orientation, aspect_ratio,
        density_r1, density_r2, density_r3,    # 다중 반경 패턴 밀도
        CD_neighbors, gap_neighbors,             # 인접 패턴 정보
        image_NILS, image_slope, image_curvature # 공중상 특성
        ]
```

**딥러닝 모델 아키텍처:**
```
Input → FC(256) → BN → ReLU
      → FC(256) → BN → ReLU
      → FC(128) → BN → ReLU
      → FC(64)  → ReLU
      → FC(1)   → etch_bias output
```
BN = Batch Normalization

**학습 데이터 파이프라인:**
```
Layout → 자동 게이지 배치
       → 리소 노광 (ArF immersion)
       → 에칭 공정
       → 자동 CD-SEM 측정 (수만 포인트)
       → etch_bias = CD_etch - CD_litho
       → 딥러닝 학습 데이터셋 구성
```

**손실 함수:**
```
L = MSE(etch_bias_pred, etch_bias_meas) + λ_L2·||W||²
```

**성능 지표:**
```
RMS_term_based: ~2.0nm
RMS_DL: ~0.9nm   (55% 감소)
Coverage_3σ: term 85% → DL 97%
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [x] ML/DL (딥러닝 에칭 모델)
- [x] 하이브리드 (대규모 데이터 + 딥러닝)

## OPC 툴 구현 관련성
- skopc 에칭 모델 모듈: 딥러닝 MLP 에칭 모델 구현 핵심 참조
- 대규모 메트롤로지 자동화: 수천~수만 게이지 자동 측정 인프라 필요
- 다중 반경 밀도 맵 계산: 에칭 모델 입력 특성 공학의 핵심
- 배치 정규화(BN): 에칭 게이지 분포 편향 처리에 효과적
- TSMC 첨단 노드(7nm/5nm) 양산 적용 사례

## 참고문헌
- Lafferty, N. et al., "Etch kernels for etch bias prediction" (2018)
- Hooker, K. et al., "ML etch models in OPC and ILT" (2021)
- Shang, S. et al., "Etch proximity correction by retargeting" (2007)

## 태그
`Model`, `SPIE`, `EtchModel`, `DeepLearning`, `MassiveMetrology`, `OPC`, `Calibration`, `TSMC`, `2020`
