# Multi-Objective and Multi-Solution Source Mask Optimization Using NSGA-II for Process Window Enhancement

## 메타데이터
- **저자**: (PubMed/SPIE 2024 - Advanced Lithography / SMO 연구)
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM) / SPIE Advanced Lithography
- **DOI/URL**: https://pubmed.ncbi.nlm.nih.gov/38439261/
- **인용수**: ~10

## 핵심 요약
NSGA-II(Non-dominated Sorting Genetic Algorithm II) 다목적 진화 알고리즘을 소스-마스크 최적화(SMO)에 적용하여 공정 윈도우(DOF × EL)를 직접 향상시키는 NSGA-SMO 방법론을 제시한다. VLIM(Variational Lithography Model)을 통해 포커스 변동 항공 이미지를 빠르게 시뮬레이션하고, NSGA-II가 DOF와 EL을 동시에 최대화하는 다중 비지배 해를 탐색한다. 기존 단목적 SMO 대비 DOF + EL 20% 이상 개선, 복잡한 패턴에서 단목적 SMO 대비 최대 4배 향상을 달성한다.

## 주요 기여
1. NSGA-II 기반 다목적 SMO로 공정 윈도우 직접 최적화
2. VLIM 기반 빠른 공정 변동 시뮬레이션 통합
3. 단일 해 대신 다수 비지배 해(Pareto frontier) 제공
4. 복잡한 패턴에서 단목적 SMO 대비 4배 공정 윈도우 향상

## Recipe/Process Flow 상세

### 기존 SMO와 NSGA-SMO의 차이
```
기존 단목적 SMO:
  목적함수: min EPE (명목 조건에서만)
  문제:
    명목에서 최적 → 공정 변동 하에서 취약
    DOF와 EL이 트레이드오프 → 한쪽만 최적화

기존 다목적 SMO (가중합 방법):
  목적함수: min (w1 × EPE + w2 × PVB)
  문제:
    가중치 w1, w2 설정 의존적
    Pareto 전선의 일부만 탐색

NSGA-SMO:
  목적함수: min EPE, max DOF, max EL (동시)
  방법: NSGA-II 진화 알고리즘
  결과: Pareto 비지배 해 집합 → 다양한 DOF/EL 균형점
  특징: 가중치 설정 불필요, 다양한 해 제공
```

### NSGA-II 알고리즘 구성
```
개체(Individual) 표현:
  소스(조명): 픽셀화된 freeform 소명 강도 분포
  마스크: OPC 바이어스 벡터 또는 CTM
  합쳐서: 소스+마스크 파라미터 벡터

목적함수 (다목적):
  f1(S, M) = -DOF  (최대화 → 최소화)
  f2(S, M) = -EL   (최대화 → 최소화)
  f3(S, M) = EPE_nominal (부가 제약)

VLIM (Variational Lithography Model) 통합:
  고속 포커스 변동 항공 이미지 계산:
    I(F, D) = I_0 + ΔI(F) + ΔI(D)
  VLIM으로 전체 공정 윈도우 (F, D) 공간 빠른 평가
  기존 완전 시뮬 대비 수십 배 빠름

NSGA-II 이터레이션:
  1. 초기 개체군 생성 (무작위 또는 현재 SMO 결과)
  2. 비지배 정렬 (Pareto rank 부여)
  3. 혼잡도(Crowding Distance) 계산
  4. 선택, 교차, 변이 → 새로운 개체군
  5. 수렴 까지 반복 (세대 수 또는 목적함수 개선 없을 때)
```

### Pareto 전선과 의사결정
```
NSGA-SMO 출력:
  Pareto 비지배 해 집합 {(S_i, M_i)}
  각 해: (DOF_i, EL_i) 트레이드오프 균형

의사결정 (해 선택):
  방법 1: 특정 DOF 요구 시 EL 최대화 해 선택
  방법 2: 제품 요구사항 기반 제약 (DOF > D_min) 후 EL 최대
  방법 3: DOF × EL 곱 최대화 해 선택

다중 해의 이점:
  - 같은 런타임으로 여러 DOF/EL 균형 탐색
  - 공정 마진 분석: 전체 Pareto 전선 시각화
  - 설계 변경 대응: 다른 해를 즉시 선택 가능
```

### 성능 결과
```
기존 SMO 대비 비교:
  NSGA-SMO vs. 단목적 SMO:
    DOF: 20%+ 향상
    EL: 20%+ 향상

  복잡한 패턴에서:
    DOF × EL: 단목적 SMO 대비 최대 4배 향상

Pareto 전선 다양성:
  다수의 DOF/EL 트레이드오프 해 탐색 성공
  단일 해만 제공하는 가중합 방법 대비 유연성 높음

VLIM 가속 효과:
  완전 공정 시뮬 대비: 수십 배 빠른 목적함수 계산
  NSGA-II 다목적 탐색 실용적 런타임에서 가능
```

## OPC 툴 구현 관련성
- **SKOPC PWO 모듈**: `skopc/pwo/` NSGA-II 기반 공정 윈도우 최적화에 SMO 결합 확장
- **VLIM 통합**: 포커스/도즈 변동 시뮬레이션을 NSGA-SMO 목적함수에 통합
- **다목적 최적화**: pymoo 라이브러리의 NSGA-II로 즉시 구현 가능
- **Pareto 해 시각화**: DOF-EL 트레이드오프 Pareto 전선 시각화 도구

## 참고문헌
- JMM / SPIE Advanced Lithography (2024)
- 관련: Process variation-aware OPC with VLIM (DAC 2006)
- 관련: SMO at full chip scale using ILT level set (SPIE 7520, 2009)
- 관련: SKOPC PWO NSGA-II 구현 (Phase 7)

## 태그
`Recipe`, `SPIE`, `SMO`, `SourceMaskOptimization`, `NSGA-II`, `MultiObjective`, `ProcessWindow`, `VLIM`, `DOF`, `EL`, `ParetoFront`, `EvolutionaryAlgorithm`, `2024`
