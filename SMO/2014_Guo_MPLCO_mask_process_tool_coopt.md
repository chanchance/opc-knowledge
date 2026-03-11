# Co-Optimization of the Mask, Process, and Lithography-Tool Parameters to Extend the Process Window

## 메타데이터
- **저자**: Xuejia Guo, Yanqiu Li, Lisong Dong, Lihui Liu
- **연도**: 2014
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS (JM3), Vol. 13, No. 1, 013015 (18 March 2014)
- **DOI/URL**: https://doi.org/10.1117/1.JMM.13.1.013015
- **인용수**: 다수

## 핵심 요약
마스크, 공정, 리소그래피 장비 파라미터를 동시에 최적화하는 MPLCO(Mask-Process-Lithography-tool parameter Co-Optimization) 방법을 개발하여 공정 마진을 확장한다. 정규화 켤레 경도법(normalized conjugate gradient algorithm)을 제안하여 MPLCO의 수렴 효율을 향상시킨다. 기존 SMO 대비 장비 파라미터(NA, 시그마 등) 추가 최적화로 공정 마진 추가 향상을 달성한다.

## 주요 기여
- 마스크 + 공정 파라미터 + 장비 파라미터(NA, sigma 등) 동시 최적화(MPLCO) 방법 개발
- 정규화 켤레 경도법으로 MPLCO 수렴 효율 향상
- 기존 SMO에 장비 파라미터 최적화를 추가하여 추가적인 공정 마진 확보
- 실제 리소그래피 장비 제약 조건 통합

## 알고리즘/수식
**MPLCO 최적화 문제:**
$$\min_{\sigma, m, \mathbf{p}} F(\sigma, m, \mathbf{p})$$
여기서 $\mathbf{p} = [NA, \sigma_{out}, \sigma_{in}, \lambda, ...]$는 장비 파라미터 벡터.

**이미징 모델 (장비 파라미터 포함):**
$$I(x; \sigma, m, \mathbf{p}) = \sum_k \sigma_k(\mathbf{p}) |h_k(x; \mathbf{p}) * m(x)|^2$$
장비 파라미터 $\mathbf{p}$ 변화에 따라 커널 $h_k$와 소스 $\sigma_k$ 모두 변화.

**정규화 켤레 경도법:**
$$\mathbf{x}^{(t+1)} = \mathbf{x}^{(t)} - \alpha^{(t)} \mathbf{d}^{(t)}$$
$$\mathbf{d}^{(t)} = \nabla F(\mathbf{x}^{(t)}) + \beta^{(t)} \mathbf{d}^{(t-1)}$$
$$\beta^{(t)} = \frac{\|\nabla F(\mathbf{x}^{(t)})\|^2}{\|\nabla F(\mathbf{x}^{(t-1)})\|^2} \quad \text{(Fletcher-Reeves)}$$

**공정 마진 목적함수:**
$$F = \sum_j EPE_j^2 + \lambda_{DOF} \frac{1}{DOF} + \lambda_{EL} \frac{1}{EL}$$

**장비 파라미터 제약:**
$$NA \in [NA_{min}, NA_{max}], \quad \sigma \in [\sigma_{min}, \sigma_{max}]$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO를 NA/sigma 장비 파라미터 최적화로 확장 시 직접 참고
- `skopc/smo/tool_param_optimizer.py` 구현 시 MPLCO 알고리즘 참고
- 정규화 켤레 경도법은 `skopc/smo/optimizers.py`에 추가 솔버로 구현 가능
- 마스크+소스+장비 파라미터 통합 최적화 플로우 설계에 활용

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Hashimoto et al., "Robust SMO methodology," Proc. SPIE 8683, 2013

## 태그
`SMO`, `SPIE`, `JM3`, `MPLCO`, `mask-process-tool-optimization`, `NA-optimization`, `sigma-optimization`, `conjugate-gradient`, `process-window`, `lithography-tool-parameters`
