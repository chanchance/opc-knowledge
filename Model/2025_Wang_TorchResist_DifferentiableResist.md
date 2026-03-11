# TorchResist: Open-Source Differentiable Resist Simulator

## 메타데이터
- **저자**: (주요 저자 Wang 등, CUHK/관련 연구그룹)
- **연도**: 2025
- **게재지/학회**: arXiv:2502.06838; SPIE Advanced Lithography + Patterning 2025
- **DOI/URL**: https://arxiv.org/abs/2502.06838; https://doi.org/10.1117/12.3062763
- **인용수**: 신규 (2025년 발표)

## 핵심 요약
오픈소스 미분 가능한 포토레지스트 시뮬레이터 TorchResist를 발표한 논문. 최대 20개의 해석 가능한(interpretable) 파라미터를 가진 화이트박스(white-box) 해석적 모델로, 포토레지스트 공정 전체를 모델링한다. GPU 병렬 연산과 미분 가능 프로그래밍(differentiable programming)을 활용하여 기존 임계값 기반 방법(threshold-based)을 능가하는 성능을 보이며, 이진 레지스트 패턴과 현상 깊이(development depth)를 동시에 출력하는 3D 시뮬레이션 기능을 제공한다. TorchLitho와 연계하여 end-to-end 미분 가능 리소그래피 파이프라인을 구성한다.

## 주요 기여
- 오픈소스 최초 완전 미분 가능한 포토레지스트 시뮬레이터 구현
- 20개 이내의 해석 가능한 파라미터로 구성된 화이트박스 모델
- GPU 가속 기반 고속 시뮬레이션
- 이진 레지스트 패턴 + 3D 현상 깊이 동시 출력
- LithoBench 데이터셋에서 픽셀 오차 및 EPE 대폭 감소
- TorchLitho와 완벽한 통합 (end-to-end autograd 지원)

## 모델 아키텍처/수식
**전체 레지스트 공정 모델링 단계:**

**1단계: 노광 에너지 분포 (Exposure Distribution)**
```
E(x, y) = ∫∫ I(x', y') · PSF_resist(x-x', y-y') dx'dy'
```
PSF_resist: 레지스트 내 이차 전자/광자 확산 커널

**2단계: 산(Acid) 농도 분포 (Photo-Acid Distribution)**
```
A(x, y) = 1 - exp(-α · E(x, y))
```
α: 레지스트 흡수 계수

**3단계: PEB 확산 (Post-Exposure Bake Diffusion)**
```
A_peb(x, y) = A(x, y) ⊗ G(x, y; σ_peb)
G(x, y; σ) = (1/2πσ²) · exp(-(x²+y²)/2σ²)
```
σ_peb: PEB 온도와 시간의 함수인 확산 길이

**4단계: 현상 (Development) - 해석적 모델**
```
R(x, y) = sigmoid((A_peb(x, y) - T_dev) / σ_dev)
```
T_dev: 현상 임계 농도
σ_dev: 현상 대비 파라미터

**3D 깊이 출력:**
```
D(x, y, z) = ∫₀ᶻ R(x, y, z') dz'
```

**미분 가능 파라미터 (총 ~20개):**
- {α, σ_peb, T_dev, σ_dev, σ_resist, ...}
- PyTorch autograd로 ∂L/∂θ 자동 계산

**성능 비교 (LithoBench):**
- 픽셀 오차: 임계값 모델 대비 ~40% 감소
- EPE: 임계값 모델 대비 ~35% 감소

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 핵심 의존성인 TorchResist의 공식 논문. `skopc/modeling/`에서 `LithoEngine(process.optical, process.resist)` 호출 시 TorchResist가 레지스트 시뮬레이션을 담당한다. GitHub: https://github.com/ShiningSord/TorchResist. 파라미터 보정 시 이 논문의 20개 해석적 파라미터를 CD-SEM 측정값으로 fitting하는 방법을 참조. 3D 현상 깊이 출력은 SKOPC의 etch 모델 연계에 활용 가능.

## 참고문헌 (핵심)
- Chen, G. et al., "Open-source differentiable lithography imaging framework," arXiv:2409.15306 (2024)
- Mack, C.A., "Lumped parameter model for chemically amplified resists," SPIE 5377 (2004)
- Cobb, N. and Zakhor, A., "Variable threshold resist model," SPIE 3679 (1999)
- Li, Y. et al., "LithoBench: Benchmarking AI computational lithography," NeurIPS 2023
- Brunner, T.A., "Why optical lithography will live forever," J. Vac. Sci. Technol. B (2003)

## 태그
`Model`, `OPC`, `ResistModel`, `TorchResist`, `OpenSource`, `Differentiable`, `GPU`, `PyTorch`, `3D`, `PEB`, `Development`, `WhiteBox`, `LithoBench`
