# Vectorial Mask Optimization Methods for Robust Optical Lithography

## 메타데이터
- **저자**: Xu Ma, Yanqiu Li, Xuejia Guo, Lisong Dong
- **연도**: 2012
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 11, No. 4, 043008
- **DOI/URL**: https://doi.org/10.1117/1.JMM.11.4.043008
- **인용수**: 다수

## 핵심 요약
NA > 0.6인 리소그래피 시스템에서 스칼라 모델의 부정확성을 극복하기 위해 벡터 이미징 모델 기반 강인(robust) 픽셀화 그래디언트 OPC 및 PSM 최적화 알고리즘을 개발한다. 파면 수차(wavefront aberration)와 편광 수차(polarization aberration)를 보정하는 마스크 최적화가 가능하며, 일반화 웨이블릿 페널티로 마스크 복잡도와 수렴 오차를 균형 있게 제어한다.

## 주요 기여
- 벡터 이미징 모델 기반 강인 픽셀화 그래디언트 OPC/PSM 최적화 개발
- 파면 수차 및 편광 수차 보정 가능한 마스크 최적화 프레임워크
- 일반화 웨이블릿 페널티로 마스크 복잡도-수렴 오차 균형 제어
- 강인성: 공정 변동(초점/노광/수차)에 강인한 마스크 최적화

## 알고리즘/수식
**벡터 이미징 모델 (TCC 형태):**
$$I(x) = \iint TCC^V(\mathbf{f}_1, \mathbf{f}_2) M(\mathbf{f}_1) M^*(\mathbf{f}_2) e^{i2\pi(\mathbf{f}_1-\mathbf{f}_2)\cdot x} d\mathbf{f}_1 d\mathbf{f}_2$$

**벡터 TCC:**
$$TCC^V(\mathbf{f}_1, \mathbf{f}_2) = \int J(\mathbf{f}_s) \sum_\alpha H_\alpha(\mathbf{f}_1+\mathbf{f}_s) H_\alpha^*(\mathbf{f}_2+\mathbf{f}_s) d\mathbf{f}_s$$
편광 성분 $\alpha \in \{x,y,z\}$에 대한 합산.

**강인 마스크 최적화 비용함수:**
$$F_{robust}(m) = \sum_{\delta \in \Delta} w_\delta \sum_j (I_j(m;\delta) - I_{target,j})^2 + \lambda_w \Omega_W(m)$$
공정 변동 집합 $\Delta$에 걸친 가중 오차 + 웨이블릿 정규화.

**그래디언트 (SOCS 기반):**
$$\frac{\partial F}{\partial m_p} = 4\sum_\delta w_\delta \sum_j (I_j - I_{t,j}) \text{Re}\left[\sum_n c_n (h_n * m)_j h_n^*(x_j - x_p)\right]$$
SOCS(Sum of Coherent Systems) 분해를 이용한 그래디언트 계산.

**일반화 웨이블릿 페널티:**
$$\Omega_W(m) = \sum_{k} |[Wm]_k|^p, \quad 1 \leq p \leq 2$$
웨이블릿 변환 $W$의 계수 $l_p$-노름으로 마스크 복잡도 제어.

**수차 포함 pupil 함수:**
$$H_\alpha(\mathbf{f}; \text{aber}) = H_\alpha^0(\mathbf{f}) \cdot \exp\left(i \sum_n a_n Z_n(\mathbf{f})\right)$$
Zernike 계수 $a_n$로 파면 수차 모델링.

## OPC 툴 SMO 구현 관련성
- SKOPC 고NA 강인 마스크 최적화 시 벡터 이미징 기반 OPC/PSM 구현 참고
- `skopc/modeling/robust_vector_opc.py`에 수차 보정 벡터 이미징 마스크 최적화 구현
- 웨이블릿 페널티는 `skopc/modeling/regularization.py`에 구현
- Ma et al. 2012 JOSAA 벡터 이미징 마스크 최적화와 함께 벡터 이미징 OPC 계열 참고

## 참고문헌 (핵심)
- Ma et al., \"Mask optimization approaches vector imaging,\" JOSAA 2012
- Ma et al., \"Pixelated SMO immersion,\" JOSAA 2013
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`OPC`, `ILT`, `JMM`, `SPIE`, `vector-imaging`, `vectorial-mask-optimization`, `robust-OPC`, `wavelet-penalty`, `aberration-compensation`, `polarization-aberration`, `high-NA`, `SOCS`, `gradient-based`
