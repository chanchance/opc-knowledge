# DiffPattern: Layout Pattern Generation via Discrete Diffusion

## 메타데이터
- **저자**: Zixiao Wang, Yunheng Shen, Wenqian Zhao, Yang Bai, Guojin Chen, Farzan Farnia, Bei Yu
- **연도**: 2023
- **게재지/학회**: DAC 2023 (Design Automation Conference), arXiv:2303.13060
- **DOI/URL**: https://arxiv.org/abs/2303.13060
- **인용수**: DAC 2023 다수 인용

## 핵심 요약
이산 확산 모델(discrete diffusion model)을 활용하여 신뢰성 있는 VLSI 레이아웃 패턴을 생성하는 DiffPattern을 제안한 논문. 순수 신경망 기반 방법의 신뢰성 문제를 해결하기 위해, 계산 효율적인 무손실 레이아웃 패턴 표현과 이산 확산 생성 방법을 결합하고, 화이트박스 패턴 평가 메커니즘으로 설계 규칙 준수를 보장한다.

## 주요 기여
- 이산 확산 모델 기반 다양한 토폴로지 생성 (연속 픽셀 대신 이산 레이아웃 표현)
- 계산 효율적인 무손실 레이아웃 패턴 인코딩/표현 방법
- 화이트박스 패턴 평가(white-box pattern assessment)로 DRC 준수 보증
- 블랙박스 신경망의 불투명성 문제 해결
- 기존 기준 방법 대비 다중 평가 기준에서 우수한 성능 달성

## 알고리즘/수식
- **이산 확산 모델**:
  - 레이아웃을 이산 토큰 시퀀스로 표현: x = {x₁, x₂, ..., xₙ} ∈ {0,1}ⁿ
  - 순방향 확산 (MASK 추가): q(xₜ|xₜ₋₁) = [1-βₜ]·I + βₜ·M_mask
  - 역방향 확산 (생성): p_θ(xₜ₋₁|xₜ) → DRC 준수 레이아웃

- **무손실 레이아웃 표현**:
  - 폴리곤 기반 레이아웃 → 효율적 이진 그리드 인코딩
  - 정보 손실 없이 레이아웃 기하구조 보존

- **화이트박스 패턴 평가**:
  - 생성 패턴 x_generated → DRC 규칙 집합 {R₁, R₂, ...}에 대해 검증
  - 명시적 설계 규칙으로 위반 감지: V = {xᵢ | ∃Rⱼ: Rⱼ(xᵢ)=FAIL}
  - 위반 시 MCMC 재샘플링 또는 후처리 수정

- **다양성 측정**:
  - 생성 패턴 집합의 고유 토폴로지 수 / 전체 생성 수

## OPC 툴 구현 관련성
SKOPC의 테스트 패턴 생성 및 GNN-OPC 훈련 데이터 증강에 활용 가능. 이산 확산 모델은 레이아웃의 이진 특성(금속 있음/없음)에 자연스럽게 적합. DRC 준수 보증 메커니즘은 `skopc/layout/drc.py`와 연동 가능. 다양한 합성 레이아웃 패턴으로 OPC 알고리즘의 일반화 성능 향상 가능.

## 참고문헌 (핵심)
- Austin et al., "Structured Denoising Diffusion Models in Discrete State Spaces" (D3PM, 2021)
- Wang et al., AdaOPC (2023) — 같은 저자(Zixiao Wang) 연관 연구
- 설계 규칙 관련 EDA/ICCAD 논문들

## 태그
`layout-generation`, `discrete-diffusion`, `DRC`, `VLSI`, `pattern-generation`, `white-box`, `DAC`, `2023`, `arxiv`
