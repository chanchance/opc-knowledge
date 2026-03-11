# Nonlinear Compressive Inverse Lithography Aided by Low-Rank Regularization

## 메타데이터
- **저자**: Xu Ma, Zhiqiang Wang, Jianchen Zhu, Shengen Zhang, Gonzalo R. Arce, Shengjie Zhao
- **연도**: 2019
- **게재지/학회**: Optics Express, Vol. 27, No. 21, pp. 29992–30008
- **DOI/URL**: https://doi.org/10.1364/OE.27.029992
- **인용수**: 다수

## 핵심 요약
마스크 패턴의 스파스성(sparsity)과 저랭크(low-rank) 특성을 동시에 활용하는 비선형 압축 역 리소그래피(compressive ILT) 방법을 제안한다. 패터닝 오차 최소화와 마스크 스파스·저랭크 정규화를 결합하여 마스크 복잡도를 줄이면서 패터닝 충실도를 향상시킨다. Split Bregman 알고리즘으로 역 최적화 문제를 효율적으로 풀이한다.

## 주요 기여
- 스파스성과 저랭크 정규화를 동시에 활용하는 비선형 압축 ILT 정식화
- Split Bregman 알고리즘으로 결합 스파스+저랭크 최적화 효율적 풀이
- 마스크 복잡도 감소와 패터닝 충실도 동시 향상
- 비선형 이미징 모델 하에서 스파스+저랭크 ILT 실증

## 알고리즘/수식
**비선형 압축 ILT 목적함수:**
$$\min_{M} F(M) + \lambda_s \|M\|_1 + \lambda_r \|M\|_*$$
패터닝 오차 $F(M)$, l1 스파스 패널티 $\|M\|_1$, 핵 노름(nuclear norm) 저랭크 패널티 $\|M\|_*$.

**변수 분리 (Split Bregman):**
보조 변수 $U, V$ 도입:
$$\min_{M, U, V} F(M) + \lambda_s \|U\|_1 + \lambda_r \|V\|_* + \frac{\mu_s}{2}\|M - U\|^2 + \frac{\mu_r}{2}\|M - V\|^2$$

**Split Bregman 반복:**
$$M^{(t+1)} = \arg\min_M F(M) + \frac{\mu_s}{2}\|M - U^{(t)} + b_s^{(t)}\|^2 + \frac{\mu_r}{2}\|M - V^{(t)} + b_r^{(t)}\|^2$$
$$U^{(t+1)} = \text{shrink}(M^{(t+1)} + b_s^{(t)}, \lambda_s/\mu_s)$$
$$V^{(t+1)} = \text{SVT}(M^{(t+1)} + b_r^{(t)}, \lambda_r/\mu_r)$$
수축 연산자(shrink)와 특이값 임계값(SVT) 연산자 적용.

**저랭크 정규화의 의미:**
마스크 패턴 행렬 $M$의 저랭크 구조 → 마스크의 반복 구조(주기성) 반영:
$$\text{rank}(M) \ll \min(m, n)$$

**핵 노름 최소화 (SVT):**
$$\text{SVT}_\tau(M) = U \text{diag}(\max(\sigma_i - \tau, 0)) V^T$$
특이값 분해 $M = U\Sigma V^T$ 후 소프트 임계값 적용.

## OPC 툴 SMO 구현 관련성
- SKOPC ILT/OPC에서 스파스+저랭크 마스크 최적화 구현 시 참고
- `skopc/modeling/opc/sparse_lowrank_ilt.py`에 Split Bregman 기반 압축 ILT 구현
- 저랭크 정규화는 반복 패턴(메모리 셀, SRAM) 마스크의 복잡도 제어에 효과적
- Wang et al. 2020 CS-SMO와 결합 시 마스크에 저랭크 + 소스에 스파스 CS 적용 가능

## 참고문헌 (핵심)
- Sun et al., "Fast nonlinear CS SMO Newton-IHTs," Optics Express 2019
- Song et al., "Inverse litho source opt CS," Optics Express 2014
- Wang et al., "Fast pixelated SMO CS," IEEE TASE 2020

## 태그
`ILT`, `Optics-Express`, `compressive-sensing`, `low-rank`, `sparse`, `nuclear-norm`, `split-Bregman`, `mask-complexity`, `nonlinear-ILT`, `SVT`, `regularization`
