# Study of EUV Stochastic Defect on Wafer Yield

## 메타데이터
- **저자**: (SPIE 12954 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295404 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010858

## 핵심 요약
EUV 리소그래피의 확률론적 결함(stochastic defect)이 웨이퍼 수율에 미치는 영향을 체계적으로 연구한다. 확률론적 결함 밀도와 수율의 상관관계를 정량화하고, OPC/SMO 관점에서 확률론적 결함을 최소화하는 전략을 제시한다.

## 주요 기여
1. **확률론적 결함-수율 상관관계**: EUV stochastic defect 밀도와 웨이퍼 수율의 정량적 관계
2. **결함 유형 분류**: 브리지(bridge), 네킹(necking), 스팟(spot) 결함의 수율 영향 분석
3. **확률론적 결함 예측 모델**: 공정 조건(도즈, 포커스)에 따른 결함 밀도 예측
4. **수율 개선 전략**: OPC/SMO를 통한 확률론적 결함 감소 방법론

## 알고리즘/수식
### 확률론적 결함 수율 모델
```
EUV 확률론적 결함 유형:
  브리지(bridge): 인접 피처 연결 결함
    P_bridge = P(CD_space < CD_min)
  네킹(necking): 라인 폭 감소 결함
    P_neck = P(CD_line < CD_min)
  스팟(spot): 국소 노출 결함 (광자 샷 노이즈)

결함 밀도:
  D_stoch = D_bridge + D_neck + D_spot
  [결함/단위 면적]

수율 모델:
  Yield = exp(-D_stoch × A_chip)
  A_chip: 칩 면적
  D_stoch: 평균 확률론적 결함 밀도
```

### 공정 조건 최적화
```
도즈 최적화:
  D_stoch ∝ exp(-dose / dose_0)
  → 도즈 증가 시 확률론적 결함 지수적 감소
  단, 처리량(throughput) 저하와 트레이드오프

포커스 최적화:
  D_stoch(focus) → 포커스 이탈 시 급증
  최적 포커스에서 D_stoch 최소

OPC 개입:
  확률론적 인식 OPC:
    SRAF 추가 → NILS 향상 → D_stoch 감소
    에지 바이어스 조정 → CD margin 확보
    → 동일 도즈에서 더 낮은 D_stoch
```

## OPC 툴 SMO 구현 관련성
- 확률론적 수율 SMO: SKOPC SMO 비용 함수에 D_stoch 항 통합
- 확률론적 OPC 보정: P_fail 맵 기반 에지 배치 최적화
- 수율 예측 연계: OPC 결과의 확률론적 수율 시뮬레이션
- 도즈-결함 트레이드오프: SMO에서 도즈 마진과 확률론적 결함 균형 최적화

## 태그
`EUV`, `stochastic`, `defect`, `yield`, `bridge`, `necking`, `P_fail`, `OPC`, `SMO`, `dose`, `SPIE`, `2024`
