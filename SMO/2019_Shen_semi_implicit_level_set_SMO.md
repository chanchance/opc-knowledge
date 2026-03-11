# Semi-Implicit Level Set Formulation for Lithographic Source and Mask Optimization

## 메타데이터
- **저자**: Yijiang Shen, Fei Peng, Zhenrong Zhang
- **연도**: 2019
- **게재지/학회**: Optics Express, Vol. 27, No. 21, pp. 29659–29668
- **DOI/URL**: https://doi.org/10.1364/OE.27.029659
- **인용수**: 다수

## 핵심 요약
레벨 셋 SMO에서 명시적 오일러 전진(explicit Euler-forward) 방식의 CFL 조건에 의한 제한적 시간 스텝 문제를 해결하는 반암묵적(semi-implicit) 레벨 셋 SMO 방법을 제안한다. 안정성 관련 항을 암묵적으로 이산화하고 연산자 분리(operator splitting)를 적용하여 소스와 마스크를 좌표 방향별로 독립적으로 업데이트한다. Thomas 알고리즘으로 삼각 선형 시스템을 풀어 수렴 속도를 크게 향상시킨다.

## 주요 기여
- CFL 조건을 극복하는 반암묵적 레벨 셋 SMO 정식화
- 연산자 분리(operator splitting)로 소스/마스크 좌표별 독립 업데이트
- Thomas 알고리즘 기반 삼각 선형 시스템의 효율적 풀이
- 거리 레벨 셋 정규화 개혁 정식화와의 결합으로 안정적 곡선 진화

## 알고리즘/수식
**레벨 셋 마스크 진화 방정식:**
$$\frac{\partial \phi}{\partial t} = -F_{mask}|\nabla \phi| + \lambda R(\phi)$$
속도 함수 $F_{mask}$로 마스크 윤곽 진화, $R(\phi)$는 거리 정규화 항.

**CFL 조건 (명시적 방법의 한계):**
$$\Delta t \leq \frac{h}{|F_{max}|}$$
명시적 방법에서 시간 스텝 $\Delta t$가 격자 간격 $h$와 최대 속도 $F_{max}$에 제한됨.

**반암묵적 이산화:**
안정성 관련 확산 항을 암묵적으로 처리:
$$\frac{\phi^{(t+1)} - \phi^{(t)}}{\Delta t} = F_{explicit}^{(t)} + D_{implicit}^{(t+1)}$$
비선형 항 $F_{explicit}$ 명시적, 확산 항 $D_{implicit}$ 암묵적.

**연산자 분리 (Operator Splitting):**
$$\phi^{(t+1/2)} = \phi^{(t)} - \Delta t \frac{\partial}{\partial x}\left(\cdot\right)_x \quad \text{(x 방향)}$$
$$\phi^{(t+1)} = \phi^{(t+1/2)} - \Delta t \frac{\partial}{\partial y}\left(\cdot\right)_y \quad \text{(y 방향)}$$
각 방향을 독립적으로 처리.

**Thomas 알고리즘 (삼각 시스템):**
각 방향의 암묵적 이산화는 삼각 행렬 시스템 $A\phi = b$:
$$a_i \phi_{i-1} + b_i \phi_i + c_i \phi_{i+1} = d_i$$
Thomas 알고리즘으로 $O(N)$ 시간에 풀이.

**소스 업데이트:**
$$\frac{\partial F_{SMO}}{\partial \sigma_k} = \sum_x \frac{\partial F}{\partial I(x)} \cdot |h_k * m|^2(x)$$
픽셀 기반 소스는 그래디언트로 업데이트.

## OPC 툴 SMO 구현 관련성
- SKOPC 레벨 셋 기반 ILT/SMO 구현에서 CFL 제약 극복 방법으로 핵심 참고
- `skopc/smo/semi_implicit_ls_smo.py`에 반암묵적 레벨 셋 SMO 구현
- 연산자 분리 + Thomas 알고리즘은 2D 레벨 셋 진화의 효율적 구현 패턴
- Shen 2018 협대역 레벨 셋 SMO의 수렴 가속 후속 연구로 함께 참고

## 참고문헌 (핵심)
- Shen, "Narrow-band level-set SMO," Optics Express 2018
- Tolani et al., "SMO level set," SPIE 7488, 2009
- Osher & Sethian, "Level set methods," JCP 1988

## 태그
`SMO`, `Optics-Express`, `level-set`, `semi-implicit`, `CFL-condition`, `operator-splitting`, `Thomas-algorithm`, `tridiagonal`, `convergence-acceleration`, `mask-contour`, `signed-distance-function`
