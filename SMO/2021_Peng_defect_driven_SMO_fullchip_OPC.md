# Lithography-Defect-Driven Source-Mask Optimization Solution for Full-Chip Optical Proximity Correction

## 메타데이터
- **저자**: Austin Peng, Stephen D. Hsu, Rafael C. Howell, Qinglin Li
- **연도**: 2021
- **게재지/학회**: Applied Optics, Vol. 60, No. 3, pp. 616–620
- **DOI/URL**: https://doi.org/10.1364/AO.409016
- **인용수**: 확인 필요

## 핵심 요약
전체 칩 OPC(광 근접 효과 보정)에서 결함 검출 메커니즘으로 SMO를 직접 구동하는 결함 주도(defect-driven) SMO 방법을 제안한다. 최적화 검증에 사용되는 전체 칩 리소그래피 인쇄 검사와 동일한 결함 감지 방식으로 최적화를 구동하여 결함 없는 출력을 실용적 실행 시간 내에 달성한다. ASML Tachyon SMO 상업 툴을 활용한 실용적 구현을 실증한다.

## 주요 기여
- 결함 감지 메커니즘으로 SMO를 직접 구동하는 결함 주도 최적화 최초 실증
- 전체 칩 규모에서 결함 기반 그래디언트 최적화 실용적 구현
- ASML Tachyon SMO를 활용한 실제 산업 플로우 실증
- 결함 없는 전체 칩 SMO 솔루션을 실용적 실행 시간 내 달성

## 알고리즘/수식
**결함 주도 SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} F_{defect}(\boldsymbol{\sigma}, m) = \sum_{d \in \mathcal{D}} w_d \cdot \text{severity}(d; \boldsymbol{\sigma}, m)$$
결함 집합 $\mathcal{D}$의 심각도 가중합을 최소화.

**결함 심각도 함수:**
$$\text{severity}(d) = \max\left(0, \frac{EPE_d - EPE_{tol}}{EPE_{tol}}\right)^2$$
허용 EPE $EPE_{tol}$을 초과하는 결함에만 페널티 부과.

**전체 칩 확장 전략:**
```
1. 전체 칩 레이아웃에서 결함 포인트 D 추출 (리소 시뮬레이션)
2. 결함 심각도 기반 가중치 w_d 부여
3. 그래디언트 기반 SMO: 결함 주도 비용함수 최소화
4. 전체 칩 리소그래피 검사 재실행 → 잔여 결함 확인
5. 결함 없을 때까지 반복
```

**그래디언트 기반 결함 최소화:**
$$\frac{\partial F_{defect}}{\partial \sigma_k} = \sum_{d \in \mathcal{D}} w_d \frac{\partial \text{severity}(d)}{\partial \sigma_k}$$

**ASML Tachyon SMO 통합:**
산업 표준 전체 칩 SMO 툴과 결함 주도 최적화 루프 통합:
$$\text{Tachyon-SMO} \xrightarrow{\text{결함 감지}} \text{결함 주도 재최적화} \xrightarrow{\text{검증}} \text{결함 없음}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 전체 칩 SMO에서 결함 주도 최적화 플로우 설계 시 핵심 참고
- `skopc/smo/defect_driven_smo.py`에 결함 감지 기반 SMO 재최적화 루프 구현
- Tsai et al. 2011 ASML Tachyon SMO 플로우의 실용적 확장 버전
- 전체 칩 OPC 검증과 SMO 최적화의 긴밀한 루프 통합 방법론 참고

## 참고문헌 (핵심)
- Tsai et al., "Full-chip SMO ASML Brion," SPIE 2011
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Nagahara et al., "SMO 28nm logic," SPIE 2010

## 태그
`SMO`, `Applied-Optics`, `defect-driven`, `full-chip-SMO`, `OPC`, `ASML`, `Tachyon-SMO`, `gradient-based`, `defect-detection`, `lithography-check`, `practical-SMO`
