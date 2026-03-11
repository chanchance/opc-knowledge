# The Inverse Optimization of Lithographic Source and Mask via GA-APSO Hybrid Algorithm

## 메타데이터
- **저자**: Junbo Liu, Ji Zhou, Haifeng Sun, Chuan Jin, Jian Wang, Song Hu
- **연도**: 2023
- **게재지/학회**: MDPI Photonics, Vol. 10, No. 6, Article 638
- **DOI/URL**: https://doi.org/10.3390/photonics10060638
- **인용수**: 확인 필요

## 핵심 요약
유전 알고리즘(GA)과 적응형 입자 군집 최적화(Adaptive PSO, APSO)를 결합한 GA-APSO 하이브리드 알고리즘으로 픽셀화 소스와 마스크의 전역 최적 분포를 역으로 구하는 SMO 방법을 제안한다. 적응형 전략으로 전역 탐색과 지역 탐색의 균형을 맞추어 전역 최솟값에 더 가까운 결과를 달성하면서 GA 및 APSO 단독 대비 패턴 오차를 크게 감소시키고 계산 시간도 단축한다.

## 주요 기여
- GA와 APSO를 결합한 GA-APSO 하이브리드로 전역/지역 탐색 균형 달성
- 적응형 전략으로 알고리즘 수렴 효율 향상
- GA 단독 대비 PE 40.13~52.94% 감소, 시간 75.91~87.00% 단축
- APSO 단독 대비 PE 10.28~33.31% 감소, 시간 48.43~58.66% 단축

## 알고리즘/수식
**GA-APSO 하이브리드 SMO:**
$$\min_{\boldsymbol{\sigma}, m} F = \sum_j PE_j^2(\boldsymbol{\sigma}, m)$$
픽셀화 소스 $\boldsymbol{\sigma}$와 마스크 $m$을 GA-APSO로 동시 최적화.

**GA 연산 (전역 탐색):**
- 선택(Selection): 적합도 기반 토너먼트 선택
- 교차(Crossover): 단일점 또는 다점 교차
- 변이(Mutation): 랜덤 비트 플립

**적응형 PSO (APSO) 속도 업데이트:**
$$v_k^{(t+1)} = w^{(t)} v_k^{(t)} + c_1^{(t)} r_1 (p_k^{best} - x_k^{(t)}) + c_2^{(t)} r_2 (g^{best} - x_k^{(t)})$$
적응형 관성 가중치 $w^{(t)}$와 가속 계수 $c_1^{(t)}, c_2^{(t)}$ 동적 조정.

**적응형 파라미터 조정:**
$$w^{(t)} = w_{max} \exp\left(-\frac{t}{T_{max}} \ln\frac{w_{max}}{w_{min}}\right)$$
지수 감소 관성 가중치.

**GA-APSO 하이브리드 플로우:**
```
1. GA로 초기 집단 생성 및 선택/교차/변이
2. 우수 개체를 PSO 초기 위치로 활용
3. APSO로 지역 정밀화
4. 수렴 체크 → GA 또는 APSO 전환
```

**성능 결과:**
- GA 대비: PE 40~53% 감소, 시간 76~87% 단축
- APSO 대비: PE 10~33% 감소, 시간 48~59% 단축

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에 GA-APSO 하이브리드 전역 최적화 구현 시 참고
- `skopc/smo/ga_apso_smo.py`에 GA+APSO 하이브리드 소스-마스크 최적화 구현
- 적응형 PSO 파라미터 조정은 Wang et al. 2021 ANCS-PSO와 함께 비교 참고
- Yang et al. 2013 RCGA SMO와 함께 유전 알고리즘 기반 SMO 계열로 참고

## 참고문헌 (핵심)
- Yang et al., "GA SMO," SPIE 2013
- Shi et al., "PSO-GA hybrid source opt," IEEE Photonics J. 2023
- Chen et al., "CMA-ES SMO," Optics Express 2020
- Wang et al., "Adaptive PSO source optimization," 2021

## 태그
`SMO`, `MDPI-Photonics`, `GA-APSO`, `genetic-algorithm`, `adaptive-PSO`, `hybrid-metaheuristic`, `gradient-free`, `global-optimization`, `pixelated-source`, `pattern-error`, `evolutionary-computation`
