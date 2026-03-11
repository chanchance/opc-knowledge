# Implementation of Different Cost Functions for EUV Mask Optimization for Next Generation Beyond 7nm

## 메타데이터
- **저자**: Fan Jiang, Alexander Tritchkov, Alex Wei, Srividya Jayaram, Yuyang Sun, Xima Zhang, James Word
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X, 1095712 (26 March 2019)
- **DOI/URL**: https://doi.org/10.1117/12.2513560

## 핵심 요약
7nm 이후 차세대 EUV 마스크 최적화를 위한 다양한 비용 함수 구현을 비교 분석한다. SRAF가 EUV의 이미지 품질 메트릭 향상과 확률론적 효과 개선에 기여함을 보이고, 여러 비용 함수 선택이 최적화 결과에 미치는 영향을 정량화한다.

## 주요 기여
1. **EUV 비용 함수 비교**: 7nm 이후 EUV 마스크 최적화에서 다양한 비용 함수 구현 평가
2. **SRAF EUV 적용 효과**: SRAF가 EUV 이미지 품질 메트릭 향상 및 확률론적 효과 개선에 기여
3. **비용 함수 선택 가이드**: OPC/ILT 최적화에서 최적 비용 함수 선택 기준 제시
4. **7nm 이후 노드 적용**: 차세대 노드에서의 EUV 마스크 최적화 전략

## 알고리즘/수식
### EUV 마스크 최적화 비용 함수 유형
```
유형 1: CD 기반 비용 함수
  Cost_CD = Σ_i ||CD_i - CD_target||²
  특성: 직관적, 빠른 수렴

유형 2: NILS 기반 비용 함수
  Cost_NILS = -Σ_i NILS_i
  특성: 이미지 대비 최대화

유형 3: 공정 창 기반 비용 함수
  Cost_PW = -min(DOF × EL)
  특성: 공정 안정성 직접 최적화

유형 4: EPE 기반 비용 함수
  Cost_EPE = Σ_i ||EPE_i||²
  특성: 엣지 배치 정확도 최적화

유형 5: 확률론적 인식 비용 함수 (EUV 특화)
  Cost_stoch = Σ_i P_fail_i
  특성: 확률론적 고장 확률 포함
```

### SRAF와 비용 함수 통합
```
SRAF 삽입 조건:
  SRAF_benefit = ΔNILS(with SRAF) - ΔNILS(without SRAF)
  MRC(SRAF) 만족: SRAF 크기/간격 제약

SRAF가 확률론적 효과에 미치는 영향:
  I_SRAF(x) = I_main(x) + I_assist(x)
  → NILS 향상 → 확률론적 고장률 감소
```

## OPC 툴 SMO 구현 관련성
- EUV SMO/OPC의 비용 함수 설계에 대한 포괄적 가이드
- SRAF 삽입 최적화와 비용 함수의 연계: 확률론적 메트릭 통합
- 7nm 이후 노드에서 비용 함수 선택이 최적화 결과에 미치는 영향
- SKOPC EUV OPC 모듈의 비용 함수 설계 시 다중 메트릭 가중합 방법론 참조

## 태그
`SMO`, `OPC`, `EUV`, `cost_function`, `SRAF`, `NILS`, `stochastic`, `7nm`, `beyond_7nm`, `SPIE`
