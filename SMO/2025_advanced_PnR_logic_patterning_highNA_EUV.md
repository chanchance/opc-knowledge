# Advanced PnR Logic Patterning Enabled by High-NA EUV Lithography

## 메타데이터
- **저자**: (SPIE 13424 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 1342410 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051054

## 핵심 요약
고NA EUV 리소그래피를 통해 구현되는 고급 PnR(Place and Route) 로직 패터닝을 다룬다. 표준 셀 레이아웃의 메탈 및 비아 레이어에서 0.55NA EUV가 가능하게 하는 새로운 패터닝 능력과 OPC/SMO 최적화 전략을 제시한다.

## 주요 기여
1. **고NA EUV PnR 로직 패터닝**: 표준 셀 기반 로직 레이아웃에서 0.55NA EUV 적용
2. **금속/비아 레이어 패터닝**: M0/M1 및 비아 레이어에서 고NA EUV 단일 노출
3. **SMO/OPC 전략**: 로직 PnR 레이아웃에 최적화된 소스-마스크 최적화
4. **DTCO 지원**: 고NA EUV 기반 디자인-기술 공동 최적화 (DTCO) 실현

## 알고리즘/수식
### 고NA EUV PnR 로직 최적화
```
PnR 로직 레이아웃 특성:
  다양한 피치 혼재 (dense + semi-isolated)
  2D 연결부 (T-junction, L-corner, line-end)
  표준 셀 경계 패턴

0.55NA EUV 패터닝 이점:
  HP_min ≈ λ/(2NA) = 13.5nm/(2×0.55) ≈ 12.3nm
  0.33NA 대비 해상도 40% 향상
  → 더 작은 피치, 더 복잡한 2D 패턴 가능

SMO 최적화 (PnR 로직):
  대표 패턴 클러스터링:
    클러스터 C_i: 유사한 피치/방향 패턴 그룹
    SMO: max_{J} Σ_i w_i · PW(C_i)

  스티칭 인식 SMO:
    상/하단 필드 동시 최적화
    스티칭 경계에서 CD 연속성 유지
```

### PnR 패터닝 성능
```
공정 창 (Process Window):
  EL×DOF 곱 최대화
  EL > 5%, DOF > 80nm 목표

EPE 예산:
  EPE_total = EPE_litho + EPE_overlay + EPE_etch
  고NA EUV로 EPE_litho 감소
  → 전체 EPE 예산 완화

로직 메탈 CD 균일성:
  LCDU < 1.5nm (3σ) 목표
  고NA EUV + 곡선형 마스크 조합
```

## OPC 툴 SMO 구현 관련성
- PnR 로직 SMO: SKOPC SMO에서 표준 셀 기반 로직 레이아웃 최적화
- 고NA EUV 전용 SMO: 0.55NA 아나모픽 광학에 특화된 소스 최적화
- DTCO 통합: PnR 설계 제약과 EUV 패터닝 능력의 공동 최적화
- 곡선형 OPC: PnR 로직 레이아웃의 비아/메탈 레이어 곡선형 마스크

## 태그
`PnR`, `logic`, `patterning`, `high_NA`, `EUV`, `0.55NA`, `SMO`, `OPC`, `DTCO`, `metal`, `via`, `SPIE`, `2025`
