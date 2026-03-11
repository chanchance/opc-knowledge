# Forming Freeform Source Shapes by Utilizing Particle Swarm Optimization to Enhance Resolution in Extreme UV Nanolithography

## 메타데이터
- **저자**: Hung-Fei Kuo, Wei-Chen Wu
- **연도**: 2015
- **게재지/학회**: IEEE Transactions on Nanotechnology, Vol. 14, pp. 322–329
- **DOI/URL**: https://doi.org/10.1109/TNANO.2015.2389256
- **인용수**: 다수

## 핵심 요약
EUV 나노리소그래피에서 해상도 향상을 위해 픽셀 기반 자유형(freeform) 소스 형상을 PSO(Particle Swarm Optimization)로 최적화하는 방법을 제안한다. PSO의 전역 탐색 능력을 활용하여 EUV 조명 소스의 픽셀화된 분포를 직접 최적화하며, 그래디언트 계산 없이 복잡한 비용함수 지형에서 최적 소스를 탐색한다.

## 주요 기여
- EUV 리소그래피에 PSO 기반 픽셀화 자유형 소스 최적화 적용
- 그래디언트 없이 복잡한 EUV 이미징 모델에서 소스 형상 최적화
- 전역 탐색 능력으로 다양한 소스 형상 탐색 가능
- EUV 해상도 향상에 기여하는 최적 자유형 소스 설계 실증

## 알고리즘/수식
**PSO 기반 소스 최적화:**
$$\min_{\boldsymbol{\sigma}} F(\boldsymbol{\sigma}) = \sum_j \left(I(x_j; \boldsymbol{\sigma}) - I_{target}(x_j)\right)^2$$
소스 픽셀 강도 벡터 $\boldsymbol{\sigma}$를 PSO로 최적화.

**PSO 속도 업데이트:**
$$v_k^{(t+1)} = w v_k^{(t)} + c_1 r_1 (p_k^{best} - \sigma_k^{(t)}) + c_2 r_2 (g^{best} - \sigma_k^{(t)})$$

**PSO 위치 업데이트:**
$$\sigma_k^{(t+1)} = \sigma_k^{(t)} + v_k^{(t+1)}$$
$$\sigma_k^{(t+1)} = \text{clip}(\sigma_k^{(t+1)}, 0, 1)$$

**EUV 이미징 모델 (픽셀 소스):**
$$I(x; \boldsymbol{\sigma}) = \sum_k \sigma_k |h_k^{EUV} * m|^2(x)$$
EUV 광학계 커널 $h_k^{EUV}$ 포함.

**관성 가중치 감소 전략:**
$$w^{(t)} = w_{max} - (w_{max} - w_{min}) \frac{t}{T_{max}}$$
반복에 따라 관성 가중치를 선형 감소 → 초기 전역 탐색, 후기 지역 탐색.

## OPC 툴 SMO 구현 관련성
- SKOPC EUV 소스 최적화에서 PSO 기반 픽셀화 자유형 소스 설계 참고
- `skopc/smo/pso_euv_source.py`에 EUV 이미징 모델 기반 PSO 소스 최적화 구현
- EUV 조명기(FlexPupil)의 픽셀화 분포 최적화에 직접 적용 가능
- Zhang et al. 2021 SL-PSO EUV SMO와 비교: 단순 PSO vs. 사회 학습 PSO 성능 비교 참고

## 참고문헌 (핵심)
- Zhang et al., "EUV SMO SL-PSO thick mask," Optics Express 2021
- Wang et al., "Adaptive PSO source optimization," 2021
- Shi et al., "PSO-GA hybrid source opt," IEEE Photonics J. 2023

## 태그
`SMO`, `IEEE-Transactions-Nanotechnology`, `EUV-lithography`, `PSO`, `particle-swarm`, `freeform-source`, `pixelated-source`, `gradient-free`, `global-optimization`, `nanolithography`
