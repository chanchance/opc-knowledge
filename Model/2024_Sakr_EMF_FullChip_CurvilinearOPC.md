# High Accuracy OPC Electromagnetic Full-Chip Modeling for Curvilinear Mask OPC and ILT

## 메타데이터
- **저자**: Sakr, E., Levinson, Z., DeLancey, R., Lee, C.J., Li, J., Chen, R., Iwanow, R., Yang, D., Hoppe, W., Latinwo, F., Lucas, K., Liu, P. (Synopsys / ASML)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III
- **DOI/URL**: https://doi.org/10.1117/12.3013089
- **인용수**: ~8

## 핵심 요약
커빌리니어(curvilinear) 마스크 OPC 및 ILT(Inverse Lithography Technology)를 위한 고정밀 OPC 전자기(EM) 전체 칩 모델링 방법론을 제시한다. 맨해튼(Manhattan) 마스크와 달리 임의 곡선 형상을 갖는 커빌리니어 마스크의 EM 효과를 전체 칩 스케일에서 정확하고 효율적으로 모델링하는 새로운 접근법을 개발한다. 리고러스 EM 시뮬레이션과 컴팩트 모델의 결합으로 정확도와 속도를 동시에 달성한다.

## 주요 기여
1. 커빌리니어 마스크 전체 칩 EM 모델링을 위한 새로운 컴팩트-리고러스 하이브리드 방법론
2. 임의 곡선 형상에서 발생하는 추가적 EM 효과(모서리 회절, 곡률 의존 효과) 정량화
3. 맨해튼 마스크 EM 모델 대비 커빌리니어 마스크에서 추가 보정 필요 항목 분석
4. 전체 칩 ILT 플로우에서 EM 모델 통합으로 패터닝 정확도 향상
5. 커빌리니어 OPC/ILT + 고정밀 EM 모델의 실제 EUV 레이어 적용 검증

## 모델 수식/아키텍처

**커빌리니어 마스크 EM 모델 (하이브리드):**
```
E_curvilinear(f) = E_Manhattan_M3D(f) + ΔE_curvilinear(f)
ΔE_curvilinear = f(local_curvature, edge_orientation, pitch_local)
```

**곡률 의존 EM 보정:**
```
ΔE_corner(f) ≈ Σ_k α_k(κ) · basis_k(f)
κ = 로컬 마스크 엣지 곡률 (1/R)
α_k = 곡률 의존 EM 산란 계수 (RCWA로 사전 계산)
```

**전체 칩 커빌리니어 공중상:**
```
I(x) = Σ_k λ_k |∫ φ_k(f) · E_curvilinear(f) · e^{i2πfx} df|²
```

**ILT 목적함수 (EM 포함):**
```
min_mask L(mask) = ||I_sim(mask; EM_model) - I_target||² + λ·R(mask)
```
R(mask) = 마스크 제조성(manufacturability) 정규화 항

**정확도 검증:**
```
EPE_EM_curvilinear vs. EPE_Kirchhoff: 개선 ~1-2nm
EPE_EM_curvilinear vs. EPE_EM_Manhattan: 추가 개선 ~0.3-0.8nm
```

## 모델 유형
- [x] 광학 모델 (EM 전자기, 커빌리니어 M3D)
- [ ] 레지스트 모델
- [ ] ML/DL
- [x] 하이브리드 (리고러스 EM + 컴팩트 커빌리니어 보정)

## OPC 툴 구현 관련성
- ILT/커빌리니어 OPC가 표준화되면서 EM 모델 정확도가 더욱 중요해짐
- skopc ILT 모듈에 커빌리니어 EM 보정 항 추가 고려
- 곡률 의존 EM 계수: RCWA 사전 계산 → 곡률 함수로 보간
- EUV 커빌리니어 마스크: 흡수체 두께 + 곡률 결합 효과 고려
- Synopsys Proteus ILT의 EM 모델 구현 이론적 기반

## 참고문헌
- Tyminski, J.K. et al., "Fast and accurate 3D mask model for full-chip OPC" (2007)
- Lam, M. et al., "M3D-EMF OPC prediction improvements" (2012)
- Yang, Y. et al., "GPU-accelerated ILT for curvilinear mask" (2024)

## 태그
`Model`, `SPIE`, `Mask3D`, `EMF`, `Curvilinear`, `ILT`, `FullChip`, `OPC`, `EUV`, `2024`
