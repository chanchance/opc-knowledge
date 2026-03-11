# Inverse Lithography Source Optimization via Particle Swarm Optimization and Genetic Combined Algorithm

## 메타데이터
- **저자**: (IEEE Photonics Journal, document 9968206, ADS: 2023IPhoJ..1526266S)
- **연도**: 2023
- **게재지/학회**: IEEE Photonics Journal, Vol. 15, No. 2, Article 26266
- **DOI/URL**: https://ieeexplore.ieee.org/document/9968206/
- **인용수**: 확인 필요

## 핵심 요약
입자 군집 최적화(PSO)와 유전 알고리즘(GA)을 결합한 하이브리드 PSOGA 알고리즘으로 픽셀화 소스의 최적 강도 분포를 결정하는 역 리소그래피 소스 최적화(SO) 방법을 제안한다. 픽셀화 소스를 최적화 변수로 디코딩하여 이산적 SO 문제를 메리트 함수 최적 탐색 문제로 변환한다. 기존 단일 GA 및 PSO 대비 수렴 능력에서 우월한 성능을 보인다.

## 주요 기여
- PSO와 GA를 결합한 고효율 하이브리드 PSOGA 알고리즘 제안
- 이산적(discrete) 소스 최적화 문제를 연속 최적화 문제로 변환하는 인코딩/디코딩 체계
- 기존 GA, PSO 단독 알고리즘 대비 수렴 속도 및 최종 해 품질 향상
- 리소그래피 이미징 성능을 역방향으로 향상시키는 메리트 함수 기반 최적화

## 알고리즘/수식
**소스 최적화 메리트 함수:**
$$F_{SO} = \sum_{j} w_j \cdot EPE_j^2 + \lambda_{NILS} \sum_{j} \frac{1}{NILS_j}$$

**PSO 업데이트 규칙:**
$$v_i^{(t+1)} = w \cdot v_i^{(t)} + c_1 r_1 (p_{best,i} - \sigma_i^{(t)}) + c_2 r_2 (g_{best} - \sigma_i^{(t)})$$
$$\sigma_i^{(t+1)} = \sigma_i^{(t)} + v_i^{(t+1)}$$

**GA 교차 및 돌연변이:**
- 교차(crossover): 두 부모 소스 패턴의 픽셀 혼합
- 돌연변이(mutation): 소스 픽셀 강도 랜덤 변동

**PSOGA 하이브리드:**
1. PSO로 전역 탐색 (global search)
2. GA로 지역 정밀화 (local refinement)
3. 두 방법의 최적 해를 교환하며 반복

**픽셀 소스 인코딩:**
$$\sigma_k \in \{0, 1\} \rightarrow \text{이진 문자열로 인코딩 후 최적화}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 소스 최적화에서 그래디언트 불가능 상황(비미분 목적함수)에서의 대안 최적화기로 활용
- `skopc/smo/source_optimizer.py`에 PSO/GA 백엔드 옵션 추가 시 직접 참고
- 이산 소스 패턴 최적화(정수 프로그래밍)가 필요한 경우 적합
- 글로벌 최적해 탐색 능력으로 그래디언트 기반 방법의 로컬 미니마 문제 보완

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO in optical lithography," IEEE TIP 2011
- Rosenbluth et al., "Optimum mask and source patterns," JM3 2002
- Global Source Optimisation Based on Adaptive Nonlinear PSO, IEEE 2021

## 태그
`SMO`, `IEEE`, `particle-swarm-optimization`, `genetic-algorithm`, `PSO-GA-hybrid`, `source-optimization`, `inverse-lithography`, `discrete-optimization`, `metaheuristic`
