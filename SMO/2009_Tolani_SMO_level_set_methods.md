# Source-Mask Co-Optimization (SMO) Using Level Set Methods

## 메타데이터
- **저자**: Vikram Tolani, Peter Hu, Danping Peng, Tom Cecil, Robert Sinn, Linyong Pang, Bob Gleason
- **연도**: 2009
- **게재지/학회**: Proc. SPIE 7488, Photomask Technology 2009, 74880Y (29 September 2009)
- **DOI/URL**: https://doi.org/10.1117/12.833430
- **인용수**: 다수

## 핵심 요약
레벨 셋(level set) 방법 기반의 역 리소그래피 기술(ILT)을 소스 최적화로 확장하여 소스-마스크 동시 최적화(SMO)를 구현하는 방법을 제안한다. 레벨 셋 함수 φ(x,y)로 마스크 윤곽을 표현하고, 소스에 대해서도 φ(p,q)로 최적 소스를 결정한다. DOF(심도) 최대화 등 ILT에서 사용되는 동일한 비용함수를 소스 최적화에도 그대로 활용하여 통일된 최적화 프레임워크를 제공한다.

## 주요 기여
- ILT 레벨 셋 방법을 소스 최적화로 자연스럽게 확장한 통합 SMO 프레임워크
- 레벨 셋 기반 마스크 윤곽 표현과 소스 강도 분포의 공동 최적화
- DOF, EL 최대화 등 공정 마진 비용함수를 소스-마스크 동시 최적화에 통합
- 32nm 이하 노드에서 ILT 마스크와 최적화 소스의 조합으로 리소그래피 성능 향상

## 알고리즘/수식
**레벨 셋 마스크 표현:**
$$m(x,y) = H(\phi(x,y))$$
여기서 $H$는 Heaviside 함수, $\phi(x,y) = 0$이 마스크 윤곽선.

**레벨 셋 소스 표현:**
$$\sigma(p,q) = H(\psi(p,q))$$
여기서 $\psi(p,q)$는 소스 도메인에서의 레벨 셋 함수.

**SMO 목적함수 (DOF 최대화):**
$$\max_{\phi, \psi} \quad DOF(\phi, \psi) = \max\{f : I_{min}(f; \phi, \psi) \geq I_{th}\}$$

**레벨 셋 업데이트 (Osher-Sethian 방정식):**
$$\frac{\partial \phi}{\partial t} = -F_{mask}(x,y) |\nabla \phi|$$
$$\frac{\partial \psi}{\partial t} = -F_{source}(p,q) |\nabla \psi|$$
여기서 $F_{mask}$, $F_{source}$는 각각 마스크/소스 도메인의 속도 함수(비용함수의 변분).

**속도 함수 도출:**
$$F_{mask}(x) = -\frac{\delta \text{Cost}}{\delta \phi(x)}, \quad F_{source}(p) = -\frac{\delta \text{Cost}}{\delta \psi(p)}$$

## OPC 툴 SMO 구현 관련성
- SKOPC에서 레벨 셋 기반 마스크 표현을 사용하는 ILT 구현 시 SMO 확장 방법 제시
- `skopc/modeling/opc/ilt.py`의 레벨 셋 ILT를 소스 최적화로 확장하는 직접적 참고
- DOF/EL 기반 공정 마진 최적화 비용함수 설계에 활용
- 위상 전환 마스크(PSM)와 레벨 셋 SMO 결합 가능성 제시

## 참고문헌 (핵심)
- Osher & Sethian, "Fronts propagating with curvature-dependent speed," JCP 1988
- Pang et al., "Level-set-based inverse lithography technology," Proc. SPIE 2006
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008

## 태그
`SMO`, `SPIE`, `level-set-methods`, `ILT`, `inverse-lithography`, `DOF-maximization`, `mask-contour`, `source-optimization`, `32nm-node`, `process-window`
