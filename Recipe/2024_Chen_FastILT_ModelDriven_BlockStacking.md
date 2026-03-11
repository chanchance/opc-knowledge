# Fast Inverse Lithography Based on a Model-Driven Block Stacking Convolutional Neural Network

## 메타데이터
- **저자**: Ruixiang Chen, Yang Zhao, Haoqin Li, Rui Chen
- **연도**: 2024 (Optics Express 2025 게재)
- **게재지/학회**: Optics Express, Vol. 33, No. 8, p. 18404 / arXiv:2412.14599
- **DOI/URL**: https://arxiv.org/abs/2412.14599
- **인용수**: N/A (2024/2025 신규)

## 핵심 요약
본 논문은 벡터 리소그래피 모델링을 기반으로 한 모델 구동(model-driven) 블록 스태킹 CNN을 제안하여 역리소그래피 기반 OPC의 마스크 생성을 가속화한다. 방대한 레이블 데이터셋 없이 비지도 학습으로 훈련 가능하며, 파동 함수 붕괴(Wave Function Collapse) 알고리즘으로 훈련 패턴 다양성을 극대화한다. 엔드-투-엔드 방식으로 마스크 복잡도를 관리하면서 실제 제조 환경의 경제적 실용성을 향상시킨다.

## 주요 기여
- **모델 구동 블록 스태킹 CNN**: 물리 리소그래피 모델을 CNN 구조에 직접 내재화한 비지도 학습 프레임워크
- **벡터 리소그래피 모델 기반**: 레이블 데이터 불필요한 훈련, 리소그래피 물리로 지도
- **WFC 패턴 다양성**: Wave Function Collapse 알고리즘으로 다양한 목표 패턴 자동 생성
- **마스크 복잡도 관리**: 제조 가능성과 인쇄 품질의 균형적 최적화

## Recipe/Process Flow 상세

### 모델 구동 블록 스태킹 CNN 파이프라인

```
[WFC 패턴 생성기]
  Wave Function Collapse 알고리즘:
  - 제약 전파(Constraint Propagation)로 타일 패턴 조합
  - 설계 규칙을 제약 조건으로 반영
  - 무작위하지만 현실적인 레이아웃 패턴 자동 생성
  → 다양한 타겟 패턴 T 생성
        ↓
[모델 구동 블록 스태킹 CNN]
  블록 스태킹 구조:
  ┌─────────────────────────────────┐
  │ Block 1: 벡터 리소그래피 시뮬레이션  │
  │  - 물리 기반 이미징 레이어          │
  │  - 수치 미분 없는 직접 모델 내장     │
  │                                  │
  │ Block 2: 마스크 예측               │
  │  - CNN으로 역문제 근사             │
  │  - 잔차 연결(Residual Connection)  │
  │                                  │
  │ Block 3: 복잡도 정규화             │
  │  - 마스크 복잡도 패널티 내장         │
  │  - 제조 가능성 제약 반영            │
  └─────────────────────────────────┘
        ↓
[비지도 학습 (Unsupervised Training)]
  손실 함수 (레이블 없이 물리 모델로만 계산):
  L = ||F(M_pred) - T||² + λ·Complexity(M_pred)
  - F: 벡터 리소그래피 순방향 모델
  - T: WFC로 생성된 타겟 패턴 (레이블)
  → ILT 정답 마스크 불필요
        ↓
[추론 (고속 마스크 생성)]
  새 타겟 T → CNN 순전파 → 최적화 마스크 즉시 출력
```

### 벡터 리소그래피 모델링 상세
전통적인 스칼라 이미징 모델 대신 벡터(편광) 효과 포함:
- 고 NA 시스템에서의 편광 효과 모델링
- TM/TE 편광 성분 분리 계산
- 3D 마스크 효과 근사 포함

리소그래피 이미지 (벡터 모델):
$$I(x,y) = |E_x(x,y)|^2 + |E_y(x,y)|^2$$

여기서 $E_x, E_y$는 전기장의 x, y 성분

### WFC(Wave Function Collapse) 패턴 생성
게임 맵 생성 알고리즘을 레이아웃 패턴 생성에 적용:
1. **타일 정의**: 반도체 레이아웃의 기본 패턴 단위 정의
2. **제약 설정**: 설계 규칙(DRC)을 타일 간 연결 제약으로 변환
3. **엔트로피 기반 선택**: 가장 낮은 엔트로피 셀부터 무작위 타일 배정
4. **제약 전파**: 인접 셀로 제약 조건 전파
5. **반복**: 전체 그리드가 결정될 때까지 반복

**장점**:
- 설계 규칙 준수하는 현실적 패턴 생성
- 훈련 데이터 무한 생성 가능
- 패턴 다양성 극대화 (over-fitting 방지)

### 모델 구동 설계의 이점
- **물리 정합성**: CNN이 리소그래피 물리 법칙 위반 솔루션 생성 방지
- **레이블 불필요**: ILT 최적 마스크 ground truth 없이 학습
- **일반화**: 새로운 패턴 유형에 강건한 일반화 능력
- **블록 재사용**: 다른 리소그래피 파라미터에 맞게 블록 교체 가능

### 성능 결과
- 엔드-투-엔드 고속 마스크 생성
- 마스크 복잡도 관리에서 전통 수치 OPC 대비 향상
- 실제 제조 경제성 개선 입증

## OPC 툴 구현 관련성
TPM-RET와 상보적으로 SKOPC에 적용 가능:
- **비지도 GNN 학습**: SKOPC GNN-OPC를 벡터 리소그래피 손실로 비지도 학습하는 전략 참조
- **WFC 데이터 생성**: SKOPC 학습 데이터 생성에 WFC 알고리즘 도입으로 패턴 다양성 향상
- **블록 스태킹 아키텍처**: GNN-OPC의 물리 모듈과 학습 모듈을 블록으로 구분하는 설계 참조
- **벡터 리소그래피**: EUV/고 NA 레시피 구현 시 TorchLitho에 벡터 모델 추가

## 참고문헌 (핵심)
- Gutowitz, "Cellular Automata" (1990) - WFC 알고리즘 기반
- Karth & Smith, "WaveFunctionCollapse is constraint solving in the wild" (2017)
- Chen et al., "DiffOPC" (ICCAD 2024)
- TorchLitho (SPIE 2024)
- Yang et al., "GAN-OPC" (IEEE TCAD 2020)

## 태그
`Fast ILT`, `Model-driven`, `Block Stacking CNN`, `Wave Function Collapse`, `Vector Lithography`, `Unsupervised`, `OPC`, `Mask Complexity`, `Optics Express`, `2024`, `Pattern Generation`
