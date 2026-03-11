# OPC and Modeling Solution to Support 0.55NA EUV Stitching

## 메타데이터
- **저자**: Zeng, Q., Xu, D., Zeng, X., Gillijns, W., Tejnil, E., Sun, Y., Fenger, G. (imec / ASML Brion / Synopsys)
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII
- **DOI/URL**: https://doi.org/10.1117/12.3034957
- **인용수**: ~8

## 핵심 요약
0.55NA 고NA EUV 리소그래피 시스템의 비동축(anamorphic) 광학계로 인해 필요한 마스크 스티칭(stitching) 공정을 지원하기 위한 OPC 및 모델링 솔루션을 제시한다. x/y 방향 4×/8× 다른 축소비 때문에 단일 노광으로 커버할 수 없는 큰 칩을 두 번 노광으로 스티칭하는 과정에서 OPC 모델이 처리해야 할 새로운 도전 과제들을 해결한다.

## 주요 기여
1. 0.55NA 비동축 EUV 스티칭을 위한 OPC 모델링 솔루션 제안
2. 스티칭 경계에서의 마스크 중첩(overlap) 처리 OPC 방법론
3. 비동축 광학 특성(4×/8×)이 OPC 모델에 미치는 영향 분석
4. 스티칭 유발 CD 변동 및 오버레이 오차의 OPC 모델 통합
5. 실제 스티칭 실험 결과와 OPC 모델 예측 비교 검증

## 모델 수식/아키텍처

**0.55NA 비동축 시스템:**
```
Mx = 4×, My = 8×
→ 단일 노광 필드 크기: x_field/4 × y_field/8
→ 칩이 y_field/8 초과 시 스티칭 필요
```

**스티칭 영역 OPC 모델:**
```
I_stitch(x,y) = I_exposure1(x,y) + I_exposure2(x,y-Δy_stitch)
```
두 노광의 공중상이 스티칭 경계에서 중첩

**스티칭 경계 OPC 타겟:**
```
CD_edge1 + CD_edge2 = CD_target × 2
→ 각 노광의 절반씩 기여하도록 OPC 분배
```

**스티칭 오버레이 오차 모델:**
```
EPE_stitch = EPE_litho + EPE_overlay
EPE_overlay = ∂CD/∂y · Δy_overlay
Δy_overlay = stitch positioning error
```

**비동축 좌표 변환:**
```
mask_coord_x = wafer_coord_x × Mx
mask_coord_y = wafer_coord_y × My
OPC_bias_x ≠ OPC_bias_y  [x/y 비대칭 보정]
```

## 모델 유형
- [x] 광학 모델 (비동축 0.55NA EUV)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc 고NA EUV 모듈: 스티칭 OPC 지원 추가
- 비동축 좌표계: x/y 독립 OPC 바이어스 처리
- 스티칭 경계 처리: 두 노광의 OPC 타겟 분배 알고리즘
- 오버레이 예산: 스티칭 오차가 OPC 정확도 요구사항에 미치는 영향
- ASML EXE:5000 시스템 + 스티칭 공정 지원 툴체인의 핵심

## 참고문헌
- Adam, K. et al., "OPC for anamorphic EUV lithography" (2017)
- Xu, D. et al., "OPC model accuracy for dry resist at 0.55NA" (2025)
- Ho, B.C.P. et al., "OPC model building for EUV" (2019)

## 태그
`Model`, `SPIE`, `HighNA`, `EUV`, `0.55NA`, `Stitching`, `Anamorphic`, `OPC`, `Overlay`, `2024`
