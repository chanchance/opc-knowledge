# L2O-ILT: Learning to Optimize Inverse Lithography Techniques

## 메타데이터
- **저자**: Su Zheng, Haoyu Yang, Haoxing Ren, Bei Yu (추정 - CUHK / NVIDIA)
- **연도**: 2024
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 43, Issue 3, March 2024
- **DOI/URL**: https://ieeexplore.ieee.org/document/10275084/ / https://dl.acm.org/doi/abs/10.1109/TCAD.2023.3323164
- **인용수**: 30+

## 핵심 요약
L2O-ILT는 ILT 반복 최적화 알고리즘을 학습 가능한 신경망으로 전개(unroll)하여 높은 해석 가능성을 유지하면서 고품질 초기 마스크를 생성하는 프레임워크다. ILT 알고리즘을 레이어로 스태킹하여 신경망을 구성하고, L2O-ILT를 통과하는 것은 반복 ILT 알고리즘을 실행하는 것과 동등하다. 교번 최적화 메커니즘과 적응적 솔루션 공간 방법으로 기존 ILT 알고리즘을 개선하고, 빠른 정제를 위한 고품질 초기 해를 제공한다.

## 주요 기여
- **알고리즘 전개(Unrolling) 신경망**: ILT 반복 알고리즘을 레이어로 전개한 해석 가능한 신경망
- **교번 최적화 메커니즘**: 마스크와 보조 변수를 교대로 최적화하는 개선된 ILT 알고리즘
- **적응적 솔루션 공간**: 최적화 중 솔루션 공간을 동적으로 조정하여 수렴 향상
- **고품질 초기해 생성**: 빠른 정제가 가능한 근-최적 초기 마스크 제공

## Recipe/Process Flow 상세

### L2O-ILT 알고리즘 전개 파이프라인

```
기존 ILT 알고리즘 (반복 구조):
  t=0: M_0 = 타겟 레이아웃 (초기화)
  t=1: M_1 = M_0 - α∇L(M_0)  ← 1회 경사 하강
  t=2: M_2 = M_1 - α∇L(M_1)  ← 2회 경사 하강
  ...
  t=K: M_K = 수렴된 최적 마스크

L2O-ILT 신경망 전개:
  각 반복 단계 t를 학습 가능한 레이어로 변환:
  M_{t+1} = Layer_t(M_t, T)
           = M_t - α_t(θ) · ∇L_t(M_t; θ_t)
  - α_t(θ): 학습 가능한 스텝 크기 (반복마다 다를 수 있음)
  - L_t(·; θ_t): 학습 가능한 손실 함수 파라미터
  - θ: 신경망 전체 파라미터
```

### 교번 최적화 메커니즘 (Alternating Optimization)

```
변수 분리: M = M_cont (연속) + M_bin (이진화 제약)

교번 단계:
Step A: M_cont 최적화 (연속 마스크)
  M_cont^{t+1} = argmin_{M} L_litho(F(M), T) + λ||M - M_bin^t||²

Step B: M_bin 업데이트 (이진화)
  M_bin^{t+1} = threshold(M_cont^{t+1})
  또는 소프트 임계화: σ(k · M_cont^{t+1})

교번 반복: A → B → A → B → ...
```

### 적응적 솔루션 공간 방법
최적화 중 솔루션 공간을 동적으로 조정:
- **확장 단계**: 수렴 초기에 넓은 솔루션 공간 탐색
- **수축 단계**: 수렴 후기에 좁은 공간에서 정밀 최적화
- **적응 조건**: 손실 함수 변화율에 따른 자동 조정

### 신경망 레이어 구조
각 전개 레이어의 구성:
```
Layer_t:
  입력: (M_t, T, 이전 보조 변수)
  처리:
    1. 현재 마스크의 리소그래피 손실 계산
    2. 학습 가능한 스텝 크기로 그래디언트 스텝
    3. 교번 최적화로 이진화 제약 처리
    4. 적응적 솔루션 공간 업데이트
  출력: (M_{t+1}, 업데이트된 보조 변수)

K개 레이어 스태킹 = K회 반복 ILT
```

### 학습 전략
- 레이블: 수치 ILT가 생성한 최적 마스크 M*
- 손실: ||M_K(θ) - M*||² + L_litho(M_K(θ), T)
- 학습: 역전파로 θ 최적화 (암묵적 미분 불필요)
- 훈련된 후: 단일 순전파로 고품질 초기 마스크 생성

### 성능 결과
- 마스크 인쇄 품질: 기존 방법 대비 향상
- 런타임: 고품질 초기해로 후속 정제 반복 대폭 감소
- 해석 가능성: ILT 알고리즘과 1-1 대응되는 레이어 구조

## OPC 툴 구현 관련성
L2O-ILT의 알고리즘 전개 접근법은 SKOPC GNN-OPC에 직접 응용 가능:
- **GNN-OPC 알고리즘 전개**: SKOPC의 반복적 모델 OPC를 L2O-ILT 방식으로 신경망으로 전개
- **학습 가능한 OPC 파라미터**: 스텝 크기, 세그먼트 이동 한계를 고정값 대신 학습
- **교번 최적화**: GNN-OPC의 연속 이동 최적화와 이진화 제약을 교번으로 처리
- **초기해 제공**: GNN-OPC 추론 결과를 수치 OPC의 고품질 초기 마스크로 활용

## 참고문헌 (핵심)
- Jiang et al., "Neural-ILT" (ICCAD 2020)
- Chen et al., "DevelSet" (ICCAD 2021)
- Yang & Ren, "ILILT" (ICML 2024)
- Andrychowicz et al., "Learning to learn by gradient descent by gradient descent" (NeurIPS 2016) - L2O 원조

## 태그
`L2O-ILT`, `Algorithm Unrolling`, `Learning to Optimize`, `ILT`, `OPC`, `Alternating Optimization`, `IEEE TCAD`, `2024`, `CUHK`, `Interpretable`, `Initial Mask`
