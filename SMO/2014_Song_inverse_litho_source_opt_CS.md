# Inverse Lithography Source Optimization via Compressive Sensing

## 메타데이터
- **저자**: Zhiyang Song, Xu Ma, Jie Gao, Jie Wang, Yanqiu Li, Gonzalo R. Arce
- **연도**: 2014
- **게재지/학회**: Optics Express, Vol. 22, No. 12, pp. 14180–14198
- **DOI/URL**: https://doi.org/10.1364/OE.22.014180
- **인용수**: 다수

## 핵심 요약
소스 최적화(source optimization, SO)를 압축 센싱(compressive sensing, CS) 기반 희소 재구성 문제로 정식화하는 방법을 제안한다. 선형화된 Bregman 알고리즘으로 특정 기저에서 희소한 최적 소스 패턴을 합성한다. 선형 SO 정식화가 기존 이차 정식화보다 에어리얼 이미지 대비를 더 효과적으로 향상시키고, 스파스 정규화가 리소그래피 공정 마진 확대에 기여함을 실증한다.

## 주요 기여
- SO를 미결정(underdetermined) 선형 문제로 정식화하여 CS 이론 적용
- 선형화된 Bregman 알고리즘으로 스파스 소스 패턴 효율적 합성
- 선형 SO 정식화의 이차 정식화 대비 우수성 실증
- 스파스 정규화를 통한 소스 제조 가능성 및 공정 마진 향상

## 알고리즘/수식
**선형 SO 정식화 (CS 기반):**
$$\min_{\boldsymbol{a}} \|\boldsymbol{a}\|_1 \quad \text{s.t.} \quad \|T\Phi\boldsymbol{a} - \boldsymbol{b}\|_2^2 \leq \epsilon$$
소스 계수 $\boldsymbol{a}$의 l1-norm 최소화, 이미징 제약 $T\Phi\boldsymbol{a} \approx \boldsymbol{b}$.

**소스 스파스 표현:**
$$\boldsymbol{\sigma} = \Phi \boldsymbol{a}, \quad \|\boldsymbol{a}\|_0 \ll N_{src}$$
기저 행렬 $\Phi$ (예: DCT, Zernike)로 소스를 희소 계수 $\boldsymbol{a}$로 표현.

**선형화된 이미징 모델:**
$$I(x) \approx T(\boldsymbol{\sigma}) \cdot \boldsymbol{\sigma} = \sum_k \sigma_k |h_k * m_0|^2(x)$$
고정 마스크 $m_0$ 하에서 소스에 대한 선형 이미징 모델.

**선형화된 Bregman 알고리즘:**
$$\boldsymbol{a}^{(t+1)} = \text{shrink}\left(\boldsymbol{a}^{(t)} + \delta \Phi^T T^T (b - T\Phi \boldsymbol{a}^{(t)}), \lambda\right)$$
Bregman 반복과 수축 연산자(shrinkage)로 l1 최소화.

**이차 정식화와 선형 정식화 비교:**
- 이차: $\min_\sigma \sum_j (I(x_j;\sigma) - I_t)^2$ → 국소 최솟값 함정 가능
- 선형 CS: l1-norm 최소화 → 전역 희소 해, 더 높은 이미지 대비

**공정 마진 향상:**
스파스 소스 + CS 정규화 → 더 날카로운 조명 분포 → 향상된 NILS, DOF.

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화에 CS 기반 선형 정식화 적용 시 핵심 참고
- `skopc/smo/cs_source_opt.py`에 선형화된 Bregman 알고리즘 기반 소스 최적화 구현
- Wang et al. 2020 CS-SMO와 함께 CS 기반 소스 최적화 방법론 비교 참고
- 스파스 소스 패턴은 FlexRay 조명기의 유한 모드 수 제약과 자연스럽게 일치

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Wang et al., "Fast pixelated SMO compressive sensing," IEEE TASE 2020
- Ma et al., "Diffraction subspace illumination opt," Optics Express 2018

## 태그
`SMO`, `Optics-Express`, `compressive-sensing`, `source-optimization`, `l1-norm`, `sparse-source`, `linearized-Bregman`, `underdetermined`, `NILS`, `process-window`, `sparse-regularization`
