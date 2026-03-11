# OPC and Modeling Solution to Support 0.55NA EUV Stitching

## 메타데이터
- **저자**: (SPIE 13215 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 13215, Optical and EUV Nanolithography XXXVII, 1321507 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3034957

## 핵심 요약
0.55NA EUV 아나모픽 광학계의 스티칭(stitching) 필드 분할 노출을 지원하기 위한 OPC 및 모델링 솔루션을 제시한다. 고NA EUV 스캐너의 아나모픽 배율(4x/8x) 구조로 인해 반쪽 필드씩 두 번 노출하는 스티칭 방식에서 OPC와 리소그래피 모델링의 일관성을 보장하는 방법론을 개발한다.

## 주요 기여
1. **스티칭 OPC 솔루션**: 0.55NA EUV 필드 분할 노출에서 OPC 일관성 유지
2. **스티칭 경계 처리**: 상/하단 필드 경계에서 CD 불연속성 최소화 OPC
3. **아나모픽 모델링**: 비대칭 NA(x/y)를 고려한 리소그래피 모델 개발
4. **플레어/수차 스티칭 보정**: 필드별 플레어/수차 차이를 OPC에 통합

## 알고리즘/수식
### 0.55NA EUV 스티칭 OPC 구조
```
아나모픽 광학계:
  NA_x = 0.55 (스캔 방향)
  NA_y = 0.33 (슬릿 방향)
  배율: M_x = 4x, M_y = 8x

스티칭 노출:
  노출 1 (상단): 마스크 상단 필드 → 웨이퍼 상단
  노출 2 (하단): 마스크 하단 필드 → 웨이퍼 하단
  스티칭 경계: 두 노출이 만나는 위치

OPC 요구사항:
  경계 위 OPC ≠ 경계 아래 OPC
  → 각 필드의 광학 조건(수차, 플레어) 반영
  → 스티칭 경계에서 CD 연속성 목표
```

### 스티칭 인식 OPC 비용 함수
```
스티칭 OPC 비용:
  Cost = Cost_upper + Cost_lower + w_stitch·Cost_boundary

Cost_boundary = Σ_{경계 패턴} ||CD_upper - CD_lower||²

필드 의존 수차 보정:
  W_upper(y_field), W_lower(y_field) 각각 보정
  → 상/하단 필드 수차 차이 보상
```

## OPC 툴 SMO 구현 관련성
- 고NA EUV 스티칭 OPC: SKOPC에서 0.55NA 스티칭 지원 OPC 모듈 설계 참조
- 필드 분할 SMO: 상/하단 필드를 각각 최적화하는 SMO 전략
- 아나모픽 모델: NA_x≠NA_y 비대칭 광학 모델 구현
- 스티칭 비용 함수: SMO/OPC 비용 함수에 경계 연속성 항 추가

## 태그
`OPC`, `EUV`, `high_NA`, `stitching`, `anamorphic`, `0p55NA`, `field_split`, `boundary`, `aberration`, `SPIE`, `2024`
