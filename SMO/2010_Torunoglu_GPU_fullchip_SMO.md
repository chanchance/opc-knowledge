# A GPU-Based Full-Chip Source-Mask Optimization Solution

## 메타데이터
- **저자**: Ilhami Torunoglu, Erich Elsen, Ahmet Karakas
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7640, Optical Microlithography XXIII, 76401L (3 March 2010)
- **DOI/URL**: https://doi.org/10.1117/12.846640
- **인용수**: 확인 필요

## 핵심 요약
전체 칩 SMO의 주요 병목인 계산 비용을 GPU(Graphics Processing Unit) 병렬 연산으로 극복하는 GPU 기반 전체 칩 SMO 솔루션을 제안한다. Aerial image 계산, TCC 분해, 그래디언트 연산 등 SMO의 핵심 연산을 GPU에서 병렬화하여 전체 칩 규모 SMO의 실용적 턴어라운드 타임(TAT)을 달성한다.

## 주요 기여
- SMO 핵심 연산(aerial image, TCC, 그래디언트)의 GPU 병렬화
- 전체 칩 규모 SMO를 실용적 시간 내에 완료하는 GPU 가속 프레임워크
- CPU 기반 SMO 대비 대폭적인 속도 향상 실증
- GPU 메모리 관리 전략으로 대규모 레이아웃 처리 지원

## 알고리즘/수식
**GPU 병렬 Aerial Image 계산:**
$$I(x_i) = \sum_k \sigma_k |h_k * m|^2(x_i), \quad i = 1, ..., N_{pixels}$$
각 픽셀 $x_i$에 대한 계산을 GPU 스레드로 병렬화.

**GPU 기반 TCC 분해:**
$$TCC = U \Lambda U^H$$
대규모 TCC 행렬의 고유값 분해를 cuBLAS/cuSolver로 가속.

**병렬 그래디언트 연산:**
$$\frac{\partial F}{\partial \sigma_k} = \sum_i \frac{\partial F}{\partial I(x_i)} \cdot |h_k * m|^2(x_i)$$
CUDA 커널로 모든 소스 픽셀 그래디언트 동시 계산.

**GPU SMO 플로우:**
```
GPU 메모리로 TCC 및 마스크 로드
CUDA 커널: 배치 aerial image 계산
CUDA 커널: 배치 EPE 및 비용함수 계산
CUDA 커널: 배치 그래디언트 계산
CPU: 소스/마스크 업데이트 (경량)
반복
```

**속도 향상 (예시):**
GPU vs. CPU: 10× ~ 100× 속도 향상 (마스크 크기에 따라 다름)

## OPC 툴 SMO 구현 관련성
- SKOPC SMO GPU 가속 구현 시 핵심 참고
- PyTorch/CUDA 기반 `skopc/litho/gpu_aerial_image.py` 구현 시 병렬화 전략 참고
- 전체 칩 SMO의 실용적 TAT 달성을 위한 GPU 활용 방법론 제공
- TCC 행렬 GPU 메모리 관리 방법 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Dam et al., "SMO from theory to practice," Proc. SPIE 7640, 2010
- Chen et al., "Diff-SMO: GPU-accelerated SMO," IEEE TCAD 2024

## 태그
`SMO`, `SPIE`, `GPU-acceleration`, `full-chip-SMO`, `CUDA`, `parallel-computing`, `aerial-image`, `TCC`, `gradient`, `TAT`, `computational-efficiency`
