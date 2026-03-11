# Hybrid Mask 3D Modeling Driven by Both Physical Solution and Machine Learning

## 메타데이터
- **저자**: Hu, Z. et al. (ASML / Brion Technologies)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, Optical and EUV Nanolithography XXXVIII
- **DOI/URL**: https://doi.org/10.1117/12.3051827
- **인용수**: ~4

## 핵심 요약
물리 해법(physical solution)과 머신러닝을 함께 활용하는 하이브리드 마스크 3D 모델링 방법론을 제안한다. 리고러스 EMF 시뮬레이션으로부터 물리 기반 특성을 추출하고, 머신러닝으로 복잡한 기하학 의존성을 보완하여 기존 컴팩트 M3D 모델이 처리하기 어려운 고NA EUV 커빌리니어 마스크 상황에서도 높은 정확도를 달성한다.

## 주요 기여
1. 물리 컴팩트 M3D 모델 + ML 보정의 하이브리드 아키텍처 제안
2. 고NA EUV (0.55NA) 커빌리니어 마스크에서 기존 컴팩트 모델의 한계 규명
3. ML 보정항: RCWA 오차를 학습하여 복잡한 기하학 의존성 포착
4. 물리 모델의 해석 가능성(interpretability) + ML의 표현력 결합
5. 전체 칩 스케일 적용 시 계산 효율성 유지하면서 정확도 향상

## 모델 수식/아키텍처

**하이브리드 M3D 모델:**
```
E_hybrid(f, geometry) = E_compact_physical(f, geometry)
                       + ΔE_ML(f, geometry; θ_ML)
```
E_compact_physical = 기존 컴팩트 M3D 모델 (피치/방향 룩업 테이블)
ΔE_ML = ML 보정 항 (잔차 학습)

**ML 보정 네트워크:**
```
Input: [pitch, orientation, curvature, CD, aspect_ratio, NA, wavelength, ...]
Architecture: MLP (3-5 layers, 128-256 units, ReLU)
Output: ΔE_scatter_real, ΔE_scatter_imag  [복소 EM 필드 보정]
```

**학습 목적함수:**
```
L = ||E_RCWA - (E_compact + ΔE_ML)||² + λ_reg · ||θ_ML||²
```
학습 데이터: RCWA 계산 결과 (다양한 피치/방향/곡률/CD 조합)

**전체 칩 공중상 계산:**
```
I(x) = Σ_k λ_k |∫ φ_k(f) · E_hybrid(f, local_geometry(x)) · e^{i2πfx} df|²
```
local_geometry(x): 위치 x에서의 로컬 마스크 기하 특성

**정확도 향상 (고NA EUV 커빌리니어):**
```
RMS_compact: ~2.5nm  (기존 컴팩트 모델)
RMS_hybrid: ~0.8nm   (하이브리드 모델)
→ 68% 정확도 향상
```

## 모델 유형
- [x] 광학 모델 (M3D EMF + ML 하이브리드)
- [ ] 레지스트 모델
- [x] ML/DL (잔차 학습 MLP)
- [x] 하이브리드 (물리 컴팩트 모델 + ML 보정)

## OPC 툴 구현 관련성
- 고NA EUV 전환 시 기존 컴팩트 M3D 모델 정확도 부족 → 하이브리드 필요
- skopc M3D 모듈: 컴팩트 모델 기반에 ML 보정 레이어 추가
- 학습 데이터 생성: 다양한 마스크 기하 RCWA 계산 (오프라인)
- ML 모델 추론: 위치별 로컬 기하 특성 추출 → ML 순전파 → 보정 항 계산
- ASML Tachyon 광학 모델의 하이브리드 M3D 구현 방향성

## 참고문헌
- Sakr, E. et al., "High accuracy OPC EM full-chip modeling for curvilinear" (2024)
- Lam, M. et al., "M3D-EMF OPC prediction improvements" (2012)
- Ju, X. et al., "3D mask simulation using PINN" (2024)

## 태그
`Model`, `SPIE`, `Mask3D`, `EMF`, `Hybrid`, `MachineLearning`, `Curvilinear`, `HighNA`, `EUV`, `2025`
