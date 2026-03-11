# Gradient-Based Fast Source Mask Optimization (SMO)

## 메타데이터
- **저자**: Jue-Chin Yu, Peichen Yu
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 7973, Optical Microlithography XXIV, 79731J
- **DOI/URL**: https://doi.org/10.1117/12.879441
- **인용수**: 확인 필요

## 핵심 요약
소스와 마스크의 서로 다른 이미지 형성 메커니즘에 기반하여 소스 최적화와 마스크 최적화를 두 단계의 순차적 과정으로 수행하는 그래디언트 기반 고속 SMO 알고리즘을 제안한다. 소스와 마스크의 물리적 차이를 활용하여 계산을 단순화하고 수렴을 가속한다.

## 주요 기여
- 소스/마스크의 서로 다른 이미지 형성 메커니즘 활용한 순차적 SMO
- 그래디언트 기반 고속 SMO 알고리즘 개발
- 소스 최적화와 마스크 최적화의 단계적 분리로 계산 효율 향상
- 순차 최적화 흐름에서의 수렴 가속

## 알고리즘/수식
**순차적 SMO 흐름:**
```
1단계: 소스 최적화 (마스크 고정)
   σ*(m_current) = argmin_σ F_EPE(σ, m_current)

2단계: 마스크 최적화 (소스 고정)
   m*(σ*) = argmin_m F_EPE(σ*, m)

반복: 수렴할 때까지 1-2단계 반복
```

**소스 그래디언트 (TCC 기반):**
$$\frac{\partial F_{EPE}}{\partial \sigma_k} = \sum_j 2EPE_j \cdot \frac{\partial EPE_j}{\partial \sigma_k}$$
$$= \sum_j 2EPE_j \cdot \frac{-1}{\left|\partial I/\partial x\right|_{x_j}} \cdot |h_k * m|^2(x_j)$$

**마스크 그래디언트 (SOCS 기반):**
$$\frac{\partial F_{EPE}}{\partial m_p} = \sum_j 2EPE_j \cdot \frac{-1}{|\partial I/\partial x|_{x_j}} \cdot 2\text{Re}\left[\sum_n c_n (h_n * m)(x_j) h_n^*(x_j - x_p)\right]$$

**소스-마스크 이미지 형성 차이:**
- 소스: $I \propto \sum_k \sigma_k |h_k * m|^2$ (이중 선형)
- 마스크: $I \propto \sum_k \sigma_k |h_k * m|^2$ (마스크 픽셀에 복소 선형)

**수렴 기준:**
$$\|F^{(t+1)} - F^{(t)}\| / \|F^{(t)}\| < \varepsilon_{conv}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 순차적 소스-마스크 최적화 구현 시 단계별 분리 전략 참고
- `skopc/smo/sequential_smo.py`에 소스/마스크 순차 최적화 구현
- Peng et al. 2011 그래디언트 SMO의 순차 최적화 변형으로 함께 참고
- Ma et al. 2013 HSMO 2단계 켤레 기울기와 함께 순차/혼합 SMO 계열 참고

## 참고문헌 (핵심)
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Ma et al., \"Hybrid SMO robust immersion,\" Applied Optics 2013
- Hsu et al., \"Innovative SMO low k1,\" SPIE 2008

## 태그
`SMO`, `SPIE`, `gradient-based`, `fast-SMO`, `sequential-optimization`, `source-optimization`, `mask-optimization`, `image-formation`, `SOCS`, `TCC`, `convergence`
