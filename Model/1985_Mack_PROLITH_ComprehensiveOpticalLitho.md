# PROLITH: A Comprehensive Optical Lithography Model

## 메타데이터
- **저자**: Chris A. Mack
- **연도**: 1985
- **게재지/학회**: SPIE Optical Microlithography IV, Vol. 538, pp. 207-220
- **DOI/URL**: https://doi.org/10.1117/12.947767; PDF: https://www.lithoguru.com/scientist/litho_papers/1985_1_PROLITH_A%20Comprehensive%20Optical%20Lithography%20Model.pdf
- **인용수**: 1000+

## 핵심 요약
리소그래피 시뮬레이션 분야의 가장 기념비적인 논문 중 하나로, 최초의 포괄적 광학 리소그래피 모델 PROLITH(Positive Resist Optical LITHography)를 소개한다. 광학 투영 시스템, 정재파(standing wave) 효과, 레지스트 노광 반응의 반응속도론적 모델, 레지스트 현상의 반응속도론적 모델을 통합한 완전한 시뮬레이션 체계를 제시한다. 개인용 컴퓨터(IBM PC)에서 실행 가능한 최초의 리소그래피 시뮬레이터로, 리소그래피 모델링을 모든 연구자와 엔지니어에게 접근 가능하게 만든 혁신적 기여를 했다.

## 주요 기여
- 최초의 포괄적 광학 리소그래피 시뮬레이터 PROLITH 개발
- 광학계, 레지스트 노광, 레지스트 현상을 통합한 완전한 시뮬레이션 체계
- 레지스트 내 정재파(standing wave) 강도의 해석적 표현식 도출
- Mack 현상 모델 (Enhanced Kinetic Model) 최초 제안
- PC에서 실행 가능한 경량 구현으로 리소그래피 모델링 민주화
- 프리베이크(prebake), 노광, PEB, 현상 전 공정 단계 모델링

## 모델 아키텍처/수식
**PROLITH의 4개 핵심 모델:**

**1. 광학 투영 모델 (Optical Projection Model):**
Hopkins 이론 기반 이미지 강도:
```
I(x) = ∫∫ TCC(f₁, f₂) · M(f₁) · M*(f₂) · exp(j2π(f₁-f₂)x) df₁df₂
```
단일 포커스(best focus)에서 부분 간섭 이미징 계산

**2. 정재파 모델 (Standing Wave Model):**
레지스트 내 강도 분포 (기판 반사로 인한 정재파):
```
I(x, z) = I₀(x) · [1 + R²·exp(-4αz) + 2R·exp(-2αz)·cos(4πnz/λ + φ_r)]
```
여기서:
- α: 레지스트 흡수 계수
- R: 기판 반사율
- n: 레지스트 굴절률
- φ_r: 반사 위상

**3. 레지스트 노광 반응속도론 모델 (Exposure Kinetics):**
Dill ABC 파라미터 모델:
```
∂M/∂t = -I · C · M
```
M: 광활성화합물(PAC) 농도 (초기값 1, 완전 노광 시 0)
C: Dill C 파라미터 (노광 반응 속도 상수)

노광 후 PAC 농도:
```
M(x, z) = exp(-C · I(x, z) · t_exp)
```

레지스트 굴절률 변화 (bleaching):
```
n_resist = A · M + B   (Dill A, B 파라미터)
α = (4π/λ) · Im(n_resist)
```

**4. 레지스트 현상 모델 (Mack Development Rate Model):**
```
R(M) = R_max · (a+1)(1-M)^n / (a + (1-M)^n) + R_min
```
여기서:
- R_max: 완전 노광 레지스트의 최대 현상 속도
- R_min: 미노광 레지스트의 최소 현상 속도
- n: 반응 차수 (레지스트 대비 조절)
- a = (n+1)/(n-1) · (1-M_th)^n  (M_th: 임계 PAC 농도)

**선형화된 Mack 모델 (단순화):**
```
R(M) ≈ R₀ · exp(-γ·M)   (M이 크지 않을 때)
```

**PROLITH 시뮬레이션 출력:**
- 레지스트 프로파일 (2D 단면)
- CD(Critical Dimension) 예측
- 공정 라티튜드(process latitude) 분석

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 물리 기반 리소그래피 모델링의 이론적 근거. PROLITH의 Mack 현상 모델은 TorchResist를 포함한 모든 현대 레지스트 시뮬레이터의 기초. SKOPC에서 TorchLitho + TorchResist를 사용하는 것은 PROLITH의 현대적 GPU 가속 버전이라고 볼 수 있다. Dill ABC 파라미터 보정은 `skopc/modeling/` 내 물리 기반 레지스트 모델 보정에 참조. 정재파 효과는 후막(thick) 레지스트 시뮬레이션에서 중요하며 KrF/ArF 공정에 해당.

## 참고문헌 (핵심)
- Hopkins, H.H., "On the diffraction theory of optical images," Proc. R. Soc. London A (1953)
- Dill, F.H. et al., "Characterization of positive photoresist," IEEE Trans. Electron Devices (1975)
- Mack, C.A., "Analytical expression for the standing wave intensity in photoresist," Appl. Opt. 25(12), 1986
- Flores, G. et al., "Photoresist development model for microlithographic simulation," J. Imaging Sci. (1984)

## 태그
`Model`, `OPC`, `PROLITH`, `OpticalModel`, `ResistModel`, `StandingWave`, `MackModel`, `DillABC`, `DevelopmentRate`, `Kinetic`, `FoundationalPaper`, `LithographySimulation`, `SPIE`
