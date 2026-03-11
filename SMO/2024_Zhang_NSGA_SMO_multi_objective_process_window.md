# Multi-Objective and Multi-Solution Source Mask Optimization Using NSGA-II for More Direct Process Window Enhancement

## 메타데이터
- **저자**: Qingyan Zhang, Junbo Liu, Haifeng Sun, Ji Zhou, Chuan Jin, Jian Wang, Yanli Li, Song Hu
- **연도**: 2024
- **게재지/학회**: Optics Express, Vol. 32, No. 4, pp. 5301–5322
- **DOI/URL**: https://doi.org/10.1364/OE.515546
- **인용수**: 확인 필요

## 핵심 요약
비우세 정렬 유전 알고리즘 II(NSGA-II)를 기반으로 하는 다목적·다해(multi-objective, multi-solution) SMO 방법(NSGA-SMO)을 제안한다. 변분 리소그래피 모델(VLIM)을 사용하여 빠른 포커스 변동 에어리얼 이미지를 계산하며, 기존 다목적 SMO 대비 DOF 및 EL을 20% 이상 향상시키고 단일 목적 SMO 대비 4배 이상 향상시킨다.

## 주요 기여
- NSGA-II 기반 다목적 SMO로 DOF와 EL의 파레토 최적 해집합 탐색
- 변분 리소그래피 모델(VLIM)로 빠른 포커스 변동 이미지 계산
- 다해(multi-solution) 특성으로 소스-마스크 설계 공간 탐색
- 기존 다목적 SMO 대비 20% 이상, 단일 목적 SMO 대비 4× 이상 DOF/EL 향상

## 알고리즘/수식
**다목적 SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} \boldsymbol{F} = [F_{EPE}(\boldsymbol{\sigma}, m), -F_{DOF}(\boldsymbol{\sigma}, m), -F_{EL}(\boldsymbol{\sigma}, m)]$$
EPE 최소화와 DOF, EL 최대화를 동시에 추구하는 다목적 최적화.

**NSGA-II 알고리즘:**
```
1. 초기 집단 P₀ 생성 (랜덤 소스/마스크)
2. 반복:
   a. 자식 집단 Q_t 생성 (교차, 변이)
   b. R_t = P_t ∪ Q_t 합집단 형성
   c. 비우세 정렬 (Nondominated Sorting): F₁, F₂, ... 전선 분리
   d. 혼잡도 거리(Crowding Distance) 계산
   e. 상위 N개 선택 → P_{t+1}
3. 최종 파레토 전선 F₁ 반환
```

**비우세 정렬:**
개체 $\boldsymbol{x}$가 $\boldsymbol{y}$를 지배(dominate):
$$\boldsymbol{x} \prec \boldsymbol{y} \iff \forall i: F_i(\boldsymbol{x}) \leq F_i(\boldsymbol{y}) \wedge \exists j: F_j(\boldsymbol{x}) < F_j(\boldsymbol{y})$$

**변분 리소그래피 모델 (VLIM):**
포커스 변동 이미지를 변분 근사:
$$I(x; \delta f) \approx I_0(x) + \delta f \cdot I_1(x) + \delta f^2 \cdot I_2(x)$$
포커스 변동 계수 $I_1, I_2$를 사전 계산하여 빠른 포커스 변동 이미지 평가.

**DOF 및 EL 지표:**
$$DOF = \max\{\delta f : CD_{error}(\delta f) \leq CD_{tol}\}$$
$$EL = \frac{D_{max} - D_{min}}{D_{nominal}} \times 100\%$$

**성능 결과:**
- 기존 다목적 SMO 대비: DOF/EL 20% 이상 향상
- 단일 목적 SMO 대비: 복잡한 패턴에서 4× 이상 향상

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 NSGA-II 기반 다목적 파레토 최적화 구현 시 핵심 참고
- `skopc/smo/nsga_smo.py`에 NSGA-II 기반 다목적 SMO 구현
- VLIM 포커스 변동 모델은 `skopc/litho/vlim.py`에 구현하여 빠른 DOF 계산에 활용
- 파레토 해집합으로 소스-마스크 설계 공간의 DOF-EL 트레이드오프 시각화 가능

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Shi et al., "PSO-GA hybrid source opt," IEEE Photonics J. 2023
- Peng et al., "Defocus antagonism SMO," Optics Express 2022

## 태그
`SMO`, `Optics-Express`, `NSGA-II`, `multi-objective`, `multi-solution`, `Pareto-optimal`, `DOF`, `EL`, `VLIM`, `evolutionary-algorithm`, `process-window`, `nondominated-sorting`
