# Enhanced OPC Recipe Coverage and Early Hotspot Detection Through Automated Layout Generation and Analysis

## 메타데이터
- **저자**: Ayman Hamouda, Mohamed Bahnas, Dan Schumacher, Ioana Graur, Ao Chen, Kareem Madkour, Hussein Ali, Jason Meiring, Neal Lafferty, Chris McGinty
- **연도**: 2017
- **게재지**: Proc. SPIE 10147, Optical Microlithography XXX, 101470R
- **DOI/URL**: https://doi.org/10.1117/12.2260769
- **인용수**: 다수 (GLOBALFOUNDRIES+Mentor Graphics 산학 협력 논문)

## 핵심 요약
대규모 현실적 설계 콘텐츠를 자동 생성하고 이를 통해 OPC 레시피 파라미터를 최적화하여 레이아웃의 공정 윈도우를 극대화하는 자동화 플로우를 제시한다. GLOBALFOUNDRIES와 Mentor Graphics의 협력 연구로, OPC 레시피 커버리지 향상과 초기(pre-tapeout) 핫스팟 검출을 통합한다.

## 주요 기여
1. 대규모 현실적 레이아웃을 자동 생성하는 플로우 개발 — 수동 패턴 구성의 한계 극복
2. 자동 생성 레이아웃으로 OPC 레시피 파라미터를 최적화하여 공정 윈도우 극대화
3. OPC 레시피 개발 초기 단계에서 핫스팟을 조기 검출하는 통합 방법론
4. GLOBALFOUNDRIES 양산 환경에서의 실증으로 실용성 검증

## 검증 방법론
- **자동 레이아웃 생성**: 실제 설계 규칙 기반으로 다양한 피치·패턴 조합의 테스트 레이아웃 자동 합성
- **OPC 레시피 최적화**: 자동 생성 레이아웃에 OPC 적용 후 공정 윈도우(DOF, EL) 측정, 파라미터 최적화
- **조기 핫스팟 검출**: OPC 레시피 개발 단계에서 공정 윈도우 마진 부족 패턴을 조기 식별
- **검증 지표**:
  - 공정 윈도우(DOF, Exposure Latitude) 마진
  - NILS(Normalized Image Log Slope) — 이미지 대비 지표
  - EPE 분포 및 핫스팟 밀도
- **자동화 분석**: 레이아웃 분석 도구로 핫스팟 패턴의 컨텍스트 분류 및 통계 생성

## 검증 지표
- EPE 허용 범위: GLOBALFOUNDRIES 공정 노드 기준 (FinFET/28nm 이하)
- 시뮬레이터: Mentor Graphics Calibre OPC + LRC 엔진
- 커버리지: 자동 생성된 대규모 레이아웃 전체 커버

## OPC 툴 구현 관련성
- **OPC 레시피 자동 최적화 플로우 구현 참조**: `RecipeRunner`와 `VerificationEngine`을 연계하여 레시피 파라미터 최적화 루프를 구현할 때 직접 참조 가능
- 자동 레이아웃 생성 기반 OPC 레시피 커버리지 테스트 방법론 — OPC 툴의 테스트 케이스 자동 생성에 활용
- 조기 핫스팟 검출 플로우는 `VerificationEngine`의 레시피 개발 단계 통합 기능으로 구현 가능
- NILS·공정 윈도우 기반 검증 지표를 OPC 레시피 품질 평가 메트릭으로 구현하는 설계 근거

## 참고문헌
- SPIE Optical Microlithography XXX 2017, Vol. 10147
- GLOBALFOUNDRIES Inc. / Mentor Graphics Corp. 기술 문서

## 태그
`Verification`, `SPIE`, `OPCRecipe`, `Hotspot`, `ProcessWindow`, `AutomatedLayout`, `NILS`, `EarlyDetection`, `FullChip`, `Calibre`
