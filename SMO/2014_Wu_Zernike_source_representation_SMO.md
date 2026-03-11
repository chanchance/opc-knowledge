# Efficient Source Mask Optimization with Zernike Polynomial Functions for Source Representation

## 메타데이터
- **저자**: Xiaofei Wu, Shiyuan Liu, Jia Li, Edmund Y. Lam
- **연도**: 2014
- **게재지/학회**: Optics Express, Vol. 22, No. 4, pp. 3924–3937
- **DOI/URL**: https://doi.org/10.1364/OE.22.003924 (PubMed PMID: 24663713)
- **인용수**: 다수

## 핵심 요약
소스 패턴을 Zernike 다항식 기저 함수의 가중 중첩으로 분해하여 SMO의 소스 최적화 변수 수를 대폭 줄이는 효율적인 SMO 알고리즘을 제안한다. Zernike 기저 함수를 활용함으로써 소스 최적화의 계산 속도를 크게 향상시키면서 동시에 패턴 충실도도 개선한다. 픽셀 단위 자유형 소스 대비 훨씬 적은 변수로 유사하거나 더 나은 최적화 결과를 달성한다.

## 주요 기여
- 소스 패턴을 Zernike 다항식으로 파라미터화하여 변수 수 대폭 감소
- 픽셀 기반 소스 표현 대비 실질적인 속도 향상 달성
- Zernike 소스 파라미터화와 그래디언트 기반 마스크 최적화 통합
- 소스 표현의 물리적 제약(조명기 제조 가능성) 자연스럽게 통합

## 알고리즘/수식
**Zernike 소스 파라미터화:**
$$\sigma(f,g) = \sum_{n,m} \alpha_{nm} Z_{nm}(f,g), \quad \sigma \geq 0$$
여기서 $Z_{nm}$은 Zernike 다항식, $\alpha_{nm}$은 최적화 계수.

**Zernike 다항식 (일부):**
- $Z_1 = 1$ (피스턴)
- $Z_2 = 2\rho\cos\theta$, $Z_3 = 2\rho\sin\theta$ (틸트)
- $Z_4 = \sqrt{3}(2\rho^2 - 1)$ (디포커스)
- $Z_{11} = \sqrt{5}(6\rho^4 - 6\rho^2 + 1)$ (구면 수차)

**변수 수 비교:**
- 픽셀 소스 ($N_{pix}$): $O(N_{pix})$ 변수 (예: 32×32 = 1024개)
- Zernike 소스 ($K$ 항): $O(K)$ 변수 (예: K=36)
→ 약 30배 변수 수 감소.

**Zernike 소스 그래디언트:**
$$\frac{\partial F}{\partial \alpha_{nm}} = \sum_{f,g} \frac{\partial F}{\partial \sigma(f,g)} \cdot Z_{nm}(f,g)$$

**SMO 목적함수:**
$$\min_{\boldsymbol{\alpha}, m} F(I(\boldsymbol{\alpha}, m)) + \lambda_m R_m(m)$$
$$\text{s.t.} \quad \sigma(f,g) = \sum_{nm} \alpha_{nm} Z_{nm}(f,g) \geq 0$$

**비음수 제약 처리:**
$$\alpha_{nm}^{(t+1)} = \max(0, \alpha_{nm}^{(t)} - \mu \nabla_{\alpha_{nm}} F)$$

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화에서 픽셀 기반 대신 Zernike 기저 파라미터화 적용 시 참고
- `skopc/smo/zernike_source.py` 구현으로 변수 수 감소 및 계산 가속화 가능
- Zernike 기저 함수는 실제 조명기(FlexRay 등)의 모드 분해와 자연스럽게 연결
- 제약 있는 소스 최적화에서 비음수 제약 처리 방법 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Li & Lam, "Efficient SMO with augmented Lagrangian," Optics Express 2013
- Ma et al., "Gradient-based SPMO," JM3 2015

## 태그
`SMO`, `Zernike-polynomial`, `source-representation`, `parametric-source`, `variable-reduction`, `computational-efficiency`, `Optics-Express`, `gradient-based`, `basis-function`, `source-parameterization`
