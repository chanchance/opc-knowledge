# Coherent Mode Decoupling: A Versatile Framework for High-Throughput Partially Coherent Light Transport

## 메타데이터
- **저자**: Han Xu, Ming Li, Shuo Wang, Zhe Ren, Peng Liu, Yi Zhang, Yuhui Dong, Liang Zhou
- **연도**: 2026
- **게재지/학회**: arXiv:2601.15776 (physics.optics)
- **DOI/URL**: https://arxiv.org/abs/2601.15776
- **인용수**: 신규 논문

## 핵심 요약
부분 간섭성(partially coherent) 광학 시스템의 파동 광학 시뮬레이션 계산 효율을 혁신적으로 향상시키는 CMD(Coherent Mode Decoupling) 프레임워크를 제안한 논문. 전통적 간섭 모드 분해(coherent mode decomposition)의 2D 모드 전파 계산 비용을 줄이기 위해 2D 모드를 효율적인 1D 성분으로 분해하고 부분 공간 압축(subspace compression)으로 비분리 결합 효과를 포착한다. 계산 리소그래피와 회절 한계 저장 링(DLSR) 코히런트 빔라인 양쪽에서 검증.

## 주요 기여
- CMDC(Coherent Mode Decoupling) 알고리즘으로 부분 간섭성 광전파 시뮬레이션 획기적 가속
- 2D 모드를 효율적 1D 성분으로 분해하여 계산 차원 축소
- 비분리 결합 효과 포착을 위한 부분 공간 압축 전략
- 계산 리소그래피(SOCS/TCC 방법) 적용에서 크기 단위 속도 향상
- DLSR 코히런트 빔라인까지 범용 적용 가능한 프레임워크

## 알고리즘/수식
- **SOCS(Sum Of Coherent Systems) 방법**:
  - 리소그래피 시스템: I(x) = Σᵢ |hᵢ * m(x)|²
  - 여기서 hᵢ: TCC의 SVD 고유함수(eigenkernels), m: 마스크
  - TCC = Σᵢ σᵢ · ψᵢ(f) · ψᵢ*(f')  (SVD 분해)

- **TCC(Transmission Cross Coefficient)**:
  - TCC(f,f') = ∫∫ J(f'') · H(f+f'') · H*(f'+f'') df''
  - J: 소스 분포(조명), H: 광학계 pupil function
  - SVD로 TCC 분해 → SOCS 커널 추출

- **CMD 분해**:
  - 2D 모드: Ψ(x,y) → Ψ_x(x) ⊗ Ψ_y(y) + 결합 보정항
  - 1D 전파: 각 차원 독립 계산 → O(N²)에서 O(N) 복잡도 축소
  - 부분 공간 압축: 저차원 표현으로 비분리 효과 근사

- **계산 복잡도**:
  - 기존 TCC/SOCS: O(N_modes × N_pixels²) 전파
  - CMD: O(N_modes × N_pixels) (1D 분해 후)

## OPC 툴 구현 관련성
SKOPC의 LithoEngine 성능 향상에 핵심 참조. `skopc/modeling/litho_engine.py`의 TCC 계산 가속화에 CMD 방법 적용 가능. TCC SVD 분해는 이미 TorchLitho에서 SOCS로 구현되어 있으나, CMD의 1D 분해로 추가 10-100배 속도 향상 가능. SMO 반복 최적화에서 매 이터레이션마다 수행하는 리소그래피 forward 패스 가속에 직접 활용.

## 참고문헌 (핵심)
- Born & Wolf, "Principles of Optics" (부분 간섭성 광학 이론)
- Hopkins (1953) — TCC 원전
- Cobb (1995) — SOCS 분해 방법 원전
- 계산 리소그래피 TCC/SVD 관련 SPIE/JM3 논문들

## 태그
`TCC`, `SOCS`, `SVD`, `partial-coherence`, `coherent-mode`, `lithography-simulation`, `computational-lithography`, `1D-decomposition`, `acceleration`, `2026`, `arxiv`
