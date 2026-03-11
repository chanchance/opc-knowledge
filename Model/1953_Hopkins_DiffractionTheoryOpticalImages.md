# On the Diffraction Theory of Optical Images

## 메타데이터
- **저자**: Harold Horace Hopkins
- **연도**: 1953
- **게재지/학회**: Proceedings of the Royal Society of London. Series A. Mathematical and Physical Sciences, Vol. 217, pp. 408-432
- **DOI/URL**: https://doi.org/10.1098/rspa.1953.0071
- **인용수**: 5000+

## 핵심 요약
광학 이미지 형성의 회절 이론을 정립한 기념비적 논문. 부분 간섭(partially coherent) 조명 하에서 광학 시스템의 이미지 형성을 수학적으로 엄밀하게 정식화했다. 물체 평면의 간섭 함수(coherence function), 이미지 형성 시스템의 회절 분포 함수, 물체의 구조 함수를 이용하여 4중 적분(four-fold integral)으로 이미지 강도를 표현한다. 이 이론은 현대 광학 리소그래피 시뮬레이션의 근간이 되는 Transmission Cross Coefficient (TCC) 개념을 최초로 도입한 논문으로, OPC 모델링 전 분야에서 가장 많이 인용되는 기초 논문 중 하나이다.

## 주요 기여
- 부분 간섭 광학 시스템의 이미지 강도 4중 적분 공식 유도
- Transmission Cross Coefficient (TCC) 개념 최초 도입
- 완전 간섭(coherent)과 완전 비간섭(incoherent) 조명의 통합된 이론적 틀 제공
- 傅리에(Fourier) 변환 기반 이미지 강도 계산 방법론 확립
- 현대 리소그래피 시뮬레이터의 이론적 토대 마련

## 모델 아키텍처/수식
**Hopkins 부분 간섭 이미지 형성 이론의 핵심:**

이미지 강도 I(x):
```
I(x) = ∫∫∫∫ J(x₁, x₂) · h(x - x₁) · h*(x - x₂) · t(x₁) · t*(x₂) dx₁ dx₂
```
여기서:
- J(x₁, x₂): 물체 평면의 상호 간섭 함수 (mutual coherence function)
- h(x): 회절 분포 함수 (점 확산 함수, PSF)
- t(x): 물체 투과율 함수 (마스크 패턴)
- *: 복소 켤레

**Fourier 공간에서의 TCC 표현:**
```
I(x) = ∫∫ TCC(f₁, f₂) · T(f₁) · T*(f₂) · exp(j2π(f₁-f₂)x) df₁ df₂
```

**TCC (Transmission Cross Coefficient) 정의:**
```
TCC(f₁, f₂) = ∫ S(f) · H(f + f₁) · H*(f + f₂) df
```
여기서:
- S(f): 유효 광원의 강도 분포 (source distribution)
- H(f): 투영 렌즈의 동공 함수 (pupil function)
  - 이상적: H(f) = 1 if |f| ≤ NA/λ, else 0
- T(f): 마스크 투과율의 Fourier 변환
- NA: 개구수 (Numerical Aperture)
- λ: 조명 파장

**TCC의 SVD 분해 (계산 효율화):**
```
TCC(f₁, f₂) ≈ Σₙ λₙ · φₙ(f₁) · φₙ*(f₂)
I(x) ≈ Σₙ λₙ · |φₙ ⊗ t(x)|²
```
n개의 고유 커널로 부분 간섭 이미징 근사 (n = 15~50이 일반적)

**완전 간섭 극한 (σ → 0):**
```
I(x) = |h ⊗ t(x)|²    (단일 PSF 합성곱의 절댓값 제곱)
```

**완전 비간섭 극한 (σ → ∞):**
```
I(x) = |h|² ⊗ |t(x)|²    (강도 PSF와 마스크 강도의 합성곱)
```

**리소그래피 적용 파라미터:**
- 부분 간섭 계수: σ = σ_outer (환형 조명 시 σ_inner도 포함)
- 노광 파장: λ (248nm KrF, 193nm ArF, 13.5nm EUV)
- 개구수: NA (0.6~1.35 immersion, EUV ~0.33)

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 모든 광학 시뮬레이션의 이론적 근거. TorchLitho(TorchOPC/TorchLitho GitHub)의 Hopkins 모델 구현이 이 논문을 직접 구현한 것. `LithoEngine(process.optical, process.resist)` 호출 시 내부적으로 TCC 커널을 계산하는데, 이 논문의 TCC 수식을 이해하면 파라미터(NA, σ, λ, 커널 수) 설정이 명확해진다. TCC SVD 분해로 n개 커널을 쓸수록 정확하지만 느려지므로, `recipes/example_arfimm.yaml`의 광학 파라미터와 커널 수를 적절히 조정 필요.

## 참고문헌 (핵심)
- Abbe, E., "Beiträge zur Theorie des Mikroskops und der mikroskopischen Wahrnehmung," Arch. Mikrosk. Anat. 9, 1873
- Born, M. and Wolf, E., "Principles of Optics," Pergamon Press (1959)
- Zernike, F., "The concept of degree of coherence," Physica 3, 1938
- van Cittert, P.H., "Die wahrscheinliche Schwingungsverteilung," Physica 1, 1934

## 태그
`Model`, `OPC`, `OpticalModel`, `Hopkins`, `TCC`, `PartialCoherence`, `Diffraction`, `PSF`, `SVD`, `Fourier`, `FoundationalPaper`, `Lithography`, `ImagingTheory`
