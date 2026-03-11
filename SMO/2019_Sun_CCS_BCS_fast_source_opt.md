# Fast Lithographic Source Optimization Method of Certain Contour Sampling-Bayesian Compressive Sensing for High Fidelity Patterning

## 메타데이터
- **저자**: Yiyu Sun, Yanqiu Li, Tie Li, Xu Yan, Enze Li, Pengzhi Wei
- **연도**: 2019
- **게재지/학회**: Optics Express, Vol. 27, No. 22, pp. 32733–32745
- **DOI/URL**: https://doi.org/10.1364/OE.27.032733
- **인용수**: 다수

## 핵심 요약
확실한 등고선 샘플링(Certain Contour Sampling, CCS)과 베이지안 압축 센싱(Bayesian Compressive Sensing, BCS)을 결합한 소스 최적화 방법(CCS-BCS-SO)을 제안한다. CCS로 소스 패턴의 유일성을 보장하고 계산 복잡도를 대폭 감소시키며, BCS를 해상도 향상 기술(RETs)에 최초 적용하여 고충실도 패턴을 보장한다. 빠른 SO와 높은 패턴 충실도를 동시에 달성한다.

## 주요 기여
- 확실한 등고선 샘플링(CCS)으로 소스 유일성 보장 및 계산 복잡도 감소
- 베이지안 압축 센싱(BCS)을 RETs에 최초 적용하여 고충실도 패턴 달성
- CCS-BCS 결합으로 빠른 SO와 높은 패턴 충실도 동시 달성
- 기존 CS 기반 SO 대비 계산 효율 및 패턴 충실도 우수성 실증

## 알고리즘/수식
**CCS-BCS-SO 목적함수:**
$$\min_{\boldsymbol{a}} \|\boldsymbol{a}\|_1 \quad \text{s.t.} \quad \|T_{CCS}\Phi\boldsymbol{a} - \boldsymbol{b}_{CCS}\|_2^2 \leq \epsilon$$
등고선 샘플링 행렬 $T_{CCS}$로 압축된 측정값 $\boldsymbol{b}_{CCS}$ 사용.

**확실한 등고선 샘플링 (CCS):**
마스크 패턴의 등고선(contour) 상의 샘플 포인트만 선택:
$$T_{CCS} = \{T_j : x_j \in \text{contour}(\text{mask})\}$$
등고선 샘플링으로 전체 이미지 대비 샘플 수 대폭 감소.

**베이지안 압축 센싱 (BCS):**
확률적 선험(prior) 모델로 소스 재구성:
$$p(\boldsymbol{\sigma}|\boldsymbol{a}) = \mathcal{N}(\Phi\boldsymbol{a}, \sigma_n^2 I)$$
$$p(\boldsymbol{a}) = \prod_i \mathcal{N}(a_i; 0, \alpha_i^{-1})$$
자동 연관도 결정(ARD) 선험으로 스파스 소스 재구성.

**BCS 사후 분포:**
$$p(\boldsymbol{a}|\boldsymbol{\sigma}) \propto \mathcal{N}(\boldsymbol{\mu}_a, \boldsymbol{\Sigma}_a)$$
$$\boldsymbol{\mu}_a = \boldsymbol{\Sigma}_a \Phi^T \sigma_n^{-2} \boldsymbol{\sigma}$$
$$\boldsymbol{\Sigma}_a^{-1} = \text{diag}(\boldsymbol{\alpha}) + \sigma_n^{-2} \Phi^T \Phi$$

**계산 복잡도 감소:**
CCS 적용 후: $|\Omega_{CCS}| \ll N_{img}$ → 행렬 연산 크기 대폭 감소.

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화에서 CCS+BCS 결합 방법 구현 시 참고
- `skopc/smo/ccs_bcs_source_opt.py`에 등고선 샘플링 기반 베이지안 CS 소스 최적화 구현
- CCS 등고선 샘플링 전략은 EPE 평가점 선택에도 응용 가능
- BCS의 확률적 소스 재구성은 소스 불확실성 정량화에 활용 가능

## 참고문헌 (핵심)
- Song et al., "Inverse litho source opt CS," Optics Express 2014
- Sun et al., "Fast nonlinear CS SMO Newton-IHTs," Optics Express 2019
- Peng et al., "Gradient-based SMO," IEEE TIP 2011

## 태그
`SMO`, `Optics-Express`, `compressive-sensing`, `Bayesian-CS`, `BCS`, `contour-sampling`, `CCS`, `source-optimization`, `sparse-source`, `fast-SO`, `ARD`, `probabilistic`
