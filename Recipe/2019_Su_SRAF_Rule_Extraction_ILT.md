# SRAF Rule Extraction and Insertion Based on Inverse Lithography Technology

## 메타데이터
- **저자**: Xiaojing Su, Pengzheng Gao, Yayi Wei, Weijie Shi
- **연도**: 2019
- **게재지**: Proc. SPIE 10961, Optical Microlithography XXXII, 109610P
- **DOI/URL**: https://doi.org/10.1117/12.2511914
- **인용수**: ~25

## 핵심 요약
ILT(Inverse Lithography Technology) 결과에서 SRAF 규칙을 추출하여 Rule-Based SRAF(RBSRAF)로 삽입하는 하이브리드 방법론. ILT 최적화의 높은 품질과 Rule-based SRAF의 빠른 실행 속도를 결합한다. 공정 변동(PV) 밴드가 기준 미달인 핫스팟 영역은 ILT로 보수하는 2단계 전략으로 개발 사이클을 단축한다.

## 주요 기여
1. ILT 결과에서 1D 및 2D SRAF 규칙 자동 추출 방법론
2. 추출된 규칙으로 전체 칩 RBSRAF 삽입 (빠른 런타임)
3. PV 밴드 기준 핫스팟을 ILT로 선택적 보수하는 2단계 전략
4. SRAF 규칙의 신뢰성 확보 (ILT 기반 규칙으로 물리적 정합성 보장)

## Recipe/Process Flow 상세

### 2단계 SRAF 삽입 흐름
```
1단계: ILT 기반 SRAF 규칙 추출
─────────────────────────────────
a) 대표 패턴 선택
   - 1D 라인-스페이스: 다양한 pitch, CD 조합
   - 2D 구조: contact/via, line-end, L-자형 등
   - 공정에 민감한 패턴 우선 선택

b) ILT 최적화 실행
   - 각 대표 패턴에 대해 ILT 수행
   - CTM(Continuous Transmission Mask) 생성
   - SRAF 위치, 크기, 형상 최적화

c) SRAF 규칙 추출
   - ILT 결과에서 SRAF 분포 패턴 분석
   - Space-Width 테이블 생성:
     * 주 패턴 CD × pitch → SRAF 폭 + 위치 (offset)
   - 규칙 테이블 형식:
     SRAF_width = f(main_CD, space)
     SRAF_offset = g(main_CD, space, SRAF_order)
   - 최대 SRAF 차수(1st, 2nd, ...) 결정

2단계: 전체 칩 RBSRAF 삽입 및 ILT 핫스팟 보수
────────────────────────────────────────────────
d) 전체 칩 Rule-Based SRAF 삽입
   - 추출된 Space-Width 테이블 적용
   - 빠른 기하학적 연산으로 전체 칩 처리
   - DRC/MRC 규칙 준수 확인

e) 공정 윈도우 검증
   - 리소그래피 시뮬레이션 실행
   - PV(Process Variation) 밴드 측정
   - 핫스팟 식별: PV 밴드 < 기준값인 영역

f) ILT 핫스팟 보수
   - 기준 미달 핫스팟 영역에만 ILT 적용
   - 국소적 ILT로 SRAF 최적화
   - 전체 칩 ILT 대비 런타임 대폭 절감
```

### SRAF 규칙 테이블 형식
```
pitch (nm) | main_CD (nm) | SRAF1_width | SRAF1_offset | SRAF2_width | SRAF2_offset
-----------|--------------|-------------|--------------|-------------|-------------
80         | 40           | 20          | 30           | -           | -
100        | 40           | 24          | 35           | -           | -
120        | 40           | 26          | 38           | 18          | 60
140        | 40           | 28          | 40           | 20          | 65
160        | 40           | 30          | 42           | 22          | 70
```

### 성능 비교
| 방법 | EPE | PV Band | 런타임 |
|------|-----|---------|--------|
| Full ILT | 최고 | 최대 | 가장 느림 |
| Rule-based SRAF | 보통 | 보통 | 가장 빠름 |
| 본 논문 (ILT규칙+RB삽입) | 높음 | 높음 | 중간 |
| 본 논문 (핫스팟 ILT 보수 포함) | 최고 수준 | 최대 수준 | 적절 |

## OPC 툴 구현 관련성
- **SKOPC SRAF 모듈**: ILT 결과에서 Space-Width 테이블 추출하는 파이프라인 구현 참조
- **하이브리드 전략**: `skopc/modeling/sraf_generator.py`에 Rule-based + ILT 보수 2단계 구조 적용 가능
- **RBSRAF 구현**: Space-Width 테이블 기반 기하학적 SRAF 삽입은 런타임 효율적
- **OpenILT 연계**: `skopc/modeling/openilt_adapter.py`의 ILT로 대표 패턴 최적화 후 규칙 추출

## 참고문헌
- Proc. SPIE 10961, Optical Microlithography XXXII (2019)
- 저자 소속: Institute of Microelectronics of Chinese Academy of Sciences
- 관련: SRAF rule extraction - An approach to extracting SRAF rules from ILT results (IEEE, 2023)
- 관련: 2D SRAF rule extraction for fast application (SPIE 10810, 2018)

## 태그
`Recipe`, `SPIE`, `SRAF`, `ILT`, `RuleExtraction`, `HybridApproach`, `ProcessVariation`, `HotspotRepair`, `Space-WidthTable`, `RecipeDevelopment`
