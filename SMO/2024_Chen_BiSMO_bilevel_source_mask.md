# Efficient Bilevel Source Mask Optimization (BiSMO)

## 메타데이터
- **저자**: Guojin Chen, Hongquan He, Peng Xu, Hao Geng, Bei Yu
- **연도**: 2024
- **게재지/학회**: DAC 2024 (Design Automation Conference)
- **DOI/URL**: https://arxiv.org/abs/2405.09548
- **인용수**: DAC 2024 게재

## 핵심 요약
기존 SMO의 순차적·교대적(sequential/alternating) 최적화 한계를 극복하는 이중 레벨(bilevel) 최적화 프레임워크 BiSMO를 제안한 논문. 가속된 Abbe 전방 이미징 모델을 통합하고 소스와 마스크의 동시 최적화를 이중 레벨 문제로 재정식화하여 세 가지 그래디언트 기반 풀이 방법을 제시한다. 기존 대비 오차 지표 40% 감소와 8배 런타임 효율 향상을 달성한 DAC 2024 최고 수준 논문.

## 주요 기여
- SMO를 이중 레벨 최적화 문제로 최초 재정식화 (BiSMO 프레임워크)
- GPU 가속 Abbe 전방 이미징으로 정확도와 계산 효율 동시 향상
- 세 가지 그래디언트 기반 이중 레벨 SMO 풀이 방법 제안
- 순차적 최적화의 성능 보증 없는 문제 해결
- 오차 지표 40% 감소, 런타임 8배 향상

## 알고리즘/수식
- **이중 레벨 SMO 정식화**:
  ```
  외부 문제 (소스 최적화):
    min_{s} F(s, m*(s))   s.t. s ∈ S_source

  내부 문제 (마스크 최적화):
    m*(s) = argmin_{m} G(s, m)   s.t. m ∈ M_mask
  ```
  - s: 소스 분포 (픽셀화된 조명), m: 마스크 패턴
  - F: 외부 목적함수 (공정 윈도우, EPE 등)
  - G: 내부 목적함수 (마스크 품질)

- **가속 Abbe 이미징**:
  - I(x) = Σⱼ sⱼ · |hⱼ * m(x)|²  (소스 픽셀 j별 합산)
  - GPU 텐서 연산으로 FFT 기반 병렬 계산

- **세 가지 그래디언트 방법**:
  1. **암묵적 미분(Implicit Differentiation)**: 내부 최적화 조건을 통한 그래디언트
     - ∂F/∂s = ∂F/∂s|직접 + ∂F/∂m · (∂²G/∂m²)⁻¹ · (∂²G/∂m∂s)
  2. **근사 그래디언트(Approximate Gradient)**: 계산 효율을 위한 근사
  3. **단일 레벨 완화(Single-level Relaxation)**: 이중 레벨을 단일 레벨로 근사

- **소스 제약**:
  - s ∈ [0,1]^N (각 픽셀 강도)
  - Σ sⱼ = 1 (에너지 보존), 물리적 실현 가능성 제약

## OPC 툴 구현 관련성
SKOPC의 `skopc/smo/` 모듈의 핵심 알고리즘으로 직접 활용 가능. 현재 SKOPC의 SMO가 소스와 마스크를 교대 최적화한다면, BiSMO의 이중 레벨 구조로 전환하여 성능 향상 가능. GPU 가속 Abbe 이미징은 `LithoEngine(process.optical, process.resist)` 호출을 텐서 배치 연산으로 대체하는 방향에 활용. 세 가지 그래디언트 방법 중 근사 그래디언트가 실용적 구현에 적합.

## 참고문헌 (핵심)
- Chen et al., TorchLitho (2024) — 같은 저자 선행 연구
- Granik, "Source optimization for image fidelity," JM3 (2004) — SMO 기초
- Liu & Ye, "IMAML" — 이중 레벨 최적화 방법
- Abbe 이미징 이론 원전

## 태그
`SMO`, `bilevel-optimization`, `source-optimization`, `mask-optimization`, `Abbe-imaging`, `gradient-based`, `GPU-acceleration`, `DAC`, `2024`, `arxiv`
