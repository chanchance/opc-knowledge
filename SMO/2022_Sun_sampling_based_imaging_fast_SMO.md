# Sampling-Based Imaging Model for Fast Source and Mask Optimization in Immersion Lithography

## 메타데이터
- **저자**: Yiyu Sun, Yanqiu Li, Guanghui Liao, Miao Yuan, Pengzhi Wei, Yaning Li, Lulu Zou, Lihui Liu
- **연도**: 2022
- **게재지/학회**: Applied Optics, Vol. 61, No. 2, pp. 523–531
- **DOI/URL**: https://doi.org/10.1364/AO.447033
- **인용수**: 확인 필요

## 핵심 요약
역 점 확산 함수(inverse point spread function)를 활용하여 계산 차원을 줄이는 샘플링 기반 이미징 모델을 수립하여 빠른 역 리소그래피를 위한 고급 프레임워크를 제공한다. 침지 리소그래피 SMO의 계산 효율을 3배 향상시키면서 패턴 충실도를 유지한다.

## 주요 기여
- 역 점 확산 함수(inverse PSF) 기반 샘플링 이미징 모델로 계산 차원 감소
- 빠른 역 리소그래피를 위한 고급 SMO 프레임워크 제공
- SMO 절차 효율성 3배 향상 달성
- 침지 리소그래피에 특화된 빠른 이미징 모델 설계

## 알고리즘/수식
**샘플링 기반 이미징 모델:**
$$I(x) \approx \sum_{k \in \mathcal{S}} \sigma_k |h_k * m|^2(x)$$
전체 소스 픽셀 대신 선택된 샘플 집합 $\mathcal{S} \subset \{1,\ldots,N_{src}\}$에서만 계산.

**역 점 확산 함수 (Inverse PSF):**
$$h_{inv}(x) = \mathcal{F}^{-1}\left[\frac{1}{H(f)}\right]$$
주파수 도메인에서 PSF의 역수로 정의된 역 PSF.

**계산 차원 감소:**
샘플링으로 TCC 행렬 크기 감소:
$$TCC_{sampled} \in \mathbb{R}^{K_s \times K_s}, \quad K_s = |\mathcal{S}| \ll N_{src}$$

**SMO 비용함수 (샘플링 기반):**
$$F_{sampled}(\boldsymbol{\sigma}, m) = \sum_j \left(I_{sampled}(x_j; \boldsymbol{\sigma}, m) - I_{target}(x_j)\right)^2$$

**속도 향상:**
계산 복잡도 $O(K_s^2 N_{pixels})$ vs. 기존 $O(N_{src}^2 N_{pixels})$:
$$\text{속도 향상} \approx \left(\frac{N_{src}}{K_s}\right)^2 \approx 3\times$$

**그래디언트 (샘플링 기반):**
$$\frac{\partial F_{sampled}}{\partial \sigma_k} = \sum_j \frac{\partial F}{\partial I(x_j)} \cdot |h_k * m|^2(x_j), \quad k \in \mathcal{S}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 빠른 침지 리소그래피 SMO 구현 시 샘플링 기반 이미징 모델 참고
- `skopc/litho/sampling_imaging.py`에 역 PSF 기반 샘플링 이미징 모델 구현
- 소스 픽셀 샘플링으로 TCC 계산 가속 — `skopc/litho/tcc.py` 최적화에 활용
- Ma et al. 2018 회절 부분공간과 함께 소스 공간 축소 전략 비교 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Pixelated SMO immersion," JOSAA 2013
- Ma et al., "Diffraction subspace illumination opt," Optics Express 2018

## 태그
`SMO`, `Applied-Optics`, `sampling-based`, `inverse-PSF`, `fast-SMO`, `immersion-lithography`, `computational-efficiency`, `TCC`, `dimension-reduction`, `3x-speedup`
