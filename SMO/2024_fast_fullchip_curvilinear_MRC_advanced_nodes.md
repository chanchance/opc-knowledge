# Fast Full Chip Curvilinear MRC for Advanced Manufacturing Nodes

## 메타데이터
- **저자**: (SPIE 12954 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295417 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3011100

## 핵심 요약
첨단 제조 노드를 위한 빠른 전체 칩 곡선형 마스크 규칙 검사(curvilinear MRC) 방법을 제시한다. ILT와 곡선형 마스크 채택이 확대됨에 따라 예리한 각도, T/Y 접합, 급격한 굴곡, 너무 작은 피처 등 마스크 제조 가능성(manufacturability) 문제를 사전에 검증하기 위한 전체 칩 CLMRC 플로우를 개발한다.

## 주요 기여
1. **전체 칩 곡선형 MRC**: 전체 칩 규모에서 빠른 곡선형 마스크 규칙 검사
2. **ILT 마스크 문제 조기 발견**: 마스크 제조 전 형상 문제 신속 스크리닝
3. **제조 가능성 보장**: 예리한 각도, T/Y 접합, 급굴곡 등 검사
4. **런타임 최적화**: 전체 칩 CLMRC를 실용적 시간 내 완료

## 알고리즘/수식
### 곡선형 MRC 검사 항목
```
CLMRC 검사 규칙:
  1. 최소 피처 크기: CD_min ≥ MRC_CD_min
  2. 최소 간격: gap_min ≥ MRC_gap_min
  3. 곡률 반경: R_curvature ≥ R_min
  4. 예리한 각도: θ_corner ≥ θ_min
  5. T/Y 접합: 접합부 크기 ≥ MRC_junction_min
  6. 급격한 굴곡: 굴곡 길이/반경 비율 ≤ 허용치

곡선형 표현:
  Bezier/B-spline 제어점 기반
  CLMRC: 연속 파라미터 t에서 위반 검사
```

### 전체 칩 런타임 최적화
```
병렬화 전략:
  - 칩 분할: 독립 타일로 분할 후 병렬 검사
  - 계층적 검사: 광역 필터 → 세부 검사

런타임 목표:
  전체 칩 CLMRC: 수 시간 이내
  (맨해튼 MRC 대비 곡선형 추가 비용 최소화)
```

## OPC 툴 SMO 구현 관련성
- 곡선형 OPC 후 MRC 통합: SKOPC 곡선형 OPC 플로우에 CLMRC 단계 추가
- 마스크 제조 가능성 보장: OPC 결과물이 마스크 제조 규칙 충족 여부 검증
- ILT 출력 검증: ML ILT + 곡선형 OPC 결과에 대한 CLMRC 적용
- EUV 테이프아웃 플로우: SMO → OPC → CLMRC → MPC 통합 플로우

## 태그
`MRC`, `curvilinear`, `ILT`, `EUV`, `manufacturability`, `full_chip`, `mask_data_preparation`, `DTCO`, `SPIE`, `2024`
