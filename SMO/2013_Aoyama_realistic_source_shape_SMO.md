# Impact of Realistic Source Shape and Flexibility on Source Mask Optimization

## 메타데이터
- **저자**: Hajime Aoyama, Yasushi Mizuno, Noriyuki Hirayanagi, Naonori Kita, Ryota Matsui, Hirohiko Izumi, Keiichi Tajima, Joachim Siebert, Wolfgang Demmerle, Tomoyuki Matsuyama
- **연도**: 2013
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 13, No. 1, 011005
- **DOI/URL**: https://doi.org/10.1117/1.JMM.13.1.011005
- **인용수**: 확인 필요

## 핵심 요약
현실적인 소스 형상(realistic source shape)과 소스 유연성(source flexibility)이 SMO 성능에 미치는 영향을 분석한다. SRAM 패턴을 타겟으로 이상적인 픽셀화 소스와 실제 조명기(FlexRay 등 프로그래머블 조명기)에서 구현 가능한 현실적인 소스 형상 사이의 차이가 SMO 결과에 어떻게 영향을 주는지 조사하며, 소스 제약 조건(source manufacturability constraints)이 최적화 성능에 미치는 영향을 정량화한다.

## 주요 기여
- 이상적 픽셀화 소스 vs. 현실적 소스 형상의 SMO 성능 차이 정량화
- 소스 유연성(flexibility) 제약이 패턴 충실도 및 공정 윈도우에 미치는 영향 분석
- FlexRay 등 프로그래머블 조명기에서 SMO 출력 소스 구현 가능성 평가
- SRAM 패턴 타겟에서 현실적 소스 형상 SMO의 실용적 지침 제시

## 알고리즘/수식
**소스 제약 조건 포함 SMO 비용함수:**
$$F(\boldsymbol{\sigma}, m) = \sum_j EPE_j^2(\boldsymbol{\sigma}, m) + \lambda_s \cdot C_{source}(\boldsymbol{\sigma})$$
소스 제조 가능성 제약 비용 $C_{source}$ 포함.

**현실적 소스 모델 (가우시안 평활화):**
$$\sigma_{real}(x) = \sigma_{ideal}(x) * g_s(x; r_s)$$
이상적 픽셀화 소스 $\sigma_{ideal}$에 평활화 커널 $g_s$ (반경 $r_s$) 적용.

**소스 충실도 평가 지표:**
$$\varepsilon_{source} = \frac{\|\sigma_{real} - \sigma_{ideal}\|_2}{\|\sigma_{ideal}\|_2}$$
이상적 소스 대비 현실적 소스 구현 오차.

**소스 유연성 (픽셀 해상도 제약):**
$$\sigma_{flex}(x) = \sum_k a_k \cdot B_k(x), \quad |a_k| \leq A_{max}$$
기저 함수 $B_k$로 소스 형상 매개변수화 및 진폭 제한.

**SMO 공정 윈도우 평가:**
$$PW = \{(\text{dose}, \text{focus}) : CD_{all} \in [CD_{target} \pm \Delta CD]\}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 소스 제약(manufacturability) 모델링 시 현실적 소스 형상 제약 참고
- `skopc/smo/source_constraints.py`에 소스 평활화 및 픽셀 해상도 제약 구현
- FlexRay/FlexPupil 등 실제 조명기 소스 구현 시 소스 충실도 평가 지표 활용
- Deng et al. 2010 SPIF 분석과 함께 실용적 SMO 소스 설계 지침으로 활용

## 참고문헌 (핵심)
- Deng et al., \"Considerations in SMO for logic,\" SPIE 2010
- Nagahara et al., \"SMO 28nm logic,\" SPIE 2010
- Dam et al., \"SMO theory to practice,\" SPIE 2010

## 태그
`SMO`, `JMM`, `SPIE`, `realistic-source`, `source-shape`, `source-flexibility`, `FlexRay`, `programmable-illuminator`, `source-constraints`, `SRAM`, `manufacturability`, `process-window`
