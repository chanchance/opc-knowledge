# An Approach to Extracting SRAF Rules from Inverse Lithography Technology Results

## 메타데이터
- **저자**: (IEEE document 10366146 - 2023 IEEE Conference)
- **연도**: 2023
- **게재지**: IEEE Conference Publication
- **DOI/URL**: https://ieeexplore.ieee.org/document/10366146/
- **인용수**: 신규 논문

## 핵심 요약
ILT(Inverse Lithography Technology) 결과에서 SRAF 규칙을 추출하여 ILT 수준의 SRAF 성능을 RBSRAF(Rule-Based SRAF)의 빠른 처리 속도로 달성하는 방법론을 제안한다. 2019년 Su et al. (SPIE)의 접근법을 IEEE 컨퍼런스에서 발전시킨 연구로, ILT-유사 RBSRAF를 통해 최적 SRAF와 규칙 기반 SRAF의 장점을 결합한다.

## 주요 기여
1. ILT 결과에서 SRAF 규칙을 추출하는 체계적 방법론 개선
2. ILT-유사 RBSRAF: ILT 성능에 근접하면서 RBSRAF 속도 유지
3. 규칙 추출 정확도와 실행 속도의 균형 최적화
4. 다양한 패턴 유형(1D/2D)에 대한 규칙 추출 일반화

## Recipe/Process Flow 상세

### ILT 기반 SRAF 규칙 추출 개선 방법론
```
목표: ILT-유사 RBSRAF 달성
  - ILT 성능: 공정 윈도우, EPE에서 ILT에 근접
  - RBSRAF 속도: 전체 칩 규칙 기반 삽입 속도 유지

1. ILT 실행 및 SRAF 분석
   - 대표 패턴 선택 (1D, 2D, 혼합)
   - ILT 최적화 실행 → 연속 마스크 생성
   - SRAF 영역 추출: ILT 마스크의 주 패턴 외 영역 분석

2. SRAF 파라미터 회귀 분석
   - ILT SRAF 분포에서 Space-Width 상관관계 회귀
   - 주 패턴 CD × space → SRAF 폭, 위치 매핑
   - 통계적 최적 규칙 도출 (평균/중앙값/최빈값)

3. 규칙 검증 및 세밀화
   - 추출된 규칙으로 RBSRAF 적용
   - ILT 결과와 RBSRAF 결과 공정 윈도우 비교
   - 차이가 큰 영역의 규칙 세밀화 (iterative refinement)

4. 최종 규칙 테이블 생성
   - 검증된 Space-Width 테이블 출력
   - 엣지 케이스 처리 (conflict, cleanup 규칙)
   - DRC 규칙 통합
```

### ILT 성능 근접 전략
```
규칙 적용:
  일반 패턴 → RBSRAF (빠른 처리)
  핫스팟 (PV 밴드 부족) → ILT 선택적 보수

성능 지표 비교:
| 지표 | 전통 RBSRAF | ILT | 본 방법 (ILT-유사 RBSRAF) |
|------|-------------|-----|--------------------------|
| EPE  | 보통        | 최소 | 낮음 (ILT에 근접)         |
| PV Band | 보통    | 최대 | 높음 (ILT에 근접)         |
| 속도 | 빠름        | 느림 | 빠름 (RBSRAF 수준)        |
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 규칙 개발**: `skopc/modeling/sraf_generator.py`의 ILT→규칙 추출 파이프라인 구현 참조
- **OpenILT 연계**: `skopc/modeling/openilt_adapter.py`로 ILT 실행 후 본 방법으로 규칙 추출
- **2019년 SPIE 논문 발전**: Su et al.(2019)의 SPIE 방법론을 IEEE 컨퍼런스에서 개선
- **RuleLearner와 상보**: 2025_Yu_RuleLearner는 OPC 규칙 추출, 본 논문은 SRAF 규칙 추출에 특화

## 참고문헌
- IEEE Conference Publication 2023, Document 10366146
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: RuleLearner: OPC Rule Extraction from ILT Engine (IEEE, 2024)
- 관련: CTM-SRAF (IEEE TCAD, 2023)

## 태그
`Recipe`, `IEEE`, `SRAF`, `ILT`, `RuleExtraction`, `RBSRAF`, `ILT-likeRBSRAF`, `ProcessWindow`, `HybridApproach`, `2023`
