# Lens Aberration Effects on OPC and Their Compensation in Optical Lithography

## 메타데이터
- **저자**: Granik, Y. et al. (Mentor Graphics / Siemens EDA)
- **연도**: 2016
- **게재지**: Proc. SPIE 9780, Optical Microlithography XXIX
- **DOI/URL**: https://doi.org/10.1117/12.2219168
- **인용수**: ~30

## 핵심 요약
제르니케 다항식으로 표현된 렌즈 수차가 OPC 모델과 패터닝 결과에 미치는 영향을 체계적으로 분석하고, 수차 보정을 OPC 모델에 통합하는 방법을 제시한다. 선형 및 이차 수차 모델을 OPC 엔진에 통합함으로써 스캐너 수차 변동에 강건한(robust) OPC 결과를 달성하는 실용적 프레임워크를 제안한다.

## 주요 기여
1. 제르니케 수차 계수가 OPC 모델 파라미터와 CD 예측에 미치는 감도 체계적 분석
2. 선형 수차 모델을 OPC TCC에 통합하는 효율적 방법
3. 스캐너간(scanner-to-scanner) 수차 변동의 OPC 영향 정량화
4. 수차 인식(aberration-aware) OPC 보정으로 CD 변동 감소 실증
5. 실제 양산 스캐너 데이터(Zernike 계수)를 활용한 OPC 모델 업데이트 전략

## 모델 수식/아키텍처

**제르니케 퓨필 함수 전개:**
```
W(ρ, θ) = Σ_{j=1}^{N} c_j · Z_j(ρ, θ)
```
표준 FRINGE 번호 매김 사용:
- Z4: 디포커스(Defocus)
- Z5,Z6: 비점수차(Astigmatism)
- Z7,Z8: 코마(Coma)
- Z9: 1차 구면수차(Spherical)
- Z10~Z36: 고차 수차

**수차 보정 TCC:**
```
TCC_aberr(f,g; f',g') = ∫∫ J(f₀)·P(f+f₀;c)·P*(f'+f₀;c) df₀
P(f;c) = A(f)·exp[i·(2π/λ)·W(f/NA;c)]
```

**선형 수차 감도 함수:**
```
∂I(x)/∂c_j|_{c=0} = Φ_j(x)   [j번째 수차 감도 공중상]
→ ΔI_aberr(x) = Σ_j c_j · Φ_j(x)  [선형 근사]
```

**OPC 수차 보정:**
```
EPE_aberr(x) = Σ_j c_j · S_j(x)
S_j(x) = ∂EPE(x)/∂c_j  [EPE 수차 감도]
→ bias_correction(x) = -Σ_j c_j · S_j(x) / NILS(x)
```

**스캐너간 수차 변동 OPC 영향:**
```
ΔCD_scanner = |Σ_j Δc_j · S_j| / NILS
Δc_j = c_j_scanner2 - c_j_scanner1  [스캐너간 수차 차이]
```

## 모델 유형
- [x] 광학 모델 (수차 모델)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc/modeling/aberration_opc.py: 제르니케 수차 → OPC 바이어스 보정
- 스캐너 수차 캘리브레이션 데이터(ILIAS/FOCAL 측정) → OPC 모델 업데이트
- 선형 모델로 충분: c_j < 5mλ 조건에서 오차 < 0.5nm
- 이차 모델 필요: 고차 수차(Z > 16) 또는 c_j > 10mλ 조건
- 스캐너 유지보수 후 수차 재측정 → OPC 모델 자동 업데이트 파이프라인

## 참고문헌
- Adam, K. et al., "Quadratic aberration model using CTC" (2011)
- Rosenbluth, A.E. et al., "Fast TCC for High NA" (2005)
- Noll, R.J., "Zernike polynomials and atmospheric turbulence" (1976)

## 태그
`Model`, `SPIE`, `Aberration`, `Zernike`, `OPC`, `ScannerVariation`, `LinearModel`, `TCC`, `2016`
