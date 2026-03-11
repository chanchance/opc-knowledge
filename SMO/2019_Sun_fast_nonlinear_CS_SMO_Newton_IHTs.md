# Fast Nonlinear Compressive Sensing Lithographic Source and Mask Optimization Method Using Newton-IHTs Algorithm

## 메타데이터
- **저자**: Yiyu Sun, Naiyuan Sheng, Tie Li, Yanqiu Li, Enze Li, Pengzhi Wei
- **연도**: 2019
- **게재지/학회**: Optics Express, Vol. 27, No. 3, pp. 2754–2770
- **DOI/URL**: https://doi.org/10.1364/OE.27.002754
- **인용수**: 다수

## 핵심 요약
비선형 압축 센싱(nonlinear compressive sensing, CS) 이론을 소스-마스크 최적화에 최초 적용하여 비선형 역 재구성 문제로 SMO를 정식화한다. 비용함수의 2차 미분을 활용하는 Newton 반복 하드 임계값(Newton-IHTs) 알고리즘을 개발하여 수렴을 가속한다. 기존 그래디언트 기반 방법 대비 9.31배, IHTs 기반 방법 대비 7.39배 속도 향상을 달성한다.

## 주요 기여
- 비선형 CS 이론을 SMO에 최초 적용하여 스파스 소스/마스크 최적화 정식화
- Newton-IHTs 알고리즘 개발로 2차 정보 활용한 수렴 가속
- 소스: 공간 기저, 마스크: 2D DCT 기저로 스파스 표현
- 그래디언트 기반 대비 9.31×, IHTs 기반 대비 7.39× 속도 향상

## 알고리즘/수식
**비선형 CS-SMO 정식화:**
$$\min_{\boldsymbol{a}_s, \boldsymbol{a}_m} F(\boldsymbol{\sigma}(\boldsymbol{a}_s), m(\boldsymbol{a}_m))$$
$$\text{s.t.} \quad \|\boldsymbol{a}_s\|_0 \leq K_s, \quad \|\boldsymbol{a}_m\|_0 \leq K_m$$
소스 계수 $\boldsymbol{a}_s$와 마스크 계수 $\boldsymbol{a}_m$의 스파스 제약 최적화.

**소스 스파스 표현 (공간 기저):**
$$\sigma = \Phi_s \boldsymbol{a}_s$$

**마스크 스파스 표현 (2D DCT 기저):**
$$m = \Phi_m \boldsymbol{a}_m, \quad [\Phi_m]_{j,k} = \text{DCT}_k(j)$$

**Newton-IHTs 알고리즘:**
그래디언트 $\boldsymbol{g}^{(t)} = \nabla_{\boldsymbol{a}} F^{(t)}$와 Hessian $\boldsymbol{H}^{(t)} = \nabla^2_{\boldsymbol{a}} F^{(t)}$를 이용:

$$\tilde{\boldsymbol{a}}^{(t+1)} = \boldsymbol{a}^{(t)} - \left(\boldsymbol{H}^{(t)}\right)^{-1} \boldsymbol{g}^{(t)}$$
Newton 방향으로 업데이트 후:
$$\boldsymbol{a}^{(t+1)} = \mathcal{H}_K\left(\tilde{\boldsymbol{a}}^{(t+1)}\right)$$
하드 임계값 연산 $\mathcal{H}_K$로 상위 $K$개 계수만 유지.

**IHTs 기반 수렴 비교:**
- 기존 그래디언트 기반 대비 속도 향상: **9.31×**
- 기존 IHTs 기반 대비 속도 향상: **7.39×**

**Hessian 근사 (연산 효율화):**
$$\boldsymbol{H}^{(t)} \approx \text{diag}\left(\frac{\partial^2 F}{\partial a_i^2}\right)$$
대각 Hessian 근사로 역행렬 연산을 $O(N)$으로 감소.

## OPC 툴 SMO 구현 관련성
- SKOPC 빠른 CS 기반 SMO 구현에서 Newton-IHTs 알고리즘 참고
- `skopc/smo/cs_smo_newton.py`에 비선형 CS-SMO 및 Newton-IHTs 구현
- DCT 기저 마스크 스파스 표현은 ILT 마스크 표현에도 응용 가능
- 기존 Wang et al. 2020 선형 CS-SMO의 비선형 확장 버전으로 성능 비교 참고

## 참고문헌 (핵심)
- Wang et al., "Fast pixelated SMO compressive sensing," IEEE TASE 2020
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Donoho, "Compressed sensing," IEEE TIT 2006

## 태그
`SMO`, `Optics-Express`, `compressive-sensing`, `nonlinear-CS`, `Newton-IHTs`, `hard-thresholding`, `DCT`, `sparse-representation`, `fast-SMO`, `second-order-optimization`, `Hessian`
