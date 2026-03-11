# L2O-ILT: Learning to Optimize Inverse Lithography Techniques

## 메타데이터
- **저자**: B. Zhu, S. Zheng, Z. Yu, G. Chen, Y. Ma, F. Yang, Bei Yu, M.D.F. Wong (CUHK)
- **연도**: 2024
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 43
- **DOI/URL**: https://doi.org/10.1109/TCAD.2023.3323164; PDF: http://www.cse.cuhk.edu.hk/~byu/papers/J103-TCAD2024-L2ILT.pdf
- **인용수**: 40+

## 핵심 요약
ILT 반복 최적화 알고리즘을 학습 가능한 신경망으로 전개(unroll)하는 L2O(Learning to Optimize) 기반 역리소그래피 프레임워크를 제안한 논문. ILT의 반복 갱신 단계를 신경망 레이어로 매핑하여 해석 가능한(interpretable) 구조를 유지하면서 학습으로 ILT 파라미터를 최적화한다. 교대 최적화(alternating optimization) 메커니즘과 적응형 해 공간(adaptive solution space) 방법으로 기존 ILT 알고리즘을 개선하며, 마스크 프린팅 가능성과 처리 속도 모두에서 이전 방법을 능가한다.

## 주요 기여
- ILT 반복 알고리즘을 학습 가능한 신경망으로 전개 (algorithm unrolling)
- 교대 최적화 메커니즘으로 수렴 속도 향상
- 적응형 해 공간(adaptive solution space) 방법 개발
- 높은 해석 가능성(interpretability): 각 레이어가 ILT 반복 단계에 대응
- 마스크 프린팅 가능성과 런타임 모두 이전 최신 방법 능가

## 모델 아키텍처/수식
**Algorithm Unrolling 개념:**

기존 ILT gradient descent 반복:
```
M_{k+1} = M_k - α_k · ∇_M L(M_k)
         = M_k - α_k · (∂L_print/∂M + λ·∂L_complexity/∂M)
```

L2O-ILT는 이를 신경망 레이어로 전개:
```
Layer k: M_{k+1} = f_θₖ(M_k, ∇_M L(M_k), h_k)
```
여기서:
- θₖ: k번째 레이어 학습 파라미터
- h_k: 보조 상태(hidden state, LSTM-like)
- f_θₖ: 학습 가능한 갱신 규칙

**L2O-ILT 전체 구조:**
```
Input: 타겟 레이아웃 Z
  ↓
M_0 = Initialize(Z)   (간단한 초기화)
  ↓
for k = 1, ..., L:
    grad_k = ∇_M L_litho(M_{k-1}, Z)
    M_k = M_{k-1} - α_k(grad_k, h_k)  ← 학습 가능한 스텝 크기
    h_k = LSTM(grad_k, h_{k-1})        ← 히스토리 정보
  ↓
M* = M_L → binarize → final mask
```

**교대 최적화 메커니즘:**
마스크 M을 주 변수와 보조 변수로 분리:
```
Phase 1: min_M L_litho(M, Z) s.t. M ∈ C_mask  (프린팅 최적화)
Phase 2: min_M L_complexity(M) s.t. L_litho ≤ ε  (복잡도 최소화)
```
교대 반복으로 두 목표 균형 달성

**적응형 해 공간:**
```
ΔM_max(k) = ΔM_max,0 · decay^k  (반복마다 탐색 범위 감소)
M_{k+1} = M_k + clip(L2O_update, -ΔM_max(k), +ΔM_max(k))
```

**리소그래피 손실:**
```
L_litho = ||sigmoid(Litho(M)/α - T) - Z||²
        + λ_PVB · PVBand(M, Z)
```

**학습:**
- 지도 학습: L2O 파라미터를 ILT 결과 마스크로 학습
- 메타 학습: 다양한 레이아웃에서 빠른 수렴을 위한 파라미터 학습

**성능 (ICCAD 2013):**
- EPE: Neural-ILT 2.0 대비 -12% 개선
- PVBand: -15% 개선
- 속도: 수치 ILT 대비 50× 향상

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 세그먼트 변위 예측에 algorithm unrolling 접근법 적용 가능. 현재 GNN이 단일 순전파로 변위를 예측하는 것과 달리, L2O 방식으로 여러 단계의 반복 개선을 신경망으로 구현하면 더 정확한 수렴이 가능. LSTM 기반 히스토리 정보 활용은 SKOPC OPC 루프의 다중 반복(multiple correction pass)에서 이전 상태 정보를 활용하는 방향으로 참조. 해석 가능성(interpretability)은 SKOPC 산업 배포 시 중요한 요건.

## 참고문헌 (핵심)
- Andrychowicz, M. et al., "Learning to learn by gradient descent by gradient descent (L2O)," NeurIPS 2016
- Liu, X. et al., "Neural-ILT 2.0," TCAD 2022
- Yang, H. et al., "GAN-OPC," DAC 2018
- Gregor, K. and LeCun, Y., "Learning fast approximations of sparse coding (LISTA)," ICML 2010

## 태그
`Model`, `OPC`, `ILT`, `L2O`, `LearningToOptimize`, `AlgorithmUnrolling`, `LSTM`, `Interpretable`, `TCAD`, `CUHK`, `AlternatingOptimization`, `AdaptiveSolutionSpace`
