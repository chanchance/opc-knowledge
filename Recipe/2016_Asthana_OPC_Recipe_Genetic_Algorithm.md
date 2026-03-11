# OPC Recipe Optimization Using Genetic Algorithm

## 메타데이터
- **저자**: Abhishek Asthana, Bill Wilkinson, Dave Power
- **연도**: 2016
- **게재지**: Proc. SPIE 9780, Optical Microlithography XXIX, 97800J
- **DOI/URL**: https://doi.org/10.1117/12.2219166
- **인용수**: ~30

## 핵심 요약
OPC 레시피 최적화의 비자명성(non-triviality) 문제를 해결하기 위해 유전 알고리즘(GA) 기법을 적용한 연구. 기존에는 파라미터 선택이 벤더 권장값이나 경험 기반으로 이루어졌으나, GA를 통해 OPC 레시피 파라미터 공간을 체계적으로 탐색하여 ORC(Optical Rule Check) 위반을 최소화하는 최적 레시피를 도출한다.

## 주요 기여
1. GA 기반 OPC 레시피 전체 최적화 방법론 제시 (선택 파라미터 기준)
2. Line-end geometry에서의 인쇄 및 비아 커버리지 개선에 GA 적용
3. 최적화된 레시피로 ORC 위반 건수 대폭 감소 입증
4. 파라미터 간 상관관계를 전체론적으로 정량화하는 프레임워크

## Recipe/Process Flow 상세

### OPC Recipe 파라미터 공간
- **단편화(Fragmentation) 파라미터**: 엣지 세그먼트 길이, 최소/최대 세그먼트, corner bias
- **수렴 파라미터**: 댐핑 팩터, 최대 이터레이션 수, EPE 목표값
- **SRAF 파라미터**: scattering bar 폭, 삽입 규칙 임계값
- **모델 파라미터**: resist threshold, MEEF 보정 계수

### 유전 알고리즘 흐름
```
1. 초기 집단 생성
   - 파라미터 범위 정의 (벤더 권장값 기준 ±범위)
   - 무작위 초기 집단 생성 (population size N)

2. 적합도 함수 (Fitness Function)
   - ORC 위반 건수 최소화
   - Line-end 인쇄 커버리지 최대화
   - 수렴 이터레이션 수 최소화

3. 선택 (Selection)
   - 토너먼트 선택 또는 roulette-wheel 방식

4. 교배 (Crossover)
   - 단일점/다중점 교배

5. 돌연변이 (Mutation)
   - 파라미터 범위 내 랜덤 변동

6. 종료 조건
   - 최대 세대 수 도달 또는 수렴 기준 충족
```

### 적용 케이스 1: OPC 레시피 전체 최적화
- 선택된 파라미터 집합에 대해 GA 탐색 수행
- 목표: ORC 위반 건수 최소화
- 결과: 최적화된 레시피로 ORC 위반 대폭 감소

### 적용 케이스 2: Line-end 기하구조 개선
- Line-end geometry에서 GA로 최적 보정 파라미터 도출
- 인쇄 커버리지 및 비아 커버리지 향상

## OPC 툴 구현 관련성
- **Recipe 파라미터 자동 탐색**: 수동 파라미터 튜닝 대체 가능
- **SKOPC 적용**: `skopc/modeling/` 내 model-based OPC 레시피 최적화 루프에 GA 통합 가능
- **평가 메트릭**: ORC 위반 건수, EPE, 수렴 이터레이션 수를 적합도 함수로 활용
- **실용성**: 초기 레시피 설정 자동화, 신규 노드 테이프아웃 시 레시피 개발 가속

## 참고문헌
- Optical Microlithography XXIX (SPIE 9780)
- GlobalFoundries Inc., Malta, NY 발표
- 관련: Auto-score system to optimize OPC recipe parameters using genetic algorithm (SPIE 9985, 2016)

## 태그
`Recipe`, `SPIE`, `GeneticAlgorithm`, `OPC-Optimization`, `ORC`, `FragmentationParameters`, `ConvergenceControl`, `GlobalFoundries`
