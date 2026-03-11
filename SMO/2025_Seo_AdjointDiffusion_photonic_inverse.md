# Physics-Guided and Fabrication-Aware Inverse Design of Photonic Devices Using Diffusion Models (AdjointDiffusion)

## 메타데이터
- **저자**: Dongjin Seo, Soobin Um, Sangbin Lee, Jong Chul Ye, Haejun Chung
- **연도**: 2025
- **게재지/학회**: arXiv:2504.17077 (physics.optics / cs.AI / physics.comp-ph)
- **DOI/URL**: https://arxiv.org/abs/2504.17077
- **인용수**: 신규 논문 (오픈소스 구현 제공)

## 핵심 요약
Adjoint 감도 그래디언트를 확산 모델(diffusion model)의 샘플링 과정에 통합하는 AdjointDiffusion 프레임워크를 제안한 논문. 제조 인식 합성 데이터로 훈련된 확산 네트워크가 각 디노이징 단계에서 물리 기반 adjoint 그래디언트 유도를 받아 고성능·제조 가능한 포토닉 소자를 생성한다. 순수 딥러닝 대비 100,000-1,000,000배 적은 시뮬레이션(약 200회)으로 MMA, SLSQP 등 비선형 최적화기보다 우수한 성능을 달성한다.

## 주요 기여
- Adjoint 감도 그래디언트와 확산 모델 샘플링의 최초 통합 (AdjointDiffusion)
- 제조 인식 이진 마스크 데이터셋으로 확산 네트워크 훈련
- 복잡한 이진화 스케줄 없이 제조성 자연스럽게 유지
- 시뮬레이션 횟수 ~200회 (순수 DL의 100만 분의 1)
- 벤트 도파관, CMOS 이미지 센서 컬러 라우터 검증
- MMA, SLSQP 등 기존 비선형 최적화기 성능 초월

## 알고리즘/수식
- **Adjoint 방법**:
  - 목적함수: FOM(θ) (성능 지표, θ: 소자 파라미터)
  - 순방향: u = F(θ) (물리 시뮬레이션)
  - Adjoint: λ = (∂F/∂u)⁻ᵀ · (∂FOM/∂u)
  - 그래디언트: ∂FOM/∂θ = ∂FOM/∂θ|직접 - λᵀ · ∂F/∂θ

- **확산 모델 샘플링**:
  - 표준 DDPM: x_{t-1} = μ_θ(x_t, t) + σ_t · ε
  - AdjointDiffusion 수정:
    x_{t-1} = μ_θ(x_t, t) + σ_t · ε - η_t · ∇_{x_t} FOM(x_t)
  - ∇_{x_t} FOM: adjoint 그래디언트 (물리 시뮬레이터에서 계산)

- **제조 인식 훈련**:
  - 훈련 데이터: 리소그래피 시뮬레이션으로 제조 후 형상 예측
  - 확산 모델이 자연적으로 제조 가능한 이진 패턴 학습

- **샘플링 효율**:
  - 순수 DL: ~10^5~10^6 시뮬레이션 필요
  - AdjointDiffusion: ~200 시뮬레이션 (adjoint으로 그래디언트 효율화)

## OPC 툴 구현 관련성
SKOPC의 SMO 모듈과 ILT 모듈에 혁신적 접근법 제공. 소스 최적화 문제에서 adjoint 그래디언트와 생성 모델을 결합하면 전통적 그래디언트 최적화의 로컬 최소값 문제 극복 가능. 마스크 생성에서 확산 모델이 제조 가능한 마스크 형상의 선험 분포를 학습하고 adjoint가 리소그래피 성능을 보장하는 결합 프레임워크 구현 가능. BOSON-1의 variation-aware 접근법과 결합하면 더욱 강건한 SMO 달성.

## 참고문헌 (핵심)
- Ho et al., "Denoising Diffusion Probabilistic Models" (DDPM, 2020)
- Adjoint 방법 원전: Lalau-Keraly et al. (2013)
- Frandsen et al., SPINS 광자소자 역설계 소프트웨어
- PRISM (arXiv:2602.15762) — 관련 리소그래피 인식 역설계

## 태그
`adjoint-method`, `diffusion-model`, `photonic-inverse-design`, `fabrication-aware`, `physics-guided`, `DDPM`, `manufacturing`, `2025`, `arxiv`, `AdjointDiffusion`
