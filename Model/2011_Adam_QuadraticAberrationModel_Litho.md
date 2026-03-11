# Fast Algorithm for Quadratic Aberration Model in Optical Lithography Based on Cross Triple Correlation

## 메타데이터
- **저자**: Adam, K. et al. (Mentor Graphics)
- **연도**: 2011
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 10, No. 2
- **DOI/URL**: https://doi.org/10.1117/1.3586797
- **인용수**: ~40

## 핵심 요약
광학 리소그래피의 이차(quadratic) 수차(aberration) 모델을 효율적으로 시뮬레이션하기 위한 고속 알고리즘을 제안한다. 일반화된 교차 삼중 상관(Cross Triple Correlation, CTC) 접근법을 통해 개별 제르니케(Zernike) 계수 간 상호작용 항을 정확하고 효율적으로 계산한다. 부분 가간섭 조명 하에서 다양한 제르니케 차수가 공중상 강도 분포에 미치는 영향을 시뮬레이션으로 검증한다.

## 주요 기여
1. 이차 수차 모델을 위한 CTC 기반 고속 알고리즘 개발
2. 선형 모델에서 포착 못하는 제르니케 계수 간 상호작용 항 계산
3. 부분 가간섭 조명(partially coherent illumination) 하 정확도 검증
4. 선형 수차 모델 대비 고차 수차 영향 정량적 분석
5. OPC 모델에 수차 의존성 통합하는 실용적 프레임워크

## 모델 수식/아키텍처

**제르니케 퓨필 함수:**
```
P(ρ,θ) = A(ρ) · exp[i·W(ρ,θ)]
W(ρ,θ) = Σ_j c_j · Z_j(ρ,θ)   [제르니케 전개]
```
c_j = j번째 제르니케 계수, Z_j = 제르니케 다항식

**선형 수차 모델 (1차 근사):**
```
ΔI_linear(x) = Σ_j c_j · Φ_j(x)
Φ_j(x) = ∂I/∂c_j|_{c=0}   [수차 감도 함수]
```

**이차 수차 모델 (2차 근사):**
```
ΔI_quadratic(x) = Σ_j c_j · Φ_j(x) + Σ_{j,k} c_j · c_k · Ψ_{jk}(x)
```
Ψ_{jk} = 교차항 감도 (CTC로 계산)

**CTC 기반 Ψ_{jk} 계산:**
```
Ψ_{jk}(x) = Re[∫∫ J(f₀) · H_j(f+f₀) · H_k*(f'+f₀) · M(f) · M*(f') e^{i2π(f-f')x} df df' df₀]
```
H_j(f) = ∂H/∂c_j (퓨필 함수의 j번째 수차 감도)

**수차 민감도 OPC 보정:**
```
EPE_aberration(x) = Σ_j c_j · (∂EPE/∂c_j) + Σ_{j,k} c_j·c_k · (∂²EPE/∂c_j∂c_k)
```

## 모델 유형
- [x] 광학 모델 (수차 모델)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델에 렌즈 수차 의존성 통합 시 핵심 참조
- 선형 모델로 충분한 경우(c_j < ~10mλ): Φ_j만 계산
- 이차 모델 필요한 경우(c_j > 10mλ 또는 고차 수차): Ψ_{jk} 추가
- skopc/modeling/aberration.py: 제르니케 계수 → 수차 보정 TCC 구현
- 스캐너 유지보수/캘리브레이션 주기에 따라 수차 계수 업데이트 필요

## 참고문헌
- Rosenbluth, A.E. et al., "Fast TCC algorithm for High NA" (2005)
- Hopkins, H.H., "On the Diffraction Theory of Optical Images" (1953)
- Noll, R.J., "Zernike polynomials and atmospheric turbulence" (1976)

## 태그
`Model`, `SPIE-JMM`, `Aberration`, `Zernike`, `QuadraticModel`, `CTC`, `OpticalModel`, `LithographySimulation`, `2011`
