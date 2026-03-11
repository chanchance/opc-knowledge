# Auto-Score System to Optimize OPC Recipe Parameters Using Genetic Algorithm

## 메타데이터
- **저자**: Liang Cao, Abhishek Asthana, Guoxiang Ning, Jui-Hsuan Feng, Jie Zhang, William Wilkinson
- **연도**: 2016
- **게재지**: Proc. SPIE 9985, Photomask Technology 2016, 998525
- **DOI/URL**: https://doi.org/10.1117/12.2241178
- **인용수**: ~15

## 핵심 요약
패턴 밀도와 설계 복잡도 증가로 OPC 레시피 튜닝이 더욱 어려워진 현실에서, EPE만 고려하는 기존 GA 방법의 한계를 극복하는 자동 점수 시스템을 제안한다. Bridge, pinch, PV 밴드 위반 등 복잡한 2D 기하구조의 특수 문제를 심각도(severity) 기준으로 식별하고 우선순위를 부여하는 점수 시스템과 이를 목적함수로 하는 GA 최적화를 결합한다.

## 주요 기여
1. OPC 레시피 문제를 심각도 기준으로 자동 분류·우선화하는 점수 시스템 알고리즘
2. POR(Plan of Record) 레시피 점수를 기준선으로 하는 상대적 평가 방법
3. 점수 시스템을 목적함수로 하는 GA 최적화 프레임워크
4. Bridge, pinch, PV 밴드 위반 등 2D 특수 구조 문제 해결에 특화

## Recipe/Process Flow 상세

### 자동 점수 시스템 (Auto-Score System)
```
1. 문제 유형 분류
   - Bridge: 인접 피처 간 단락(합선) 위험
   - Pinch: 피처 폭 과도한 감소
   - PV Band 위반: 공정 변동 후 불량 인쇄
   - EPE 과잉: 에지 배치 오차 초과
   - Necking/Bulging: 선폭 불균일

2. 심각도 가중치 할당
   - 각 문제 유형별 심각도 점수 (S_type)
   - 위반 강도별 가중치 (크면 점수 높음)
   - 점수 = Σ_i (S_type_i × severity_i × count_i)

3. POR 레시피 기준선 설정
   - 현재 POR 레시피로 OPC 실행
   - 기준선 점수 (S_POR) 계산
   - 목표: S_optimized < S_POR

4. 점수 집계
   - 전체 테스트 패턴에 대해 점수 합산
   - 레시피 품질의 종합적 정량화
```

### GA 최적화 프레임워크 (점수 기반)
```
1. 파라미터 공간 정의
   - OPC 레시피 파라미터 (세분화, 수렴, SRAF 등)
   - 각 파라미터 탐색 범위

2. 초기 집단
   - POR 레시피를 중심으로 변동 생성
   - 집단 크기 N

3. 적합도 평가 (Auto-Score)
   For each individual (레시피):
     - OPC 실행
     - Auto-score 계산 (bridge + pinch + PV + EPE 가중합)
     - 적합도 = -score (최소화 목표)

4. GA 연산
   - 선택: 엘리트 보존 + 토너먼트
   - 교배: 파라미터 단위 교환
   - 돌연변이: 가우시안 변동

5. 최적 레시피 선택
   - 점수 최소화 레시피 = 최적 레시피
   - POR 대비 점수 감소량으로 개선도 정량화
```

### 기존 방법 대비 개선점
```
기존 GA (EPE만 고려):
  - EPE는 개선되나 bridge/pinch/PV 위반 해결 못함
  - 특수 2D 구조에서 실패 가능

Auto-Score GA:
  - bridge, pinch, PV 밴드 위반을 점수에 통합
  - 심각도 우선순위로 가장 중요한 문제 먼저 해결
  - 복잡한 2D 레이아웃에서 더 포괄적 개선
```

## OPC 툴 구현 관련성
- **SKOPC 레시피 최적화**: `skopc/modeling/` OPC 평가 루프에 Auto-Score 시스템 통합 가능
- **점수 시스템**: Bridge, pinch, PV 밴드 위반을 포함하는 종합 레시피 품질 지표 구현
- **GA 목적함수**: EPE 외에 특수 구조 위반을 포함하는 더 강건한 목적함수
- **2016년 GA 연구 확장**: Asthana et al.(2016) OPC Recipe GA의 점수 시스템 강화 버전

## 참고문헌
- Proc. SPIE 9985, Photomask Technology 2016
- 관련: OPC recipe optimization using genetic algorithm (SPIE 9780, 2016) — 동일 Asthana 그룹
- 저자 소속: GLOBALFOUNDRIES

## 태그
`Recipe`, `SPIE`, `GeneticAlgorithm`, `AutoScore`, `OPC-Optimization`, `Bridge`, `Pinch`, `PVBand`, `SeverityRanking`, `GlobalFoundries`
