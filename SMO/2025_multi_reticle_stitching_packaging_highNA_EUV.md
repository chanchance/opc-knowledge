# Multi-Reticle Stitching: Applications from Packaging to High-NA EUV

## 메타데이터
- **저자**: Christopher M. Bottoms, Richard C. Johnson, Romain J. Lallement, Cheuk Wun Wong, Alex R. Hubbard, Sarah N. Chowdhury, Jed H. Rankin
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134240O (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051542

## 핵심 요약
패키징에서 고NA EUV까지 다양한 응용 분야에서의 다중 레티클 스티칭 기술을 종합적으로 다룬다. i-라인, DUV, EUV 기술에 걸친 스티치 공정 데이터 분석을 포함하여 마스크 설계, 공정, 계측 관점에서 다중 레티클 스티칭의 현황과 과제를 정리한다.

## 주요 기여
1. **다중 레티클 스티칭 종합 개요**: i-라인/DUV/EUV 기술에서의 스티칭 기술 발전 체계화
2. **패키징 스티칭**: 대면적 패키지 기판에서의 레티클 스티칭 적용
3. **고NA EUV 스티칭**: 아나모픽 필드에서의 상/하단 필드 스티칭 특성 분석
4. **마스크 설계-공정-계측 통합**: 스티칭 최적화를 위한 통합적 접근법

## 알고리즘/수식
### 다중 레티클 스티칭 기술 비교
```
스티칭 기술 발전 단계:
  i-라인 스티칭: 큰 스티치 오버레이 허용 (μm 수준)
  DUV 스티칭: nm 수준 오버레이 요구
  EUV 0.33NA 스티칭: 선택적 (옵션)
  EUV 0.55NA 스티칭: 필수 (아나모픽 필드 분할)

스티칭 오버레이 오차:
  ΔCD_stitch = f(overlay_error, image_contrast)
  overlay_error_3σ < stitch_budget

패키징 스티칭:
  대면적 패키지 기판: 단일 레티클 필드 초과
  → 여러 레티클 스티칭으로 대면적 패턴 형성
  오버레이 요구: μm ~ 수십 nm (패키지 레벨)

고NA EUV 스티칭:
  상단/하단 필드 각 26mm × 8.25mm
  스티칭 정밀도: <2nm (3σ) 필요
```

### 스티칭 공정 최적화
```
마스크 설계 관점:
  스티칭 경계 레이아웃 제약:
    - 활성 소자 분할 금지
    - 스티칭 경계 CD 균일성 최대화

공정 관점:
  스티치 오버레이 = 스캐너 오버레이 + 마스크 등록 오차
  스캐너 성능: TWINSCAN EXE 시리즈 오버레이 spec

계측 관점:
  스티칭 경계 CD 측정: 상/하단 CD 차이 모니터링
  오버레이 측정: 스티칭 경계 정렬 오차 추적
```

## OPC 툴 SMO 구현 관련성
- 스티칭 OPC 맥락: 다양한 기술 노드에서의 스티칭 역사적 발전 이해
- 고NA EUV 스티칭 설계: 마스크 설계 제약과 OPC 전략 연계
- 패키징 스티칭: SKOPC가 패키징 응용까지 확장 시 참고
- 스티칭 계측 연계: OPC 교정을 위한 스티칭 경계 계측 방법론

## 태그
`stitching`, `multi_reticle`, `EUV`, `high_NA`, `packaging`, `DUV`, `overlay`, `mask_design`, `metrology`, `SPIE`, `2025`
