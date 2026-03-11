# OPC Strategies to Reduce Failure Rates with Rigorous Resist Model Stochastic Simulations in EUVL

## 메타데이터
- **저자**: Alessandro Vaglio Pret, Trey Graves, David Blankenship, Stewart A. Robertson, Patrick Lee, John J. Biafore
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X, 109570J
- **DOI/URL**: https://doi.org/10.1117/12.2515124

## 핵심 요약
EUV 리소그래피의 확률론적(stochastic) 효과가 최종 리소그래피 성능을 제한하는 주요 인자임을 분석하고, 5nm 노드 SRAM 셀에서 다양한 OPC 전략과 레지스트 특성이 고장률(failure rate)에 미치는 영향을 정량적으로 평가한다. 유기 화학 증폭 레지스트(CAR)와 금속 산화물 레지스트(MOR) 비교 연구를 포함한다.

## 주요 기여
1. **확률론적 OPC 전략 비교**: 4가지 OPC 접근법의 고장률 정량 비교
2. **금속 산화물 레지스트 장점 시연**: MOR가 CAR 대비 확률론적 고장률 대폭 감소
3. **엄격한 통계적 검증**: ~180만 시뮬레이션(5σ)으로 ppm 수준 고장률 정량화
4. **공정 창 분석**: 포커스-도즈 행렬 전반에 걸친 고장률 맵핑

## 알고리즘/수식
### 4가지 OPC 전략
1. **케이스 1**: 마스크 바이어싱에 의한 공중 이미지 최적화 (유기 CAR 시뮬레이션)
2. **케이스 2a**: 모델 기반 OPC + 유기 레지스트 모델
3. **케이스 2b**: 모델 기반 OPC + 금속 산화물 레지스트 모델
4. **케이스 3**: 엄격한 확률론적 모델링으로 강화된 모델 기반 OPC (유기 레지스트)

### 확률론적 시뮬레이션 방법
- 공정 창 생성: 각 포커스-도즈 조합에서 ~2150회(3.5σ) 확률론적 시뮬레이션
- 최적 포커스-도즈 조건 결정: 모든 조합에서 고장률 분석
- 정밀 검증: 최적 조건에서 ~180만 회(5σ) 시험 실행
- 비용 함수: 수축/브리징 패턴 고장률 포함한 확률론적 메트릭

### 핵심 수식
```
P_fail = P(CD < CD_min) + P(CD > CD_max)
F(focus, dose) = mean_stochastic_simulations(~2150 runs)
최종 ppm = ~1.8M 시뮬레이션 기반 통계
```

## OPC 툴 SMO 구현 관련성
- EUV SMO 비용 함수에 확률론적 고장률 항목 포함 필요성 시사
- 단순 CD/EPE 최적화를 넘어 ppm 수준 고장률 제어가 차세대 OPC의 핵심
- MOR 레지스트 모델 채택 시 SMO 비용 함수 재설계 필요
- 확률론적 시뮬레이션 기반 공정 창 최적화: 계산 비용 대 정확도 트레이드오프

## 태그
`SMO`, `OPC`, `EUV`, `stochastic`, `resist_model`, `failure_rate`, `SRAM`, `CAR`, `MOR`, `process_window`, `SPIE`
