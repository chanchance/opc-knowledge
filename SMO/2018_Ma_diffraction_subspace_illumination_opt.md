# Optimization of Lithography Source Illumination Arrays Using Diffraction Subspaces

## 메타데이터
- **저자**: Xu Ma, Zhiqiang Wang, Haijun Lin, Yanqiu Li, Gonzalo R. Arce, Lu Zhang
- **연도**: 2018
- **게재지/학회**: Optics Express, Vol. 26, No. 4, pp. 3738–3755
- **DOI/URL**: https://doi.org/10.1364/OE.26.003738
- **인용수**: 다수

## 핵심 요약
회절 부분공간(diffraction subspace) 기반 압축 센싱(CS)과 lp-norm 재구성 알고리즘을 활용한 효율적이고 강인한 조명 최적화(Illumination Layout Optimization, ILO) 방법을 제안한다. 마스크 패턴의 서로 다른 회절 차수 간 간섭을 유도하는 소스 픽셀만을 포함하는 부분공간에서 최적화하여 최적화 변수 수를 대폭 줄이고 계산 속도를 향상시킨다. 45nm 및 14nm 기술 노드에서 검증한다.

## 주요 기여
- 마스크 회절 구조에 기반한 소스 부분공간 정의로 최적화 변수 수 대폭 감소
- lp-norm (0 < p < 1) 재구성으로 l1-norm 대비 더 강인한 스파스 소스 복원
- 부분공간 CS로 계산 속도 및 강인성 동시 향상
- 45nm, 14nm 노드에서 기존 적응형 CS 대비 우수한 성능 실증

## 알고리즘/수식
**회절 부분공간 정의:**
마스크의 회절 스펙트럼에서 간섭 성분을 생성하는 소스 픽셀 집합:
$$\mathcal{S}_{sub} = \{k : \exists \text{ 회절 차수 } (p,q), (p',q') \text{ s.t. } (f_k + p\lambda/d) \in \text{pupil}, (f_k + p'\lambda/d) \in \text{pupil}\}$$
부분공간 $\mathcal{S}_{sub} \subset \mathcal{S}_{all}$에서만 소스 최적화.

**lp-norm 재구성 (0 < p < 1):**
$$\min_{\boldsymbol{a}} \|F(\boldsymbol{a}) - \boldsymbol{b}\|_2^2 + \lambda \|\boldsymbol{a}\|_p^p$$
lp 정규화로 스파스 소스 패턴 복원 (l1보다 강인).

**소스 스파스 표현:**
$$\boldsymbol{\sigma} = \Phi \boldsymbol{a}, \quad \boldsymbol{a} \in \mathbb{R}^{K}, \quad K \ll N_{src}$$
기저 행렬 $\Phi$로 소스를 희소 계수 $\boldsymbol{a}$로 표현.

**ILO 비용함수 (에어리얼 이미지 기반):**
$$F(\boldsymbol{a}) = \sum_j \left(I(x_j; \boldsymbol{\sigma}(\boldsymbol{a})) - I_{target}(x_j)\right)^2$$

**부분공간 최적화의 변수 감소:**
$$|\mathcal{S}_{sub}| \ll |\mathcal{S}_{all}|$$
부분공간 크기는 전체 소스 픽셀 수보다 훨씬 작아 계산량 감소.

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화 시 회절 부분공간으로 탐색 공간 축소 전략 참고
- `skopc/smo/subspace_source_opt.py`에 마스크 회절 구조 기반 소스 부분공간 정의
- lp-norm (p < 1) 정규화는 스파스 소스 패턴 생성에 l1보다 효과적
- Wang et al. 2020 CS-SMO와 비교: 마스크 변수에도 부분공간 CS 확장 가능

## 참고문헌 (핵심)
- Wang et al., "Fast pixelated SMO compressive sensing," IEEE TASE 2020
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Gradient EUV SMO," IEEE TCI 2019

## 태그
`SMO`, `Optics-Express`, `diffraction-subspace`, `compressive-sensing`, `lp-norm`, `illumination-optimization`, `sparse-source`, `subspace-optimization`, `45nm`, `14nm`, `computational-efficiency`
