# Feasibility Studies of Source and Mask Optimization

## 메타데이터
- **저자**: Toshiharu Nakashima, Tomoyuki Matsuyama, Soichi Owa
- **연도**: 2009
- **게재지/학회**: Proc. SPIE 7520, Lithography Asia 2009, 75200C
- **DOI/URL**: https://doi.org/10.1117/12.837161
- **인용수**: 확인 필요

## 핵심 요약
SMO 소프트웨어의 효율성을 연구하고 현재 45nm 노드 SRAM 셀 레이어(Active, Gate, Metal)에서 SMO가 효과적임을 입증한다. 저 k1 리소그래피에서 선택된 임계 패턴에 대한 패턴 충실도와 콘트라스트를 유지하는 SMO의 실용 가능성을 검토하며, 22nm 하프피치 공정까지의 적용 전망을 분석한다. Nikon Corp.

## 주요 기여
- 45nm 노드 SRAM 셀 레이어에서 SMO 효율성 입증
- 저 k1 리소그래피에서 SMO 실용 가능성 분석
- 22nm 하프피치 이하 리소그래피에서의 SMO 적용 전망
- SMO 소프트웨어 개발 및 SRAM Active/Gate/Metal 레이어 검증

## 알고리즘/수식
**저 k1 패턴 충실도 유지 SMO:**
$$\boldsymbol{\sigma}^* = \arg\min_\sigma \sum_{p \in \mathcal{P}_{critical}} \sum_j EPE_j^2(\boldsymbol{\sigma}, m_p)$$
임계 패턴 집합 $\mathcal{P}_{critical}$에서 소스 최적화.

**SRAM 셀 패턴 충실도 평가:**
$$F_{SRAM}(\boldsymbol{\sigma}) = \sum_{layer \in \{Active, Gate, Metal\}} w_{layer} \sum_j EPE_j^2(\boldsymbol{\sigma}, m_{layer})$$
SRAM 레이어별 가중 EPE 합.

**콘트라스트 (NILS) 요구 조건:**
$$NILS_j = ILS_j \cdot CD_j \geq NILS_{min}$$
임계 패턴에서 최소 NILS 조건 충족.

**k1 인자 (45nm 노드):**
$$k_1 = \frac{CD \cdot NA}{\lambda} = \frac{45nm \cdot 1.35}{193nm} \approx 0.31$$
저 k1 체계에서 SMO 필요성.

**22nm 적용 전망:**
$$k_1^{22nm} = \frac{22nm \cdot 1.35}{193nm} \approx 0.15 \rightarrow \text{더욱 강화된 SMO 필요}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SRAM 레이어별 SMO 구현 시 레이어 특성을 고려한 패턴 선택 참고
- `skopc/smo/sram_layer_smo.py`에 SRAM 다중 레이어 SMO 구현
- Matsuyama et al. 2009 ArF 스캐너 SMO와 함께 Nikon SMO 연구 계열 참고
- Aoyama et al. 2013 현실적 소스 형상 SMO와 함께 실용적 SMO 계열 참고

## 참고문헌 (핵심)
- Matsuyama et al., \"SMO ArF scanner study,\" SPIE 2009
- Deng et al., \"Considerations in SMO logic,\" SPIE 2010
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `feasibility`, `45nm`, `SRAM`, `Nikon`, `low-k1`, `pattern-fidelity`, `NILS`, `ArF-immersion`, `22nm`, `Active-Gate-Metal`
