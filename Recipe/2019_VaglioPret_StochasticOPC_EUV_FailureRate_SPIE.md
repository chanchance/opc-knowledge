# OPC Strategies to Reduce Failure Rates with Rigorous Resist Model Stochastic Simulations in EUVL

## 메타데이터
- **저자**: Alessandro Vaglio Pret, Trey Graves, David Blankenship, Stewart A. Robertson, Patrick Lee, John J. Biafore
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X, 2515124
- **DOI/URL**: https://doi.org/10.1117/12.2515124
- **인용수**: ~45

## 핵심 요약
EUV 리소그래피에서 확률론적(stochastic) 공정 변동을 고려한 OPC 전략이 패터닝 실패율을 어떻게 줄이는지 분석한다. 5nm 기술 노드의 다크필드 SRAM 셀을 대상으로, 마스크 바이어싱부터 리고러스 확률론적 레지스트 모델 강화 OPC까지 4가지 OPC 전략을 비교하고, 유기 화학 증폭(CAR) 레지스트와 금속 산화물(MOR) 레지스트의 실패율 차이를 정량화한다. 확률론적 시뮬레이션 기반 OPC가 EUV 패터닝 실패율 저감에 효과적임을 실증한다.

## 주요 기여
1. EUV 확률론적 OPC 4가지 전략의 정량적 실패율 비교
2. CAR vs. MOR 레지스트 실패율 차이 분석 (5nm 노드)
3. 리고러스 확률론적 레지스트 모델 강화 OPC로 실패율 최소화
4. OPC-검증 흐름에 확률론적 핫스팟 스크리닝 필요성 제시

## Recipe/Process Flow 상세

### EUV 확률론적 효과와 패터닝 실패
```
EUV 광자 샷 노이즈:
  EUV 파장 (13.5nm): 광자 에너지 = hc/λ = 92eV (DUV 대비 ~14×)
  동일 도즈: 훨씬 적은 광자 수 → 강한 샷 노이즈
  픽셀당 광자 수: 수십~수백 개 (5nm 노드 최소 피처)
  포아송 분포: σ = √N → 상대 변동 = 1/√N 증가

레지스트 확률론적 효과:
  CAG (화학 증폭 레지스트):
    광산 발생 확률적 → 국소 농도 변동 → LWR/LCDU
  분자 크기: 확산 길이 (~5-20nm) vs. 피처 크기 비교
  MOR (금속 산화물 레지스트):
    낮은 블러, 낮은 샷 노이즈 민감도
    더 낮은 실패율 가능성

패터닝 실패 유형:
  브리지(Bridge): 두 패턴이 불완전하게 연결
  단선(Break): 연속 라인이 끊김
  홀 미인쇄(Missing contact): 컨택 홀 미형성
```

### 4가지 OPC 전략 비교
```
전략 1: 항공 이미지 최적화 (마스크 바이어싱 + 확률론적 시뮬)
  방법: 단순 CD 바이어스 + 포커스-도즈 매트릭스 확률론적 시뮬
  목적: 공정 윈도우 중심에서 실패율 최소화
  한계: 레지스트 물리 미반영

전략 2: Model-based OPC + CAR 레지스트
  방법: 리소그래피 컴팩트 모델 (CAR 레지스트 포함) + MB-OPC
  목적: 레지스트 거동 반영 명목 OPC
  한계: 확률론적 효과 미반영 → 여전히 실패 위험

전략 3: Model-based OPC + MOR 레지스트
  방법: MOR 레지스트 컴팩트 모델 + MB-OPC
  효과: MOR의 낮은 블러/샷 노이즈 → 낮은 실패율
  비교: CAR 대비 7nm 노드에서 유의미한 개선

전략 4: 확률론적 모델 강화 OPC (리고러스)
  방법: 리고러스 확률론적 레지스트 모델 + OPC
    Monte Carlo 시뮬: ~2150 샘플(3.5σ) per 포커스-도즈 포인트
    최종 검증: ~1.8M 트라이얼(5σ) at 최적 조건
  목적: 직접 실패율 최소화 OPC
  결과: 4가지 전략 중 최저 실패율
```

### 확률론적 OPC 방법론
```
공정 윈도우 생성 (확률론적):
  각 (Focus, Dose) 포인트에서 ~2150회 Monte Carlo 시뮬
  실패율 맵: P_fail(F, D) = 브리지 + 단선 + 홀 미인쇄 확률
  최적 F, D: P_fail 최소화 포인트 선택

OPC 목적함수 (확률론적 강화):
  기존: L_OPC = Σ (CD_sim - CD_target)²
  확률론적: L_OPC = Σ P_fail(M) + λ × L_EPE(M)
  → 마스크 M을 실패율 직접 최소화 방향으로 최적화

검증 단계:
  최적 조건에서 1.8M 트라이얼 (5σ) 시뮬레이션
  ppm (parts per million) 수준 실패율 정량화
  OPC 결과의 확률론적 마진 검증
```

### 레지스트 비교 결과
```
CAR vs. MOR (5nm 노드):
  CAR 레지스트:
    높은 블러 → 국소 CD 변동 (LCDU) 큼
    실패율: 수십~수백 ppm 수준 (목표 달성 어려움)

  MOR (Metal-Oxide Resist):
    낮은 블러 (광자 직접 흡수, 확산 적음)
    낮은 샷 노이즈 민감도
    실패율: CAR 대비 수 배 낮음
    7nm에서도 유의미한 이점
    5nm에서 더 두드러진 MOR 이점

전략 4 + MOR:
  최저 실패율 조합 → 5nm EUV 양산 경로 제시
```

## OPC 툴 구현 관련성
- **SKOPC 확률론적 OPC**: `skopc/modeling/litho_engine.py`에 Monte Carlo 확률론적 시뮬 추가
- **실패율 목적함수**: OPC 최적화에 P_fail 기반 손실 함수 통합
- **레지스트 모델 선택**: CAR vs. MOR 레지스트 파라미터 선택 옵션
- **EUV 공정 윈도우**: 확률론적 공정 윈도우 계산으로 실제 EUV 마진 정량화

## 참고문헌
- Proc. SPIE 10957, EUV Lithography X (March 2019)
- 저자 소속: KLA Corporation (John J. Biafore 그룹)
- 관련: Stochastic effects in EUV lithography - DeBisschop (JMM 2017)
- 관련: Compact modeling of stochastics in OPC (SPIE 12494, 2023)
- 관련: EUV OPC modeling requirements (SPIE 9048, 2014)

## 태그
`Recipe`, `SPIE`, `EUV`, `Stochastic`, `OPC`, `FailureRate`, `ResistModel`, `MonteCarlo`, `CAR`, `MOR`, `MetalOxideResist`, `ShotNoise`, `ProcessWindow`, `SRAM`, `5nm`, `2019`
