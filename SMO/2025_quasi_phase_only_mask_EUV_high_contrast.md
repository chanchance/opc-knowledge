# Quasi Phase-Only Mask (POM) for High Contrast EUV Imaging

## 메타데이터
- **저자**: (SPIE 13424 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134241J (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051257

## 핵심 요약
EUV 리소그래피에서 고대비 이미징을 위한 준위상 전용 마스크(Quasi Phase-Only Mask, POM) 개념을 제시한다. 흡수층의 진폭 변조를 최소화하고 위상 변조를 극대화하는 POM 설계로 EUV 이미지 콘트라스트를 향상시키고 M3D 효과를 완화하는 새로운 마스크 접근법을 탐구한다.

## 주요 기여
1. **준위상 전용 마스크(POM) 개념**: 진폭보다 위상 변조를 우선하는 새로운 EUV 마스크 설계
2. **고대비 EUV 이미징**: POM의 위상 효과로 이미지 콘트라스트 극대화
3. **M3D 효과 완화**: 얇은 흡수층 + 위상 변조로 마스크 3D 효과 감소
4. **OPC/SMO 연계**: POM 마스크에 적합한 소스-마스크 최적화 전략

## 알고리즘/수식
### 준위상 전용 마스크 원리
```
기존 EUV 이진 마스크:
  흡수층: 진폭 변조 (A_absorber ≈ 0, A_background = 1)
  위상 변조: 부차적

POM (Phase-Only Mask) 개념:
  목표: A_absorber ≈ A_background (진폭 동일)
  위상 차이: Δφ = π (완전 위상 전용)
  → 진폭: |E_absorber| ≈ |E_background|
  → 위상: φ_absorber - φ_background ≈ π
  → 완전 파괴 간섭 → 높은 이미지 콘트라스트

준위상(Quasi): 이상적 위상 전용 마스크의 현실적 근사
  낮은 흡수 + 큰 위상 이동 마스크 재료 조합
  → 기존 TaBN 대비 더 높은 NILS
```

### POM OPC/SMO 연계
```
POM 이미지 형성:
  I(x) ∝ |∑_k σ_k TCC_k ⊗ M_POM|²
  M_POM: 복소 마스크 투과율 (거의 상수 진폭, 이진 위상)

OPC 모델:
  POM 전용 OPC 모델 필요
  위상 마스크 특성에 맞는 보정 알고리즘

SMO:
  POM 마스크 + 소스 동시 최적화
  위상 이동 효과를 활용하는 소스 형상 설계
  → Dipole, Quasar 등 위상 이동 최적 소스
```

## OPC 툴 SMO 구현 관련성
- POM 마스크 OPC: SKOPC에서 준위상 전용 마스크의 복소 투과율 모델 지원
- 위상 마스크 SMO: POM 마스크와 소스를 공동 최적화하는 SMO 알고리즘
- 고대비 이미징 최적화: EUV POM의 위상 효과를 최대화하는 소스-마스크 설계
- 차세대 마스크 지원: TaBN → Low-n → POM으로의 마스크 기술 발전에 대응

## 태그
`POM`, `phase_only_mask`, `EUV`, `high_contrast`, `imaging`, `M3D`, `OPC`, `SMO`, `phase_shift`, `NILS`, `SPIE`, `2025`
