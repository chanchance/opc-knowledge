# Ultrafast Source Mask Optimization via Conditional Discrete Diffusion

## 메타데이터
- **저자**: Guojin Chen, Zixiao Wang, Bei Yu, Martin D.F. Wong
- **연도**: 2024
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (July 2024)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10419017/
- **인용수**: 확인 필요

## 핵심 요약
조건부 이산 확산 모델(conditional discrete diffusion model)을 활용하여 소스-마스크 최적화(SMO)를 초고속으로 수행하는 Diff-SMO 프레임워크를 제안한다. Abbe 이론에 기반한 GPU 가속 리소그래피 시뮬레이터를 개발하고, 소스와 마스크를 동시에 정밀화하는 최적화 범위를 확장한다. 기존 방법이 마스크 최적화 가속에 집중한 것과 달리 소스 최적화 기법 향상에 주안점을 두며, 이산 확산 모델로 준최적 소스를 생성한다.

## 주요 기여
- 소스 최적화에 이산 확산 모델 최초 적용으로 SMO 초고속화
- Abbe 이론 기반 GPU 가속 리소그래피 시뮬레이터 구현
- 소스와 마스크 동시 정밀화하는 확장된 SMO 최적화 범위
- 기존 학술 리소그래피 모델 제약을 벗어난 산업급 SMO 성능 달성

## 알고리즘/수식
**Abbe 이론 기반 이미징 모델:**
$$I(x) = \sum_k J(f_k) |h(x; f_k) * m(x)|^2$$
여기서 $J(f_k)$는 소스 픽셀 강도, GPU 병렬 연산으로 고속화.

**이산 확산 소스 생성:**
소스 패턴을 이산 변수 $\sigma \in \{0, 1\}^N$으로 표현하고 조건부 확산 과정으로 생성:
$$q(\sigma^{(t)} | \sigma^{(t-1)}) = \text{Cat}(\sigma^{(t)}; \mathbf{Q}_t \sigma^{(t-1)})$$
여기서 $\mathbf{Q}_t$는 전환 행렬, $t$는 확산 시간.

**역방향 확산 (소스 생성):**
$$p_\theta(\sigma^{(t-1)} | \sigma^{(t)}, c) = \text{Cat}(\sigma^{(t-1)}; \tilde{\mathbf{Q}}_t \sigma^{(t)}, c)$$
조건 $c$: 타깃 패턴 및 마스크 정보.

**SMO 최적화 플로우:**
1. 이산 확산 모델로 초기 소스 $\sigma_0$ 생성 (빠른 글로벌 탐색)
2. 생성된 소스로 마스크 최적화 (ILT 또는 그래디언트)
3. 최적화된 마스크로 소스 정밀화
4. 수렴까지 반복

**GPU 가속 리소그래피 시뮬레이터:**
- 배치 aerial image 계산: 다중 클립 병렬 처리
- TCC 행렬 GPU 메모리 캐싱
- 기울기 역전파(backpropagation)로 마스크 최적화 통합

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 이산 확산 기반 소스 초기화 방법으로 활용 가능
- `skopc/smo/diffusion_source_init.py` 구현 시 직접 참고
- GPU 가속 Abbe 시뮬레이터 설계를 `skopc/litho/gpu_simulator.py`에 참고
- 이산 소스 표현(0/1 픽셀)과 연속 소스 표현 간 변환 방법 제시

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Chen et al., "BiSMO: Bilevel Source Mask Optimization," DAC 2024
- Wang et al., "DiffPattern: discrete diffusion for layout," DAC 2023

## 태그
`SMO`, `IEEE`, `diffusion-model`, `discrete-diffusion`, `Diff-SMO`, `GPU-acceleration`, `Abbe-theory`, `source-optimization`, `deep-learning`, `generative-model`, `TCAD`
