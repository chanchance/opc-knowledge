# Process Optimization Through Model-Based SRAF Printing Prediction

## 메타데이터
- **저자**: Ramya Viswanathan, Jaione Tirapu Azpiroz, Punitha Selvam
- **연도**: 2012
- **게재지**: Proc. SPIE 8326, Optical Microlithography XXV
- **DOI/URL**: https://doi.org/10.1117/12.916731
- **인용수**: ~25

## 핵심 요약
SRAF(Sub-Resolution Assist Feature)가 웨이퍼에 인쇄될 가능성을 모델 기반으로 예측하여 SRAF 크기 및 배치를 자동으로 최적화하는 방법론을 제시한다. 기존 SRAF 삽입 흐름에서는 SRAF가 실제로 인쇄되지 않음을 검증하는 단계가 부족했으나, 본 논문은 리소그래피 시뮬레이션으로 SRAF 인쇄 확률을 예측하고 이를 SRAF 크기/위치 최적화에 피드백하는 통합 흐름을 구축한다.

## 주요 기여
1. 모델 기반 SRAF 인쇄 가능성 예측 방법론
2. SRAF 인쇄 예측을 SRAF 크기/배치 최적화에 통합
3. 공정 최적화: SRAF 비인쇄 마진과 주 패턴 공정 윈도우의 동시 개선
4. IBM Research의 SRAF 자동화 흐름에서 실증

## Recipe/Process Flow 상세

### SRAF 인쇄 문제의 중요성
```
SRAF 역할:
  - 주 패턴의 공정 윈도우 확대 (격리 패턴 → 밀집 환경)
  - SRAF 자체는 웨이퍼에 인쇄되면 안 됨 (결함 유발)

SRAF 인쇄 위험:
  - SRAF가 너무 크면: 웨이퍼에 인쇄됨 → 회로 결함
  - SRAF가 너무 작으면: 공정 윈도우 향상 효과 미미
  - 공정 변동(dose, focus): 인쇄 마진 변화

기존 SRAF 흐름의 한계:
  - Rule-based SRAF: Space-Width 테이블 기반 크기 결정
    → 최악 조건에서 인쇄 여부 미검증
  - Model-based SRAF: 항공 이미지 기반 최적화
    → 공정 변동 하에서 SRAF 인쇄 확률 미고려
```

### SRAF 인쇄 예측 모델
```
인쇄 예측 방법:
  입력: SRAF 형상 + 주변 패턴 + 공정 조건
  출력: SRAF 인쇄 확률 또는 인쇄 CD (< 0이면 미인쇄)

시뮬레이션 기반 예측:
  1. 항공 이미지 계산 (컴팩트 광학 모델)
  2. 레지스트 시뮬레이션 (컴팩트 레지스트 모델)
  3. SRAF 위치에서 예상 CD 계산:
     CD_SRAF > 0 → 인쇄 위험
     CD_SRAF < 0 → 안전 (미인쇄)

공정 변동 고려:
  (Focus, Dose) 공간에서 복수 조건 평가
  PV 밴드 내 모든 조건에서 CD_SRAF < 0 요구
  → SRAF 인쇄 마진(SRAF Print Margin)으로 정량화
```

### 통합 최적화 흐름
```
SRAF 인쇄 예측 통합 OPC/SRAF 흐름:

1단계: 초기 SRAF 배치 (Rule-based 또는 MB-SRAF)
   - 공정 윈도우 최대화 목적으로 SRAF 배치

2단계: SRAF 인쇄 예측
   - 각 SRAF에 대해 공정 변동 조건에서 CD 계산
   - SRAF 인쇄 마진 계산:
     M_print = min_{(F,D)∈PW} (CD_threshold - CD_SRAF(F,D))

3단계: SRAF 크기 조정
   a) M_print < M_min (인쇄 위험): SRAF 크기 축소
   b) M_print > M_max (과도한 여유): SRAF 크기 확대
      (더 큰 SRAF로 공정 윈도우 추가 향상)
   c) 크기 조정 → 주 패턴 공정 윈도우 재평가

4단계: 수렴 검사
   모든 SRAF: M_min < M_print < M_max
   주 패턴 공정 윈도우: 목표 달성
   → 완료

5단계: OPC 실행 (주 패턴 + 최종 SRAF 포함)
```

### 어레이 엣지(Array Edge) 최적화
```
어레이 엣지 문제:
  밀집 패턴 어레이의 가장자리 패턴:
  - 한쪽은 밀집 환경, 다른 쪽은 격리
  - → 어레이 내부와 다른 CD 인쇄
  - → SRAF 배치로 어레이 엣지 균일화 필요

어레이 엣지 SRAF 최적화:
  1. 어레이 엣지 패턴 식별
  2. 어레이 내부 CD = 어레이 엣지 CD 목표
  3. SRAF 크기/위치 최적화로 엣지 균일화
  4. 엣지 SRAF 인쇄 마진 검증
```

### 성능 결과 (IBM SRDC 45nm 공정)
```
SRAF 인쇄 마진:
  최적화 전: 일부 SRAF 인쇄 위험
  최적화 후: 모든 SRAF 충분한 인쇄 마진

주 패턴 공정 윈도우:
  SRAF 인쇄 최적화와 공정 윈도우 동시 개선
  도즈 마진(EL): 향상
  DOF: 유지 또는 향상

어레이 엣지 균일도:
  엣지 패턴 CD 편차: 감소
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 인쇄 검증**: `skopc/modeling/sraf_generator.py`에 SRAF 인쇄 마진 계산 추가
- **공정 변동 SRAF 검사**: `skopc/pwo/` 공정 윈도우 평가 시 SRAF 인쇄 확률 함께 출력
- **SRAF 크기 자동 조정**: SRAF 인쇄 마진 피드백으로 SRAF 크기 자동 최적화 루프
- **어레이 엣지 처리**: 배치 러너에서 어레이 엣지 패턴을 별도 식별하여 특수 처리

## 참고문헌
- Proc. SPIE 8326, Optical Microlithography XXV (2012)
- 저자 소속: IBM Semiconductor Research and Development Center
- 관련: Automatic assist feature placement optimization (SPIE 6730, 2007)
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: SRAF printing prediction using ANN (SPIE 11327, 2020)

## 태그
`Recipe`, `SPIE`, `SRAF`, `PrintingPrediction`, `ModelBased`, `ProcessOptimization`, `ProcessWindow`, `ArrayEdge`, `IBM`, `45nm`, `2012`
