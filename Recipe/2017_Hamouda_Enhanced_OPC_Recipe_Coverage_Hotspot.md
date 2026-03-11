# Enhanced OPC Recipe Coverage and Early Hotspot Detection Through Automated Layout Generation and Analysis

## 메타데이터
- **저자**: Ayman Hamouda, Mohamed Bahnas, Dan Schumacher, Ioana Graur, Ao Chen, Kareem Madkour, Hussein Ali, Jason Meiring, Neal Lafferty, Chris McGinty
- **연도**: 2017
- **게재지**: Proc. SPIE 10147, Optical Microlithography XXX, 101470R
- **DOI/URL**: https://doi.org/10.1117/12.2260769
- **인용수**: ~25

## 핵심 요약
첨단 반도체 양산 공정을 위한 OPC 레시피는 다양한 패턴에 걸쳐 설계 충실도(design fidelity)와 최대 공정 윈도우를 달성하도록 섬세하게 조정된 파라미터 집합이다. 본 논문은 자동화된 레이아웃 생성 및 분석을 통해 OPC 레시피 커버리지를 향상시키고 조기 핫스팟을 탐지하는 방법론을 제시한다.

## 주요 기여
1. 초기 설계 콘텐츠가 제한된 상황에서 레시피 개발을 위한 자동화 레이아웃 생성 방법론
2. OPC 레시피 커버리지 향상을 위한 체계적 패턴 분류 및 분석 프레임워크
3. 조기 핫스팟 탐지 기법 — 실제 설계 콘텐츠 없이도 잠재 핫스팟 식별
4. 이전 노드 레시피를 신규 노드에 적응시키는 반복적 개발 프로세스

## Recipe/Process Flow 상세

### OPC Recipe 개발 일반 프로세스
```
1. 기준점 설정
   - 이전 노드 레시피를 초기 출발점으로 사용
   - 테스트 패턴 기반 파라미터 조정

2. 자동화 레이아웃 생성
   - 설계 규칙 기반 합성 패턴 생성
   - 공정에 민감한 구조물 (dense lines, isolated, line-end, 2D 구조) 포함
   - 실제 설계 콘텐츠 없이 레시피 테스트 가능

3. 패턴 분류 (Pattern Classification)
   - 패턴 유형별 그룹화 (1D/2D, pitch range, density)
   - 각 그룹에 대해 레시피 커버리지 평가

4. OPC 레시피 실행 및 평가
   - 각 패턴 그룹에 대해 OPC 수행
   - EPE, CD uniformity, 공정 윈도우 지표 측정

5. 핫스팟 탐지
   - 자동화 분석으로 ORC 위반 패턴 식별
   - 조기 피드백으로 레시피 파라미터 재조정

6. 레시피 최종화
   - 전체 패턴 커버리지 확인
   - 양산 레이아웃 검증
```

### 레시피 커버리지 지표
- **패턴 커버리지**: 설계 규칙 공간에서 테스트된 패턴 비율
- **EPE 통계**: RMS EPE, max EPE, 3σ EPE
- **핫스팟 밀도**: ORC 위반 건수 / 테스트 패턴 수
- **공정 윈도우**: 노광 여유도(exposure latitude) × 초점 심도(depth of focus)

## OPC 툴 구현 관련성
- **SKOPC Recipe Runner**: `skopc/recipe/` 배치 실행기에서 자동 패턴 생성 및 레시피 커버리지 평가 통합 가능
- **조기 검증**: 레시피 개발 초기 단계에서 핫스팟 탐지로 개발 비용 절감
- **커버리지 메트릭**: 레시피 품질 정량화를 위한 표준 지표 제공
- **자동화 레이아웃**: 합성 테스트 패턴 생성기 구현 참조

## 참고문헌
- Optical Microlithography XXX (SPIE 10147), 2017
- 관련: OPC recipe optimization using genetic algorithm (SPIE 9780, 2016)

## 태그
`Recipe`, `SPIE`, `HotspotDetection`, `RecipeCoverage`, `AutomatedLayout`, `PatternClassification`, `OPC-Flow`, `ProcessWindow`
