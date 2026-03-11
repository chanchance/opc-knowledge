# CTM-SRAF: Continuous Transmission Mask-Based Constraint-Aware Subresolution Assist Feature Generation

## 메타데이터
- **저자**: Yuzhe Ma, Ziyang Yu, Guojin Chen, Peiyu Liao, Bei Yu, Martin D.F. Wong
- **연도**: 2023
- **게재지**: IEEE Transactions on Computer-Aided Design (TCAD), Vol. 42, No. 10, pp. 3402–3411
- **DOI/URL**: https://doi.org/10.1109/TCAD.2023.3239559
- **인용수**: ~30

## 핵심 요약
연속 투과 마스크(CTM: Continuous Transmission Mask)의 강도 분포를 활용하여 설계 규칙을 준수하는 SRAF를 자동 생성하는 CTM-SRAF 방법을 제안한다. CTM 강도 분포에서 SRAF 생성을 가이드하고, 설계 규칙을 이차 제약 정수 프로그래밍으로 형식화하여 빠르게 해결하며, 프로브 기반 SRAF 진화 방법으로 SRAF 형상을 결정한다. ICCAD 2013 벤치마크에서 EPE, L2 손실, PV Band 모두 개선을 달성한다.

## 주요 기여
1. CTM 강도 분포에서 최적 SRAF 위치 자동 도출
2. 설계 규칙(MRC)을 이차 제약 정수 프로그래밍으로 형식화 + 빠른 해법
3. 프로브 기반 SRAF 진화(evolution)로 최적 SRAF 형상 결정
4. ICCAD 2013 벤치마크: EPE, L2, PV Band 모두 개선

## Recipe/Process Flow 상세

### CTM 기반 SRAF 생성의 동기
```
기존 SRAF 방법:
  Rule-based SRAF: Space-Width 테이블 → 단순하지만 부정확
  Model-based SRAF: 리소그래피 시뮬 기반 → 정확하지만 느림
  ILT SRAF: ILT 최적화 내 자동 생성 → 최고 품질, 가장 느림

CTM (Continuous Transmission Mask):
  기존 이진 마스크 (0 또는 1) 대신
  연속 투과율 t(x) ∈ [0, 1] 허용
  CTM 최적화: 더 자유로운 마스크 → 더 나은 공정 윈도우
  CTM 강도 분포: 최적 SRAF 위치 자연스럽게 지시

CTM-SRAF 핵심 아이디어:
  CTM 최적화 결과 → SRAF 위치/형상 힌트 추출
  → 설계 규칙 준수 이진 SRAF 생성
  → CTM 품질의 SRAF를 규칙 준수 이진 마스크로 구현
```

### CTM 기반 SRAF 위치 도출
```
CTM 최적화:
  목적함수: min_t ||I(t) - target||² + λ × R(t)
  t(x): 연속 투과율 (0 ≤ t ≤ 1)
  I(t): Hopkins 모델 항공 이미지
  R(t): 정규화 (이진화 유도)

CTM 강도 해석:
  t(x) > threshold_main: 주 패턴 → 불투명 영역
  t(x) ≈ intermediate: SRAF 후보 → 반투명 영역
  t(x) < threshold_clear: 투명 영역

SRAF 후보 영역 추출:
  SRAF 후보: t(x) ∈ [t_sraf_low, t_sraf_high]
  강도 레벨: CTM 최적화가 SRAF 필요성 암묵적 표현
  공간 위치: CTM 강도 분포의 반투명 영역 위치
```

### 제약 인식 SRAF 생성
```
이진화 제약 (설계 규칙):
  SRAF 크기: w_min ≤ w_sraf ≤ w_max
  SRAF-주 패턴 거리: d_min ≤ d ≤ d_max
  SRAF-SRAF 거리: d_ss_min 이상
  SRAF 인쇄 방지: SRAF 노광 강도 < resist_threshold

이차 제약 정수 프로그래밍:
  변수: SRAF 배치 여부 (이진) + 크기/위치 (연속)
  목적: CTM 강도와의 일치 최대화
  제약: 위 설계 규칙을 이차 제약으로 형식화
  해법: 효율적 분기 한정 또는 반이완(semi-relaxation) 알고리즘

프로브 기반 SRAF 진화:
  초기 SRAF: CTM 강도 기반 직사각형 시드
  진화: 프로브(소규모 형상 변형)로 SRAF 형상 개선
    - 폭 확장/축소: EPE 개선 여부 평가
    - 위치 이동: 설계 규칙 내 이동
    - 추가/제거: 공정 윈도우 기여도 평가
  수렴까지 반복
```

### 성능 결과 (ICCAD 2013 벤치마크)
```
평가 지표:
  EPE (Edge Placement Error): 시뮬 CD - 타겟 CD 오차
  L2 손실: 시뮬 이미지 - 타겟 이미지 L2 거리
  PV Band (공정 변동 밴드): 포커스-도즈 변동 마진

CTM-SRAF vs. Rule-based SRAF:
  EPE: 감소
  L2: 감소
  PV Band: 감소 (더 넓은 공정 윈도우)

CTM-SRAF vs. Model-based SRAF:
  동등하거나 근접한 품질
  속도: CTM-SRAF가 더 빠름 (정수 프로그래밍 기반)
```

## OPC 툴 구현 관련성
- **SKOPC CTM-SRAF**: `skopc/modeling/sraf_generator.py`에 CTM 강도 기반 SRAF 생성 추가
- **CTM 최적화**: OPC 실행 전 CTM 최적화로 SRAF 위치 후보 도출
- **설계 규칙 프로그래밍**: MRC 제약을 정수 프로그래밍으로 SRAF 규칙 준수 보장
- **프로브 진화**: SRAF 형상 최적화에 프로브 기반 진화 방법 적용

## 참고문헌
- IEEE TCAD, Vol. 42, No. 10, pp. 3402–3411 (2023)
- 저자 소속: CUHK (Bei Yu, Martin Wong 그룹)
- 관련: RuleLearner (TCAD 2025)
- 관련: GAN SRAF placement (SPIE 11613, 2021)
- 관련: SRAF placement RL (ICCAD 2022)

## 태그
`Recipe`, `IEEE`, `TCAD`, `SRAF`, `CTM`, `ContinuousTransmissionMask`, `ConstraintAware`, `IntegerProgramming`, `MaskRuleCheck`, `ProcessWindow`, `CUHK`, `BeiYu`, `2023`
