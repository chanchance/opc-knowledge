# Considering MEEF in Inverse Lithography Technology (ILT) and Source Mask Optimization (SMO)

## 메타데이터
- **저자**: Linyong Pang, Guangming Xiao, Vikram Tolani, Peter Hu, Thomas Cecil, Thuc Dam, Ki-Ho Baik, Bob Gleason
- **연도**: 2008
- **게재지/학회**: Proc. SPIE 7122, Photomask Technology 2008, 71221W
- **DOI/URL**: https://doi.org/10.1117/12.803801
- **인용수**: 다수

## 핵심 요약
역 리소그래피 기술(ILT)에서 MEEF(마스크 오차 증폭 인자)를 비용함수의 비선형 인자로 포함시켜 공정 윈도우(PW) 및 EPE 최적화와 동시에 MEEF를 최소화한다. ILT를 통한 소스-마스크 동시 최적화(SMO)에서 마스크 복잡도와 소스 설계의 균형을 맞추어 추가적인 이득을 제공한다. Luminescent Technologies.

## 주요 기여
- MEEF를 ILT 비용함수에 비선형 인자로 통합
- PW, EPE, MEEF 동시 최적화 프레임워크 구축
- ILT 기반 SMO에서 마스크 복잡도-소스 설계 균형 달성
- 레벨셋 ILT SMO에서 MEEF 제어 방법론 제시

## 알고리즘/수식
**MEEF 정의:**
$$MEEF = \frac{\partial CD_{wafer}}{\partial CD_{mask}} \cdot M$$
마스크 CD 변화에 대한 웨이퍼 CD 변화 비율 (배율 $M$ 포함).

**MEEF 포함 ILT 비용함수:**
$$F_{ILT}(m, \boldsymbol{\sigma}) = \sum_j EPE_j^2 + \lambda_{PW} F_{PW} + \lambda_{MEEF} \sum_j MEEF_j^2$$
EPE + 공정 윈도우 + MEEF 항의 가중 합.

**MEEF 그래디언트:**
$$\frac{\partial MEEF_j}{\partial m_p} = \frac{\partial^2 CD_j}{\partial m_p \partial \Delta m}\bigg|_{\Delta m=0}$$
마스크 픽셀 $m_p$에 대한 MEEF 편미분.

**레벨셋 ILT SMO:**
$$\frac{\partial \phi}{\partial t} = -\nabla_\phi F_{ILT}(\phi, \boldsymbol{\sigma})$$
레벨셋 함수 $\phi$로 마스크를 표현하여 ILT 진화.

**MEEF 최소화 소스 최적화:**
$$\boldsymbol{\sigma}^* = \arg\min_\boldsymbol{\sigma} \left[F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{MEEF} \sum_j MEEF_j(\boldsymbol{\sigma}, m)\right]$$

## OPC 툴 SMO 구현 관련성
- SKOPC ILT/SMO에서 MEEF 제어 비용함수 설계 시 참고
- `skopc/modeling/meef_ilt.py`에 MEEF 포함 ILT 비용함수 구현
- `skopc/litho/meef.py`에 MEEF 계산 및 그래디언트 구현
- Peng et al. 2011 그래디언트 SMO의 이전 Luminescent Technologies 연구로 함께 참고

## 참고문헌 (핵심)
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Tolani et al., \"SMO level set methods,\" SPIE 2009
- Dam et al., \"SMO theory to practice,\" SPIE 2010

## 태그
`SMO`, `ILT`, `SPIE`, `MEEF`, `mask-error-enhancement`, `level-set`, `process-window`, `EPE`, `Luminescent-Technologies`, `inverse-lithography`, `cost-function`, `MEEF-minimization`
