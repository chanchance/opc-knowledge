# Full-Chip Lithography Simulation and Design Analysis: How OPC Is Changing IC Design

## 메타데이터
- **저자**: Chris Spence
- **연도**: 2005
- **게재지**: Proc. SPIE 5751, Emerging Lithographic Technologies IX
- **DOI/URL**: https://doi.org/10.1117/12.608020
- **인용수**: ~160 (논문 + ~160 특허 인용)

## 핵심 요약
10년 전 연구 주제에 불과했던 Model-Based OPC(MB-OPC)가 90nm 양산 핵심 기술로 자리잡기까지의 발전 과정을 총망라한 리뷰 논문이다. 풀칩 리소그래피 시뮬레이션이 OPC 흐름에 통합되면서 IC 설계 방법론을 어떻게 변화시키고 있는지를 분석한다. MB-OPC의 기술적 도전 해결(계산 효율, 모델 정확도, 수렴 안정성), 풀칩 LRC(Lithography Rule Check), OPC-인식 설계 흐름, 그리고 미래 노드를 위한 도전 과제를 포괄적으로 기술한다.

## 주요 기여
1. Model-Based OPC의 기술 발전사 및 90nm 양산 적용 과정 정리
2. 풀칩 리소그래피 시뮬레이션의 OPC 통합 방법론 개요
3. LRC(Lithography Rule Check)의 OPC 검증 흐름 통합
4. OPC가 IC 설계 규칙(Design Rule)을 변화시키는 방식 분석

## Recipe/Process Flow 상세

### Model-Based OPC 발전 과정 (1990s → 2005)
```
1990년대 초 (OPC 도입기):
  - Rule-Based OPC (RB-OPC): 직관적 수정 규칙
  - 단순 바이어스 (줄이기/늘리기)
  - 한계: 90nm 이하 노드에서 정확도 부족

1990년대 후반 (Model-Based OPC 연구):
  - 리소그래피 물리 모델 기반 보정
  - 계산 복잡도: 풀칩 적용 불가 (너무 느림)
  - 일부 핫스팟에만 선택적 적용

2000년대 초반 (MB-OPC 발전):
  - 컴팩트 모델 개선: 정확도 + 속도 균형
  - 병렬 컴퓨팅: 클러스터 기반 분산 처리
  - 130nm 노드: MB-OPC 부분 적용

2005년 당시 (90nm 양산 핵심):
  - MB-OPC: 90nm 게이트/메탈 레이어 필수
  - 전체 칩 적용: 24-48시간 TAT
  - OPC 인프라: 수천 CPU 클러스터 일반화
```

### 풀칩 MB-OPC 흐름 (2005년 기준)
```
입력: 설계 GDS + 공정 모델 + OPC 레시피

단계 1: 레이아웃 분해 (Layout Fracturing)
  - 전체 칩을 처리 가능한 타일/클립으로 분할
  - 레이어별 독립 처리

단계 2: 세그먼트화 (Fragmentation/Dissection)
  - 각 폴리곤 엣지를 OPC 세그먼트로 분할
  - 세그먼트 크기: 수십~수백 nm

단계 3: 이터레이션 루프 (OPC Iteration)
  For each segment:
    1. 리소그래피 시뮬레이션 (컴팩트 모델)
    2. EPE 계산
    3. 세그먼트 이동 (Feedback 또는 Newton-Raphson)
  수렴 기준 충족 시 종료 (통상 5-10 이터레이션)

단계 4: 검증 (Post-OPC Verification / LRC)
  - OPC 후 레이아웃에서 리소그래피 시뮬
  - 핫스팟 감지: EPE 기준 초과 패턴
  - 공정 윈도우 평가

출력: OPC된 마스크 레이아웃
```

### 풀칩 LRC(Lithography Rule Check)
```
LRC 정의:
  OPC 전/후 레이아웃에서 리소그래피 시뮬 기반 검사
  = DRC(Design Rule Check)의 리소그래피 인식 확장

LRC 의의:
  - 기존 DRC: 기하학 규칙 (CD > 최소 폭 등)
  - LRC: 실제 인쇄 CD 예측으로 검사
  → 공정 변동, 패턴 의존 효과 반영

LRC 항목:
  - Bridge/Short: 인접 패턴 간 융합 위험
  - Pinch/Open: 패턴 너무 좁아지는 위험
  - 공정 윈도우: DOF, EL 기준 미달 패턴

OPC 흐름 통합:
  MB-OPC 후 → LRC → 핫스팟 리포트
  핫스팟: 수작업 수정 또는 재-OPC
```

### OPC가 IC 설계를 바꾼 방식
```
설계 규칙 변화:
  이전: 순수 기하학 기반 설계 규칙
  OPC 시대: 리소그래피 인식 설계 규칙 (LARD)
    - OPC-친화적 패턴 권장
    - 안티-핫스팟 설계 규칙 추가
    - Metal pitch/width 규칙: OPC 수렴성 고려

설계-공정 공동 최적화 (DTCO):
  - OPC 결과를 설계 단계에서 예측
  - 설계 변경으로 OPC 문제 사전 예방
  - 표준 셀 설계에 OPC 인식 적용

EDA 툴 통합:
  - 시뮬레이션 기반 LVS/DRC (물리 검증)
  - OPC-인식 라우팅: 라우터가 OPC 결과 예측
  - 풀칩 LRC 흐름: 테이프아웃 필수 단계로
```

### 미래 노드 도전 과제 (2005 시점 예측)
```
65nm 노드 이하 (2005 당시 로드맵):
  - k1 < 0.3 → SRAF 필수화
  - 이중 노광 또는 다중 패터닝 필요
  - OPC 런타임: 72-120시간 예상
  - 수차 보정(APC) 통합 필요

컴퓨팅 인프라:
  - 클러스터 규모 더욱 확대 필요
  - 분산 OPC 알고리즘 최적화
  - 모델 정확도 vs. 런타임 균형이 핵심 과제
```

## OPC 툴 구현 관련성
- **SKOPC 역사적 맥락**: MB-OPC 기술 발전의 역사적 레퍼런스, SKOPC 설계 방향 수립 기반
- **LRC 구현**: `skopc/modeling/` OPC 후 검증 단계(LRC)를 표준 흐름에 통합
- **풀칩 타일 처리**: `skopc/recipe/` 배치 러너에서 전체 칩을 타일로 분할 처리하는 아키텍처
- **핫스팟 리포트**: OPC 검증 결과를 핫스팟 리포트로 출력하는 표준 인터페이스

## 참고문헌
- Proc. SPIE 5751, Emerging Lithographic Technologies IX (2005)
- 저자 소속: Synopsys
- 관련: Physical simulation for verification and OPC on full chip level (SPIE 7973, 2011)
- 관련: Optimized hardware and software for fast full-chip simulation (SPIE 5754, 2005)
- 관련: Roadmap to sub-nanometer OPC model accuracy (SPIE 8441, 2012)

## 태그
`Recipe`, `SPIE`, `FullChipOPC`, `ModelBasedOPC`, `LithoSimulation`, `LRC`, `HotspotDetection`, `OPC-History`, `90nm`, `DesignAnalysis`, `Synopsys`, `2005`
