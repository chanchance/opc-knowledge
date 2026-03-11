# Acceleration Method for Source Mask Optimization at 7nm Technology Node

## 메타데이터
- **저자**: Xiaojing Su, Lisong Dong, Yunyun Hao, Yajuan Su, Yayi Wei
- **연도**: 2021
- **게재지/학회**: Proc. SPIE 11855, Photomask Technology 2021, 118550Y
- **DOI/URL**: https://doi.org/10.1117/12.2600884
- **인용수**: 확인 필요

## 핵심 요약
7nm 기술 노드에서 SMO의 긴 실행 시간을 단축하기 위한 가속 워크플로우를 제안한다. SMO 후보 수를 줄여 총 런타임을 감소시키는 새로운 가속 방법론을 개발하여 적격 중첩 공정 윈도우를 유지하면서 최적화 효율을 향상시킨다.

## 주요 기여
- SMO 후보 수 감소로 총 런타임 단축하는 가속 워크플로우
- 7nm 임계 레이어 SMO 반복 프로세스 단축 방법론
- 적격 중첩 공정 윈도우 유지하면서 효율 향상
- SMO 후보 선택 및 필터링 전략

## 알고리즘/수식
**가속 SMO 워크플로우:**
```
1. 초기 후보 집합: C_all = {모든 소스 후보}
2. 후보 필터링: C_filtered ⊂ C_all (빠른 평가로 불량 후보 제거)
3. 정밀 SMO: σ* = argmin F_SMO(σ, m) for σ ∈ C_filtered
4. 공정 윈도우 검증: PW_overlap ≥ PW_spec
```

**후보 필터링 기준:**
$$\mathcal{C}_{filtered} = \{c \in \mathcal{C}_{all} : F_{quick}(c) \leq F_{threshold}\}$$
빠른 평가 비용함수 $F_{quick}$으로 후보 사전 필터링.

**중첩 공정 윈도우 최대화:**
$$PW_{overlap} = \bigcap_{p \in \mathcal{P}_{critical}} PW_p(\boldsymbol{\sigma}, m_p)$$

**가속 비율:**
$$\text{Speedup} = \frac{T_{conventional}}{T_{accelerated}} = \frac{|\mathcal{C}_{all}|}{|\mathcal{C}_{filtered}|} \cdot \frac{T_{full}}{T_{quick}}$$

**SMO 비용함수 (7nm 노드):**
$$F_{SMO}(\boldsymbol{\sigma}, m) = \sum_j EPE_j^2 + \lambda_{PW} F_{PW} + \lambda_{ILS} F_{ILS}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 가속 워크플로우 구현 시 후보 필터링 전략 참고
- `skopc/smo/accelerated_smo.py`에 후보 필터링 기반 가속 SMO 구현
- Sun et al. 2022 샘플링 기반 이미징 3× 가속과 함께 SMO 가속 계열 참고
- Su et al. 2021 설계 패턴 라이브러리 SMO와 함께 7nm SMO 최적화 계열 참고

## 참고문헌 (핵심)
- Su et al., \"SMO design pattern library 7nm,\" SPIE 2021
- Sun et al., \"Sampling-based imaging fast SMO,\" Applied Optics 2022
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `7nm`, `acceleration`, `candidate-filtering`, `runtime-reduction`, `process-window`, `overlap-PW`, `Photomask-Technology`, `Institute-of-Microelectronics`
