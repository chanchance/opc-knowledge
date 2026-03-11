# Source Optimization and Mask Design to Minimize MEEF in Low k1 Lithography

## 메타데이터
- **저자**: Guangming Xiao, Tom Cecil, Linyong Pang, Bob Gleason, John McCarty
- **연도**: 2008
- **게재지/학회**: Proc. SPIE 7028, Photomask and Next-Generation Lithography Mask Technology XV, 70280T
- **DOI/URL**: https://doi.org/10.1117/12.793036
- **인용수**: 다수

## 핵심 요약
저 k1 리소그래피에서 MEEF(마스크 오차 증폭 인자)를 최소화하기 위한 소스 최적화 및 마스크 설계 방법을 제시한다. 기존 컷라인 접근법의 한계를 극복하는 에지 기반 2D MEEF 분석 기법을 도입하고, MEEF 인식 공통 공정 윈도우 계산과 공정 변동 밴드 생성 방법을 제안한다. ILT 기반 MEEF 인식 SMO 및 설계 규칙 탐색 결과를 제시한다.

## 주요 기여
- 에지 기반 2D MEEF 분석 기법으로 MEEF 핫스팟 식별
- 픽셀 기반 2D MEEF 컬러 맵 생성 방법
- MEEF 인식 공통 공정 윈도우 계산
- MEEF 인식 SMO (ILT 기반)로 MEEF 최소화

## 알고리즘/수식
**에지 기반 2D MEEF:**
$$MEEF_{edge}(s) = \frac{\partial CD_{wafer}(s)}{\partial CD_{mask}(s)} \cdot M$$
에지 위치 $s$에서 국소 MEEF 계산.

**픽셀 기반 2D MEEF 컬러 맵:**
$$MEEF_{map}(x) = \left|\frac{\partial I(x)}{\partial \delta m} / \frac{\partial I(x)}{\partial x}\right|$$
이미지 강도 $I$의 마스크 CD 변화 및 위치 변화에 대한 편미분 비율.

**MEEF 인식 공정 윈도우:**
$$PW_{MEEF} = \{(\text{dose}, \text{focus}) : MEEF_{all}(dose, focus) \leq MEEF_{spec}\}$$
MEEF 스펙 이하의 조건만 허용하는 공정 윈도우.

**MEEF 인식 SMO 비용함수:**
$$F_{MEEF-SMO}(\boldsymbol{\sigma}, m) = F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{MEEF} \sum_j MEEF_j^2(\boldsymbol{\sigma}, m)$$

**MEEF 공정 변동 밴드:**
$$PVB_{MEEF}(x) = \max_{(\text{dose}, \text{focus}) \in PW} \left|CD(x; dose, focus) - CD_{nom}(x)\right| \cdot MEEF(x)$$

## OPC 툴 SMO 구현 관련성
- SKOPC에서 MEEF 인식 ILT/SMO 구현 시 에지 기반 2D MEEF 분석 참고
- `skopc/litho/meef_2d.py`에 픽셀 기반 2D MEEF 컬러 맵 구현
- `skopc/smo/meef_aware_smo.py`에 MEEF 인식 SMO 비용함수 구현
- Pang et al. 2008 MEEF ILT/SMO와 함께 Luminescent Technologies MEEF SMO 계열 참고

## 참고문헌 (핵심)
- Pang et al., \"MEEF ILT SMO,\" SPIE 2008
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Dam et al., \"SMO theory to practice,\" SPIE 2010

## 태그
`SMO`, `ILT`, `SPIE`, `MEEF`, `MEEF-aware`, `2D-MEEF`, `edge-based-MEEF`, `process-window`, `low-k1`, `mask-error-enhancement`, `Luminescent-Technologies`, `design-rule`
