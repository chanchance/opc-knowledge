# A Study of Source and Mask Optimization for ArF Scanners

## 메타데이터
- **저자**: Tomoyuki Matsuyama, Toshiharu Nakashima, Tomoya Noda
- **연도**: 2009
- **게재지/학회**: Proc. SPIE 7274, Optical Microlithography XXII, 727408
- **DOI/URL**: https://doi.org/10.1117/12.813400
- **인용수**: 확인 필요

## 핵심 요약
45nm 노드 이하 ArF 침지 스캐너에서의 SMO 효과를 연구하고 ArF 노광 장치에 대한 SMO 적용 방법을 논한다. SMO가 주요 해상도 향상 기술(RET)로서 침지 리소그래피에서 어떻게 작동하는지 분석하며, ArF 스캐너의 소스 및 마스크 최적화에 대한 실용적 지침을 제공한다. Nikon Corp.

## 주요 기여
- 45nm 이하 ArF 침지 스캐너에서 SMO 효과 분석
- ArF 스캐너 특성을 고려한 SMO 적용 방법론
- 소스 형상과 마스크 설계의 상호 의존성 분석
- 실제 ArF 노광 장치에서의 SMO 실용적 지침

## 알고리즘/수식
**ArF 침지 이미징 모델:**
$$I(x) = \sum_k \sigma_k |h_k * m|^2(x)$$
침지 리소그래피(NA > 1) 부분 결맞음 이미징.

**ArF 소스 최적화:**
$$\boldsymbol{\sigma}^* = \arg\min_{\boldsymbol{\sigma}} \sum_j EPE_j^2(\boldsymbol{\sigma}, m_j)$$
ArF 스캐너 소스 픽셀 최적화.

**공정 윈도우 평가 (ArF 45nm):**
$$PW_{ArF} = \{(dose, focus) : CD \in [CD_{target} \pm 10\%], \, NA \leq 1.35\}$$

**SMO 이점 (ArF 스캐너):**
$$\Delta DOF_{SMO} = DOF_{SMO} - DOF_{conventional} > 0$$
SMO로 달성되는 초점 심도 향상.

**k1 인자 (ArF 침지):**
$$k_1 = \frac{CD \cdot NA}{\lambda} = \frac{45nm \cdot 1.35}{193nm} \approx 0.31$$
저 k1 체계에서 SMO 필요성.

## OPC 툴 SMO 구현 관련성
- SKOPC ArF 침지 리소그래피 SMO 구현 시 실제 스캐너 특성 고려 방법 참고
- `skopc/litho/arf_immersion_model.py`에 ArF 침지 이미징 모델 구현
- Deng et al. 2010, Nagahara et al. 2010과 함께 ArF 스캐너 SMO 실용 계열 참고

## 참고문헌 (핵심)
- Dam et al., \"SMO theory to practice,\" SPIE 2010
- Nagahara et al., \"SMO 28nm logic,\" SPIE 2010
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `ArF`, `immersion-lithography`, `scanner`, `45nm`, `Nikon`, `source-optimization`, `process-window`, `low-k1`, `NA-1.35`
