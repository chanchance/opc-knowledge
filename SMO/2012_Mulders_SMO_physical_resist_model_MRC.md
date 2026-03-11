# Source-Mask Optimization Incorporating a Physical Resist Model and Manufacturability Constraints

## 메타데이터
- **저자**: Thomas Mülders, Vitaliy Domnenko, Bernd Küchler, Hans-Jürgen Stock, Ulrich Klostermann, Peter De Bisschop
- **연도**: 2012
- **게재지/학회**: Proc. SPIE 8326, Optical Microlithography XXV, 83260G
- **DOI/URL**: https://doi.org/10.1117/12.914047
- **인용수**: 확인 필요

## 핵심 요약
물리적 레지스트 모델을 SMO에 통합하고 마스크 규칙 제약(mask rule constraints, MRC)을 최적화 중에 적용하는 방법을 개발한다. 가변 소스 및 마스크 형상에 대해 단순화된 레지스트 처리보다 더 예측력이 높은 보정된 물리적 레지스트 모델을 SMO에 결합하여 물리적으로 더 현실적인 SMO 결과를 얻는다.

## 주요 기여
- 보정된 물리적 레지스트 모델의 SMO 통합
- 마스크 규칙 제약(MRC) 최적화 중 적용
- 리소그래피 엄밀 시뮬레이션과 SMO 결합
- 가변 소스/마스크 형상에서 향상된 예측 정확도

## 알고리즘/수식
**물리적 레지스트 모델 포함 SMO 비용함수:**
$$F_{resist-SMO}(\boldsymbol{\sigma}, m) = \sum_j EPE_j^2(\boldsymbol{\sigma}, m; M_{resist})$$
물리적 레지스트 모델 $M_{resist}$ 포함.

**물리적 레지스트 모델 (확산-반응):**
$$C_{resist}(x) = \int I(x') \cdot K_{PAC}(x-x') dx'$$
$$CD(x) = f_{threshold}(C_{resist}(x))$$
광산 농도(PAC) 분포 $C_{resist}$와 임계값 함수.

**마스크 규칙 제약 (MRC) 페널티:**
$$C_{MRC}(m) = \sum_{r \in MRC} \max(0, \text{violation}(m; r))^2$$
MRC 위반량의 제곱합 페널티.

**MRC 포함 비용함수:**
$$F_{total}(\boldsymbol{\sigma}, m) = F_{resist-SMO}(\boldsymbol{\sigma}, m) + \lambda_{MRC} C_{MRC}(m)$$

**레지스트 그래디언트:**
$$\frac{\partial F}{\partial m_p} = \sum_j \frac{\partial F}{\partial EPE_j} \cdot \frac{\partial EPE_j}{\partial CD_j} \cdot \frac{\partial CD_j}{\partial I_j} \cdot \frac{\partial I_j}{\partial m_p}$$
레지스트 모델을 통한 체인 룰 그래디언트.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 물리적 레지스트 모델 통합 시 참고
- `skopc/smo/resist_model_smo.py`에 물리적 레지스트 모델 포함 SMO 구현
- MRC 페널티는 `skopc/modeling/mrc_constraints.py`에 구현
- Socha et al. 2010 설계 준수 SMO와 함께 제조 가능성 제약 SMO 계열 참고

## 참고문헌 (핵심)
- Socha et al., \"Design compliant SMO,\" SPIE 2010
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Aoyama et al., \"Realistic source shape SMO,\" JM3 2013

## 태그
`SMO`, `SPIE`, `physical-resist-model`, `MRC`, `mask-rule-constraints`, `manufacturability`, `resist-model`, `PAC`, `rigorous-simulation`, `process-window`
