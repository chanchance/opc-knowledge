# Level-Set Based Mask Synthesis with a Vector Imaging Model

## 메타데이터
- **저자**: Yijiang Shen
- **연도**: 2017
- **게재지/학회**: Optics Express, Vol. 25, No. 18, pp. 21775–21790
- **DOI/URL**: https://doi.org/10.1364/OE.25.021775
- **인용수**: 확인 필요

## 핵심 요약
22nm 이하 기술 노드에서 스칼라 이미징 모델의 부정확성을 극복하기 위해 벡터 이미징 모델을 기반으로 한 레벨셋 마스크 합성(level-set mask synthesis) 방법을 개발한다. 광마스크 합성을 역 이미징 문제로 정식화하고 안정적인 시간 의존 변분 레벨셋 모델로 재표현하여 켤레 기울기(conjugate gradient) 방법과 유한 차분 기법으로 풀어 패턴 충실도, EPE, 수렴 성능을 동시에 개선한다.

## 주요 기여
- 벡터 이미징 모델 기반 레벨셋 마스크 합성 프레임워크 개발
- 안정적 시간 의존 변분 레벨셋 모델로 역 이미징 문제 정식화
- 켤레 기울기 + 최적 시간 스텝 유한 차분으로 수렴 가속
- 패턴 충실도, EPE, 계산 가속 동시 개선

## 알고리즘/수식
**벡터 이미징 강도 모델:**
$$I(x) = \sum_k \sigma_k \sum_{\alpha \in \{x,y,z\}} \left| \int M(\mathbf{f}) H_{k,\alpha}(\mathbf{f}) e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f} \right|^2$$
TE/TM/z 편광 성분별 pupil $H_{k,\alpha}$ 포함 벡터 TCC 기반 강도.

**레벨셋 마스크 표현:**
$$m(x) = \mathcal{H}(\phi(x)) = \begin{cases} 1 & \phi(x) > 0 \\ 0 & \phi(x) \leq 0 \end{cases}$$
레벨셋 함수 $\phi$의 헤비사이드 함수로 이진 마스크 표현.

**변분 레벨셋 비용함수:**
$$F(\phi) = \sum_j \left(I(x_j; \phi) - I_{target,j}\right)^2 + \lambda_\phi \int |\nabla \phi| \, dx$$
이미지 충실도 항 + 레벨셋 정규화(perimeter) 항.

**레벨셋 진화 방정식 (시간 의존 모델):**
$$\frac{\partial \phi}{\partial t} = -\frac{\partial F}{\partial \phi} = -\sum_j (I_j - I_{t,j}) \frac{\partial I_j}{\partial \phi} + \lambda_\phi \nabla \cdot \left(\frac{\nabla \phi}{|\nabla \phi|}\right)$$

**켤레 기울기 그래디언트 (벡터 모델):**
$$\frac{\partial F}{\partial \phi_p} = \delta(\phi_p) \cdot \sum_j (I_j - I_{t,j}) \frac{\partial I_j}{\partial m_p}$$
디렉 델타 $\delta(\phi_p)$를 통한 레벨셋 그래디언트.

**최적 시간 스텝 (CFL 조건 완화):**
$$\Delta t^* = \arg\min_{\Delta t} F(\phi - \Delta t \cdot \nabla_\phi F)$$

## OPC 툴 SMO 구현 관련성
- SKOPC 고NA 벡터 이미징 기반 레벨셋 ILT 구현 시 핵심 참고
- `skopc/modeling/vector_level_set_ilt.py`에 벡터 이미징 레벨셋 마스크 합성 구현
- Shen et al. 2018 narrow-band level-set SMO의 이전 단계 벡터 이미징 확장
- Ma et al. 2012 JOSAA 벡터 마스크 최적화와 함께 벡터 이미징 계열 참고

## 참고문헌 (핵심)
- Ma et al., \"Mask optimization approaches vector imaging,\" JOSAA 2012
- Shen et al., \"Narrow-band level-set SMO,\" Optics Express 2018
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`ILT`, `OPC`, `Optics-Express`, `level-set`, `vector-imaging`, `mask-synthesis`, `conjugate-gradient`, `variational`, `high-NA`, `TE-TM-z`, `22nm`, `inverse-lithography`
