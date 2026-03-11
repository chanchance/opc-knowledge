# Optimization of EUV Patterning Using Computational Lithography for Large-Area Stochastic Hot Spot Prediction

## 메타데이터
- **저자**: Jae Young Choi et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134240A (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051180

## 핵심 요약
전산 리소그래피를 이용한 대면적 확률론적 핫스팟 예측으로 EUV 패터닝을 최적화하는 방법을 제시한다. EUV 리소그래피에서 확률론적 결함이 수율에 미치는 영향을 대면적으로 예측하고, 이를 OPC/SMO 최적화에 통합하여 확률론적 핫스팟을 사전에 제거한다.

## 주요 기여
1. **대면적 확률론적 핫스팟 예측**: 전체 칩 수준에서 EUV 확률론적 결함 위치 예측
2. **전산 리소그래피 최적화**: 확률론적 핫스팟 기반 OPC/SMO 최적화
3. **수율 영향 분석**: 확률론적 결함 밀도와 디바이스 수율의 상관관계
4. **EUV 스케일링 지원**: DUV 한계를 넘는 EUV 첨단 노드에서 수율 향상

## 알고리즘/수식
### 대면적 확률론적 핫스팟 예측 방법
```
EUV 확률론적 결함 모델:
  P_fail(x, y) = f(NILS(x, y), dose, resist_params)
  → 위치별 결함 확률 맵 생성

대면적 핫스팟 예측:
  Hot_spot = {(x, y) : P_fail(x, y) > P_threshold}
  P_threshold: 수율 요구사항 기반 설정

전산 리소그래피 최적화:
  min_{J, M} Σ_{(x,y) ∈ Hot_spot} P_fail(x, y)
  + w_CD · Σ_i ||CD_i - CD_t||²

대면적 처리 전략:
  전체 칩 분할 → 타일별 병렬 확률론적 시뮬레이션
  핫스팟 위치 취합 → 타겟된 OPC/SMO 재최적화
```

### 수율-핫스팟 연계
```
디바이스 수율 예측:
  Yield = Π_{모든 셀} (1 - P_fail_cell)
  ≈ exp(-N_cells × P_fail_avg)  (희소 결함 근사)

핫스팟 최소화 효과:
  핫스팟 제거 → P_fail 감소 → 수율 향상
  목표: P_fail_avg < 1/N_cells (수율 > 50% 조건)
```

## OPC 툴 SMO 구현 관련성
- 대면적 확률론적 OPC: SKOPC에서 전체 칩 stochastic 핫스팟 예측 및 보정
- SMO 확률론적 비용 함수: P_fail(x, y) 맵을 SMO 비용 함수에 통합
- 수율 예측 연계: OPC/SMO 결과의 수율 영향 시뮬레이션
- EUV 첨단 노드 지원: 확률론적 OPC가 필수인 EUV 선단 노드 지원

## 태그
`EUV`, `stochastic`, `hotspot`, `computational_lithography`, `large_area`, `yield`, `OPC`, `SMO`, `P_fail`, `SPIE`, `2025`
