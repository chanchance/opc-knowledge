# Source Mask Optimization (SMO) at Full Chip Scale Using Inverse Lithography Technology (ILT) Based on Level Set Methods

## 메타데이터
- **저자**: Linyong Pang, Peter Hu, Danping Peng, Dongxue Chen, Tom Cecil, Lin He, Guangming Xiao, Vikram Tolani, Thuc Dam, Ki-Ho Baik, Bob Gleason
- **연도**: 2009
- **게재지/학회**: Proc. SPIE 7520, Lithography Asia 2009, 75200X
- **DOI/URL**: https://doi.org/10.1117/12.843578
- **인용수**: 다수

## 핵심 요약
레벨셋 방법 기반 역 리소그래피 기술(ILT)을 이용하여 단일 클립에서 다중 클립, 풀칩 규모까지 SMO를 확장하는 계산 프레임워크를 제시한다. 레벨셋 함수로 마스크 윤곽을 표현하고 소스 최적화를 동시에 수행하는 ILT 기반 SMO 방법론을 확립하여 풀칩 규모의 소스-마스크 공동 최적화를 달성한다. Luminescent Technologies.

## 주요 기여
- ILT 레벨셋 기반 SMO를 풀칩 규모로 확장하는 프레임워크
- 단일 클립 → 다중 클립 → 풀칩 SMO 확장 방법론
- 레벨셋 함수 기반 마스크 표현과 소스 최적화 동시 수행
- 풀칩 ILT SMO의 계산 효율 및 실용성 입증

## 알고리즘/수식
**레벨셋 마스크 표현:**
$$m(x) = \mathcal{H}(\phi(x)), \quad \phi(x) \in \mathbb{R}$$
레벨셋 함수 $\phi$의 헤비사이드 함수로 이진 마스크 표현.

**ILT SMO 비용함수:**
$$F_{ILT-SMO}(\phi, \boldsymbol{\sigma}) = \sum_j EPE_j^2(\phi, \boldsymbol{\sigma}) + \lambda_{PW} F_{PW}(\phi, \boldsymbol{\sigma}) + \lambda_{MEEF} F_{MEEF}(\phi, \boldsymbol{\sigma})$$
EPE + 공정 윈도우 + MEEF 항 포함.

**레벨셋 진화 방정식:**
$$\frac{\partial \phi}{\partial t} = -\frac{\partial F_{ILT-SMO}}{\partial \phi} = -\delta(\phi) \sum_j (I_j - I_{t,j}) \frac{\partial I_j}{\partial m}$$

**소스 그래디언트 업데이트:**
$$\sigma_k^{(t+1)} = \sigma_k^{(t)} - \eta \frac{\partial F_{ILT-SMO}}{\partial \sigma_k}$$

**풀칩 SMO 다중 클립 확장:**
$$F_{fullchip}(\phi_{global}, \boldsymbol{\sigma}) = \sum_{c \in \mathcal{C}_{critical}} w_c \sum_j EPE_j^2(\phi_c, \boldsymbol{\sigma})$$
임계 클립 집합 $\mathcal{C}_{critical}$에서 공통 소스 $\boldsymbol{\sigma}$, 클립별 마스크 $\phi_c$ 최적화.

## OPC 툴 SMO 구현 관련성
- SKOPC 레벨셋 ILT 기반 풀칩 SMO 구현 시 핵심 참고
- `skopc/smo/ilt_smo_fullchip.py`에 레벨셋 ILT SMO 풀칩 확장 구현
- Tolani et al. 2009 레벨셋 SMO와 함께 Luminescent Technologies ILT SMO 계열 참고
- Peng et al. 2011 그래디언트 SMO의 이전 단계 ILT SMO로 함께 참고

## 참고문헌 (핵심)
- Tolani et al., \"SMO level set methods,\" SPIE 2009
- Pang et al., \"MEEF ILT SMO,\" SPIE 2008
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `ILT`, `SPIE`, `level-set`, `full-chip`, `inverse-lithography`, `Luminescent-Technologies`, `multi-clip`, `EPE`, `MEEF`, `process-window`, `mask-contour`
