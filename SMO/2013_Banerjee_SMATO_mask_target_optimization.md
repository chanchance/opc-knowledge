# Methods for Joint Optimization of Mask and Design Targets for Improving Lithographic Process Window

## 메타데이터
- **저자**: Shayak Banerjee, Kanak B. Agarwal, Michael Orshansky
- **연도**: 2013
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 12, No. 2, 023014
- **DOI/URL**: https://doi.org/10.1117/1.JMM.12.2.023014
- **인용수**: 확인 필요

## 핵심 요약
마스크와 설계 타겟 형상을 동시에 수정하여 리소그래피 공정 윈도우를 개선하는 동시 마스크-타겟 최적화(SMATO, Simultaneous Mask And Target Optimization) 방법을 제안한다. 윤곽 충실도와 강인성을 최대화하는 비용함수를 설계하고, PMI(공정 제조 가능성 지수)를 15.4% 감소시키며 레이아웃 핫스팟을 69% 줄이는 효과를 5.5% 런타임 오버헤드로 달성한다.

## 주요 기여
- 마스크-설계 타겟 동시 최적화(SMATO) 방법 제안
- 윤곽 충실도 + 공정 강인성 최대화 비용함수 설계
- PMI 15.4% 감소, 핫스팟 69% 감소 달성
- 런타임 오버헤드 5.5%의 효율적 알고리즘

## 알고리즘/수식
**SMATO 비용함수:**
$$F_{SMATO}(m, d) = \sum_j \left(I_j(m) - I_{target}(d)\right)^2 + \lambda_r \cdot R(m, d)$$
마스크 $m$과 설계 타겟 $d$를 동시 최적화. 강인성 항 $R(m,d)$ 포함.

**공정 제조 가능성 지수 (PMI):**
$$PMI = \frac{1}{N} \sum_j \max\left(0, EPE_j - EPE_{spec}\right)^2$$
스펙 초과 EPE의 제곱합 평균.

**동시 마스크-타겟 업데이트:**
$$m^{(t+1)} = m^{(t)} - \alpha_m \nabla_m F_{SMATO}$$
$$d^{(t+1)} = d^{(t)} - \alpha_d \nabla_d F_{SMATO}$$
마스크와 설계 타겟을 교대로 업데이트.

**타겟 형상 변형 제약:**
$$\|d - d_0\|_\infty \leq \Delta d_{max}$$
원본 설계 타겟 $d_0$에서 최대 허용 이동량 $\Delta d_{max}$ 제한.

**강인성 항 (공정 변동):**
$$R(m, d) = \sum_{\delta \in \Delta} w_\delta \sum_j (I_j(m;\delta) - I_{target}(d))^2$$
공정 변동 집합 $\Delta$ (초점/노광)에 대한 가중 오차.

## OPC 툴 SMO 구현 관련성
- SKOPC OPC에서 마스크-설계 타겟 공동 최적화 시 SMATO 프레임워크 참고
- `skopc/modeling/smato.py`에 마스크-타겟 동시 최적화 구현
- PMI 지표는 `skopc/modeling/metrics.py`에 구현
- 핫스팟 감소 효과는 Li et al. 2012 핫스팟 인식 SMO와 함께 참고

## 참고문헌 (핵심)
- Li et al., \"Hotspot-aware fast SMO,\" Optics Express 2012
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Ma et al., \"Pixelated SMO immersion,\" JOSAA 2013

## 태그
`SMO`, `OPC`, `JMM`, `SPIE`, `SMATO`, `mask-target-optimization`, `design-target`, `PMI`, `hotspot`, `process-window`, `robustness`, `IBM`
