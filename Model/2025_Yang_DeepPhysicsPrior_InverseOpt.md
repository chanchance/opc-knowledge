# Deep Physics Prior for First Order Inverse Optimization

## 메타데이터
- **저자**: Haoyu Yang, Kamyar Azizzadenesheli, Haoxing Ren (NVIDIA Research)
- **연도**: 2025
- **게재지/학회**: arXiv:2504.20278 (April 2025)
- **DOI/URL**: https://arxiv.org/abs/2504.20278
- **인용수**: 신규 (2025년 4월 발표)

## 핵심 요약
명시적 수학적 표현이 없는 시스템에서 1차(first-order) gradient 기반 역최적화(inverse optimization)를 가능하게 하는 새로운 방법론 Deep Physics Prior (DPP)를 제안한 논문. 반도체 제조, 구조 공학, 재료 과학, 유체 역학 등 다양한 역설계 문제에 적용된다. 기존 생성형 AI(계산 비용 높음)와 베이즈 최적화(확장성 제한, 노이즈 민감성)의 단점을 극복한다. 역리소그래피(ILT) 응용에서 최신 기법과 비교하여 우수한 결과를 보인다.

## 주요 기여
- 명시적 수식 없는 시스템에서 1차 gradient 역최적화 가능하게 하는 DPP 방법론
- 물리 prior를 딥러닝 surrogate에 내재화하여 gradient 계산 가능
- 생성형 AI와 베이즈 최적화의 한계 극복
- 반도체 제조(ILT), 구조 공학, 재료 과학 등 다분야 검증
- 역리소그래피에서 state-of-the-art 성능 달성

## 모델 아키텍처/수식
**역최적화 문제 정식화:**

순방향 시스템: y = f(x)  (명시적 수식 없음 또는 미분 불가)
역문제: x* = argmin_x L(f(x), y_target)

DPP의 핵심: 미분 가능한 surrogate로 gradient 확보
```
x* ≈ argmin_x L(f̂_θ(x), y_target)
∂L/∂x ≈ ∂L/∂f̂ · ∂f̂/∂x   (surrogate로 gradient 계산)
```

**Deep Physics Prior (DPP) 구조:**

```
물리 시뮬레이터 f(x) → [데이터 수집] → 학습 데이터 {(xᵢ, yᵢ)}
                                        ↓
                              [Physics-informed Surrogate f̂_θ]
                              물리 방정식을 제약 조건으로 사용:
                              L_physics = ||PDE_residual(f̂_θ)||²
                                        ↓
                              [Gradient-based Inverse Optimization]
                              x* = argmin_x L(f̂_θ(x), y_target)
                              using: ∂L/∂x via autograd
```

**Physics Prior 통합:**
- 물리 방정식 잔차(PDE residual) 손실로 surrogate 학습 정규화
- 물리적으로 타당한 해 공간으로 최적화 제약
- 도메인 지식으로 데이터 효율성 향상

**역리소그래피(ILT) 적용:**
순방향 모델: I_wafer = f(mask)  (리소그래피 시뮬레이션)
역문제: mask* = argmin_mask L(f(mask), target_layout)

DPP 적용:
```
f̂_θ(mask) ≈ f(mask)  (TorchLitho-inspired surrogate)
L_litho = ||f̂_θ(mask) - target||² + λ·L_EPE + μ·L_complexity
mask* = mask_0 - α·∂L_litho/∂mask  (gradient descent)
```

**다른 도메인 적용:**
- 구조 공학: 하중 → 변형 역설계
- 재료 과학: 마이크로구조 → 물성 역추정
- 유체 역학: 유동 패턴 → 경계 조건 역추정

**성능 (ILT 벤치마크):**
- EPE: Neural-ILT 2.0 대비 -10% 개선
- PVBand: -12% 개선
- 속도: gradient ILT 대비 50×

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 ILT 최적화 모듈 구현에 핵심 참조. 특히 TorchLitho가 미분 불가능하거나 계산이 느린 경우, DPP의 physics-informed surrogate를 대신 사용하여 gradient 기반 마스크 최적화를 가능하게 한다. SKOPC의 `skopc/modeling/` 내 OPC 최적화 루프에서 surrogate 모델 기반 gradient descent를 구현할 때 이 논문의 방법론 적용 가능.

## 참고문헌 (핵심)
- Raissi, M. et al., "Physics-informed neural networks," J. Comput. Phys. (2019)
- Yang, H. et al., "ILILT," ICML 2024
- Yang, H. et al., "Dual-band optics-inspired NN," DAC 2022
- Chen, G. et al., "Open-source differentiable lithography," arXiv:2409.15306 (2024)
- Snoek, J. et al., "Practical Bayesian optimization of ML algorithms," NeurIPS 2012

## 태그
`Model`, `OPC`, `ILT`, `InverseOptimization`, `DeepPhysicsPrior`, `Surrogate`, `PhysicsInformed`, `GradientBased`, `NVIDIA`, `MultiDomain`, `FirstOrder`, `arXiv`
