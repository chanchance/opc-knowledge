# Fast Lithography Simulation Under Focus Variations for OPC and Layout Optimizations

## 메타데이터
- **저자**: Ye, J. et al. (Mentor Graphics)
- **연도**: 2006
- **게재지**: Proc. SPIE 6156, Design and Process Integration for Microelectronic Manufacturing IV
- **DOI/URL**: https://doi.org/10.1117/12.658110
- **인용수**: ~60

## 핵심 요약
임의의 디포커스(defocus) 조건에서 공중상을 해석적으로 계산하는 공식을 유도하여, 포커스 변동을 포함한 고속 리소그래피 시뮬레이션을 OPC 및 레이아웃 최적화에 적용하는 방법을 제시한다. 임의 조명 방식(illumination scheme)과 이진·PSM 마스크 모두에 적용 가능한 범용 공식으로, 단일 포커스 시뮬레이션 대비 약 2-3배의 런타임 증가만으로 전체 포커스 범위를 커버한다.

## 주요 기여
1. 임의 디포커스에서 공중상의 해석적 공식 유도 (조명·마스크 종류 무관)
2. 포커스 변동 포함 시 2-3× 런타임 증가만으로 전체 FEM 범위 시뮬레이션
3. OPC 모델에 포커스 변동 통합하는 실용적 프레임워크
4. 공정 윈도우 OPC(PW-OPC) 구현의 이론적 기반 제공
5. 베스트 포커스 이동(BFS) 예측 및 DOF(Depth of Focus) 최적화 적용

## 모델 수식/아키텍처

**포커스 의존 퓨필 함수:**
```
H(f,g; Δz) = H₀(f,g) · exp[i·π·λ·Δz·(f²+g²) / (NA²)]
```
Δz = 디포커스 양, λ = 파장, NA = 개구수

**포커스 의존 TCC:**
```
TCC(f,g; f',g'; Δz) = ∫∫ J(f₀,g₀)·H(f+f₀,g+g₀;Δz)·H*(f'+f₀,g'+g₀;Δz) df₀dg₀
```

**해석적 분해 (포커스 항 분리):**
```
TCC(Δz) = Σ_k λ_k(Δz) · φ_k(f,g;Δz) · φ_k*(f',g';Δz)
         ≈ Σ_k [Σ_m α_{k,m} · Δz^m] · φ_k(f,g) · φ_k*(f',g')
```
α_{k,m} = 포커스 계수 (사전 계산), m = 0,1,2 (0차~2차 포커스 항)

**공정 윈도우 OPC 목적함수:**
```
EPE_PW = max_{Δz∈[-DOF/2, DOF/2], ΔE∈[-ΔE_range, ΔE_range]} |EPE(Δz, ΔE)|
```
→ 전체 공정 창에서 최대 EPE 최소화

**Focus-Exposure 매트릭스 커버리지:**
```
{(Δz_i, ΔE_j)} for i=1..N_focus, j=1..N_dose
→ 해석적 공식으로 N_focus × N_dose 조합 신속 평가
```

## 모델 유형
- [x] 광학 모델
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc PW-OPC(공정 윈도우 OPC) 구현의 핵심 광학 모델 참조
- 포커스 항 분리 → 사전 계산된 계수 테이블로 런타임 최소화
- FEM(Focus-Exposure Matrix) 모델 캘리브레이션에 직접 적용
- 공정 윈도우 검증(PW verification): 동일 해석 공식으로 빠른 검증 가능
- skopc/modeling/focus_model.py: TCC(Δz) 해석 공식 구현

## 참고문헌
- Hopkins, H.H., "On the Diffraction Theory of Optical Images" (1953)
- Yu, P. et al., "True Process Variation Aware OPC" (2007)
- Rosenbluth, A.E. et al., "Fast TCC for High NA" (2005)

## 태그
`Model`, `SPIE`, `FocusModel`, `Defocus`, `ProcessWindow`, `OPC`, `FEM`, `DOF`, `PWOPC`, `2006`
