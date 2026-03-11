# Compact Modeling of Stochastics and Application in OPC

## 메타데이터
- **저자**: Werner Gillijns, Jae-uk Lee, Ryan Ryoung-han Kim, Chih-I Wei, Xima Zhang, Azat Latypov, Germain Fenger, John Sturtevant
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940J
- **DOI/URL**: https://doi.org/10.1117/12.2658260

## 핵심 요약
EUV 리소그래피 도입으로 종래의 결정론적(deterministic) OPC 컴팩트 모델로는 대응 불가능해진 확률론적 변동성을 다루기 위해, 경험적 상관관계를 기반으로 개발된 stochastic 컴팩트 모델을 OPC 루프에 직접 적용한 연구. advanced random logic 및 SRAM 설계의 via 레이어에서 stochastic 실패율 감소 효과를 검증한다.

## 주요 기여
1. **Stochastic 컴팩트 모델 OPC 통합**: 기존 hotspot 예측용 stochastic 모델을 실제 OPC 보정 루프에 적용한 최초 사례 중 하나
2. **다양한 OPC 전략 비교**: standard OPC vs stochastic-aware OPC의 실패율 비교
3. **캘리브레이션된 stochastic 모델**: via 레이어 대상 calibrated stochastic model 사용
4. **로직 + SRAM 커버리지**: 두 가지 설계 타입에서 검증하여 범용성 확보

## Recipe/Flow 상세
- **대상 레이어**: Via 레이어 (advanced random logic + SRAM)
- **모델 유형**: Calibrated stochastic compact model
  - 이미지 메트릭(NILS, ILS 등)과 stochastic 변동성의 경험적 상관관계 기반
- **OPC 전략 실험**:
  1. Standard deterministic OPC
  2. Stochastic model-driven OPC (비용함수에 stochastic 항 포함)
  3. Conservative bias + stochastic 결합
- **평가 지표**: stochastic failure rate (SFR), LCDU (Local CD Uniformity)
- **EUV 특화 고려사항**: 광자 수 부족 → 포아송 노이즈 → CD 변동 → 실패율 증가

## OPC 툴 구현 관련성
- EUV OPC 모델 확장: deterministic 모델 위에 stochastic 층 추가
- OPC 비용 함수에 failure probability term 통합 방법론
- Via 레이어 OPC 수렴 전략 (stochastic 고려 시 bias 조정 방향)
- `stochastic_model.py` 구현 참고: 이미지 메트릭 → SFR 매핑 함수

## 태그
`Stochastic`, `EUV`, `OPC`, `CompactModel`, `Via`, `SRAM`, `SPIE`, `2023`
