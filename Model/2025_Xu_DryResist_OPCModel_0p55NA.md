# OPC Model Accuracy of Dry Resist Readiness for 0.55NA EUVL by Using Low-n Bright Field Mask

## 메타데이터
- **저자**: Xu, D., Gillijns, W., Jambaldinni, S., Hwang, S., De Silva, A., Fenger, G. (imec / ASML / Synopsys)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV
- **DOI/URL**: https://doi.org/10.1117/12.3051855
- **인용수**: ~2

## 핵심 요약
0.55NA EUV 리소그래피를 위한 건식(dry) 레지스트 공정의 OPC 모델 정확도를 low-n 밝은 필드(bright field) 감쇠 위상 이동 마스크(attenuated PSM)와 함께 평가한다. imec N2 노드(28nm 피치) 메탈 설계를 사용하여 NXE:3400 스캐너에서 웨이퍼 노광을 수행하고, 건식 레지스트의 OPC 모델 구축 가능성과 캘리브레이션 정확도를 실험적으로 검증한다.

## 주요 기여
1. 0.55NA EUV용 건식 레지스트 OPC 모델 구축 최초 실험적 검증
2. Low-n 밝은 필드 마스크와 건식 레지스트의 OPC 모델 정확도 평가
3. imec N2 노드(28nm 피치) 실제 메탈 레이어에서의 캘리브레이션 결과
4. 기존 습식(wet) 레지스트 OPC 모델 대비 건식 레지스트 특유 모델 파라미터 분석
5. 0.55NA 전환을 위한 OPC 모델 빌딩 워크플로우 가이드라인

## 모델 수식/아키텍처

**건식 레지스트 특성 (vs. 습식):**
```
Dry resist: 용매 없이 현상 → 수축 효과 상이
           → 레지스트 프로파일, LER 특성 다름
Wet resist: 용매 기반 현상 → 팽윤/수축 복잡
```

**Low-n 밝은 필드 마스크 (BF-aPS):**
```
t_mask(f) = 1 (background) * exp(iφ_attenuator)  [밝은 필드]
φ_attenuator: 위상 이동 (low-n 재료로 구현)
T_attenuator: 투과율 (일반 aPS보다 낮은 위상 대비)
```

**0.55NA EUV OPC 모델 구성요소:**
```
CD(x,y) = f(I_optical(x,y; NA=0.55, anamorphic)
           + I_flare_0.55NA(x,y)
           + I_shadow_0.55NA(x,y)
           + Resist_dry(x,y))
```

**캘리브레이션 결과:**
```
Target node: imec N2, Metal layer
Pitch: 28nm
Scanner: NXE:3400 (0.33NA, 0.55NA 선행 연구용)
RMS_calibration: < 1.5nm (목표 달성)
```

**건식 레지스트 OPC 모델 파라미터 차이:**
```
σ_blur_dry < σ_blur_wet  (확산 거리 작음)
γ_contrast_dry > γ_contrast_wet  (더 높은 감마)
→ CM1 계수 c_k 상이 → 재캘리브레이션 필수
```

## 모델 유형
- [x] 광학 모델 (0.55NA 비동축 EUV 광학)
- [x] 레지스트 모델 (건식 레지스트)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- 0.55NA EUV 전환 시 건식 레지스트 OPC 모델 재구축 필요
- skopc EUV 모듈: 비동축 TCC + 건식 레지스트 파라미터 지원
- 건식 레지스트 특성: 스핀 코팅 없음, 진공 현상 → 기존 모델과 상이
- imec N2(28nm 피치) 노드: 현재 최첨단 기술 노드 OPC 요구사항
- 마스크 종류: low-n BF-aPS → OPC 마스크 모델 파라미터 업데이트 필요

## 참고문헌
- Adam, K. et al., "OPC for anamorphic EUV lithography" (2017)
- Ho, B.C.P. et al., "OPC model building for EUV" (2019)
- Zeng, Q. et al., "OPC and modeling for 0.55NA EUV stitching" (2024)

## 태그
`Model`, `SPIE`, `HighNA`, `EUV`, `0.55NA`, `DryResist`, `OPCModel`, `Calibration`, `imecN2`, `2025`
