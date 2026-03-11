# Optical Proximity Correction for Anamorphic Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: Adam, K. et al. (Mentor Graphics / Siemens EDA)
- **연도**: 2017
- **게재지**: Proc. SPIE 10450, Photomask Technology + EUV Lithography 2017
- **DOI/URL**: https://doi.org/10.1117/12.2280548
- **인용수**: ~35

## 핵심 요약
0.55NA EUV 리소그래피에 사용되는 비동축(anamorphic) 광학계의 OPC 모델 수정 사항을 체계적으로 분석한다. 비동축 광학계는 x/y 방향으로 서로 다른 축소비(4×/8×)를 사용하여 마스크 크기를 2× 확대하는 특성이 있으며, 이로 인한 마스크 EM 효과, 비동축 이미징, 마스크 제조 변화 등의 OPC 모델 추가 고려사항을 도메인 분해법(DDM)으로 처리한다.

## 주요 기여
1. 비동축 EUV(0.55NA) OPC에 필요한 추가 모델 요소 최초 체계적 정립
2. Domain Decomposition Method(DDM)으로 비동축 마스크 EM 효과 모델링
3. 비동축 광학계의 x/y 비대칭 TCC 계산 방법
4. 마스크 제조 변화(MFV)의 비동축 OPC 모델 영향 분석
5. 고NA EUV RET(Resolution Enhancement Technique) 가이드라인 제시

## 모델 수식/아키텍처

**비동축 광학계 축소비:**
```
Mx = 4× (x 방향)
My = 8× (y 방향)
→ 마스크 CD_x = wafer CD_x × 4
   마스크 CD_y = wafer CD_y × 8
```

**비동축 TCC:**
```
TCC_anamorphic(fx, fy; fx', fy') = ∫∫ J(f0x,f0y)
  · H(fx/Mx+f0x, fy/My+f0y)
  · H*(fx'/Mx+f0x, fy'/My+f0y) df0x df0y
```
Mx ≠ My → x/y 비대칭 TCC → 방향 의존 OPC 보정 필수

**DDM 기반 마스크 EM 모델:**
```
E_mask(x,y) = Σ_segments E_segment(x-x_seg, y-y_seg)
```
각 마스크 세그먼트의 근접장을 개별 계산 후 합산

**비동축 그림자 효과:**
```
Δx_shadow_x = H_absorber · tan(θ_CRA_x) / Mx
Δy_shadow_y = H_absorber · tan(θ_CRA_y) / My
→ x/y 방향 그림자 보정량 상이
```

**OPC 타겟 변환 (비동축):**
```
CD_mask_x = (CD_wafer_x + OPC_bias_x) × Mx
CD_mask_y = (CD_wafer_y + OPC_bias_y) × My
```

## 모델 유형
- [x] 광학 모델 (비동축 TCC, EM)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc 고NA EUV(0.55NA) 모듈: 비동축 TCC + 비대칭 좌표계 처리
- 마스크 좌표: x 방향 4× 확대, y 방향 8× 확대로 별도 처리
- OPC 바이어스: x/y 독립 계산 후 비동축 마스크 좌표로 변환
- ASML EXE:5000 시스템 적용 대상 OPC 모델 이론적 기반
- 비동축 마스크 필기(Stitching): OPC 모델과 스티칭 영역 처리 연계

## 참고문헌
- Ho, B.C.P. et al., "OPC model building for EUV lithography" (2019)
- Flagello, D.G. et al., "EUV flare and proximity modeling" (2011)
- ASML EXE:5000 (0.55NA) high-NA EUV scanner specifications

## 태그
`Model`, `SPIE`, `HighNA`, `EUV`, `Anamorphic`, `OPC`, `DDM`, `0.55NA`, `TCC`, `2017`
