# Full Field Stitching-Aware High-NA EUV OPC/RET Flow

## 메타데이터
- **저자**: Zachary Levinson, Yunqiang Zhang, Linghui Wu, Sean Chang, Shaowen Gao, Kevin Yang, Andy Dawes, Kevin Lucas
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250H (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3052709

## 핵심 요약
고NA EUV 스티칭 적용에서 공정 및 마스크 변동을 통한 패터닝 제어를 보장하는 OPC/RET 마스크 합성 단계를 다룬다. 전체 필드 스티칭 인식 OPC/RET 플로우를 개발하여 상/하단 필드 경계에서 패턴 연속성과 CD 일관성을 보장한다.

## 주요 기여
1. **스티칭 인식 OPC 플로우**: 고NA EUV 필드 스티칭을 명시적으로 고려한 OPC/RET 합성 플로우
2. **공정/마스크 변동 강건성**: 스티칭 경계에서 공정 변동(도즈, 포커스)과 마스크 변동에 강건한 OPC
3. **RET 통합**: SRAF 배치, 편광 최적화 등 RET를 스티칭 경계와 통합
4. **전체 필드 최적화**: 상단/하단 절반 필드를 동시에 고려한 전체 필드 OPC 최적화

## 알고리즘/수식
### 스티칭 인식 OPC/RET 플로우
```
고NA EUV 아나모픽 광학:
  NA_x = 0.55, NA_y = 0.33
  배율: M_x = 4x, M_y = 8x
  필드: 상단 절반 + 하단 절반 (각 26mm × 8.25mm)

스티칭 인식 OPC 목표:
  CD_upper(Y_stitch-ε) ≈ CD_lower(Y_stitch+ε)
  EPE_stitch = |CD_upper - CD_lower| < threshold

OPC/RET 플로우:
  1. 스티칭 경계 Y_stitch 결정
  2. 상단 필드 OPC/RET 합성
     - 스티칭 경계 근처: 경계 조건 적용
  3. 하단 필드 OPC/RET 합성
     - 상단 OPC 결과와 경계 일관성 강제
  4. 스티칭 경계 OPC 수렴 검증
```

### 강건성 최적화
```
공정 변동 강건성:
  Robust_OPC = argmin_{M} [EPE_nominal + w_var · EPE_variation]
  EPE_variation = Σ_{dose,focus} ||CD(dose,focus) - CD_target||²

마스크 변동 강건성:
  MEF 제어: ΔCD_wafer / ΔCD_mask < MEF_threshold
  스티칭 경계에서 MEF 최소화

RET 통합:
  SRAF: 스티칭 경계 근처 SRAF 배치 최적화
  → 스티칭 경계 NILS 향상
  → 도즈/포커스 변동에 대한 공정 창 확대
```

## OPC 툴 SMO 구현 관련성
- 스티칭 인식 OPC 플로우: SKOPC의 고NA EUV 스티칭 OPC 모듈 핵심 참고
- 경계 조건 OPC: 상/하단 필드 경계에서 CD 연속성 보장하는 OPC 알고리즘
- RET 스티칭 통합: SRAF/편광 최적화와 스티칭 OPC의 통합 플로우
- 강건성 OPC: 공정/마스크 변동에 강건한 스티칭 경계 OPC 설계

## 태그
`OPC`, `RET`, `stitching`, `high_NA`, `EUV`, `0.55NA`, `field_split`, `process_variation`, `mask_variation`, `SRAF`, `DTCO`, `SPIE`, `2025`
