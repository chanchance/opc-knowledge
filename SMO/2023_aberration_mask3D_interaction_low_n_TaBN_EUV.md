# Interaction Between Aberrations and Mask 3D Effects for Low-n and Ta-Based Absorbers in EUV Lithography

## 메타데이터
- **저자**: (JMM 저자 정보)
- **연도**: 2023
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 22, Issue 2, 024402
- **DOI/URL**: https://doi.org/10.1117/1.JMM.22.2.024402

## 핵심 요약
EUV 리소그래피에서 렌즈 수차(aberration)와 마스크 3D(M3D) 효과 간의 상호작용을 low-n 흡수층과 TaBN(Ta 기반) 흡수층 마스크에 대해 분석한다. 고립 피처(isolated feature) 이미징에서 마스크 바이어스 및 보조 피처(assist feature)가 수차 영향 최소화에 필수적임을 보이고, 보조 피처 위치 최적화로 홀수 수차(odd aberration)의 영향을 줄이는 방법을 제시한다.

## 주요 기여
1. **수차-M3D 상호작용 분석**: 렌즈 수차와 마스크 3D 효과의 결합 영향 정량화
2. **흡수층 재료 비교**: low-n 흡수층 vs TaBN에서 수차/M3D 상호작용 차이
3. **보조 피처 위치 최적화**: assist feature 위치로 홀수 수차 영향 최소화
4. **피치 간 포커스 범위 최소화**: 보조 피처 최적화로 through-pitch BFS 균일화

## 알고리즘/수식
### 수차-M3D 결합 이미징 모델
```
수차 + M3D 결합 효과:
  CD(pitch, W, M3D) = CD_scalar(pitch)
                    + ΔCD_aberr(W_k, pitch)
                    + ΔCD_M3D(material, pitch)
                    + ΔCD_interaction(W_k, M3D)

여기서:
  W_k: k번째 Zernike 수차 계수
  ΔCD_interaction: 수차-M3D 교차항 (non-linear 효과)

홀수 수차 영향 (odd Zernike):
  ΔCD_odd = Σ_{k=odd} c_k · Z_k(ρ, θ) → 이미지 이동/비대칭
  → 보조 피처 위치 조정으로 ΔCD_odd 최소화 가능
```

### 보조 피처 위치 최적화
```
보조 피처 위치 최적화:
  SRAF_pos* = argmin_{SRAF_pos} ||BFS(pitch) - BFS_target||²
              subject to: MRC(SRAF) ≥ MRC_min

흡수층별 최적 SRAF 위치:
  low-n 흡수층: BFS 특성 다름 → 다른 SRAF 위치 최적
  TaBN 흡수층: 기존 최적화 결과 적용 가능
```

## OPC 툴 SMO 구현 관련성
- 수차-M3D 결합 모델: SKOPC SMO 비용 함수에 수차-M3D 교차항 포함
- 흡수층 재료별 SMO: low-n vs TaBN에 따른 SRAF 위치 최적화 분기
- 보조 피처 최적화: SMO에서 SRAF 삽입 + 위치 최적화를 수차 인식으로 확장
- 홀수 수차 보상: SMO 소스 형상으로 홀수 수차 영향 경감 전략

## 태그
`EUV`, `aberration`, `M3D`, `low_n`, `TaBN`, `mask_absorber`, `SRAF`, `assist_feature`, `odd_aberration`, `BFS`, `through_pitch`, `JMM`
