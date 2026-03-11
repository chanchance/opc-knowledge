# Process Window Tripling by Optimized SRAF Placement Rules

## 메타데이터
- **저자**: (IEEE document 7491081 - AP/DFM Advanced Patterning)
- **연도**: 2016
- **게재지**: IEEE Conference Publication (AP/DFM: Advanced Patterning / Design for Manufacturability)
- **DOI/URL**: https://ieeexplore.ieee.org/document/7491081/
- **인용수**: ~30

## 핵심 요약
SRAF(Sub-Resolution Assist Feature) 배치 규칙을 최적화함으로써 해당 레이어의 리소그래피 공정 윈도우 심도(Depth of Focus, DOF)를 거의 3배로 증가시키는 방법론을 보고한다. 체계적인 SRAF 규칙 최적화가 공정 윈도우 확대에 얼마나 결정적인 역할을 하는지 정량적으로 입증한 연구이다.

## 주요 기여
1. SRAF 배치 규칙 최적화로 공정 윈도우 DOF 3배 향상 달성
2. SRAF 규칙 파라미터(폭, 이격, 위치)와 공정 윈도우 간 정량적 상관관계 분석
3. 최적화된 SRAF 규칙의 체계적 개발 방법론
4. DFM(Design for Manufacturability) 관점에서 SRAF 규칙 중요성 입증

## Recipe/Process Flow 상세

### SRAF 배치 규칙 파라미터 공간
```
1D 라인-스페이스 패턴의 SRAF 규칙:
- SRAF 폭 (w_SRAF): 마스크 상 SRAF 크기
- SRAF 이격 거리 (d_SRAF): 주 패턴 에지에서 SRAF 에지까지 거리
- SRAF 개수 (n_SRAF): 주 패턴 양쪽 배치 개수
- 다중 SRAF 간격 (Δd): 1st, 2nd SRAF 간 간격

2D 패턴 SRAF 추가 규칙:
- 2D 코너 처리: 코너 주변 SRAF 배치 규칙
- Line-end SRAF: 라인 끝단 주변 규칙
- Conflict 해결: SRAF 간 최소 이격
```

### SRAF 규칙 최적화 프로세스
```
1. 공정 윈도우 평가 메트릭 정의
   - DOF (Depth of Focus): 초점 심도
   - EL (Exposure Latitude): 노광 여유
   - PW 면적 = DOF × EL (Bossung 곡선 기반)

2. 파라미터 스위프 (Parameter Sweep)
   - w_SRAF 범위: [MFR_min, λ/NA × factor]
   - d_SRAF 범위: [MFR_min_spacing, max_useful_distance]
   - 각 파라미터 조합에 대해 리소그래피 시뮬레이션 실행

3. 공정 윈도우 맵 작성
   - 2D 파라미터 공간에서 DOF/EL 등고선 플롯
   - 최적 파라미터 영역 식별

4. 최적 규칙 결정
   - DOF 최대화 기준 규칙 선택
   - 마스크 제조 규칙(MRC) 제약 준수 확인

5. 검증 및 규칙 테이블 확정
   - 검증 패턴 세트에서 성능 확인
   - Space-Width 규칙 테이블 최종화
```

### 공정 윈도우 개선 결과
```
최적화 전 (기본 SRAF 규칙):
  DOF: X nm (기준)
  EL: Y %

최적화 후 (최적 SRAF 규칙):
  DOF: ~3X nm (3배 향상)
  EL: Y' % (유지 또는 향상)

핵심: SRAF 규칙 한 세트의 최적화만으로 3X DOF 달성
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 규칙 개발**: `skopc/modeling/sraf_generator.py`의 Space-Width 테이블 생성 시 공정 윈도우 최적화 기준 적용 참조
- **PWO 연계**: `skopc/pwo/` NSGA-II 기반 공정 윈도우 최적화와 직접 연계 — SRAF 파라미터를 최적화 변수로 사용 가능
- **공정 윈도우 3배**: 제한된 수의 규칙 파라미터 최적화로 달성 가능한 공정 윈도우 개선 상한선 이해
- **규칙 테이블 구조**: Space-Width 규칙 테이블 형식이 SKOPC YAML 레시피와 호환 가능

## 참고문헌
- IEEE AP/DFM Conference 2016, Document 7491081
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: SRAF Placement based on Genetic Algorithm (IEEE, 2019)

## 태그
`Recipe`, `IEEE`, `SRAF`, `ProcessWindow`, `DepthOfFocus`, `RuleOptimization`, `DFM`, `Space-WidthTable`, `DOF-Tripling`
