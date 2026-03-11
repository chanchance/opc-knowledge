# OPC Model Prediction Capability Improvements by Accounting for Mask 3D-EMF Effects

## 메타데이터
- **저자**: Lam, M. et al. (Synopsys)
- **연도**: 2012
- **게재지**: Proc. SPIE 8326, Optical Microlithography XXV
- **DOI/URL**: https://doi.org/10.1117/12.916863
- **인용수**: ~55

## 핵심 요약
전체 칩 리고러스 3D 마스크 모델링은 계산 비용 때문에 불가능하지만, 근사 시뮬레이션 기법을 통해 3D 마스크 전자기(EMF) 효과를 OPC 모델에 반영할 수 있음을 보인다. 이 접근법이 OPC 모델의 예측 능력을 크게 향상시킴을 immersion 리소그래피 실험 데이터로 실증한다. 기존 Kirchhoff 근사 모델 대비 2D 구조 및 다양한 피치에서의 CD 예측 오차를 50% 이상 감소시킨다.

## 주요 기여
1. 근사 M3D-EMF 방법으로 전체 칩 OPC에서 3D 마스크 효과 반영 가능성 실증
2. Kirchhoff vs. 근사 M3D 모델의 정량적 정확도 비교 (CD 예측 오차 50% 감소)
3. 특정 조명 조건(off-axis illumination)에서 M3D 효과의 방향 의존성 분석
4. 실제 양산 공정 데이터(193nm immersion, NA 1.35)에서의 검증
5. OPC 캘리브레이션 게이지 선택 시 M3D 효과 고려 가이드라인

## 모델 수식/아키텍처

**Kirchhoff(박막) 마스크 투과 함수:**
```
t_K(x,y) = rect_function  [이진 0/1]
```

**M3D-EMF 보정 계수 (룩업 테이블):**
```
t_M3D(f) = t_K(f) · C_M3D(f, pitch, azimuth, polarization)
C_M3D: RCWA로 사전 계산 → 피치/방향별 복소 보정 인자
```

**OPC 모델 내 M3D 통합:**
```
I_OPC(x) = Σ_k λ_k |∫ φ_k(f) · t_M3D(f) · e^{i2πfx} df|²
```
φ_k = SOCS 커널, t_M3D = M3D 보정된 마스크 스펙트럼

**Best Focus Shift (M3D 유발):**
```
ΔBF = ΔBF_ref + (∂ΔBF/∂pitch) · Δpitch
```
방향·피치별 기울기로 선형 보간

**모델 정확도 향상 정량화:**
```
Improvement = (RMS_Kirchhoff - RMS_M3D) / RMS_Kirchhoff × 100%
```
실험: 2D 코너 구조에서 52% 향상, 1D 패턴에서 18% 향상

## 모델 유형
- [x] 광학 모델 (M3D EMF)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc M3D 컴팩트 모델 구현 시 RCWA 사전 계산 + 보간 전략 참조
- 193nm ArF immersion NA 1.35: M3D 효과가 CD 예측에 수 nm 영향
- 조명 조건(off-axis 정도)에 따라 M3D 효과 크기 달라짐
- 게이지 선택: 다양한 피치(100nm~500nm) + 방향(H/V/45°) 포함 필수
- 전체 칩 OPC 런타임: 컴팩트 M3D 룩업 테이블 방식으로 허용 범위 내 유지

## 참고문헌
- Tyminski, J.K. et al., "Fast and accurate 3D mask model for full-chip OPC" (2007)
- Erdmann, A. et al., "Mask 3D effects on resist model calibration" (2009)
- Szucs, A. et al., "Advanced OPC Mask-3D and Resist-3D modeling" (2014)

## 태그
`Model`, `SPIE`, `Mask3D`, `EMF`, `RCWA`, `CompactModel`, `OPC`, `Immersion`, `Calibration`, `2012`
