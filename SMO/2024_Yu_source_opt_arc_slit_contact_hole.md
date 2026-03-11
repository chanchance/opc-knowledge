# Source Optimization for the Whole Arc Slit with Minimum Optical Proximity Correction Applied to Contact Hole Patterns

## 메타데이터
- **저자**: Da-Kyung Yu, Min-Woo Kim, Gug-Yong Kim, Yu-Jin Chae, Seung-woo Son, Michael Yeung, Hye-Keun Oh
- **연도**: 2024
- **게재지**: Proc. SPIE 13215, International Conference on Extreme Ultraviolet Lithography 2024, 132151A (12 November 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3036974

## 핵심 요약
고NA EUV 리소그래피의 DRAM 콘택트 홀 패터닝에서 아크 슬릿(arc slit) 전체에 걸친 강도 변동과 비대칭 광학계(anamorphic optics)로 인한 x/y 방향 CD 차이를 해결하기 위해 전체 아크 슬릿을 고려한 소스 최적화를 수행한다.

## 주요 기여
1. **전체 아크 슬릿 소스 최적화**: 슬릿 중심-가장자리 강도 변동을 고려한 소스 최적화
2. **비대칭 광학계 CD 보정**: 0.55NA 비대칭 광학계에서 x/y 방향 CD 차이 최소화
3. **최소 OPC**: 소스 최적화로 OPC 복잡도 경감
4. **공정 마진 향상**: 수직/수평 패턴 모두에서 공정 마진 개선

## 알고리즘/수식
### 전체 아크 슬릿 소스 최적화
```
고NA EUV 슬릿 좌표: (x_slit, y_field) ∈ 아크 영역

문제:
  I_center(x_slit=0) ≠ I_edge(x_slit=±L/2)
  → 슬릿 위치에 따른 강도 변동 → CD 불균일

소스 최적화 (슬릿 평균화):
min_{J} Σ_{x_s} Σ_{p} ||CD(x_s, p, J) - CD_target||²

여기서:
- x_s: 슬릿 위치 (center to edge)
- p: 패턴 피치/방향
- CD(x_s, p, J): 슬릿 위치 x_s에서 피치 p의 CD

비대칭 광학계 보정:
  0.55NA: 4× (x방향) × 8× (y방향) 축소
  → x/y CD 차이 발생 → 소스 비대칭 보정
```

### 임계값 레벨 조정
```
임계값 레벨을 통한 강도 보정:
  I_eff(x, y) = I_illum(x, y) / I_thresh(x_slit)

슬릿 의존 임계값 조정으로 CD 균일성 확보
```

## OPC 툴 SMO 구현 관련성
- 고NA EUV SMO에서 아크 슬릿 강도 분포 비균일성 모델링 필요
- 비대칭 광학계(4×/8× 축소): x/y 방향 독립적 소스 최적화 필요
- 슬릿 평균화 소스 최적화: SMO 비용 함수에 슬릿 위치 가중 평균 도입
- 콘택트 홀 DRAM 레이어의 전체 슬릿 공정 마진 최적화 방법론

## 태그
`source_optimization`, `EUV`, `high_NA`, `arc_slit`, `contact_hole`, `DRAM`, `anamorphic`, `0.55NA`, `minimum_OPC`, `CD_uniformity`, `SPIE`
