# An Innovative Stitching Solution for Multipatterning Compliant Routing Metal Layers Beyond 2nm

## 메타데이터
- **저자**: (SPIE 13425 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250T (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3047850

## 핵심 요약
2nm 이하 노드에서 다중 패터닝 호환 라우팅 메탈 레이어를 위한 혁신적인 스티칭 솔루션을 제시한다. 고NA EUV의 아나모픽 필드 분할 스티칭과 다중 패터닝을 결합하여 2nm 이하 메탈 라우팅 레이어의 패터닝을 실현하는 새로운 접근법을 개발한다.

## 주요 기여
1. **다중 패터닝 + 스티칭 통합**: MP(다중 패터닝)와 고NA EUV 스티칭을 결합한 혁신적 솔루션
2. **2nm 이하 메탈 라우팅**: 극한 노드에서의 라우팅 메탈 레이어 패터닝 실현
3. **스티칭 호환 레이아웃**: 다중 패터닝 규칙과 스티칭 경계 요구사항을 동시에 만족하는 레이아웃
4. **DTCO 통합**: 설계-기술 공동 최적화 관점에서의 스티칭+MP 솔루션

## 알고리즘/수식
### 다중 패터닝 호환 스티칭 솔루션
```
2nm 이하 노드 패터닝 도전:
  메탈 피치 < 20nm
  0.55NA EUV 단일 노출 한계 → MP 필요
  고NA EUV 스티칭 → 필드 분할 필수

스티칭 + 다중 패터닝 통합:
  Layer decomposition:
    M_total = M_upper_exp1 + M_upper_exp2  (SADP)
            ∪ M_lower_exp1 + M_lower_exp2
  스티칭 경계: M_upper ↔ M_lower 경계

  레이아웃 제약:
    MP 규칙: 인접 피처 다른 마스크에 배치
    스티칭 규칙: 경계에서 활성 소자 없음
    두 제약 동시 만족하는 레이아웃 탐색

최적화 문제:
  min stitch_CD_error + MP_coloring_violation
  subject to: DRC, MP_rules, stitch_boundary_rules
```

### 스티칭 경계 OPC
```
다중 패터닝 스티칭 OPC:
  상단 필드 노출 1 (exp1_upper):
    OPC_11 최적화
  상단 필드 노출 2 (exp2_upper):
    OPC_12 최적화, exp1과 정합성 유지
  하단 필드 유사하게 처리

경계 연속성:
  ΔCD_stitch < threshold (각 MP 레이어에서)
  오버레이 오차: 두 노출 간 + 상하단 노출 간
```

## OPC 툴 SMO 구현 관련성
- 다중 패터닝 스티칭 OPC: SKOPC에서 MP+스티칭 복합 OPC 플로우 지원
- 2nm 이하 노드 지원: 극한 노드에서의 복합 패터닝 전략 OPC 지원
- DTCO 통합: 레이아웃 분해와 OPC를 공동으로 최적화하는 DTCO 플로우
- 경계 연속성 OPC: 다중 노출 경계에서 CD 연속성 보장 알고리즘

## 태그
`stitching`, `multipatterning`, `metal`, `2nm`, `EUV`, `high_NA`, `SADP`, `DTCO`, `OPC`, `routing`, `SPIE`, `2025`
