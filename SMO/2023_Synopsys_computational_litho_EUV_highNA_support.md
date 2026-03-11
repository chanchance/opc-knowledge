# Computational Lithography Solutions to Support EUV High-NA Patterning

## 메타데이터
- **저자**: (Synopsys/ASML 저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2658XXX

## 핵심 요약
고NA EUV(0.55NA) 패터닝을 지원하기 위한 전산 리소그래피 솔루션을 제시한다. 아나모픽 광학계로 인한 스티칭 분할, 증강된 M3D 효과, 확률론적 이슈, 곡선형 마스크 요구 등 고NA EUV 특유의 계산적 도전을 해결하는 SMO/OPC/ILT 방법론을 소개한다.

## 주요 기여
1. **고NA EUV 계산 리소그래피 플로우**: 아나모픽 수치 개구(NA_x=0.55, NA_y=0.33) 지원 OPC/SMO
2. **스티칭 인식 최적화**: 필드 분할 노출에서의 OPC/RET 일관성 확보
3. **증강 M3D 처리**: 고NA에서 더욱 강화된 마스크 3D 효과 보정 방법
4. **확률론적 지원**: ppm 수준 EUV 고장 확률을 비용 함수에 통합

## 알고리즘/수식
### 고NA EUV 아나모픽 광학 모델
```
아나모픽 NA:
  NA_x = 0.55 (스캔 방향)
  NA_y = 0.33 (슬릿 방향)
  → 비대칭 해상도: Δx_min ≠ Δy_min

스티칭 분할:
  전체 필드 = Upper half + Lower half
  스티칭 경계에서 CD/OVL 연속성 보장 필요

M3D 강화 (고NA):
  고NA에서 경사 입사각 증가 → 마스크 옆면 회절 강화
  M3D_correction(high-NA) > M3D_correction(0.33NA)
```

### SMO/OPC 비용 함수 (고NA EUV)
```
Cost = Σ_y_f Σ_i [w_CD·||CD_i - CD_t||² + w_EPE·||EPE_i||²
       + w_stoch·P_fail_i + w_stitch·||ΔCD_stitch||²]

여기서:
  w_stitch: 스티칭 경계 CD 불연속성 패널티 가중치
  P_fail_i: 확률론적 고장 확률
  y_f: 필드 위치 (전체 아크 슬릿)
```

## OPC 툴 SMO 구현 관련성
- 고NA EUV 지원 SMO 엔진: 아나모픽 광학 모델 추가 필요
- 스티칭 인식 OPC: 필드 분할 경계 처리 모듈
- M3D 강화 보정: 고NA 전용 엄격 마스크 모델 분기
- SKOPC SMO/OPC 모듈에서 고NA 모드 설계 참조

## 태그
`SMO`, `OPC`, `EUV`, `high_NA`, `anamorphic`, `stitching`, `M3D`, `stochastic`, `curvilinear`, `DTCO`, `SPIE`, `Synopsys`
