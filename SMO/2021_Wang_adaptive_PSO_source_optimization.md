# Global Source Optimisation Based on Adaptive Nonlinear Particle Swarm Optimisation Algorithm for Inverse Lithography

## 메타데이터
- **저자**: Wang J, Liu J B, Hu S
- **연도**: 2021
- **게재지/학회**: IEEE Photonics Journal (IEEE document 9508817); Opto-Electronic Engineering, Vol. 48, No. 9, 210167
- **DOI/URL**: https://ieeexplore.ieee.org/document/9508817/ ; https://doi.org/10.12086/oee.2021.210167
- **인용수**: 확인 필요

## 핵심 요약
적응형 비선형 제어 전략(ANCS)을 결합한 입자 군집 최적화(PSO) 알고리즘으로 역 리소그래피 기술(ILT)에서 픽셀 기반 조명 소스 형상을 전역 최적화한다. ANCS-PSO 알고리즘은 입자 학습 인자를 적응적으로 조정하여 로컬 최적해를 탈출하고, 비선형 제어 접근법으로 탐색 범위를 확장하면서 수렴 속도를 향상시킨다.

## 주요 기여
- 적응형 비선형 제어 전략(ANCS)과 PSO 결합으로 글로벌 소스 최적화
- 학습 인자 적응적 조정으로 로컬 미니마 탈출 능력 향상
- 비선형 제어로 탐색 범위 확장 및 수렴 가속화
- 기존 PSO 대비 우수한 전역 수렴성 및 최종 해 품질 실증

## 알고리즘/수식
**표준 PSO 업데이트:**
$$v_i^{(t+1)} = w v_i^{(t)} + c_1 r_1 (p_{best,i} - \sigma_i^{(t)}) + c_2 r_2 (g_{best} - \sigma_i^{(t)})$$
$$\sigma_i^{(t+1)} = \sigma_i^{(t)} + v_i^{(t+1)}$$

**ANCS: 적응형 학습 인자 조정:**
$$c_1^{(t)} = c_{1,max} - \frac{(c_{1,max} - c_{1,min}) \cdot t}{T_{max}}$$
$$c_2^{(t)} = c_{2,min} + \frac{(c_{2,max} - c_{2,min}) \cdot t}{T_{max}}$$
초기: 자기 인지력 $c_1$ 크게, 사회 인지력 $c_2$ 작게 → 점차 역전.

**비선형 관성 가중치 감소:**
$$w^{(t)} = w_{max} - (w_{max} - w_{min}) \cdot \left(\frac{t}{T_{max}}\right)^2$$

**소스 최적화 메리트 함수:**
$$F_{SO}(\sigma) = \sum_j EPE_j^2(\sigma) + \lambda_{NILS} \sum_j \frac{1}{NILS_j(\sigma)}$$
여기서 $\sigma$는 픽셀 소스 강도 벡터.

**소스 제약:**
$$\sigma_k \in [0, 1], \quad k = 1, ..., N_{pixels}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화에서 PSO 기반 글로벌 탐색 구현 시 ANCS 전략 적용
- 그래디언트 기반 방법의 로컬 미니마 문제를 글로벌 탐색으로 보완
- `skopc/smo/global_source_optimizer.py` 구현 시 ANCS-PSO 알고리즘 참고
- 학습 인자 스케줄링 방법은 다른 메타휴리스틱 알고리즘에도 일반화 적용 가능

## 참고문헌 (핵심)
- Kennedy & Eberhart, "Particle swarm optimization," IEEE ICNN 1995
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Shi et al., "Inverse lithography SO via PSO-GA," IEEE Photonics Journal 2023

## 태그
`SMO`, `IEEE`, `particle-swarm-optimization`, `ANCS-PSO`, `global-optimization`, `source-optimization`, `adaptive-learning-factor`, `nonlinear-control`, `inverse-lithography`, `metaheuristic`
