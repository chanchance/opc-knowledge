# A Novel Methodology for Decomposition and Stitching Optimization

## 메타데이터
- **저자**: (SPIE 13425 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 1342504 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050037

## 핵심 요약
고NA EUV 리소그래피의 아나모픽 광학계에서 필수적인 필드 분할(decomposition) 및 스티칭(stitching) 최적화를 위한 새로운 방법론을 제시한다. 전체 칩을 상/하단 절반으로 분할하여 두 번 노출하는 스티칭 방식에서 최적의 분할 경계 위치와 OPC 일관성을 보장하는 전략을 개발한다.

## 주요 기여
1. **분해-스티칭 최적화 방법론**: 고NA EUV 필드 분할 위치와 OPC 일관성 동시 최적화
2. **스티칭 경계 최적 위치 결정**: 회로 설계 관점에서 최적 분할 경계 탐색
3. **OPC 연속성 보장**: 상/하단 필드 OPC 결과의 스티칭 경계 연속성 확보
4. **전체 칩 스케일 적용**: 실제 로직/메모리 설계에 분해-스티칭 최적화 적용

## 알고리즘/수식
### 필드 분해-스티칭 최적화
```
고NA EUV 아나모픽 광학 설정:
  NA_x = 0.55, NA_y = 0.33
  배율: M_x = 4x, M_y = 8x
  필드 크기: 26mm × 16.5mm (웨이퍼 상)
  → 상단 절반 + 하단 절반으로 분할

분해 최적화:
  스티칭 경계 위치 Y_stitch 결정
  제약: 회로 기능 유지 (활성 소자 분할 금지)
  목표: 스티칭 경계에서 CD 불연속성 최소화

스티칭 경계 OPC:
  CD_upper(Y_stitch-) ≈ CD_lower(Y_stitch+)
  ΔCD_stitch = |CD_upper - CD_lower| < ΔCD_threshold

수치 최적화:
  Y_stitch* = argmin_{Y_stitch} [ΔCD_stitch + penalty(circuit_violation)]
```

### 분해-스티칭 비용 함수
```
분해-스티칭 SMO/OPC 비용:
  Cost_total = Cost_upper + Cost_lower + w_stitch · Cost_stitch

  Cost_stitch = Σ_{경계 패턴} ||CD_upper - CD_lower||²
              + w_overlay · ||overlay_error||²

  overlay_error: 두 노출 간 오버레이 오차
```

## OPC 툴 SMO 구현 관련성
- 필드 분해 최적화: SKOPC에서 고NA EUV 스티칭 분해 위치 자동 최적화
- 스티칭 인식 SMO: 상/하단 필드를 동시에 고려한 SMO 비용 함수
- OPC 연속성: 스티칭 경계에서 OPC CD 연속성 보장 알고리즘
- 전체 칩 적용: 실제 로직/메모리 설계에서 스티칭 최적화 실용화

## 태그
`EUV`, `high_NA`, `stitching`, `decomposition`, `anamorphic`, `OPC`, `SMO`, `field_split`, `DTCO`, `SPIE`, `2025`
