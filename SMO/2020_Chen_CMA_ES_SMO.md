# Source Mask Optimization Using the Covariance Matrix Adaptation Evolution Strategy

## 메타데이터
- **저자**: Guodong Chen, Xuelong Li, Yu Xiong, Hao Jiang, Shiyuan Liu
- **연도**: 2020
- **게재지/학회**: Optics Express, Vol. 28, No. 22, pp. 33371–33385
- **DOI/URL**: https://doi.org/10.1364/OE.28.033371
- **인용수**: 다수

## 핵심 요약
공분산 행렬 적응 진화 전략(Covariance Matrix Adaptation Evolution Strategy, CMA-ES)을 소스-마스크 최적화에 적용하는 방법을 제안한다. 포인트 소스 위치를 직접 최적화 변수로 사용하여 조명 분포를 구성하며, 그래디언트 없이 전역 탐색 능력을 갖춘 SMO를 구현한다. 기존 픽셀 기반 그래디언트 SMO 대비 더 다양한 소스 형상 탐색이 가능하며 지역 최솟값 회피 성능을 입증한다.

## 주요 기여
- CMA-ES를 SMO에 최초 적용하여 그래디언트 없는 전역 소스 최적화 구현
- 포인트 소스 위치 직접 최적화를 통한 연속 소스 파라미터화
- 공분산 행렬 적응으로 탐색 방향 자동 학습 및 수렴 가속
- 기존 그래디언트 기반 SMO 대비 우수한 지역 최솟값 회피 실증

## 알고리즘/수식
**CMA-ES 기반 SMO 목적함수:**
$$\min_{\boldsymbol{\theta}} F(\boldsymbol{\theta}) = \sum_j EPE_j^2(\boldsymbol{\sigma}(\boldsymbol{\theta}), m)$$
여기서 $\boldsymbol{\theta}$는 포인트 소스 위치 벡터.

**포인트 소스 파라미터화:**
$$\sigma(f,g) = \sum_{i=1}^{N_p} w_i \cdot \delta(f - f_i, g - g_i)$$
$N_p$개 포인트 소스의 위치 $(f_i, g_i)$와 가중치 $w_i$를 최적화.

**CMA-ES 샘플링:**
$$\boldsymbol{\theta}^{(k+1)}_i \sim \mathcal{N}(\boldsymbol{m}^{(k)}, (\sigma^{(k)})^2 \boldsymbol{C}^{(k)}), \quad i=1,\ldots,\lambda$$
평균 $\boldsymbol{m}$, 스텝 크기 $\sigma$, 공분산 행렬 $\boldsymbol{C}$의 적응적 갱신.

**공분산 행렬 갱신 (Rank-1 업데이트):**
$$\boldsymbol{C}^{(k+1)} = (1-c_1)\boldsymbol{C}^{(k)} + c_1 \boldsymbol{p}_c \boldsymbol{p}_c^T$$
진화 경로 $\boldsymbol{p}_c$를 활용한 공분산 행렬 적응.

**Rank-$\mu$ 업데이트:**
$$\boldsymbol{C}^{(k+1)} \mathrel{+}= c_\mu \sum_{i=1}^{\mu} w_i \boldsymbol{y}_{i:\lambda} \boldsymbol{y}_{i:\lambda}^T$$
상위 $\mu$개 개체로 공분산 행렬 갱신.

**스텝 크기 제어 (CSA):**
$$\sigma^{(k+1)} = \sigma^{(k)} \exp\left(\frac{c_\sigma}{d_\sigma}\left(\frac{||\boldsymbol{p}_\sigma||}{E||\mathcal{N}(0,I)||} - 1\right)\right)$$
누적 스텝 크기 적응으로 수렴 속도 자동 조절.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에 CMA-ES 기반 전역 소스 최적화 추가 시 핵심 참고
- `skopc/smo/cmaes_smo.py` 구현으로 그래디언트 계산 없는 소스 최적화 가능
- 포인트 소스 파라미터화는 FlexRay/FlexPupil 조명기의 이산 모드 표현과 자연스럽게 연결
- 그래디언트 기반 SMO와 CMA-ES의 하이브리드 워크플로 (전역 탐색 → 로컬 정밀화) 설계 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Hansen & Ostermeier, "CMA-ES," Evol. Comp. 2001
- Shi et al., "PSO-GA hybrid source optimization," IEEE Photonics J. 2023
- Wang et al., "Adaptive PSO source optimization," 2021

## 태그
`SMO`, `Optics-Express`, `CMA-ES`, `covariance-matrix-adaptation`, `evolution-strategy`, `gradient-free`, `global-optimization`, `point-source`, `metaheuristic`, `source-parameterization`, `evolutionary-computation`
