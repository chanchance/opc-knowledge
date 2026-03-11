# Understanding and Measuring EUV Mask 3D Effects

## 메타데이터
- **저자**: (SPIE 12953 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical Microlithography XXXVI, 129530F (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3012400

## 핵심 요약
EUV 리소그래피에서 마스크 3D(M3D) 효과를 이해하고 측정하는 방법론을 제시한다. M3D 효과가 EUV 이미징에 미치는 영향을 정량화하고, 실험적 측정과 시뮬레이션을 통해 M3D 보정 방법의 유효성을 검증한다.

## 주요 기여
1. **M3D 효과 정량화**: EUV 마스크 3D 전자기장 효과의 체계적 측정 방법론
2. **M3D 시뮬레이션 검증**: 실험 데이터와 RCWA/EMF 시뮬레이션 비교
3. **M3D 보정 평가**: OPC/SMO에서 M3D 보정 방법의 효과 정량화
4. **고NA EUV M3D**: 0.55NA 이상에서 더욱 강화되는 M3D 효과 분석

## 알고리즘/수식
### EUV M3D 효과 모델
```
마스크 3D 효과:
  EUV 반사형 마스크 구조:
    기판 (Si/Mo 다층막) + 흡수층 (TaBN, ~60nm)
    → 흡수층 높이 >> λ_EUV (13.5nm)
    → 경사 입사각(6°)에서 강한 3D 효과 발생

M3D 효과 성분:
  1. 수평 이미지 이동 (Best Focus Shift): BFS(pitch)
  2. 마스크 바이어스 보정: ΔCD_M3D(pitch, orientation)
  3. 베스트 포커스 비대칭: BF asymmetry (H vs V)

측정 방법:
  M3D_meas = CD_litho_result - CD_scalar_model
  → scalar 모델과 실제 웨이퍼 결과 차이로 M3D 성분 추출
```

### M3D 보정 통합
```
OPC/SMO M3D 보정:
  CD_corrected = CD_scalar + M3D_correction(pitch, NA, 흡수층 재료)

Look-Up Table 방식:
  M3D_LUT[pitch][orientation][focus] = ΔCD_M3D
  → OPC 보정에 실시간 적용
```

## OPC 툴 SMO 구현 관련성
- M3D 보정 통합: SKOPC OPC/SMO 엔진에서 M3D LUT 기반 보정 모듈
- 고NA EUV 설계: M3D 효과 강화에 대응한 SMO 비용 함수 조정
- 흡수층 재료별 M3D: TaBN vs low-n vs attPSM 별 M3D 보정 파라미터
- 측정-시뮬레이션 비교: OPC 모델 보정 시 M3D 성분 분리 방법론

## 태그
`M3D`, `EUV`, `mask_3D_effects`, `measurement`, `OPC_correction`, `high_NA`, `BFS`, `RCWA`, `EMF`, `SPIE`
